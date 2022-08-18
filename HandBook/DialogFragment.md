# Dialog Fragments

A fragment that displays a dialog window, floating on top of its activity's window. This fragment contains a Dialog object, which it displays as appropriate based on the fragment's state. Control of the dialog (deciding when to show, hide, dismiss it) should be done through the API here, not with direct calls on the dialog.



## Steps

1. Create a layout file for DialogFragment[^1]
2. Create a Java/Kotlin file to handle the logic for DialogFragment extending `DialogFragment`[^2]
3. In `onCreateView` method inflate the layout using `getLayoutInflater().inflate(...)`
4. Set the logic for the views using inflater view from 3rd step.
5. Now in required Activity create a logic to launch the dialog i.e. with a button press.[^3]
6. Use `dialogFragment.showNow()` to show the dialog. `show()` can also be used but it is asynchronous. 

**Notes**:-

**By using Tag of DialogFragment, we can use it anywhere in our application using `mFragmentDialog = findFragmentByTag("MyDialog")`**

**If using CardView as parent view for cardView with rounded corners, when called dialog will create a rectangular background for itself and to remove those corners we have to set dialog background to transparent with `Objects.requireNonNull(getDialog()).getWindow().setBackgroundDrawable(new ColorDrawable(Color.TRANSPARENT));`

## More

- [Android official website](https://developer.android.com/reference/android/app/DialogFragment)
- @[youtube](SkFcDWt9GV4)
- @[youtube](alV6wxrbULs)







[^1]:Layout for DialogFragment

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/linear"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <EditText
        android:id="@+id/name"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="textPersonName"
        android:text="Name" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="horizontal">

        <Button
            android:id="@+id/button0"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Cancel" />

        <Button
            android:id="@+id/button2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="OK" />
    </LinearLayout>
</LinearLayout>
```



[^2]:Java Code for DialogFragment

```java
public class mDialogFragment extends DialogFragment {

    private EditText editText;
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState)
    {
        View view = getLayoutInflater().inflate(R.layout.dialog_layout, container, false);

        view.findViewById(R.id.button2).setOnClickListener(this::buttonOK);
        view.findViewById(R.id.button0).setOnClickListener(view1 -> getDialog().dismiss());

        editText = view.findViewById(R.id.name);

        return view;
    }
    private void buttonOK(View view1) {
        String name = editText.getText().toString();
        TextView entry = getActivity().findViewById(R.id.textView);
        entry.setText(name);
        getDialog().dismiss();
    }
}
```

[^3]: Java code for showing Dialog Fragment

```java
{	...
    ...
    ...
	binding.fragDialog.setOnClickListener(this::showDialog);
}
    private void showDialog(View view) {
        mDialogFragment dialogFragment = new mDialogFragment();
        
        dialogFragment.setCancelable(false);
        // dialogFragment.show(getSupportFragmentManager(), "MyDialog");
        dialogFragment.showNow(getSupportFragmentManager(), "MyDialog");
    }
}
```

