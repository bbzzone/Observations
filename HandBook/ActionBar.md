# ActionBar

Native Action bar coming with a theme may act differently on different android versions. most probably below lollipop. So for this reason it is preferred to use `ToolBar` instead of default `actionBar` but here we will use default `actionBar` with theme

1. create a menu resource in `res/menu/menu_items`[^1]
2. override `onCreateOptionsMenu` method and `onOptionsItemSelected`.[^2]
3. `onCreatedOptionsMenu` is similar to `onCreate` as it is used to create menu.
4. in `onCreatedOptionsMenu` we will inflate the layouts and can bind menu items to their respective views.
5. `onOptionsItemSelected` function will take necessary actions on a particular key event.

**If any changes are made in menu one should call `invalidateOptionsMenu()` to invalidate the current options menu. On calling this method, `onCreateOptionMenu` will be called again and it will create the view from scratch again**.

To add a backbutton on the action bar for any activity, just call `getSupportActionBar().setDisplayHomeAsUpEnabled(true);` before setting the contentView of the given activity. To define the back activity, add parent activity to the activity where you want to switch back on pressing back button.

```java
// Code for adding BackButton in activity
super.onCreate(savedInstanceState);
getSupportActionBar().setTitle("Add Note");
getSupportActionBar().setDisplayHomeAsUpEnabled(true);
binding = ActivityTakeNoteBinding.inflate(getLayoutInflater());

setContentView(binding.getRoot());

// Somewhere in Mainfest file
<activity
    android:name=".TakeNote"
	android:exported="false"
    android:parentActivityName=".MainActivity" /> // This is the line used to set parent activity
```



#### Change text color

Add below line to your themes

`<item name="android:actionMenuTextColor">@color/your_color</item>`. If it fails than use a spanable string.

```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    MenuInflater inflater = getMenuInflater();
    inflater.inflate(R.menu.your_menu, menu);

    int positionOfMenuItem = 0; // or whatever...
    MenuItem item = menu.getItem(positionOfMenuItem);
    SpannableString s = new SpannableString("My red MenuItem");
    s.setSpan(new ForegroundColorSpan(Color.RED), 0, s.length(), 0);
    item.setTitle(s);
    return true;
}
```



## Code

[^1]:menu_items code

```xml
<menu xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/item1"
        android:icon="@drawable/ic_start"
        app:showAsAction="ifRoom"
        android:title="item 1" />
    <item android:id="@+id/item2"
        android:title="item 2"
        app:showAsAction="never"/>

    <group
        android:id="@+id/group">
        <item android:id="@+id/group_1"
            android:title="group 1"
            app:showAsAction="never"/>
        <item android:id="@+id/group_2"
            android:title="group 2"
            app:showAsAction="never"/>
        <item android:id="@+id/group_3"
            android:title="group 3"
            app:showAsAction="never"/>
    </group>

    <item android:id="@+id/item3"
        android:title="Item 3">
        <menu>
            <item android:id="@+id/subItem1"
                android:title="subItem 1" />

            <item android:id="@+id/subItem2"
                android:title="SubItem 2"/>

            <item android:id="@+id/subItem3"
                android:title="subItem 3"/>
        </menu>
    </item>
</menu>
```



[^2]:java code

```java
Menu menu0;
// ActionBar Menu
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main, menu);
    menu0 = menu;
    return true;
}

@Override
public boolean onOptionsItemSelected(@NonNull MenuItem item) {
    switch (item.getItemId()) {
        case R.id.item1:
            // start some service
            return true;
        case R.id.item2:
            // launch some activity
            return true;
        case R.id.item3:
            // start new activity
            return true;
        case R.id.subItem1:
            // submenu item
            return true;
        case R.id.subItem2:
            // submenu item2
            return true;
        case R.id.subItem3:
            // si3
            return true;
        case R.id.group_1:
            // gi1
            return true;
        case R.id.group_2:
            // gi2
            return true;
        case R.id.group_3:
            // gi3
            return true;
        default:
            return super.onOptionsItemSelected(item);
    }
}
```





## More

- [official website](https://developer.android.com/training/appbar)
- 