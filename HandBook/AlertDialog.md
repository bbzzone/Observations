
# Alert Dialog

A dialog is a small window that prompts the user to make a decision or enter additional information. A dialog does not fill the screen and is normally used for modal events that require users to take an action before they can proceed. One can create AlertDialog directly without creating layout as a layout is already defined for AlertDialog in Android Library.

But to create Custom Dialogs one need to create a layout for the dialog.

To create an Alert Dialog there is no need to to anything in layout or xml file. It can be created directly from java class (activities, fragments etc.).

## Steps

### Alert Dialog

1. First we need to create a builder Object i.e. `AlertDialog.Builder`[^1]
2. To create a builder object we need to pass a context. This is very important step because by default AlertDialog needs an activity context, so passing application context or basecontext may crash the application. **_REASON: AlertDialog needs a Window to create dialog but it can only do so if context passed to it has layout parameters ([more info here](https://stackoverflow.com/a/39676728/14276207)), and that is only possible when activity is being displayed on screen So passing context of an activity which is not active or passing application context will always crash the application._**
3. AlertDialog.Builder will create a builder object but we need an instance of `AlertDialog` itself. To get an instance of `AlertDialog` we need to call `create()` on instance of builder
4. After getting Instance of AlertDialog we can call `show()` on it to show alert.

### Single Choice Dialog

1. Again we need to create an Alert Dialog Builder as in above part
2. Beside adding parameters like positive button, negative button etc. we also need to add [setSingleChoiceItems](<https://developer.android.com/reference/android/app/AlertDialog.Builder#setSingleChoiceItems(java.lang.CharSequence[],%20int,%20android.content.DialogInterface.OnClickListener)>) to show items.
3. This can be used in cases where you have to select one item from the list and you need to confirm it after selecting one. []
4. `setSingleChoiceItems` will take 3 arguments in general cases. 1st one will be the String array of choices, 2nd one will be to select which item should be preselected (index start from 0) and 3rd argument will tell what to do when user clicks on a single choice from provided items.
5. We again need to call `singleChoice.create().show()` to create and show the dialog.

### Multi Choice Dialog

1. Similar to [Single Choice Dialog](#Single-Choice-Dialog) but instead of using `setSingleChoiceItems` we need to use [setMultiChoiceItems](<https://developer.android.com/reference/android/app/AlertDialog.Builder#setMultiChoiceItems(java.lang.CharSequence[],%20boolean[],%20android.content.DialogInterface.OnMultiChoiceClickListener)>)[^3]
2. `setMessage` can not be used with `setMultiChoiceItems`, If you are using it than no items will be shown.
3. `setTitle` can be used to set a title
4. `setMultiChoiceItems` takes 3 arguments unlike Single Choice. 1st argument will be the list of items to be shown (_String array_), 2nd argument will tell which items will be preselected (_Boolean array_). **for no items pass _null_**. 3rd argument will be for onClickListener.
5. In onClickListner 3 arguments will be passed. 1st will be dialogInterface, 2nd is integer to tell index of the item which was clicked and 3rd will be a boolean to represent the clicked item was selected or deselected.


## More

- [Date Picker Dialog](https://developer.android.com/reference/android/app/DatePickerDialog)

- [Time Picker Dialog](https://developer.android.com/reference/android/app/TimePickerDialog)

- **Official Website:** [Alert Dialog](https://developer.android.com/reference/android/app/AlertDialog)

- @[youtube](PqRp3-t9GPM)


[^1]: Alert Dialog
```java
AlertDialog.Builder alert = new AlertDialog.Builder(this);
        alert.setTitle("Dialog")
                .setMessage("This is the message for dialog")
                .setNegativeButtonIcon(AppCompatResources
                        .getDrawable(this, R.drawable.ic_baseline_pending_24))
                .setNegativeButton("", (a,b)->
                    Toast.makeText(getBaseContext(), "Negative Button",                                                 Toast.LENGTH_SHORT).show()
                )
                .setPositiveButtonIcon(AppCompatResources
                        .getDrawable(this, R.drawable.ic_baseline_done_24))
                .setPositiveButton("", (a,b) -> a.dismiss())
                .setNeutralButton("neutral", (a,b) -> Toast
                        .makeText(this, "neutral button", Toast.LENGTH_SHORT).show());
button0.setOnClickListener(this::click);
// button to create alert dialog
public void click(View view) {
    alert.create().show();
}
```

[^2]: java code for single Choice item
```java
private void SingleItemDialog() {
        final String[] favorite = {"Rohit", "Virat", "Dhoni"};
        single = new AlertDialog.Builder(this);
        single.setSingleChoiceItems(favorite, 0, (dialogInterface, i) ->
                    Toast.makeText(getBaseContext(), "You selected " + favorite[i],
                                    Toast.LENGTH_SHORT)
                            .show()
        )
                .setPositiveButton("select",
                        (dialogInterface, i) -> dialogInterface.dismiss())
                .setNegativeButton("dismiss",
                        ((dialogInterface, i) -> dialogInterface.dismiss()));
    }
// onClick method to create dialog
public void singleClick(View view) {
        single.create().show();
    }
```


[^3]: java code for multiChoice
```java
private void MultiChoiceDialog() {
    // Array for items to be shown in Dialog
    final String[] fruits = {"Apple", "LadyFinger", "Banana", "Orange", "Car"};
    // Array for preselected items. (must be primitive type) -> All set to false automatically
    final boolean[] checked = {false, false, false, false, false};
    multi = new AlertDialog.Builder(this);
    multi.setTitle("Select Correct Ones");
    multi.setMultiChoiceItems(fruits, null, (dialogInterface, i, isChecked) -> {
        if (isChecked) Toast.makeText(getBaseContext(),
                                      "You checked " + fruits[i], Toast.LENGTH_SHORT).show();
        else Toast.makeText(getBaseContext(),
                            "You unchecked " + fruits[i], Toast.LENGTH_SHORT).show();
    })
        .setPositiveButton("Done", (dialogInterface, i) -> {
            Toast.makeText(getBaseContext(), "Done", Toast.LENGTH_SHORT).show();
        });
}
// button onClick listner to create mutlichoice dialog
public void multiClick(View view) {
    multi.create().show();
}
```

