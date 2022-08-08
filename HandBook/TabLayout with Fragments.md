# TabLayout with Fragments

Using TabLayout with **ViewPager2 and Fragments** is useful when we have to create an application like a chat app or some app with fixed number of sections. We still have to create an adapter in such cases.

1. In `activity_main.xml` file create TabLayout as parent layout for tabs.[^1]
2. Add tabs inside `TabLayout` as children with `TabItem`
3. Add a ViewPager2 just below TabLayout[^1] and Create Fragments for each tab.
4. Create Adapter for ViewPager extending `FragmentStateAdapter`.[^2]
5. Implement abstract methods and in `getItemCount` return total number of tabs
6. In `createFragment`[^2] method return Fragments required according to position.
7. Now in MainActivity create instance of the adater and attach it with viewPager.[^3]
8. At this point ViewPager and TabLayout are ready to work on their own but we need them to work simultaneously So we need to attach them with each other.
9. Attach Tabs with viewPager using `addOnTabSelectedListener` of TabLayout. This will move set ViewPager's position according to selected tab.
10. Attach ViewPager with Tabs using `registerOnPageChangeCallback` so that on swiping viewpager's position selected tab automatically changes in TabLayout.



## More

- @[youtube](pIKdHeOjYNw)





[^1]: main_activity file for tab's layout

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:orientation="vertical"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tabLayout"
        app:tabMode="auto"
        app:tabIndicatorAnimationMode="fade"
        app:tabSelectedTextColor="@color/purple_200"
        app:tabTextColor="@color/white"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <com.google.android.material.tabs.TabItem
            android:text="Chats"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <com.google.android.material.tabs.TabItem
            android:text="Stories"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <com.google.android.material.tabs.TabItem
            android:text="Calls"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

    </com.google.android.material.tabs.TabLayout>

    <androidx.viewpager2.widget.ViewPager2
        android:id="@+id/viewPager"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```

[^2]: Adapter for ViewPager

```java
public class MyViewPagerAdapter extends FragmentStateAdapter {

    public MyViewPagerAdapter(@NonNull FragmentActivity fragmentActivity) {
        super(fragmentActivity);
    }

    @NonNull
    @Override
    public Fragment createFragment(int position) {

        switch (position) {
            case 0:
                return new Fragment1();
            case 1:
                return new Fragment2();
            default:
                return new Fragment3();
        }
    }

    @Override
    public int getItemCount() {
        return 3;
    }
}
```



[^3]: Attach Both views with each other in MainActivity

```java
// Create adapter for viewPager.
MyViewPagerAdapter viewPagerAdapter = new MyViewPagerAdapter(this);
viewPager2.setAdapter(viewPagerAdapter);


// to change viewPager position when a tab is selected
tabLayout.addOnTabSelectedListener(new TabLayout.OnTabSelectedListener() {
    @Override
    public void onTabSelected(TabLayout.Tab tab) {
        viewPager2.setCurrentItem(tab.getPosition());
    }
    @Override
    public void onTabUnselected(TabLayout.Tab tab) {}
    @Override
    public void onTabReselected(TabLayout.Tab tab) {}
}
                                  );


// to change the selected tab when fragments on ViewPager are swiped
viewPager2.registerOnPageChangeCallback(new ViewPager2.OnPageChangeCallback() {
    @Override
    public void onPageSelected(int position) {
        super.onPageSelected(position);
        Objects.requireNonNull(tabLayout.getTabAt(position)).select();
    }
});
```

