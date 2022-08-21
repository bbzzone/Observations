# Bottom App Bar

For using `BottomAppBar` we need to use `CoordinatorLayout`. `BottomAppBar` is a wrapper for `BottomNavigationView`, So `BottomNavigationView` can be used without `BottomAppBar` so that we don't have to use `CoordinatorLayout`. But it can be helpful if we need to add a floating action button.

1. Create menu items in `res/menu` folder for items to be shown in bottom bar.
2. Create `BottomNavigationView` wrapped in `BottomAppBar`.
3. Add a floating action button if neccessary.
4. In java code set background for `BottomNavigationView` to null otherwise it will give some shadow effect.



**menu_items.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android">

    <item android:title="Home"
        android:id="@+id/home"
        android:icon="@drawable/ic_home"/>

    <item android:title="Search"
        android:id="@+id/search"
        android:icon="@drawable/ic_search"/>

    <item android:id="@+id/placeHolder"
        android:title="" />

    <item android:title="Item"
        android:id="@+id/profile"
        android:icon="@drawable/ic_person"/>

    <item android:title="Item"
        android:id="@+id/settings"
        android:icon="@drawable/ic_settings"/>
</menu>
```



**activity_main.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.coordinatorlayout.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <com.google.android.material.bottomappbar.BottomAppBar
        android:id="@+id/bottomBar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:fabCradleMargin="5dp"
        app:fabCradleRoundedCornerRadius="20dp"
        android:layout_gravity="bottom">

        <com.google.android.material.bottomnavigation.BottomNavigationView
            android:id="@+id/bottomItems"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@android:color/transparent"
            app:menu="@menu/bottom_menu"
            android:layout_marginEnd="16dp"/>

    </com.google.android.material.bottomappbar.BottomAppBar>

    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/fab"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/ic_add"
        app:layout_anchor="@id/bottomBar"/>

</androidx.coordinatorlayout.widget.CoordinatorLayout>
```



**MainActivity.java**

```java
public class MainActivity extends AppCompatActivity {

    ActivityMainBinding binding;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        // To remove the shadow effect of BottomNavigationView.
        binding.bottomItems.setBackground(null);

        // get the item by index.
        MenuItem home = binding.bottomItems.getMenu().getItem(0);
        home.setOnMenuItemClickListener(new MenuItem.OnMenuItemClickListener() {
            @Override
            public boolean onMenuItemClick(MenuItem item) {
                return true;
            }
        });
        
        
        // We can also add an itemSelected listener using below code
        binding.bottomItems.setOnItemSelectedListener(new NavigationBarView.OnItemSelectedListener() {
            @Override
            public boolean onNavigationItemSelected(@NonNull MenuItem item) {

                switch (item.getItemId()) {
                    case R.id.home:
                        break;
                    case R.id.search:
                        break;
                    case R.id.profile:
                        break;
                    case R.id.settings:
                        break;
                }

                return true;
            }
        });
    }
}
```

