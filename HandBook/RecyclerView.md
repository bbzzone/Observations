# RecyclerView

RecyclerView makes it easy to efficiently display large sets of data. You supply the data and define how each item looks, and the RecyclerView library dynamically creates the elements when they're needed.

As the name implies, RecyclerView *recycles* those individual elements. When an item scrolls off the screen, RecyclerView doesn't destroy its view. Instead, RecyclerView reuses the view for new items that have scrolled onscreen. This reuse vastly improves performance, improving your app's responsiveness and reducing power consumption.

## Creating a RecyclerView

1. Add RecyclerView in layout xml file for the activity.[^1]
2. Create a custom layout for items shown in RecyclerView.[^2]
3. Create a custom Adapter for RecyclerView to process items[^3]
   1. extend custom class with `RecyclerView.Adapter<>`.
   2. implement neccessory methods like `getItemCount, onBindViewHolder, onCreateViewHolder`
   3. Create inner class to bind view's from custom layout from 2nd step to the adapter.
   4. inflate layout in `onCreateViewHolder` method.
   5. set Views as per requirement in `onBindViewHolder`.
4. Set LayoutManager for recyclerView with `binding.recycler.setLayoutManager(new LinearLayoutManager(this))`[^4]
5. Get RecyclerView by using `findViewById` or by using `viewBindings` and attach it with an object of custom Adapter created in previous step.[^4]



### Layouts for RecyclerView

#### Horizontal Scroll

While creating `LayoutManger` for RecyclerView use `recyclerView.setLayoutManger(new LinearLayoutManager(this, RecyclerView.HORIZONTAL, true))`. 2nd Parameter in this view will give the direction to fill the elements and 3rd paramenter will reverse the view if true. i.e. In general items will be shown from top to bottom but if `reverseLayout` is true than item shown will be from bottom to top. So in Horizontal mode this will cause elements to show in rtl manner.

```java
binding.recycler.setLayoutManager(new LinearLayoutManager(this, RecyclerView.HORIZONTAL, true));
```



### Adding Swipe/drag control for elements

Elements can be set to swipe horizontally or vertically. For that we need a `ItemTouchHelper`. Drag can be used to reposition elements and swipe can be used for different actions like deleting elements or archiving elements. 

**Adding swipe controls**

Create `ItemTouchHelper` and attach it with recyclerView with `attachToRecyclerView( binding.recycler)`. `ItemTouchHelper` needs a callback to do actions and that callback will implement abstract methods `onMove` and `onSwiped`. `onMove` will handle drags and `onSwiped` will handle swipes.



 callback in `ItemTouchHelper` needs 2 arguments 1st one will be used for drag direction and 2nd one will be used for swipe directions. To disable one of these put that callback to 0. One can also give multiple directions by using `|` between 2 values like `ItemTouchHelper.LEFT | ItemTouchHelper.RIGHT`.

```java
new ItemTouchHelper(new ItemTouchHelper.SimpleCallback(ItemTouchHelper.UP, ItemTouchHelper.LEFT|ItemTouchHelper.RIGHT) {
            @Override
            public boolean onMove(
                @NonNull RecyclerView recyclerView, 
                @NonNull RecyclerView.ViewHolder viewHolder, 
                @NonNull RecyclerView.ViewHolder target) {
                return false;
            }

            @Override
            public void onSwiped(
                @NonNull RecyclerView.ViewHolder viewHolder, 
                int direction) {
                
                int position = viewHolder.getAdapterPosition();
                String item = arrayList.get(position);

                // Remove the item from list 
                // and notify adapter for remove effect
                arrayList.remove(position);
                adapter.notifyItemRemoved(position);

                AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity.this);
                builder.setTitle("Delete Item?");
                builder.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        dialog.dismiss();
                    }
                });
                builder.setNegativeButton("No", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        // reinsert the element to arrayList
                        // notify adapter about inserted item.
                        arrayList.add(position, item);
                        adapter.notifyItemInserted(position);
                        binding.recycler.scrollToPosition(position);
                    }
                }).create().show();
            }
        }).attachToRecyclerView(binding.recycler);
```

 in `onSwiped` method we get the viewHolder for the item we swiped. And direction of swipe. If one wants to implement both right and left swipes than this is useful. One can act on both direction differently by using a simple if statement.

```java
if (direction == ItemTouchHelper.RIGHT) {
    // Do Right Swipe Stuff
} else {
    // Do Left Swipe Stuff
}
```



For drags one gets both viewHolder's, postion we started to drag from and position we dragged to. One can get both positions by using `viewHolder.getAdapterPostion()` and `target.getAdapterPostion()` these will give 'from' and 'to' positions respectively.

```java
new ItemTouchHelper(new ItemTouchHelper.SimpleCallback(
    ItemTouchHelper.UP, 
    ItemTouchHelper.LEFT|ItemTouchHelper.RIGHT) {
            @Override
            public boolean onMove(
                @NonNull RecyclerView recyclerView, 
                @NonNull RecyclerView.ViewHolder viewHolder, 
                @NonNull RecyclerView.ViewHolder target) {

                int from = viewHolder.getAdapterPosition();
                int to = target.getAdapterPosition();

                String element = arrayList.get(from);

                arrayList.remove(from);
                arrayList.add(to, element);
                adapter.notifyItemMoved(from, to);

                binding.recycler.scrollToPosition(to);

                return false;
            }

            @Override
            public void onSwiped(
                @NonNull RecyclerView.ViewHolder viewHolder,
                int direction) {}
        }).attachToRecyclerView(binding.recycler);
```



To swipe only a small portion of the item one can override `onChildDraw` method inside `ItemTouchHelper.SimpleCallback` and in super call change the dimensions value to `dX/2` or `dX/4` whatever necessary.

```java
@Override
public void onChildDraw(
                @NonNull Canvas c, 
                @NonNull RecyclerView recyclerView, 
                @NonNull RecyclerView.ViewHolder viewHolder, 
                float dX, 
                float dY, 
                int actionState, 
                boolean isCurrentlyActive) 
{
    
    super.onChildDraw(
            c, 
            recyclerView, 
            viewHolder, 
            dX/4, // decrease the value if you want to swipe only 25% of the view. 
            dY, 
            actionState, 
            isCurrentlyActive
    	);
}
```

This method is also helpful to set icons in right or left direction and setting a click on them.

```java
@Override
public void onChildDraw(Canvas c, RecyclerView recyclerView, RecyclerView.ViewHolder viewHolder, float dX, float dY, int actionState, boolean isCurrentlyActive) {

    Bitmap icon;
    if (actionState == ItemTouchHelper.ACTION_STATE_SWIPE) {

        View itemView = viewHolder.itemView;
        float height = (float) itemView.getBottom() - (float) itemView.getTop();
        float width = height / 3;

        if (dX > 0) {
            p.setColor(Color.parseColor("#388E3C"));
            RectF background = new RectF((float) itemView.getLeft(),
                                         (float) itemView.getTop(), dX, 
                                         (float) itemView.getBottom());
            c.drawRect(background, p);
            icon = BitmapFactory.decodeResource(getResources(),
                                                R.drawable.ic_mode_edit_white_24dp);
            RectF icon_dest = new RectF((float) itemView.getLeft() + width, 
                                        (float) itemView.getTop() + width, 
                                        (float) itemView.getLeft() + 2 * width, 
                                        (float) itemView.getBottom() - width);
            c.drawBitmap(icon, null, icon_dest, p);
        } else if (dX < 0) {
            p.setColor(Color.parseColor("#D32F2F"));
            RectF background = new RectF((float) itemView.getRight() + dX, 
                                         (float) itemView.getTop(), 
                                         (float) itemView.getRight(), 
                                         (float) itemView.getBottom());
            c.drawRect(background, p);
            icon = BitmapFactory.decodeResource(getResources(),
                                                R.drawable.ic_delete_white_24dp);
            RectF icon_dest = new RectF((float) itemView.getRight() - 2 * width, 
                                        (float) itemView.getTop() + width, 
                                        (float) itemView.getRight() - width, 
                                        (float) itemView.getBottom() - width);
            c.drawBitmap(icon, null, icon_dest, p);
        }
    }
    super.onChildDraw(c, recyclerView, viewHolder, 
                      dX, dY, actionState, isCurrentlyActive);
}
```



#### Scroll To a particular position

There are many methods for scroll in RecyclerView but these are few commonly used ones.

- `binding.recycler.scrollToPostion(int position)` will also show some animation.
- `binding.recyler.smoothScrollToPosition(int position)`
- `binding.recycler.scrollBy(int x, int y);`
- `binding.recycler.scrollTo(int x, int y);`



#### Adding divider between elements

- default divider -> `binding.recycler.addItemDecoration(new DividerItemDecoration(this, DividerItemDecoration.VERTICAL));`

- custom divider -> 

  - ```java
    DividerItemDecoration decoration = new DividerItemDecoration(this,DividerItemDecoration.VERTICAL);
    decoration.setDrawable(R.id.custom_drawable);
    binding.recycler.addItemDecoration(decoration);
    ```



### Adding getPostion/setOnItemClickListener

There are few ways to add setOnItemClickListener but all can be wrapped in same logic. RecyclerView is a Container which contains various views inside it. So to add a click listener to a single item, we need to define click listener for each item. That is only possible in ViewHolder class.

1. implement `View.onClickListener` interface on ViewHolder class (Not necessary but is a standard)
2. In class constructor add an item click listener to whole view and add a method to call onClick
3. Create a method to `setOnItemClickListener` and an interface `onItemClickListener` with abstract method `void onClick(int position)`.
4. `onClick` method will be used to process clicks but for now we need to save an reference to `onItemClickListener` object to call `onClick` from `ViewHolder` class.

```java
public class RecyclerAdapter extends RecyclerView.Adapter<RecyclerAdapter.HoldView> {

    onItemClickListener listener;
    ArrayList<String> arrayList;
    public RecyclerAdapter(ArrayList<String> arrayList) {
        this.arrayList = arrayList;
    }

    @NonNull
    @Override
    public HoldView onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {...}

    @Override
    public void onBindViewHolder(@NonNull HoldView holder, int position) {...}

    @Override
    public int getItemCount() {...}

    // Implement onClickListner (Not necessary, will work find without it)
    class HoldView extends RecyclerView.ViewHolder implements View.OnClickListener {
        TextView textView;
        public HoldView(@NonNull View itemView) {
            super(itemView);
            textView = itemView.findViewById(R.id.textView);
            itemView.setOnClickListener(this::onClick);
        }

        @Override
        public void onClick(View v) {
            listener.onClick(getAdapterPosition());
        }
    }

    // Interface to handle onItemClickListener
    public interface onItemClickListener {
        void onClick(int position);
    }

    // method to setOnItemClickListener
    public void setOnItemClickListener(onItemClickListener onItemClickListener) {
        this.listener = onItemClickListener;
    }
}
```



### Infinite Scroll in RecyclerView

We just have to add items when items in recyclerView are ending. [this question](https://stackoverflow.com/questions/26543131/how-to-implement-endless-list-with-recyclerview) will help.

```java
LinearLayoutManger linearLayoutManager = new LinearLayoutManger(this);
binding.recycler.addOnScrollListener(new RecyclerView.OnScrollListener() {
    @Override
    public void onScrolled(@NonNull RecyclerView recyclerView, int dx, int dy) {
        if (dy > 0) {
            int visibleItemCount = manager.getChildCount();
            int totalItems = manager.getItemCount();
            int invisibleItems = manager.findFirstVisibleItemPosition();

            if (totalItems <= visibleItemCount + invisibleItems) {
                // Add more items to the recyclerview
                arrayList.add("Something")
                    adapter.notifyItemInserted(arrayList.size()-1);
            }
        }
    }
});
```

   

### RecyclerView Scrolling Items one by one

Create a custom class extending LinearShapeHelper and override the method `findTargetSnapPosition`. 

```java
public class SnapHelperOneByOne extends LinearSnapHelper {

    @Override
    public int findTargetSnapPosition (
            RecyclerView.LayoutManager layoutManager, 
            int velocityX, 
            int velocityY
   		 ) 
    {

        if (!(layoutManager instanceof RecyclerView
              					.SmoothScroller.ScrollVectorProvider)) {
            return RecyclerView.NO_POSITION;
        }

        final View currentView = findSnapView(layoutManager);

        if (currentView == null) {
            return RecyclerView.NO_POSITION;
        }

        LinearLayoutManager myLayoutManager = (LinearLayoutManager) layoutManager;

        int position1 = myLayoutManager.findFirstVisibleItemPosition();
        int position2 = myLayoutManager.findLastVisibleItemPosition();

        int currentPosition = layoutManager.getPosition(currentView);

        if (velocityX > 400) {
            currentPosition = position2;
        } else if (velocityX < 400) {
            currentPosition = position1;
        }

        if (currentPosition == RecyclerView.NO_POSITION) {
            return RecyclerView.NO_POSITION;
        }

        return currentPosition;
    }
}
```

Create the instance of this class and attach it with `RecyclerView`

```java
LinearSnapHelper linearSnapHelper = new SnapHelperOneByOne();
linearSnapHelper.attachToRecyclerView(recyclerView);
```











[^1]: RecyclerView layout

```xml
<androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        />
```



[^2]: Item's View 

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:background="@color/teal_200"
    android:layout_marginVertical="7dp"
    android:layout_marginHorizontal="7dp">

    <TextView
        android:id="@+id/textView"
        android:textSize="24sp"
        android:layout_marginVertical="7dp"
        android:paddingVertical="30dp"
        android:gravity="center"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

</LinearLayout>
```



[^3]:Adapter for Recyclerview

```java
public class RecyclerAdapter extends RecyclerView.Adapter<RecyclerAdapter.HoldView> {

    ArrayList<String> arrayList;
    // Constructor for RecyclerAdapter to get data
    public RecyclerAdapter(ArrayList<String> arrayList) {
        this.arrayList = arrayList;
    }

    @NonNull
    @Override
    public HoldView onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(
                R.layout.item_view,
                parent,
                false
        );
        return new HoldView(view);
    }

    @Override
    public void onBindViewHolder(@NonNull HoldView holder, int position) {
        holder.textView.setText(arrayList.get(position));
    }

    @Override
    public int getItemCount() {
        return arrayList.size();
    }
	// Class shouldn't have to be static necessarily
    static class HoldView extends RecyclerView.ViewHolder {
        TextView textView;
        public HoldView(@NonNull View itemView) {
            super(itemView);
            textView = itemView.findViewById(R.id.textView);
        }
    }
}
```

[^4]: MainActivity

```java
RecyclerAdapter adapter = new RecyclerAdapter(arrayList);
binding.recycler.setLayoutManager(new LinearLayoutManager(this));
binding.recycler.setAdapter(adapter);
```





# ToDo

- Custom kind of scroll with **LinearSnapHelper**.