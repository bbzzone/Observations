# Intents

These can be used to start a new Activity. Share data between activities and many more things.

## String Activity

1. Create an Intent in the activity with `Intent intent = new Intent(CurrentActivity.this, NextActivity.class)`. 
2. pass data to the intent, which can be useful for the next activity with `intent.putExtra()`
3. startActivity with `startActivity(intent)`
4. Create intent in second activity and get data with `intent.getStringExtra(), getIntExtra()` etc.

```java
// In Activity 1
ntent intent = new Intent(MainActivity.this, MainActivity2.class);
intent.putExtra("TAG", 32);
startActivity(intent);

// In Activity 2
Intent intent = getIntent();
int value = intent.getIntExtra("TAG", 0);
binding.textView2.setText("Value received: " + value);
```

**Intents can be used to set Flags for the activities(launch modes) like singleTop, standard and way more like intent.setFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT).** 



## Starting Parent Activity from Child Activity

There will be cases where we need a different activity to get some information to show in mainActivity. In such cases we have to start child activity, than put information in child activity. Get that information back from child activity to parent activity. That is not possible if we can try that with simply putting data in intents from child activity and wish that will be accepted in parent activity. In such cases we need special call to childActivity with `startActivityForResult` which is now deprecated and it's replacement is to use activity launchers.

### startActivityForResult

1. In the parent Activity set Intent flag normally as one would do for a simple activity call `new Intent(CurrentActivity.this, NextActivity.class)`.
2. Put any data in the intent which is required in nextActivity i.e. `intent.putExtra("TAG", 23)`
3. start activity with `startActivityForResult(intent, REQUEST_CODE)`.
4. In the child activity get the intent with `getIntent()` and also get any required data using `intent.getIntExtra("TAG", DEFAULT_VALUE)`
5. process the data if necessary. 
6. put the processed value in the intent by `intent.putExtra("TAG", RESULT)` and than use `setResult(RESULT_CODE, intent)` 
7. Result code can be ***RESULT_OK*** or ***RESULT_CANCELED***.
8. Now go back in parent activity and override the method `onActivityResult`.
9. In that method compare your requestCode with the requestCode received and after that process your data as per result_code.
10. method `onActivityResult` will contain requests of all childActivities so it is important that you should be careful with request code of each activity. 

```java
// Calling Child Activity From Parent Activity
Intent intent = new Intent(MainActivity.this, MainActivity2.class);
intent.putExtra("TAG", 4262);
startActivityForResult(intent, 12);

// Returning to Parent Activity from Child Activity.
String result = "This is the result String";  // This will be the processed data
Intent i = getIntent();
i.putExtra("VALUE", result);
setResult(RESULT_OK, i);
finish();

// Handle Request in ParentActivity
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode == 12) {
        if (data != null && resultCode == RESULT_OK) {
            String value = data.getStringExtra("VALUE");
            binding.textView.setText(value);
        }
    }
}
```



### Using ActivityResultLauncher

This is the new recommended way to handle child activities in android.

1. Create a launcher for Child Activity with `registerForActivityResult`.
2. This will take 2 parameters :-
   1. A contract (A contract specifies that an activity can be called with an input of type `I` and produce an output of type `O`. Makes calling an activity for result type-safe.
   2. Callback Handler. (It is the function which will handle the result from the child activity)
3. implement `onActivityResult` method of callback interface to handle the request.
4. `onActivityResult` method will receive `ActivityResult` object, which can be used to get data and result code from the child activity.
5. get result code by using `result.getResultCode()` and get intent by using `result.getData()`. 
6. Now create intent for the childActivity and put required data in the intent.
7. launch the intent by using `ActivityResultLauncher` object. `launcher.launch(intent)`
8. In child Activity create intent with `getIntent` and put processed data in that.
9. now setResult of the childActivity with `setResult(RESULT_OK, intent)`



```java
// Create Launcher in Parent Activity
ActivityResultLauncher<Intent> launcher;
launcher = registerForActivityResult(
    new ActivityResultContracts.StartActivityForResult(),	// contract
    new ActivityResultCallback<ActivityResult>() {			// callback
        @Override
        public void onActivityResult(ActivityResult result) {
            // get result code and data.
            int resultCode = result.getResultCode();
            Intent data = result.getData();
            // process data according to result
            if (data != null && resultCode == RESULT_OK) {
                binding.textView.setText(data.getStringExtra("VALUE"));
            } else if (data != null && resultCode == RESULT_CANCELED) {
                Log.d(TAG, "onActivityResult: Result_canceled");
            }
        }
    });

// Launch the ChildActivity from Parent Activity.
Intent intent = new Intent(MainActivity.this, MainActivity2.class);
intent.putExtra("TAG", 4262);
launcher.launch(intent);


// Process data and return from ChildActivity
String result = "This is the result String";
Intent i = getIntent();
i.putExtra("VALUE", result);
setResult(RESULT_OK, i);		// Set result for MainActivity to handle
finish();						// finish current activity.
```

