
# FrameLayout

A Fragment **represents a reusable portion of your app's UI**. A fragment defines and manages its own layout, has its own lifecycle, and can handle its own input events. Fragments cannot live on their own i.e. they must be hosted by an activity or another fragment.



**Video Below is helpful to understand when to use fragments over activities**
@[youtube](RS1IACnZLy4)



To use Fragments, we need to use FrameLayout which will act as a container for fragments.

It is also important to create Fragments to fill in Frame Layout with their java class[^1] and respective layout[^2]. 

Unlike Activities, fragments are created with `onCreateView` which will return a **`view`** to the fragment and in `onViewCreated` method we can access the elements from the layout of that particular fragment.

## Steps

1. Create FrameLayout in required activity with following code [^3]
2. Create Fragment Classes[^1] and their corresponding layouts[^2]
3. To access views of Fragment class use `onViewCreated` method from Fragment class.
4. To change content of a Frame Layout, ***FragmentManager*** and ***FragmentTransaction*** is required.
5. **`transaction.replace`** is used to change the fragment in Frame Layout.
6. Create instances of fragment classes in activity containing the Frame Layout and use FragmentManger to change content of Frame[^4] 

**instead of using `fragmentTransaction.replace(R.id.frameLayout, frag)` one can use `fragmentTransaction.add(R.id.frameLayout, frag)`. The latter will add the fragments to the stack.**



## Fragment BackStack

BackStack doesn't work automatically in Fragments, we need to set it in the backStack with `fragmentTransaction.addToBackStack(null)`. 

- Instead of null one can pass a string value like `fragTrn.addToBackStack("FragChat")` and suppose we added 3 more fragments to stack but now we want to jump back to **FragChat** than we can use `popToBackStack("FragChat", 0)`. This will remove all the fragments above FragChat in BackStack. Most Probably one will use `popToBackStack` in `onBackPressed` method. [More Info Here](https://stackoverflow.com/a/55024545/14276207)



## List Fragments

List Fragments are similar to ListView in Fragments



### Creating ListFragments

1. Create a Layout in Activity to store Fragment i.e. FrameLayout
2. Now create a new Fragment and create a ListView inside it and **set it's id to `android:id="@android:id/list"`** 
3. In Fragment Class instead of extending Fragment extend `ListFragment`. This will give access to properties like `setListAdapter`
4. In the Fragment Class Create an ArrayAdapter `ArrayAdapter.createFromResource` or a generic Adapter and pass the String array you want to display.
5. attach adapter to listView with `setListAdapter(arrayAdapter)`
6. To attach a click listener use `getListView().setOnItemClickListener()`[^5] method

## Codes

[^3]:layout code below

```xml
<FrameLayout
        android:id="@+id/fragment"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintHeight_percent="0.9"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintWidth_percent="1" />
```

[^1]: java code for fragment
~~~java
public class FragmentOne extends Fragment {
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_one, container, false);
    }
    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        TextView textView = view.findViewById(R.id.textView1);
        textView.setText("Hell no this is 1st one");
    }
}
```
~~~

[^2]:layout code for fragments
```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".Fragments.FragmentOne">
    <TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:textSize="30sp"
        android:textStyle="bold"
        android:text="Fragment One"/>
</FrameLayout>
```



[^4]:java code for transactions
```java
// get a FragmentManager to handle Fragments
FragmentManager fragmentManager = getSupportFragmentManager();
toggleButton = findViewById(R.id.button);
// instances of both fragments
FragmentOne fragmentOne = new FragmentOne();
FragmentTwo fragmentTwo = new FragmentTwo();
toggleButton.setOnCheckedChangeListener((compoundButton, b) -> {
    FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
    if (b) fragmentTransaction.replace(R.id.fragment, fragmentTwo).commit();
    else fragmentTransaction.replace(R.id.fragment, fragmentOne).commit();
});
```



[^5]:java code for Click logic in ListFragment

```java
@Override
public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
    super.onViewCreated(view, savedInstanceState);

    ArrayAdapter<String> arrayAdapter = new ArrayAdapter<>(getActivity(),                                                android.R.layout.simple_list_item_1, 													   getResources().getStringArray(R.array.countries));
    setListAdapter(arrayAdapter);

    getListView().setOnItemClickListener((parent, view1, position, id) ->
                                         {
                                             Toast.makeText(getContext(), "" + position,													Toast.LENGTH_SHORT).show();
                                             Intent intent = new Intent(getActivity(), 														Activity2.class);
                                             intent.putExtra("POSITION", position);
                                             startActivity(intent);
                                         });
}
```



## More

- Official website: [Android Developers](https://developer.android.com/guide/fragments)

- [Fragment Lifecycle](https://www.geeksforgeeks.org/fragment-lifecycle-in-android/)

- @[youtube](vAI7RSPxOA)

- @[youtube](WVPH48lUzGY)