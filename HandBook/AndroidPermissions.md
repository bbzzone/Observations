# Android Permissions

Permissions an application require needs to be defined in **AndroidManifest.xml** file.

Permissions in android are categorised in many parts but these 2 are the important ones:

1. Install Time Permissions
2. RunTime Permissions



## Install Time Permissions

Install-time permissions give your app limited access to restricted data, and they allow your app to perform restricted actions that minimally affect the system or other apps. When you declare install-time permissions in your app, the system automatically grants your app the permissions when the user installs your app.



## Runtime Permissions

Runtime permissions, also known as dangerous permissions, give your app additional access to restricted data, and they allow your app to perform restricted actions that more substantially affect the system and other apps. Therefore, you need to [request runtime permissions](https://developer.android.com/training/permissions/requesting) in your app before you can access the restricted data or perform restricted actions. When your app requests a runtime permission, the system presents a runtime permission prompt.

Many runtime permissions access *private user data*, a special type of restricted data that includes potentially sensitive information. Examples of private user data include location and contact information.



### Best Practices to ask for Runtime Permissions

- **Request minimum number of permissions as possible**
- **Associate runtime permissions with specific actions**
  - Request permissions as late into the flow of your app's use cases as possible. For example, if your app allows users to send audio messages to others, wait until the user has navigated to the messaging screen and has pressed the **Send audio message** button. After the user presses the button, your app can then request access to the microphone.
- When you include a library, you also inherit its permission requirements. Be aware of the permissions that each dependency requires, and what those permissions are used for.

## Standard Way of Requesting Runtime Permissions

1. Declare the permissions required by application in Manifest file.
2. Design your app's UX so that specific actions in your app are associated with specific runtime permissions. By doing this user will have some idea why the particular permission is neccessory
3. When user try to invoke the task or action in your app which requires that particular permission check if user has already granted the permission or not.
4. If not granted, show user a dialog or something to show why this permission is required if that is neccessory and after that request for the permission.
5. Check whether user allowed the permission or denied and show a response in accordance to that.



### Check Permission status

This can be done with `checkSelfPermission(String permission)` method from and Activity or better to use `ContextCompat.checkSelfPermission(Context context, String permission)`. To check for a permission below code can be used

```java
boolean permission = (ContextCompat.checkSelfPermission(this, READ_EXTERNAL_STORAGE)
                == PackageManager.PERMISSION_GRANTED);
```

   or 

```java
boolean permission = (checkSelfPermission(READ_EXTERNAL_STORAGE) == PackageManager.PERMISSION_GRANTED);
```

In some application below API level 30 or Android R snippet below can be used

```java
if (SDK_INT >= Build.VERSION_CODES.R) {
    return Environment.isExternalStorageManager();
} else {
 	return ContextCompat.checkSelfPermission(this, READ_EXTERNAL_STORAGE) 
        		== PackageManager.PERMISSION_GRANTED);   
}
```



### Requesting Runtime Permissions

Similar like checking permission requesting permissions in android can be done with simple function `requestPermissions(String[] permissions, int requestCode)` or with `ActivityCompat.requestPermissions(Context context, String[] permissions, int requestCode)` To request for permission below snippets can be used

```java
requestPermissions(new String[] {
    				READ_EXTERNAL_STORAGE, 
    				CAMERA, 
    				ACCESS_COARSE_LOCATION}
                   23);
```

**OR**

```java
ActivityCompat.requestPermissions(new String[] {CAMERA}, 542);
```

2nd int value can be anything it is just a tag value

One more important function is `shouldShowRequestPermissionRationale(String permission)` or `ActivityCompat.shouldShowRequestPermissionRationale(Context context, String permission)`. If calling this function returns true than it is a reminder that user had previously declined this permission and if he again declines the permission by clicking **Never ask Again**,no permission request dialog will be shown to the user next time. So it is a good idea to show some information about why app needs this permission before creating a permission request to increase acceptance rate.

`requestPermissions` will make a callback to `onRequestPermissionsResult`. 

**Handle user responses**

This can be done by **Overriding** *onRequestPermissionResult* in Activity which will get a callback automatically from `requestPermissions`. There we can handle user response with the logic below

```java
@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    super.onRequestPermissionsResult(requestCode, permissions, grantResults);
    if (requestCode == 0) {..do this..}
    else if (requestCode == 1){
        if (grantResults.length > 0) {
            for (int i = 0; i < grantResults.length; i++) {
                Log.d(TAG, "onRequestPermissionsResult: " 
                      + permissions[i] + ": " 
                      + grantResults[i]);
            }
        }
    }
}
```

In above function String[] permission will have all the permission which were requested in called requestCode (This is when requestCode comes handy). Corresponding indeces in grantResult integer array will be results for permissions (0 for GRANTED and -1 for DENIED).

### Recommended way for Runtime Permissions

To request single permission use `RequestPermission` and for multiple permissions use `RequestMultiplePermissions` 

**Steps (Single Permission)**

1. Create an `ActivityResultLauncher<String>` Object.
2. `launcher = registerForActivityResult(ActivityResultContract contract, ActivityResultCallback callback)`
3. 1st parameter will decide which kind of permission we are requesting like single permission or multilple permissions.
4. 2nd Argument will decide what to do if user accepted or rejected the permission.
5. when launcher is created give a `launch()` call to create permission dialog.  

**JAVA code for Single Permission**

```java
ActivityResultLauncher<String> launcher;
launcher = registerForActivityResult(
                new ActivityResultContracts.RequestPermission(),
                isGranted -> {
                    if (isGranted) {
                        // Do something
                    } else {
                        // Do something else
                    }
                }
        );

// Now call for permission whenever required with
launcher.launch();
```

**Steps(Multiple Permissions)**

1. Create an `ActivityResultLauncher<String[]>` Object. **this time we have to create String[] launcher unlike String launcher as in single permission**
2. `launcher = registerForActivityResult(ActivityResultContract contract, ActivityResultCallback callback)`
3. 1st parameter contract will be `new RequestMultiplePermissions()`
4. 2nd parameter will be a callback with a `Map` where key will be permission and value will be a boolean to state if permission was accepted or not.

**JAVA code for multiple permissions**

```java
launcher = registerForActivityResult(
                new ActivityResultContracts.RequestMultiplePermissions(),
                new ActivityResultCallback<Map<String, Boolean>>() {
                    @Override
                    public void onActivityResult(Map<String, Boolean> result) {
                        if (result.get(READ_EXTERNAL_STORAGE) != null) {
                            if (result.get(READ_EXTERNAL_STORAGE)) {
                                // Do stuff granted
                            } else {
                                // Do stuff declined
                            }
                        }
                        if (result.get(CAMERA) != null) {
                            if (result.get(CAMERA)) {
                                // Granted
                            } else {
                                // declined
                            }
                        }
                        if (result.get(RECORD_AUDIO) != null) {
                            if (result.get(RECORD_AUDIO)) {
                                // Granted
                            } else {
                                // denied
                            }
                        }
                    }
                }
        );

// to launch create a function which will 1st check 
// whether permissions already granted or not
private void requestPermissions() {
        ArrayList<String> stringArrayList = new ArrayList<>();
        if (checkSelfPermission(READ_EXTERNAL_STORAGE) != 
            							PackageManager.PERMISSION_GRANTED) {
            stringArrayList.add(READ_EXTERNAL_STORAGE);
        }
        if (checkSelfPermission(CAMERA) != PackageManager.PERMISSION_GRANTED) {
            stringArrayList.add(CAMERA);
        }
        if (checkSelfPermission(RECORD_AUDIO) != PackageManager.PERMISSION_GRANTED) {
            stringArrayList.add(RECORD_AUDIO);
        }

		// Launch the permission launcher from here.
        if (!stringArrayList.isEmpty()) {
            launcher.launch(stringArrayList.toArray(new String[0]));
        }
    }
```

