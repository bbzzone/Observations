# ViewPager

ViewPager is a swipable view. Like banners on some websites. This can be used with Tablayout to add a swip feature to switch to different screen (i.e. left swipe in whatsapp application can swipe you to calls or stories section). 

This uses Adapter to show items in the viewpager through a customLayout which is inflated in Adapter for ViewPager.

## Steps

1. In MainActivity layout add a ViewPager2 item.[^1]
2. Create a custom Layout for ViewPager items.[^2]
3. Create an Adapter Class for ViewPager extending `RecyclerView.Adapter<>`[^3]
4. Implement an inner class to set the view for Adapter and implement abstract methods.
5. in `onBindViewHolder` attach the values to the items with views in custom layout for viewpager created in 2nd step.
6. Now create an instance of the CustomAdapterClass from step 3 and attach it with adapter.[^4]
7. Now one can select the orientation of swipe with `viewPager2.setOrientation( ViewPager2.ORIENTATION_VERTICAL);`. Default orientation is Horizontal.
8. One can also implement fake drag using fakeDragmethods.



### Attach TabLayout with ViewPager

1. In activity main layout add Tablayout above Viewpager2 from above[^5]
2. In MainActivity.java file bind TabLayout with its view in layout file
3. After binding Create a new `TabLayoutMediator` to attach Viewpager with TabLayout.[^6]
4. After creating Mediator call attach on it.
5. **There is much more one can do in Mediator other than setting Titles like showing message indicators etc.**
6. We can add TabSelectedListeners in Java code
   1. **onTabSelected** will be called when tab is selected
   2. **onTabUnselected** will be called when tab is deselected
   3. **onTabReselected** will be called if we press on the tab where we already are. 









## More

- ViewPager2 @[youtube](-wB_JE_PRTo)
- ViewPager2 with infinite scrolling, autoScroll @[youtube](iA9iqygq11Q)
- TabLayout with ViewPager2 @[youtube](h41FnEH91D0)
- Insta Reels like app @[youtube](PhqhYUwkCXM)



[^1]:main_activity layout

```xml
<androidx.viewpager2.widget.ViewPager2
        android:id="@+id/viewPager"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

[^2]: custom_layout for Viewpager

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center">

    <TextView
        android:id="@+id/textView"
        android:minWidth="200dp"
        android:minHeight="40dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</LinearLayout>
```

[^3]: Adapter class for Viewpager

```java
public class ViewPagerAdapter extends RecyclerView.Adapter<ViewPagerAdapter.ViewPagerHolder>{

    private final String[] values;
    ViewPagerAdapter(String[] values) {
        this.values = values;
    }

    @NonNull
    @Override
    public ViewPagerHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(
                R.layout.view_pager_items,
                parent,
                false
        );
        return new ViewPagerHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull ViewPagerHolder holder, int position) {
        holder.textView.setText(values[position]);
    }

    @Override
    public int getItemCount() {
        return values.length;
    }

    protected static class ViewPagerHolder extends RecyclerView.ViewHolder {
        public TextView textView;
        public ViewPagerHolder(@NonNull View itemView) {
            super(itemView);
            textView = itemView.findViewById(R.id.textView);
        }
    }
}
```

[^4]: MainActivity for creating instance of adapter

```java
viewPager2 = findViewById(R.id.viewPager);

ViewPagerAdapter adapter = new ViewPagerAdapter(items);

viewPager2.setAdapter(adapter);
// To set swipe orientation to vertical
viewPager2.setOrientation(ViewPager2.ORIENTATION_VERTICAL);

// Fake Drag in Viewpager 2
viewPager2.beginFakeDrag();
// negative value means swipe to left or up according to orientation.
viewPager2.fakeDragBy(-10f);
viewPager2.endFakeDrag();

tabLayout.addOnTabSelectedListener(new TabLayout.OnTabSelectedListener() {
            @Override
            public void onTabSelected(TabLayout.Tab tab) {
                Toast.makeText(getBaseContext(), "Tab Selected " + tab.getText(),
                        Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onTabUnselected(TabLayout.Tab tab) {
                Toast.makeText(getBaseContext(), "Tab UnSelected " + tab.getText(),
                        Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onTabReselected(TabLayout.Tab tab) {
                Toast.makeText(getBaseContext(), "Tab Reselected " + tab.getText(),
                        Toast.LENGTH_SHORT).show();
            }
        });
```

[^5]: Update MainActivity Layout

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:orientation="vertical"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tabLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:tabMode="scrollable"
        />

    <androidx.viewpager2.widget.ViewPager2
        android:id="@+id/viewPager"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```

[^6]:Updated MainActivity java file

```java
ViewPagerAdapter adapter = new ViewPagerAdapter(items);
viewPager2.setAdapter(adapter);

new TabLayoutMediator(tabLayout, viewPager2, (tab, position) -> {
    tab.setText("Page " + (position + 1));
}).attach();
```

