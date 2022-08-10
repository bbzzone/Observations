# Basics

- **MainActivity.java**: `(Project Folder)/app/src/main/java/(package name)/MainActivity.java`
- **MainActivity.xml**: `(Project Folder)/app/src/main/res/layout/activity_main.xml`
- **Gradle Script**: `(Project Folder)/build.gradle`
- **Manifest**: `(Project Folder)/src/main/AndroidManifest.xml`

## build.gradle

This file contains information like minimum sdk, application id, application version code etc.

```json
plugins {
    id 'com.android.application'
}

android {
    compileSdk 32

    defaultConfig {
        applicationId "com.redheadhammer.testing"
        minSdk 23
        targetSdk 32
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

dependencies {
    implementation 'androidx.appcompat:appcompat:1.3.0'
    implementation 'com.google.android.material:material:1.4.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.0.4'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.3'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
}
```

It also contain very important option **dependencies** which is the dependencies required to build the application.

## Manifest File

This file contains the information about the application like, application name, icon, theme information etc. More importantly this will have permission which application is going to use on device. It also contain information about screen orientation.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.redheadhammer.testing">

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="App_testing"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar">
        <activity
            android:name=".MainActivity"
            android:screenOrientation="fullSensor"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

## Resources folder (res)

This folder contains many different other folders and is located at `(Project Folder)/app/src/main/res`. This folder contain various other folders for different purposes, like `drawables, mipmap, values, layout`.

- layout folder contains the _activity_main.xml_ file
- **drawable** contains the pictures for the project.
- **mipmap** folders contain some pictures of different resolutions, which are used for devices with different resolutions. mipmap folders are **(mipmap-hdpi, mipmap-anydpi-v24, mipmap-dpi etc.)**
- **values** folder contains variables which are assigned some values which can be pointed by their representatives anywhere in the project.
- **values folder** also contains **theme** information (i.e. light theme or dark theme) both are represented by **themes.xml** but one is present in values folder and another in **values-night**.

### Drawable

This folder also contains various design files like (button designs, )

# Layouts

A layout is a visual structure for an application

1. Linear Layout
2. Relative Layout
3. Table Layout
4. Constrait Layout

## Linear Layout

This is the layout which will place elements linearly i.e. either horizontaly or vertically.

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">


    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:id="@+id/realText"
            android:layout_width="180dp"
            android:layout_height="wrap_content"
            android:text="Username"
            android:textAlignment="center" />

        <TextView
            android:id="@+id/unrealText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Password"
            android:textAlignment="center" />

    </LinearLayout>

    <Button
        android:id="@+id/submit"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Submit"
        android:textStyle="bold" />

</LinearLayout>
```

The above code creates 2 LinearLayouts. 1st one is Vertical and another 2nd layout as its child which will be horizontal. Now horizontal will contain 2 textViews one will be for username and another will be for password. Now as 2nd element of Vertically layout we have a **Submit** button.

## Relative Layout

This is the layout which will place elements relative to each other. There are some attributes which can help achieve this like **(android:layout_below="@+id/button1", android:layout_above="@+id/button1")**

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button1"
        android:text="Button1"
        android:textStyle="bold"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        />

    <Button
        android:id="@+id/button2"
        android:text="Button2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@+id/button1"
        android:layout_centerHorizontal="true"
        />
    <Button
        android:id="@+id/button0"
        android:text="Button 0"
        android:textStyle="bold"
        android:layout_above="@+id/button1"
        android:layout_centerHorizontal="true"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
</RelativeLayout>
```

In this code Button 1 is created in Relative layout which is **centered vertically and horizontally** than another button 2 is created which will be be set to be below button 1 using `android:layout_below="@+id/button1"` and another button with name Button 0 is created which is also placed above button 1 with `android:layout_above="@+id/button1"`.

` android:layout_centerHorizontal="true"` and ` android:layout_centerVertical="true"` will not work in linear layout or table layout.

## Table Layout

This is the layout which will have some rows and columns. To create a row one need to evoke table row

```xml
<?xml version="1.0" encoding="utf-8" ?>

<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:divider="?android:attr/dividerHorizontal"
    android:showDividers="middle|end"
    tools:context=".MainActivity"
    android:orientation="vertical">


    <TableRow
        android:paddingStart="10dp"
        android:paddingEnd="10dp"
        android:divider="?android:attr/dividerHorizontal"
        android:showDividers="middle|beginning|end"
        >
    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:gravity="center_vertical"
        android:layout_height="wrap_content"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:text="@string/app_name"
        android:textSize="30sp"
        android:textStyle="bold"
        android:textColor="#FF1234"
        />

        <TextView
            android:id="@+id/textView1"
            android:layout_width="wrap_content"
            android:gravity="center_vertical"
            android:layout_height="wrap_content"
            android:text="@string/app_name"
            android:layout_marginStart="10dp"
            android:layout_marginEnd="10dp"
            android:textSize="30sp"
            android:textStyle="bold"
            android:textColor="#FF1234"
            />
    </TableRow>


    <TableRow
        android:paddingStart="10dp"
        android:paddingEnd="10dp"
        >
        <TextView
            android:id="@+id/textView9"
            android:layout_width="wrap_content"
            android:gravity="center_vertical"
            android:layout_height="wrap_content"
            android:layout_marginStart="10dp"
            android:layout_marginEnd="10dp"
            android:text="@string/app_name"
            android:textSize="30sp"
            android:textStyle="bold"
            android:textColor="#FF1234"
            />

        <TextView
            android:id="@+id/textView4"
            android:layout_width="wrap_content"
            android:gravity="center_vertical"
            android:layout_height="wrap_content"
            android:text="@string/app_name"
            android:layout_marginStart="10dp"
            android:layout_marginEnd="10dp"
            android:textSize="30sp"
            android:textStyle="bold"
            android:textColor="#FF1234"
            />
    </TableRow>
    <TableRow
        android:paddingStart="10dp"
        android:paddingEnd="10dp"
        >
        <TextView
            android:id="@+id/textView23"
            android:layout_width="wrap_content"
            android:gravity="center_vertical"
            android:layout_marginStart="10dp"
            android:layout_marginEnd="10dp"
            android:layout_height="wrap_content"
            android:text="@string/app_name"
            android:textSize="30sp"
            android:textStyle="bold"
            android:textColor="#FF1234"
            />

        <TextView
            android:id="@+id/textView154"
            android:layout_width="wrap_content"
            android:gravity="center_vertical"
            android:layout_height="wrap_content"
            android:layout_marginStart="10dp"
            android:layout_marginEnd="10dp"
            android:text="@string/app_name"
            android:textSize="30sp"
            android:textStyle="bold"
            android:textColor="#FF1234"
            />
    </TableRow>
</TableLayout>
```

This contains a Table Layout than 3 Table Rows, each Row contains 2 TextViews with some values.

- Between each row there is a seprator which is created with these attributes
  - `android:divider="?android:attr/dividerHorizontal"` one can use a custom divider using drawables i.e. `android:divider="@drawable/myDivider"`
  - `android:showDividers="middle|end"` this is used to tell set the position of the divider. this can be set to `beginning, middle, end and none`

# Other Components

## TextViews

TextViews are fields which contain some text in it. These have many properties which can be used to customize their looks.

```xml
<TextView
          android:id="@+id/textView4"
          android:layout_width="wrap_content"
          android:gravity="center_vertical"
          android:layout_height="wrap_content"
          android:text="@string/app_name"
          android:layout_marginStart="10dp"
          android:layout_marginEnd="10dp"
          android:textSize="30sp"
          android:textStyle="bold"
          android:textColor="#FF1234"
          />
```

There are few other properties like gravity `android:gravity="center".` Don't confuse this with layout_gravity. that is the gravity of the element in a layout like gravity of textView in TableRow.

### Accessing TextView from java code

```java
// findViewById(int value)
TextView text;
text = findViewById(R.Id.textView4)

// Accessing text from java code
text.setBackgroundColor(0xffff12);
text.setText("Something");
text.setAllCaps(true);
text.setCursorVisible(true);
text.setGravity(2);
text.setHeight(345);
text.setWidth(745);
```

### Adding Listeners

```java
text.setOnClickListener(view -> text.setText("Click"));
text.setOnLongClickListener(view -> {
    if (text.getText() == "Something") text.setText("Value");
    else text.setText("Something");
    return true;
});
```

On click Listener will be invoked on single press on textView. `setOnLongClickListener` will be invoked when textView is long pressed. Now if lamda function passed to `setOnLongClickListener` will return true than it will indicate that the event has been handled and listener should stop now, but if received false than it will continue to listen for other events (i.e. release event which can invoke `onClickListener`, same is true for other values like `onTouchListener`).

_So if `setOnLongClickListener` return false than on releasing the textView it will again trigger `setOnClickListener as it need to watch for other listener events (here release event)`_.

There are 3 possible events **LONG PRESS, RELEASE, PRESS**. If one doesn't care about it than `setOnClickListener` will do the pretty much work. But there are cases where where RELEASE and PRESS have significant role and this can be achieved with

```java
text.setOnTouchListener((view, motionEvent) -> {
    if (motionEvent.getAction() == MotionEvent.ACTION_UP){
        text.setText("TouchR");	// on release
        text.setBackgroundColor(Color.BLACK);
    } else if (motionEvent.getAction() == MotionEvent.ACTION_DOWN){
        text.setText("TouchP"); // on press
        text.setBackgroundColor(Color.BLUE);
    }
    return true;
});
```

## Buttons

These are clickable buttons and can be configured to be of different sizes

```xml
<Button
android:id="@+id/button0"
android:text="Button 0"
android:clickable="false"
android:focusable="true"
android:layout_centerHorizontal="true"
android:layout_width="200dp"
android:layout_height="wrap_content"
android:paddingTop="10dp"
android:paddingBottom="10dp"
/>

<Button
android:id="@+id/button1"
android:background="@color/black"
android:text="Button 1"
android:textStyle="bold"
android:layout_centerHorizontal="true"
android:enabled="true"
android:layout_marginTop="20dp"
android:layout_marginBottom="20dp"
android:layout_below="@+id/button0"
android:layout_width="200dp"
android:layout_height="wrap_content"
/>

```

These have many properties like enable, clickable, background, textColor etc. which can be used to modify those

- Clickable property is to make button respond on different click events.
- Clickable will only trigger after setting the property in java file and won't work if set false in xml activity_main.xml file.

### Accessing Button and Adding Listener

```java
button0 = findViewById(R.id.button0);
button1 = findViewById(R.id.button1);

text = findViewById(R.id.text);
button0.setOnClickListener(view -> {
    if (text.getText().equals("Click"))
        text.setText("change");
    else text.setText("Click");
    button0.setFocusable(!(button0.isFocusable()));
});

button1.setOnClickListener(view -> {
    button0.setClickable(false);
	button1.setEnabled(false);
    button0.setVisibility(View.INVISIBLE);
    button1.setVisibility(View.INVISIBLE);
});

// Other way
button.setOnClickListener(new View.onClickListener(){
    @override
    public void onClick(View view) {
        System.out.println("Hellz");
    }
})

```

As per above code button0 will toggle value of textView when clicked and button1 will make button0 unclickable and will disable the itself.

Moreover when pressed button1, it will also make button0 and button1 INVISIBLE.

### Creating custom-buttons

In Android-Studio one can create drawables by going to **New->Drawable resource file** and after following some prompts one will be in a xml file defining shape. There one can create a shape using xml code

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" 							android:shape="rectangle"
>
    <corners
        android:radius="20dp"
    />
    <solid
        android:color="#4F4F4F"
    />
    <padding
        android:left="0dp"
        android:top="0dp"
        android:right="0dp"
        android:bottom="0dp"
    />
    <size
        android:width="270dp"
        android:height="60dp"
    />
    <stroke
        android:width="3dp"
        android:color="#142487"
    />
</shape>
```

This is the code for a button and should be saved in drawable folder. To use this in `main_activity.xml` file just add a line `android:background="@drawable/sqcircle"` in the button tag like below

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >
    <Button
        android:id="@+id/button0"
        android:text="Button 0"
        android:paddingTop="10dp"
        android:paddingBottom="10dp"
        android:background="@drawable/sqcircle"
        android:layout_centerHorizontal="true"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        />
</RelativeLayout>
```

On [This website](https://angrytools.com/android/button/) one can create custom buttons and can save them into xml files.

Below is code for some buttons created using material ui from google.

```xml
    <com.google.android.material.button.MaterialButton
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Normal"
        android:layout_centerHorizontal="true"
        />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button2"
        android:text="Contained"
        android:textSize="20sp"
        android:layout_marginTop="20dp"
        android:layout_marginBottom="20dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/button1"
        android:layout_centerHorizontal="true"
        style="@style/Widget.Material3.Button.OutlinedButton"
        app:strokeColor="#128BEB"
        app:strokeWidth="2dp"
        />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button3"
        android:layout_width="120dp"
        android:layout_height="120dp"
        android:layout_below="@id/button2"
        android:layout_centerHorizontal="true"
        android:text="Circle"
        app:cornerRadius="90dp"
        app:strokeColor="@color/teal_200"
        app:strokeWidth="3dp" />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/button3"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="20dp"
        android:layout_marginBottom="20dp"
        android:background="@drawable/gradient"
        android:text="Gradient"
        android:textSize="18sp"
        app:backgroundTintMode="multiply" />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button5"
        android:text="Round Gradient"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/button4"
        android:layout_centerHorizontal="true"
        android:background="@drawable/gradient2"
        android:textSize="18sp"
        app:backgroundTintMode="multiply" />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button6"
        android:text="Icon"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="20dp"
        android:layout_marginBottom="20dp"
        android:layout_below="@id/button5"
        app:cornerRadius="20dp"
        app:icon="@drawable/no_drinks_24"
        app:strokeColor="#48DFDD"
        app:backgroundTintMode="screen"
        app:strokeWidth="2dp"
        app:iconGravity="end"
        />
```

## EditTexts

EditText can be used to take input text like, _username, password, num-password, address etc._ .

Values can be checked for null with `TextUtils.isEmpty(myString)`. `Objects.requireNonNullElse(obj, default_value)` will not work as that is only supported with 1.9+ jdk versions.

```xml
<?xml version="1.0" encoding="utf-8" ?>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:divider="?actionBarDivider"
    android:showDividers="middle"
    android:gravity="center_horizontal"
    xmlns:app="http://schemas.android.com/apk/res-auto">


    <EditText
        android:id="@+id/editTextTextPersonName"
        android:layout_marginStart="20dp"
        android:layout_marginEnd="20dp"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:ems="10"

        android:autofillHints="username"
        android:inputType="textPersonName"
        android:maxLength="10"
        android:hint="Username"
        />

    <EditText
        android:id="@+id/editTextTextPassword"
        android:layout_marginStart="20dp"
        android:layout_marginEnd="20dp"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:ems="10"
        android:minEms="6"

        android:autofillHints="password"
        android:inputType="textPassword"
        android:hint="Enter password" />

    <EditText
        android:id="@+id/phone"
        android:layout_marginStart="20dp"
        android:layout_marginEnd="20dp"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"

        android:inputType="phone"
        android:autofillHints="phone"
        android:hint="Phone"
        />

    <EditText
        android:id="@+id/email"
        android:layout_marginStart="20dp"
        android:layout_marginEnd="20dp"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"

        android:inputType="textEmailAddress"
        android:autofillHints="emailAddress"
        android:hint="Email"
        />

    <EditText
        android:id="@+id/age"
        android:layout_marginStart="20dp"
        android:layout_marginEnd="20dp"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"

        android:inputType="numberDecimal"
        android:importantForAutofill="no"
        android:hint="Age"
        />
    <com.google.android.material.button.MaterialButton
        android:id="@+id/button0"
        android:layout_width="match_parent"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:text="Submit"
        android:textSize="20sp"
        android:layout_height="wrap_content"
        style="@style/Widget.Material3.Button.OutlinedButton"
        app:strokeColor="@color/purple_700"
        app:strokeWidth="3dp"
        />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button1"
        android:layout_width="match_parent"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:text="Useless"
        android:textSize="16sp"
        app:cornerRadius="30dp"
        app:icon="@drawable/no_drinks_24"
        app:iconGravity="textEnd"
        android:layout_height="wrap_content"
        />

    <TextView
        android:id="@+id/result"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:layout_height="wrap_content"
        android:layout_width="match_parent"
        android:visibility="invisible"
        />

</LinearLayout>
```

This is the xml code for a user data menu where there are some **EditText** with some buttons and handled with below java code. All Edittext are same above but have `android:inputType="numberDecimal"` set which will tell what kind of input this need so android will present with the required keyboard style. `android:hint="Username"` and `android:maxLength="10"` are other 2 useful methods.

`android:autofillHints="username"`: this is used to tell the android system that the value inside this field will be a username so that android will serve accordigly i.e. will give username suggestions, This can be disabled with `android:importantForAutofill="no"` property.

`android:hint="Username"` is used to give hint for the value (will be written in username field in faded letters).

```java
package com.redheadhammer.testing;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.text.TextUtils;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;


public class MainActivity extends AppCompatActivity{

    Button submit, useless;
    EditText username, passwd, age, phone, email;
    TextView result;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        submit = findViewById(R.id.button0);
        useless = findViewById(R.id.button1);

        username = findViewById(R.id.editTextTextPersonName);
        passwd = findViewById(R.id.editTextTextPassword);

        age = findViewById(R.id.age);
        phone = findViewById(R.id.phone);
        email = findViewById(R.id.email);

        result = findViewById(R.id.result);

        submit.setOnClickListener(view -> {
            String name = username.getText().toString();
            String pass = passwd.getText().toString();

            if ((TextUtils.isEmpty(name) && checkLen(name, 5))||
                    (TextUtils.isEmpty(pass) && checkLen(pass, 5))){
                name = "Wrong Values";
                pass = "Wrong Values";
            }
            result.setText("Welcome " + name + "! you are stupid");
            result.setVisibility(View.VISIBLE);
        });
    }
    static boolean checkLen(String str, int permitted){
        return str.length() >= permitted;
    }
}
```

Above is the java code to handle the backend processing. `username.setError("Wrong value")` can be used to set an error if some kind of wrong field is received as a response.

Custom Edit texts can be used with more wide options like MaterialEditText but that needed to be added in dependencies to be used. more info [here](https://github.com/rengwuxian/MaterialEditText)

### TextInputLayout

This can be used as a wrapper around **EditText or TextInputEditText** which will give too much functionality to a EditText. Below is a xml code for a layout taking username, password and phone using TextInputLayout and using TextInputEditText as child (also contain 2 buttons and 1 textView).

```xml
<?xml version="1.0" encoding="utf-8" ?>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:divider="?actionBarDivider"
    android:showDividers="middle"
    android:gravity="center_horizontal"
    xmlns:app="http://schemas.android.com/apk/res-auto">


    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/username"
        style="@style/Widget.Material3.Button.OutlinedButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:boxCornerRadiusTopStart="30dp"
        app:boxCornerRadiusTopEnd="30dp"
        app:boxCornerRadiusBottomEnd="30dp"
        app:boxCornerRadiusBottomStart="30dp"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="15dp"
        android:layout_marginEnd="15dp"
        app:boxStrokeWidth="2dp"
        app:boxStrokeColor="@color/teal_200"
        app:boxStrokeErrorColor="#E80E0E"

        android:hint="Username"
        app:startIconDrawable="@drawable/user"
        app:startIconTint="@color/purple_500"
        app:endIconMode="clear_text"
        app:prefixTextColor="@color/red"
        app:prefixText="id."
        app:counterEnabled="true"
        app:counterMaxLength="20"
        app:counterOverflowTextAppearance="@style/TextAppearance.Compat.Notification.Info"
        app:helperTextEnabled="false"
        app:helperText="between 5-20"
        >
        <com.google.android.material.textfield.TextInputEditText
            android:inputType="text"
            android:minHeight="48dp"
            android:maxLength="20"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />

    </com.google.android.material.textfield.TextInputLayout>

    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/passwd"
        style="@style/Widget.Material3.Button.OutlinedButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:boxCornerRadiusTopStart="30dp"
        app:boxCornerRadiusTopEnd="30dp"
        app:boxCornerRadiusBottomEnd="30dp"
        app:boxCornerRadiusBottomStart="30dp"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="15dp"
        android:layout_marginEnd="15dp"
        app:boxStrokeWidth="2dp"
        app:boxStrokeColor="@color/teal_200"
        app:boxStrokeErrorColor="#E80E0E"

        android:hint="Password"
        app:startIconDrawable="@drawable/ic_baseline_lock_24"
        app:startIconTint="@color/purple_500"
        app:endIconMode="password_toggle"
        app:prefixTextColor="@color/ic_launcher_background"
        app:counterEnabled="true"
        app:counterMaxLength="10"
        app:helperText="between 6-10"
        app:helperTextEnabled="false"
        >

        <com.google.android.material.textfield.TextInputEditText
            android:inputType="textPassword"
            android:minHeight="48dp"
            android:maxLength="10"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />

    </com.google.android.material.textfield.TextInputLayout>


    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/phone"
        style="@style/Widget.Material3.Button.OutlinedButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"

        app:boxCornerRadiusTopStart="30dp"
        app:boxCornerRadiusTopEnd="30dp"
        app:boxCornerRadiusBottomEnd="30dp"
        app:boxCornerRadiusBottomStart="30dp"

        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="15dp"
        android:layout_marginEnd="15dp"

        app:boxStrokeWidth="2dp"
        app:boxStrokeColor="@color/teal_200"
        app:boxStrokeErrorColor="#E80E0E"

        android:hint="Phone"
        app:startIconDrawable="@drawable/ic_baseline_local_phone_24"
        app:startIconTint="@color/purple_500"
        app:endIconMode="custom"
        app:endIconDrawable="@drawable/ic_baseline_local_phone_24"
        app:prefixTextColor="@color/ic_launcher_background"
        app:counterEnabled="true"
        app:counterMaxLength="10"
        >

        <com.google.android.material.textfield.TextInputEditText
            android:inputType="phone"
            android:minHeight="48dp"
            android:maxLength="10"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />

    </com.google.android.material.textfield.TextInputLayout>


    <com.google.android.material.button.MaterialButton
        android:id="@+id/button0"
        android:layout_width="match_parent"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:text="Submit"
        android:enabled="false"
        android:textSize="20sp"
        android:layout_height="wrap_content"
        app:strokeColor="@color/purple_700"
        app:strokeWidth="3dp"
        />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button1"
        android:layout_width="match_parent"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:text="Useless"
        android:textSize="16sp"
        app:cornerRadius="30dp"
        app:icon="@drawable/no_drinks_24"
        app:iconGravity="textEnd"
        android:layout_height="wrap_content"
        />

    <TextView
        android:id="@+id/result"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="10dp"
        android:layout_marginStart="10dp"
        android:layout_marginEnd="10dp"
        android:layout_height="wrap_content"
        android:layout_width="match_parent"
        android:visibility="invisible"
        />

</LinearLayout>
```

TextInputLayout provides counter functionality which will show a counter for input chars. If input goes above given set value it will turn that red, but it can't stop taking input above that value. To restrict user to enter chars upto a limit set `maxLength` in `TextInputEditText`.

We can also set a text watcher for a field like during input in username or anyother field with every change in char value it will process according to text watcher methods.

There is the simple java code

```java
private Button useless, submit;
private TextInputLayout username, passwd, phone;
private EditText username0, passwd0, phone0;
private TextView result;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    submit = findViewById(R.id.button0);
    result = findViewById(R.id.result);

    username = findViewById(R.id.username);
    passwd = findViewById(R.id.passwd);
    phone = findViewById(R.id.phone);

    username0 = username.getEditText();
    passwd0 = passwd.getEditText();
    phone0 = phone.getEditText();

    username0.addTextChangedListener(watcher);
    passwd0.addTextChangedListener(watcher);
    phone0.addTextChangedListener(watcher);

    submit.setOnClickListener(view -> {
        if (username0.getText().toString().equals("bhavuksharma2202") &&
            passwd0.getText().toString().equals("123456")) {
            result.setText("Hello Bhavuk you are useless");
            username.setErrorEnabled(false);
            passwd.setErrorEnabled(false);
            Toast.makeText(this, "Wah bhai", Toast.LENGTH_SHORT).show();
        } else {
            result.setText("Kon hai be tu");
            username.setError("invalid");
            passwd.setError("invalid");
            Toast.makeText(this, "Daffa ho", Toast.LENGTH_SHORT).show();
        }
        result.setVisibility(View.VISIBLE);
    });
}
private final TextWatcher watcher = new TextWatcher() {
    @Override
    public void beforeTextChanged(CharSequence charSequence, int i, int i1, int i2) { }

    @Override
    public void onTextChanged(CharSequence charSequence, int i, int i1, int i2) {
        submit.setEnabled(!username0.getText().toString().trim().isEmpty() && !passwd0.getText().toString().trim().isEmpty()
                          && !phone0.getText().toString().trim().isEmpty());
        username.setErrorEnabled(false);
        passwd.setErrorEnabled(false);
    }

    @Override
    public void afterTextChanged(Editable editable) {}
};
```

## ImageView

These are used to add images to the application. It is simple to use and below is xml code snippet just for imageView

```xml
<ImageView
android:id="@+id/img"
android:layout_width="match_parent"
android:layout_height="250dp"
android:layout_marginStart="10dp"
android:layout_marginTop="5dp"
android:layout_marginEnd="10dp"
android:layout_marginBottom="5dp"

android:adjustViewBounds="true"
app:srcCompat="@drawable/android_logo"
android:contentDescription="Android Photo"
android:scaleType="fitCenter"
/>
```

`srcCompat` is the attribute which will be set as content of image View. `content description` is used by screen readers. `scaleType` is important as this will align the image in **ImageView**.

**Important:** `app:srcCompat` is used to integrate vector images and draw them. But `android:src` is used to draw images with their own resolution. For vector images one need to add this in build.gradel file

```java
android {
   defaultConfig {
     vectorDrawables.useSupportLibrary = true
    }
 }
```

For java code we are simply setting image in imageView according to a string we received from textEdit and after pressing submit button the image there will change.

```java
submit.setOnClickListener(view -> {
    String value = text.getText().toString().trim();
    if (value.equals(array[0])) image.setImageResource(R.drawable.space);
    else if (value.equals(array[1])) image.setImageResource(R.drawable.android_logo);
    else if (value.equals(array[2])) image.setImageResource(R.drawable.java);
    else text.setError("No value " + value);
});
```

### ShapeableImageView

To achive different type of images views one can use shapeableImageView, but for that you need some styles defined. Below xml file contains some styles **(place this file in `res/values`)**.

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>

    <style name="circular">
        <item name="cornerSize">50%</item>
    </style>

    <style name="RoundSquare">
        <item name="cornerSize">20%</item>
    </style>

    <style name="CornerCut">
        <item name="cornerSize">30%</item>
        <item name="cornerFamily"> cut</item>
    </style>

    <style name="DiamondCut">
        <item name="cornerSize">50%</item>
        <item name="cornerFamily">cut</item>
    </style>

    <style name="SpecificCornerCut">
        <item name="cornerSizeTopRight">20%</item>
        <item name="cornerSizeBottomLeft">20%</item>
        <item name="cornerFamily">cut</item>
    </style>

    <style name="SpecificCornerCurve">
        <item name="cornerSizeTopRight">30%</item>
        <item name="cornerSizeBottomLeft">30%</item>
        <item name="cornerFamily">rounded</item>
    </style>
</resources>
```

Each style can be applied by setting `app:shapeAppearanceOverlay="@style/styleName"`

Below is the xml code for different design layouts using above styles

```xml
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:divider="?actionBarDivider"
    android:showDividers="middle"
    android:gravity="center_horizontal"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <TableRow
        android:divider="?actionBarDivider"
        android:showDividers="middle"
        android:gravity="center_horizontal"
        >

    <com.google.android.material.imageview.ShapeableImageView
        android:id="@+id/circular"
        android:layout_width="180dp"
        android:layout_height="180dp"
        android:src="@drawable/square2"
        app:shapeAppearanceOverlay="@style/circular"
        />

    <com.google.android.material.imageview.ShapeableImageView
        android:id="@+id/value"
        android:layout_width="180dp"
        android:layout_height="180dp"
        android:src="@drawable/square2"
        app:shapeAppearanceOverlay="@style/circular"
        app:strokeWidth="5dp"
        app:strokeColor="#2196F3"
        />
    </TableRow>

    <TableRow
        android:divider="?actionBarDivider"
        android:showDividers="middle"
        android:gravity="center_horizontal"
        >

        <com.google.android.material.imageview.ShapeableImageView
            android:id="@+id/roundSquare"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:src="@drawable/square2"
            app:shapeAppearanceOverlay="@style/RoundSquare"
            />

        <com.google.android.material.imageview.ShapeableImageView
            android:id="@+id/sfa"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:src="@drawable/square2"
            app:shapeAppearanceOverlay="@style/CornerCut"
            />
    </TableRow>

    <TableRow
        android:divider="?actionBarDivider"
        android:showDividers="middle"
        android:gravity="center_horizontal"
        >

        <com.google.android.material.imageview.ShapeableImageView
            android:id="@+id/DiamondCut"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:src="@drawable/square2"
            app:shapeAppearanceOverlay="@style/SpecificCornerCurve"
            />

        <com.google.android.material.imageview.ShapeableImageView
            android:id="@+id/SpecificCorner"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:src="@drawable/square2"
            app:shapeAppearanceOverlay="@style/SpecificCornerCut"
            />
    </TableRow>

</TableLayout>
```

In java code this can be accessed and background image can be changed with below methods

```java
circular.setImageResource(R.drawable.space);
value.setImageResource(R.drawable.space);
RoundSquare.setImageResource(R.drawable.space);
sfa.setImageResource(R.drawable.space);
DiamondCut.setImageResource(R.drawable.space);
SpecificCorner.setImageResource(R.drawable.space);
```

**where circular, value, RoundSquare etc are ShapeableImageViews**.

there are other methods available also like `setBackgroundResource` and many more.

## CheckBox

There is the xml for checkbox, there are MaterialCheckBox also with some greater ability.

```xml
<CheckBox
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:checked="true"
        android:id="@+id/born"
        android:text="Born in 2000"
        />

<com.google.android.material.checkbox.MaterialCheckBox
        android:id="@+id/name"
        android:text="Name Starts with: A"
        android:checked="false"
        />

<CheckBox
        android:id="@+id/age"
        android:text="Age is 22 or 23"
        />
```

Some java code to control the above layout

```java
 submit.setOnClickListener(view -> {
     if (age.isChecked() && name.isChecked() && born.isChecked()){
         Toast.makeText(this, "you are the Special one for me", Toast.LENGTH_LONG).show();
     } else {
         age.setChecked(false);
         name.setChecked(false);
         born.setChecked(false);
         Toast.makeText(this, "You are not the Special one", Toast.LENGTH_LONG).show();
     }
 });
```

## RadioButtons

These are the buttons which are used to select one option from some bunch of other options. These are similar to CheckBoxes.

These need to be defined in **RadioGroup**. From one RadioGroup one can select a single item.

If a RadioButton is outside RadioGroup without having its own RadioGroup it can be selected with 1 item selected from RadioBox. Like if we have 5 RadioButtons and no one is wrapped in RadioGroup than all 5 can be selected once.

```xml
<RadioGroup
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:divider="?actionBarDivider"
        android:showDividers="middle"
        >

        <RadioButton
            android:id="@+id/yellow"
            android:text="Yellow"
            android:gravity="center_vertical"
            android:textSize="18sp"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            />

        <RadioButton
            android:id="@+id/blue"
            android:text="Blue"
            android:checked="true"
            android:textSize="18sp"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />

        <RadioButton
            android:id="@+id/red"
            android:text="Red"
            android:textSize="18sp"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />
</RadioGroup>
```

Java Code to handle these buttons or process on them

```java
blue = findViewById(R.id.blue);
yellow = findViewById(R.id.yellow);
red = findViewById(R.id.red);

submit = findViewById(R.id.submit);

submit.setOnClickListener(this::onClick);
}

private void onClick(View view) {
    if (blue.isChecked()) submit.setStrokeColor(ColorStateList.valueOf(Color.BLUE));
    else if (yellow.isChecked()) submit.setStrokeColor(ColorStateList.valueOf(Color.YELLOW));
    else if (red.isChecked()) submit.setStrokeColor(ColorStateList.valueOf(Color.RED));
    else submit.setStrokeColor(ColorStateList.valueOf(Color.TRANSPARENT));
}
```

blue, yellow, red are RadioButtons defined in a RadioGroup and submit is a materialButton.

## ToggleButton

This is a toggle button which will have only 2 values on and off. One can set onText and offText for this button

```xml
<ToggleButton
        android:id="@+id/toggle"
        android:layout_marginVertical="10dp"
        android:textOff="Kid Girl"
        android:textOn="Hot Girl"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@drawable/gradient2"
        />
```

To add a listener we need `setOnCheckedChangeListener` instead of `setOnClickListener`

```java
toggle.setOnCheckedChangeListener(this::onToggle);

 private void onToggle(CompoundButton compoundButton, boolean b){
     if (b) img.setImageResource(R.drawable.square2);
     else img.setImageResource(R.drawable.square);
 }
```

We can use this layout for a quiz app where toggle button will be used to show or hide the answer from the user.

## Spinner

This is a drop down selector. It will list a bunch of options from which we need to select one

Here is the xml code for Spinner

```xml
<TextView
          android:id="@+id/entry"
          android:text="Select Continent"
          android:textSize="22sp"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          />

<Spinner
         android:id="@+id/spinner"
         android:contentDescription="This is a selector"
         android:textAlignment="center"
         android:layout_width="200dp"
         android:layout_height="50dp"
         />
```

To make entries for a spinner one can specify entries with `android:entries="@array/countries"`. Here countries is a xml resource file which has values given as a string array and saved in values folder.

To make spinner connect with database we need to create an adapter which and we will use it to interact with backend.

```java
spinner = findViewById(R.id.spinner);
adapter = ArrayAdapter.createFromResource(this, R.array.Continents,
                                          android.R.layout.simple_spinner_item);

adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
spinner.setAdapter(adapter);
text = findViewById(R.id.result);

spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
    @Override
    public void onItemSelected(AdapterView<?> adapterView, View view, int i, long l) {
        String cont = adapterView.getItemAtPosition(i).toString();
        text.setText(cont);
        text.setVisibility(View.VISIBLE);
    }
    @Override
    public void onNothingSelected(AdapterView<?> adapterView) {}
});
```

## Creating Adapter

### Raw Adapter

```java
ArrayAdapter adapter;
adapter = ArrayAdapter.createFromResource(this,
    R.array.continents, android.R.layout.simple_spinner_dropdown_item);
adapter.dropDownViewResource(android.R.layout.simple_spinner_item);
// attach Adapter with a spinner
spinner.setAdapter(adapter);
```

### Generic Adapter

```java
ArrayAdapter<String> adapter;
adapter = new ArrayAdapter<String>(this,
                           android.R.layout.simple_spinner_item,
                                  gerResources().getStringArray(
                                  	R.array.Countries)
                                  );
// below line is not necessary
adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
// attach Adapter with spinner
spinner.setAdapter(adapter);
```

# User Interactions

## Toast

`Toast.makeText(this, "Hey there", Toast.LENGTH_SHORT).show();`

### Custom Toast

custom_toast is a xml file defined in drawable folders.

```java
LayoutInflater inflater = getLayoutInflater();
View layout = inflater.inflate(R.layout.custom_toast, (ViewGroup) 							findViewById(R.id.layout));

Toast toast = new Toast(getApplicationContext());
toast.setGravity(Gravity.CENTER, 0 , 0);
toast.setDuration(Toast.LENGTH_LONG);
toast.setView(layout);

button = findViewById(R.id.button);

button.setOnClickListener(view -> {
    toast.show();
});
```

Values for textView in custom toast or ImageView can be changed by finding the value within layout using findViewById

```java
TextView text;
text = layout.findViewById(R.id.text);
text.setText("New value");

// Similar for ImageView
ShapeableImageView image;
image = layout.findViewById(R.id.image);
image.setImageResource(R.drawable.image2);
```

**custom_toast.xml file below**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/layout"
    android:background="#29ACE4"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">

    <com.google.android.material.imageview.ShapeableImageView
        android:id="@+id/image"
        android:contentDescription="Useless image"
        android:src="@drawable/square"
        app:shapeAppearanceOverlay="@style/circular"
        android:layout_width="60dp"
        android:layout_height="60dp"
        />
    <TextView
        android:id="@+id/text"
        android:paddingHorizontal="10dp"
        android:textColor="@color/blue"
        android:textSize="24sp"
        android:text="Toast"
        android:layout_width="match_parent"
        android:layout_height="60dp"
        />

</LinearLayout>
```

[this is another way to define custom toast](https://stackoverflow.com/questions/16788827/change-text-and-icon-in-a-custom-toast/16789027#16789027)

## Snackbar Message

This is similar to Toast message but can be modified to do an action on pressing a button. Passing application context to snackbar message may cause Application to crash.

```java
table = findViewById(R.id.table);
button = findViewById(R.id.button);

button.setOnClickListener(view -> {
    Snackbar.make(context: table, "This is Snack", Snackbar.LENGTH_SHORT).
        setAction("Close", view1 -> {}).show();
});
```

Button can be set with `setAction` method. 1st parameter to this method will be the text for the button. 2nd parameter will be the method which will be called when button is pressed. If the method is empty than it will simply close the **Snackbar** message.

## Dialog Message

Dialog Message should use activity context, if application context is used it will give an error. One can get **Application context** with

> getApplication()
>
> getApplicationContext()
>
> getBaseContext() // offers activity context
>
> MainActivity.this // offers activity context

implementation of Dialog message is below

```java
button.setOnClickListener(view -> showDialogMessage());
}

private void showDialogMessage() {
    AlertDialog.Builder alert = new AlertDialog.Builder(this);
    alert.setTitle("Delete").setMessage("Do you want to make button invisible").
        setNegativeButton("No", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                button.setText("Negative");
                dialogInterface.cancel();
            }
        })
        .setPositiveButton("Yes", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                button.setText("Positive");
            }
        }).show();
    alert.create();
}
```

We need to create a AlertDialog by passing the activity context not application context.

1. `setTitle:` will set the title for the dialog box
2. `setMessage:` will set the dialog message question
3. `setNegativeButton:` will set the negative button
4. `setPositiveButton:` will set the positive button
5. in the end we need to use `.show()` method
6. `dialogInterface.cancel()` to close the dialog
7. `alert.setCancelable(false):` So that it can't get canceled with back button.

# List and Views

## List View

ListView is kind of a scrollable view which can contain many elements. To add elements in ListView we need to set an adapter for the ListView.

```xml
    <ListView
        android:id="@+id/list"
        android:layout_width="374dp"
        android:layout_height="532dp"
        android:layout_marginTop="23dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
```

This is the way to set ListView.

**Creating adapter for ListView**

```java
ArrayAdapter<String> adapter;
String[] array = getResources().getStringArray(R.array.countries);
adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_checked, array);
```

**Attaching the Adapter with Listview**

```java
ListView listView;
listView = findViewById(R.id.list);
listView.setAdapter(adapter);
```

**Adding listener to listview**

```java
list.setOnItemClickListener(new AdapterView.OnItemClickListener() {
    @Override
    public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
        String value = adapterView.getItemAtPosition(i).toString();
        Toast.makeText(getBaseContext(), "You selected " + value , Toast.LENGTH_LONG).show();
    }
});
```

In above method the over-ridden method **onItemClick**, adapterView is AdapterView, and value i represents the position of the clicked item. So with `adapterView.getItemAtPosition(i)` will return the item itself.

## Recycler View

Here we need to create a design format for elements in RecyclerView, which will be another layout file containing some xml code.

**card_design.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:paddingVertical="4dp"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <androidx.cardview.widget.CardView
        android:id="@+id/cardView"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:paddingVertical="5dp"
        app:cardCornerRadius="15dp"
        app:cardElevation="12dp"
        android:backgroundTint="#343438"
        app:layout_constraintDimensionRatio="5"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_gravity="start"
            android:paddingHorizontal="5dp"
            android:paddingVertical="5dp"
            app:layout_constraintBottom_toBottomOf="@+id/country_name"
            app:layout_constraintTop_toBottomOf="@+id/country_name">

            <TextView
                android:id="@+id/country_name"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginStart="20dp"
                android:text="Country"
                android:textSize="20sp"
                android:textStyle="bold"
                app:layout_constraintBottom_toTopOf="@+id/information"
                app:layout_constraintStart_toEndOf="@+id/flag"
                app:layout_constraintTop_toTopOf="parent" />

            <TextView
                android:id="@+id/information"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="about country"
                android:textSize="16sp"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintStart_toStartOf="@+id/country_name"
                app:layout_constraintTop_toBottomOf="@+id/country_name" />

            <com.google.android.material.imageview.ShapeableImageView
                android:id="@+id/flag"
                android:layout_width="0dp"
                android:layout_height="0dp"
                android:layout_margin="10dp"
                android:paddingHorizontal="5dp"
                android:paddingVertical="5dp"
                android:scaleType="centerCrop"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintHeight_percent="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                app:layout_constraintWidth_percent="0.15"
                app:shapeAppearanceOverlay="@style/RoundSquare"
                app:srcCompat="@drawable/australia"
                app:strokeColor="@color/red"
                app:strokeWidth="2dp" />

        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.cardview.widget.CardView>

</androidx.constraintlayout.widget.ConstraintLayout>
```

Above design contains a Constraint layout which contains a **CardView** again containing a Constraint layout. Now that inner Constraint layout contains some other layouts as **ImageView, TextView**.

**activity_main.xml** (only **RecyclerView** tag shown here)

```xml
<androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="10dp"
        android:layout_marginTop="16dp"
        android:layout_marginEnd="10dp"
        tools:listitem="@layout/card_design"
        android:orientation="horizontal"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintDimensionRatio="1.5"
        app:layout_constraintTop_toTopOf="parent" />
```

Now rest of the work lies in the java part.

1. Create data fields for data to be filled in different elements of CardView i.e. Images, Strings
2. Create a RecyclerView object pointing to RecyclerView with `findViewById(R.id.recycler)`
3. Create a new class for a Adapter to Recycler extending `RecyclerView.Adapter <RecyclerAdapter.CountryViewHolder>`
4. Create a constructor for the class taking context as context may be a requirement in different parts of the code
5. Now create a inner class `public class CountryViewHolder extends RecyclerView.ViewHolder`

   1. Create super constructor. itemView in `super(itemView)` will be a view pointing to the view holding custom_toast layout So this should be used to modify elements in the custom_toast.

6. Implement all the abstract methods
   1. `public int getItemCount()`,
   2. `public CountryViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType)`
   3. `public void onBindViewHolder(@NonNull CountryViewHolder holder, int position)`
7. `getItemCount` will simply give the number of element to be created for RecyclerView
8. `onCreateViewHolder` will create a View for Recycler elements, which is done with LayoutInflater and this View will be returned from this method. This is where we attach `custom_card.xml` to the recyclerView elements
9. `onBindViewHolder` is used to modify the elements in recyclerView i.e. setting or modifying textViews, ImageViews, Buttons etc.

Below is the java code for ActivityMain.java

```java
package com.redheadhammer.testing;


import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import android.os.Bundle;

import java.util.ArrayList;


public class MainActivity extends AppCompatActivity{

    private RecyclerView recyclerView;
    private  RecyclerAdapter adapter;

    private final ArrayList<String> countries = new ArrayList<>();
    private final ArrayList<String> detailList = new ArrayList<>();
    private final ArrayList<Integer> countryFlags = new ArrayList<>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Create Layout Manager for recyclerView
        recyclerView = findViewById(R.id.recycler);
        recyclerView.setLayoutManager(new LinearLayoutManager(MainActivity.this));

        countries.add("Argentina");
        countries.add("Australia");
        countries.add("Canada");
        countries.add("India");
        countries.add("NewZealand");

        detailList.add("Country in South-America");
        detailList.add("Country in Oceania Region");
        detailList.add("Country in North-America");
        detailList.add("Country in Asia");
        detailList.add("Country in Oceania Region");

        countryFlags.add(R.drawable.argentina);
        countryFlags.add(R.drawable.australia);
        countryFlags.add(R.drawable.canada);
        countryFlags.add(R.drawable.india);
        countryFlags.add(R.drawable.newzeland);

        adapter = new RecyclerAdapter(getBaseContext(), countries, detailList, countryFlags);
        recyclerView.setAdapter(adapter);

    }
}
```

Below is the code for **RecyclerAdapter.java**

```java
package com.redheadhammer.testing;

import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.cardview.widget.CardView;
import androidx.recyclerview.widget.RecyclerView;

import java.util.ArrayList;

public class RecyclerAdapter extends  RecyclerView.Adapter<RecyclerAdapter.CountryViewHolder>{
    Context context;
    ArrayList<String> countries;
    ArrayList<String> detailList;
    ArrayList<Integer> flagImages;


    public RecyclerAdapter(Context context, ArrayList<String> countries,
                           ArrayList<String> detailList, ArrayList<Integer> flagImages) {
        this.context = context;
        this.countries = countries;
        this.detailList = detailList;
        this.flagImages = flagImages;
    }

    // connect the custom_design with recycler View (So it is the reason recycler view know which design to display)
    @NonNull
    @Override
    public CountryViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.card_design,
                parent, false);

        return new CountryViewHolder(view);
    }

    // to show data in recycler view with data passed
    @Override
    public void onBindViewHolder(@NonNull CountryViewHolder holder, int position) {
        holder.country.setText(countries.get(position));
        holder.detail.setText(detailList.get(position));
        holder.flag.setImageResource(flagImages.get(position));

        holder.card.setOnClickListener(view -> {
            Toast toast = new Toast(context);
            toast.setDuration(Toast.LENGTH_SHORT);
            toast.setText("You selected: " + countries.get(position));
            toast.show();
        });
    }

    // total no. of cards to view
    @Override
    public int getItemCount() { return countries.size(); }

    public static class CountryViewHolder extends RecyclerView.ViewHolder {
        TextView country;
        TextView detail;
        ImageView flag;
        CardView card;

        public CountryViewHolder(@NonNull View itemView) {
            super(itemView);
            country = itemView.findViewById(R.id.country_name);
            detail = itemView.findViewById(R.id.information);
            flag = itemView.findViewById(R.id.flag);
            card = itemView.findViewById(R.id.cardView);
        }
    }
}
```

## GridView

This will add the elements in vertical and horizontally without any big effort.

**xml code for activity_main**

```xml
<?xml version="1.0" encoding="utf-8" ?>

<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/table"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:clipToPadding="true"
    android:divider="?actionBarDivider"
    android:gravity="center_horizontal"
    android:orientation="vertical"
    android:showDividers="middle">

    <GridView
        android:id="@+id/grid"
        android:gravity="center"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHeight_percent="0.98"
        app:layout_constraintWidth_percent="0.95"
        app:layout_constraintVertical_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:numColumns="3"
        tools:listitem="@layout/grid_element"
        >
    </GridView>

</androidx.constraintlayout.widget.ConstraintLayout>
```

Now we need to define a custom layout i.e. `grid_element` here to define element layout in grid

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="100sp"
    android:layout_height="wrap_content"
    android:orientation="vertical">

    <ImageView
        android:id="@+id/image"
        android:src="@drawable/australia"
        android:layout_width="match_parent"
        android:layout_height="70sp"
        />

    <TextView
        android:id="@+id/text"
        android:text="@string/app_name"
        android:textSize="24sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        />


</LinearLayout>
```

This is again similar with RecyclerView as we have to create a custom adapter with below java code.

```java
public class GridAdapter extends BaseAdapter {
    Context context;
    ArrayList<String> countries;
    ArrayList<Integer> flags;
    TextView text;
    ImageView image;

    public GridAdapter(Context context, ArrayList<String> countries, ArrayList<Integer> flags) {
        this.context = context;
        this.countries = countries;
        this.flags = flags;
    }

    @Override
    public int getCount() {
        return countries.size();
    }

    @Override
    public Object getItem(int i) {
        return i;
    }

    @Override
    public long getItemId(int i) {
        return i;
    }

    @Override
    public View getView(int i, View view, ViewGroup viewGroup) {
        @SuppressLint("ViewHolder") View newView = LayoutInflater.from(this.context).inflate(R.layout.grid_element,
                        viewGroup, false);

        text = newView.findViewById(R.id.text);
        image = newView.findViewById(R.id.image);

        text.setText(countries.get(i));
        image.setImageResource(flags.get(i));
        return newView;
    }
}
```

and Now we can modify the **MainActivity.java** as below

```java
public class MainActivity extends AppCompatActivity{

    GridView gridView;

    private final ArrayList<String> countries = new ArrayList<>();
    private final ArrayList<Integer> countryFlags = new ArrayList<>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        fill();
        gridView = findViewById(R.id.grid);

        GridAdapter gridAdapter = new GridAdapter(this, countries, countryFlags);
        gridView.setAdapter(gridAdapter);

        gridView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
                TextView textView = view.findViewById(R.id.text);
                String value = textView.getText().toString();
                Toast.makeText(getBaseContext(), "You selected: " + value, Toast.LENGTH_SHORT).show();
            }
        });
    }
    public void fill(){
        countries.add("Argentina");
        countryFlags.add(R.drawable.argentina);

        countries.add("Australia");
        countryFlags.add(R.drawable.australia);

        countries.add("Canada");
        countryFlags.add(R.drawable.canada);

        countries.add("India");
        countryFlags.add(R.drawable.india);

        countries.add("New Zealand");
        countryFlags.add(R.drawable.newzeland);
    }
}
```

## ScrollView

This will add the ability of scrolling in a view. To implement this on a Layout just wrap the target layout in ScrollView like below.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView
    android:divider="?actionBarDivider"
    android:showDividers="middle"
    android:dividerPadding="5dp"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity"
    android:layout_gravity="center"
    android:padding="10dp"
    >

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler"
        android:layout_gravity="center_horizontal"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        />

</ScrollView>
```

**Like ScrollView Horizontal ScrollView is also a thing which can be implemented like ScrollView**. We just have to wrap the Layout with `HorizontalScrollView.`

To scroll the elements to the right we can run

- `binding.scroll.fullScroll(HorizontalScrollView.FOCUS_RIGHT)`
- if view is not scrolling to the last element it maybe because layout isn't done building itself and scrollView scroll itself. This can be resolved with a delay with `binding.scroll.postDelayed(() -> binding.scroll.fullScroll(HorizontalScrollView.FOCUS_RIGHT), 100);`
- Above method will add a delay of particular time in the scrolling but we can simply put the **Right Scroll** to start after current iteration of UI Loop with `binding.scroll.post(() -> binding.scroll.fullScroll(HorizontalScrollView.FOCUS_RIGHT));`
- Use `android:fillViewport="true"` to strech the ScrollView's contents.

## WebView

WebViews are the views which can load an url in allowed space in the application. If your intention is to create an application with only WebView don't create any layout for activity_main. Just create a webView and `setContentView` to the WebView itself and load the url as intended.

```java
public class MainActivity extends AppCompatActivity {

    WebView webView = new WebView(getBaseContext());

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(webView);
        webView.loads("https://developer.android.com/");
```

Or one can create a layout with some Buttons or EditTexts in it as below one.

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    android:divider="?actionBarDivider"
    android:showDividers="middle"
    android:dividerPadding="5dp"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity"
    android:layout_gravity="center"
    >

    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/textInputLayout"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintTop_toBottomOf="@+id/webView"
        app:layout_constraintStart_toStartOf="@+id/webView"
        app:layout_constraintEnd_toEndOf="@+id/webView"
        app:layout_constraintWidth_percent="0.9"
        app:layout_constraintHeight_percent="0.1"
        app:boxCornerRadiusTopStart="5dp"
        app:boxCornerRadiusTopEnd="5dp"
        app:boxCornerRadiusBottomEnd="5dp"
        app:boxCornerRadiusBottomStart="5dp"
        app:boxStrokeColor="@color/teal_700"
        app:boxStrokeWidth="5dp"
        app:endIconMode="clear_text"
        app:prefixText="https://"
        app:prefixTextColor="@color/red"
        >
        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/url"
            android:hint="@string/url"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="textUri"
            />
    </com.google.android.material.textfield.TextInputLayout>

    <WebView
        android:id="@+id/webView"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintHeight_percent="0.7"
        app:layout_constraintWidth_percent="0.9"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintVertical_bias="0.15"
        />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button"
        android:text="@string/Button0"
        android:layout_width="0dp"
        android:layout_height="0dp"
        style="@style/Widget.Material3.Button.OutlinedButton"
        app:layout_constraintStart_toStartOf="@+id/webView"
        app:layout_constraintEnd_toEndOf="@+id/webView"
        app:layout_constraintTop_toBottomOf="@+id/textInputLayout"
        app:layout_constraintDimensionRatio="6"
        />

  </androidx.constraintlayout.widget.ConstraintLayout>
```

Now in java code attach Views from `main_activity`.

1. Before doing anything just **give Internet permission** to the application from manifest file with

   1. ```xml
      <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
      ```

   2. ```xml
      <uses-permission android:name="android.permission.INTERNET"
      ```

2. **Set a WebView Client** for the webView otherwise all the links will open in default browser `webView.setWebViewClient(new WebViewClient)`

3. Access WebSettings with `WebSettings webSettings = webView.getSettings()` and enable javaScript with `webSettings.setJavaScriptEnabled(true)`

4. **Load a link** with webView.loadUrl("https://developers.android.com");

5. **To load a link with no encryption i.e. http** we need to set `android:usesCleartextTraffic="true"` in manifest file in application tag

Below is the MainActivity.java file

```java
package com.redheadhammer.a0_another;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.text.TextUtils;
import android.view.View;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.Button;

import com.google.android.material.textfield.TextInputEditText;


public class MainActivity extends AppCompatActivity {

    WebView webView;
    TextInputEditText url;
    Button button;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        webView = findViewById(R.id.webView);
        url = findViewById(R.id.url);
        button = findViewById(R.id.button);

        button.setOnClickListener(this::onClick);
    }

    public void onClick(View view) {
        String web;
        if (!TextUtils.isEmpty(url.getText()))
            web = "https://" + url.getText().toString();
        else web = getResources().getString(R.string.default_url);

        // will open link in webView not in external browser
        webView.setWebViewClient(new WebViewClient());
		// webView.setWebChromeClient(new WebChromeClient());
        WebSettings webSettings = webView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        // to load a link
        webView.loadUrl(web);
    }

    @Override
    public void onBackPressed() {
        if (webView.canGoBack()) webView.goBack();
        else super.onBackPressed();
    }
}
```

If we press back button our application will close if we didn't modified the `onBackPressed` method.

## GridView

This is similar to Recycler View but it can have columns too. **As per official developer android website:** A view that shows items in two-dimensional scrolling grid. The items in the grid come from the `ListAdapter` associated with this view.

```xml
<GridView
        android:id="@+id/grid_numbers"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintHeight_percent="0.472"
        android:gravity="center"
        android:numColumns="4"
        android:paddingTop="6dp"
        android:paddingHorizontal="5dp"
        android:listSelector="@android:color/transparent"
        tools:listitem="@layout/button_item"
        tools:visibility="invisible"
        android:stretchMode="columnWidth"
        android:horizontalSpacing="10dp"
        android:verticalSpacing="5dp"
        />
```

1. `numsColumns` will set the number of columns in the grid. If there is no particular number we can always set for gridView to set those flexibly with `android:numsColumns:"autofit"` or if we have a number we can directly set it to 3,4 etc.
2. `horizontalSpacing` will set the spacing between columns and `verticalSpacing` will set the the spacing between rows.
3. `stretchMode` defines how columns should stretch to fill empty space if any.
4. Set `listSelector` to transparent, So on clicking it should not show any effects, in case we are defining our custom click effects.

**To Connect data to the GridView, we need to create an Adapter as we needed in Recycler**

1. Create a `GridAdapter extending BaseAdapter` and implement abstract methods.
2. Set `getCount's` return value as data length or array size we are showing content from.
3. Now we need to create view from layout file which can be done with LayoutInflater and this needs to be done in `getView` method.
4. Now create the adapter in Activity which contains the GridView and set it with `gridView.setAdapter(new MyCustomAdapter());`

**Adapter Class**

```java
public class GridAdapter extends BaseAdapter {

    private final String[] button_values;
    private final Context context;
    public GridAdapter(String[] values, Context context) {
        this.button_values = values;
        this.context = context;
    }

    @Override
    public int getCount() {
        return button_values.length;
    }

    @Override
    public Object getItem(int position) {
        return null;
    }

    @Override
    public long getItemId(int position) {
        return 0;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        if (convertView == null) {
            LayoutInflater inflater = (LayoutInflater) context.getSystemService(
                    Context.LAYOUT_INFLATER_SERVICE);
            convertView = inflater.inflate(R.layout.button_item, parent, false);
        }
        TextView text = convertView.findViewById(R.id.keypad_item);
        text.setText(
                this.button_values[position]
        );
        return convertView;
    }
}
```

**Using in Activity Class**

```java
binding = ActivityMainBinding.inflate(getLayoutInflater());
setContentView(binding.getRoot());

binding.gridNumbers.setAdapter(new GridAdapter(
    getResources().getStringArray(R.array.grid_buttons),
    MainActivity.this
));

binding.gridNumbers.setOnItemClickListener(((parent, view, position, id) ->
                            Toast.makeText(
									MainActivity.this,
						            "You clicked " + getResources()
                                    .getStringArray(R.array.grid_buttons)[position],
                                     Toast.LENGTH_SHORT).show()                                          ));
```

## GridLayout

GridLayout is similar to GridView visually but to in GridLayout we have to define every element seprately unlike gridView.

**Grid Layout Element**

- `layout_row` will specify row number of the element
- `layout_column` will specify column number of the element
- `layout_columnWeight` will specify space allowed to the element in a Column
- `layout_rowWeight` will specify space allowed to the element in a Row
- `layout_rowSpan` will specify how many rows given element can capture. (This can be used to show a button with higher importance like = button in some calculators)
- `layout_columnSpan` will specify how many columns given element can capture. (This is similar to `layout_rowSpan` but will increase width of the element)

```xml
<GridLayout
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="1"
            android:rowOrderPreserved="true"
            android:rowCount="3"
            android:columnCount="4"
            >

    <TextView
              android:text="TextView 0-0"
              android:layout_rowWeight="1"
              android:layout_columnWeight="1"
              android:layout_row="0"
              android:layout_column="0"
              android:background="@color/teal_200"
              />

    <TextView
              android:text="TextView 0-1"
              android:layout_rowWeight="1"
              android:layout_columnWeight="1"
              android:layout_row="0"
              android:layout_column="1"
              android:layout_rowSpan="2"
              android:background="@color/purple_200"
              />

    <TextView
              android:text="TextView 0-1"
              android:layout_rowWeight="1"
              android:layout_columnWeight="1"
              android:layout_row="1"
              android:layout_column="0"
              android:background="@color/teal_700"
              />

    <TextView
              android:text="TextView 1-1"
              android:layout_rowWeight="1"
              android:layout_columnWeight="1"
              android:layout_row="2"
              android:layout_column="0"
              android:layout_columnSpan="2"
              android:background="@color/teal_200"
              />
</GridLayout>
```

# Components and LifeCycles

## Application Lifecycle

Application has a lifecycle itself. When Application is lauched it will call `onCreate()` method followed by many other method calls for app to work properly

- **On lauching an app** after `onCreate`, `onStart` and `onResume` methods will be called which will keep the activity running.
- **On Switching Activity** Application will call `onPause` method will be called, when user gets back to the current activity it will call `onResume` again.
- **Putting the Application in background** will call `onStop` method and when user gets back to the application itself `onRestart` method will be called followed by `onStart` and `onResume`
- **On closing the app** will call `onDestroy` method.

These methods can be used in the `MainActivity.java` class like onCreate

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Log.d("DEBUG", "onCreate: ");
    }

    @Override
    public void onBackPressed() {
        Log.d("DEBUG", "onBackPressed");
        super.onBackPressed();
    }

    @Override
    protected void onStart() {
        Log.d("DEBUG", "onStart");
        super.onStart();
    }

    @Override
    protected void onResume() {
        Log.d("DEBUG", "onResume");
        super.onResume();
    }

    @Override
    protected void onPause() {
        Log.d("DEBUG", "onPause");
        super.onPause();
    }

    @Override
    protected void onStop() {
        Log.d("DEBUG", "onStop");
        super.onStop();
    }

    @Override
    protected void onDestroy() {
        Log.d("DEBUG", "onDestroy");
        super.onDestroy();
    }
}
```

These methods can be used to save any work during various stages of apps like going to background, onClosing etc.

## Activity Lifecycle

1st activity will launch by calling these in order `onCreate(), onStart(), onResume()` when 2nd Activity will be called 1st activity will goes to a pause and will call `onPause()`. Now 2nd activity will start and call these in order `onCreate(), onStart(), onResume()`. When `onResume()` will be called for 2nd activity it will stop the 1st activity by calling `onStop()` on 1st activity.

One can test this by creating another activity and calling it wil below code.

```java
Intent second = new Intent(getApplicationContext(), MainActivity2.class);
startActivity(second);
```

When phone is rotated Activity is destoryed and created again. So all the data will be lost if not saved before or during `onDestroy` call.

### Activity Backstack

- `finishAffinity()` will clear the whole activity stack except the current activity.
- calling `finish()` right after launching activity will remove that activity from stack.
- Override `onBackPressed()` for any custom action

### Dark Mode Checker

```java
public boolean checkDarkTheme(){
        int theme = getApplicationContext().getResources().getConfiguration().
                uiMode & Configuration.UI_MODE_NIGHT_MASK;
        return (theme & Configuration.UI_MODE_NIGHT_YES) != 0;
    }
```

Change Dark Mode

```java
toggle.setOnCheckedChangeListener((compoundButton, isChecked) -> {
    if (isChecked)
        AppCompatDelegate.setDefaultNightMode(AppCompatDelegate.MODE_NIGHT_YES);
    else
        AppCompatDelegate.setDefaultNightMode(AppCompatDelegate.MODE_NIGHT_NO);
});
```

## Fragment LifeCycle

Fragments are very important part of an application and moreover it is considered good practise to use these whenever you can because they are more performant than activities.

### Frame Layout

activity_main.xml (only FrameLayout)

```xml
<FrameLayout
             android:id="@+id/fragment"
             android:layout_width="0dp"
             android:layout_height="0dp"
             app:layout_constraintHeight_percent="0.85"
             app:layout_constraintWidth_percent="0.95"
             app:layout_constraintStart_toStartOf="parent"
             app:layout_constraintEnd_toEndOf="parent"
             app:layout_constraintTop_toTopOf="parent"
             app:layout_constraintBottom_toTopOf="@id/fragment1"
             />
```

create layouts and classes for different fragments. like below

A fragment java class will look like below

```java
public class FirstFragment extends Fragment {

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_first, container, false);
    }
}
```

It may contain other methods as per its lifecycle and other methods. **onCreateView** method is important to override as that is the one creating the view for fragment. We also need to create a layout file by the name as passed to inflater (**fragment_first** here. To use this or create fragment in FrameLayout we have to create the FragmentManager in main activity as below

```java
private void replace(Fragment fragment) {
        FragmentManager fragmentManager = getSupportFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        fragmentTransaction.replace(R.id.fragment, fragment);
        fragmentTransaction.commit();
    }
```

With replace method one can replace the fragment in FrameLayout.

When a fragment is created it will call these functions in order `onAttach, onCreate, onCreatView, onStart, onResume` and this will keep running the fragment. When a fragment is killed it will call these function in order again `onPause, onStop, onDestroyView, onDestroy, onDeattach`.

### fragments

## Services

It is android component that works in background and can be helpful for long running tasks. Services doesn't need any design interface. Another application interface can start a service

3 types of services in Android

- **Forground Service**
- **BackGround Services**
- **Bound Service**

There are 2 types of **Service Classes**

- **Standard Service Class** (This will use the same thread as the application so may affect app performance)
- **Intent Service Class** (Will extends )

We need to add service class to **Manifest file** for it to work properly. `<service android:name=".SomeService"/>` where SomeService is the class name. Remeber to add `<service>` tag in `<application>` tag.

In the below layout we have created 2 buttons 1 to start a service and another to stop the service. Both buttons onClickListeners are defined below

```java
frg1 = findViewById(R.id.fragment1);
frg2 = findViewById(R.id.fragment2);

frg1.setOnClickListener(view -> {
    Intent service = new Intent(getApplicationContext(), SomeService.class);
    startService(service);
});

frg2.setOnClickListener(view -> {
    Intent service = new Intent(getApplicationContext(), SomeService.class);
    stopService(service);
});
```

Below is the code for `SomeService class` defined in Manifest as well as in `MainActivity.java` while creating intent for service

```java
public class SomeService extends Service {

    @Override
    public void onCreate() {
        super.onCreate();
        Log.i("INFO", "onCreate");
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        Log.i("INFO", "onDestroy");
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Log.i("INFO", "onStart");
//        stopSelf();
        return super.onStartCommand(intent, flags, startId);
    }

    @Override
    public IBinder onBind(Intent intent) {
        // TODO: Return the communication channel to the service.
        throw new UnsupportedOperationException("Not yet implemented");
    }
}
```

While starting the service it will call these methods in order `onCreate, onStartCommand` . If one wants to stop the service `onDestroy` will be called.

## Broadcast Receiver

Broadcast receiver is a way for Application and Operating system to interact on different events. If an application wants an info related to something it needs to be subscribed to that service. For e.g. If application is subscribed to Battery low service, Broadcaster will broadcast when battery is low and send the a message to all the subscribed applications. Similar warnings can be issued for various other tasks (i.e. Airplane Mode, Wifi State, Charging etc.).

When a broadcast is sent, the system automatically routes the broadcast to apps that have subscribed to receive that particular type of broadcast.

Broadcast Messages can be used between 2 applications but mostly it is used in between system and application.

**From API level 26 (Orio)** BroadCast Reciver must be created in java class not manifest file. and for below API Levels create it in the Manifest file.

In Manifest file add

```xml
<receiver android:name=".Broadcast"
          android:exported="false">
    <intent-filter>
        <action android:name="android.intent.action.ACTION_POWER_CONNECTED"/>
        <action android:name="android.intent.action.AIRPLANE_MODE"/>
    </intent-filter>
</receiver>
```

where `.Broadcast` is the name of the BroadCast receiver class code for which is given below

```java
public class Broadcast extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context, "Airplane Mode", Toast.LENGTH_SHORT).show();
    }
}
```

while sending a Braodcast message system also sends a boolean value which can be fetched with

```java
boolean isPlaneMode = intent.getBooleanExtra("state", false);
```

on isPlaneMode true device will in Airplane mode.

**These type of receivers which are defined in manifest file are called `context register receivers `.**

Nothing different we just need to remove the BroadCast from Manifest file and than declare it in `MainActivity.java` file. We need to register the BroadCaster in `onStart` method and unregister in `onStop` method because if we create it in `onCreate` method, it will receive the broadcast when it is in background if app is not distroyed. So this is how one should do it

```java
public class MainActivity extends AppCompatActivity {

    // Broadcast is the class defined above
    Broadcast broad = new Broadcast();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    protected void onStart() {
        super.onStart();
        IntentFilter filter = new IntentFilter();
        filter.addAction(Intent.ACTION_AIRPLANE_MODE_CHANGED);

        this.registerReceiver(broad, filter);
    }

    @Override
    protected void onStop() {
        super.onStop();
        this.unregisterReceiver(broad);
    }
}
```

### Checking Internet Connection with BroadCast Receiver

`InternetStatus` class will check if internet is connected or not.

```java
public class InternetStatus {

    public static boolean checkStatus(Context context) {
        ConnectivityManager connectivityManager = (ConnectivityManager) context.getSystemService(
                Context.CONNECTIVITY_SERVICE);

        NetworkInfo networkInfo = connectivityManager.getActiveNetworkInfo();
        if (networkInfo != null) {
            return true;
        } else {
            return false;
        }
    }
}
```

`InternetReceiver` class will extends `BroadcastReceiver` and will be activated whenever **Connection change is received**. To know the connectivity status it will use `InternetStatus` class (defined above).

**NOTE:- INSTEAD OF CREATING A FULLY NEW CLASS ONE CAN ALSO CREATE A PRIVATE METHOD IN BELOW CLASS TO CHECK INTERNET STATUS**

```java
public class InternetReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        Log.d("DEBUG", "Broadcast received");
        boolean connected = InternetStatus.checkStatus(context);
        Toast.makeText(context, "Connection " + connected,
                Toast.LENGTH_LONG).show();
    }
}
```

Below is `MainActivity.java` class. In here we are creating the Receiver and registering it onStart and unregistering it onStop.

```java
public class MainActivity extends AppCompatActivity{
    InternetReceiver internetReceiver;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        internetReceiver = new InternetReceiver();

    }

    @Override
    protected void onStart() {
        super.onStart();
        IntentFilter filter = new IntentFilter();
        filter.addAction(ConnectivityManager.CONNECTIVITY_ACTION);
        this.registerReceiver(internetReceiver, filter);
        Log.d("DEBUG", "Registering receiver");
    }

    @Override
    protected void onStop() {
        super.onStop();
        this.unregisterReceiver(internetReceiver);
        Log.d("DEBUG", "unregistering receiver");
    }
}
```

## Intent

It is android component which can bind 2 components at runtime i.e. activity to another activity, activity to a service.

We need to create 2 activities, Main and Secandary. Will call Secandary from MainActivity with the help of intent

layouts for both activities (**main_activity**)

```xml
<?xml version="1.0" encoding="utf-8" ?>

<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/table"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:clipToPadding="true"
    android:divider="?actionBarDivider"
    android:gravity="center_horizontal"
    android:orientation="vertical"
    android:showDividers="middle">

    <EditText
        android:id="@+id/username"
        android:layout_marginHorizontal="10dp"
        android:hint="@string/username"
        android:inputType="text"
        android:autofillHints="username"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintWidth_percent="0.9"
        app:layout_constraintHeight_percent="0.09"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toTopOf="@id/submit"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        />

    <Button
        android:id="@+id/submit"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:text="@string/submit"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHeight_percent="0.08"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/username"
        app:layout_constraintWidth_percent="0.4" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

**(activity_main2)**

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/argentina"
    tools:context=".MainActivity2">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/lolified"
        android:textColor="@color/black"
        android:textSize="30sp"
        app:layout_constraintVertical_bias="0.15"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

Java code for **MainActivity**

```java
public class MainActivity extends AppCompatActivity{

    EditText userName;
    Button submit;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        userName = findViewById(R.id.username);
        submit = findViewById(R.id.submit);

        submit.setOnClickListener(view -> {
            String value = userName.getText().toString();
            if (value.equals("noob")) {
                Intent intent = new Intent(this, MainActivity2.class);
                intent.putExtra("UserName", value);
                this.startActivity(intent);
            } else {
                userName.setError("go away");
            }
        });
    }
}
```

java code for **Main_Activity2**

```java
public class MainActivity2 extends AppCompatActivity {

    TextView userName;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);
        userName = findViewById(R.id.textView);
        Intent intent = getIntent();
        String name =  intent.getStringExtra("UserName");
        userName.setText(String.format("%s%s", getString(R.string.neub), name));
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        Toast.makeText(getBaseContext(), "Why are u running", Toast.LENGTH_SHORT).show();
    }
}
```

Here using Intent we are switching to 2nd Activity from 1st Activity.

We can send data from one activity to another activity using intent which we are actually doing in above code. In `MainActivity.java`, we are using `intent.putExtra("UserName", value);` here String UserName will act like a key to a value which we can extract in another activity by using the **UserName** value with `intent.getStringExtra("UserName")`

## Shared Preferences

These are used to save data, these will keep data even if application is closed. These can be used to keep previous score in a game.

- To save a value one must create a SharedPrefrences object with `SharedPrefrences sharedPref = getSharedPrefrences(String:Name, MODE_PRIVATE)`;
- To put data in SharedPrefrences one must use Editor. `SharedPrefrences.Editor = editor.putString("Key", "value")`
- now to commit changes one can use `editor.commit` but `editor.apply()` is preffred as it will do the same work but in background.

A simple app is below which will save values when **save** button is pressed and retrieve those when another button is pressed

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_gravity="center"
    android:divider="?actionBarDivider"
    android:dividerPadding="5dp"
    android:orientation="vertical"
    android:showDividers="middle"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/title"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter title"
        android:textSize="20sp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <EditText
        android:id="@+id/detail"
        android:layout_marginTop="20dp"
        android:layout_width="match_parent"
        android:layout_height="100dp"
        app:layout_constraintTop_toBottomOf="@+id/title"
        android:textSize="20sp"
        android:hint="Enter details"
        app:layout_constraintStart_toStartOf="parent"/>

    <Button
        android:id="@+id/save"
        android:text="Save"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        app:layout_constraintTop_toBottomOf="@id/detail"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        />
    <TextView
        android:id="@+id/savedText"
        android:layout_width="match_parent"
        android:text="Nothing till now"
        android:layout_height="250dp"
        android:layout_marginTop="150dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/save"/>

    <Button
        android:id="@+id/getDetails"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Get"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        android:layout_marginBottom="90dp"
        />
</androidx.constraintlayout.widget.ConstraintLayout>
```

Below is the MainActivity.java file

```java
package com.redheadhammer.a0_another;

import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.util.concurrent.atomic.AtomicReference;

public class MainActivity extends AppCompatActivity {

    SharedPreferences sharedPref;
    EditText title, details;
    Button button, getDetails;
    TextView textView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        title = findViewById(R.id.title);
        details = findViewById(R.id.detail);
        button = findViewById(R.id.save);
        getDetails = findViewById(R.id.getDetails);
        textView = findViewById(R.id.savedText);


        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String head  = title.getText().toString();
                String info = details.getText().toString();
                sharedPref = getSharedPreferences("Data", MODE_PRIVATE);
                SharedPreferences.Editor editor = sharedPref.edit();
                editor.putString(head, info);
                editor.apply();
            }
        });

        getDetails.setOnClickListener(view -> {
            String head  = title.getText().toString();
            sharedPref = getSharedPreferences("Data", MODE_PRIVATE);
            String output = sharedPref.getString( head, "Value not saved");
            Toast.makeText(this, "value is " + output, Toast.LENGTH_SHORT).show();
            textView.setText(output);
        });
    }
}
```

# Reading and Writing to device memory

This Class can be used to read and write in a file

```java

public class FileHelper {

    public static String FILE = "todo_list.dat";

    public static void writeData(ArrayList<String> itemList, Context context) {
        FileOutputStream fileOutputStream = null;
        try {
            fileOutputStream = context.openFileOutput(FILE, MODE_PRIVATE);
            ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);

            objectOutputStream.writeObject(itemList);
            objectOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    public static ArrayList<String> readData(Context context) {
        ArrayList<String> itemList = null;

        try {
            FileInputStream fileInputStream = context.openFileInput(FILE);
            ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);

            itemList = (ArrayList<String>)objectInputStream.readObject();
        }
        catch (FileNotFoundException e) {
            itemList = new ArrayList<String>();
        }
        catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }

        return itemList;
    }
}
```

File types can be changed according to requirement like from `ArrayList<String> to Tree` or anything else. Read and write function can be modified according to the input type.

# Splash Screen (Launch Screen)

### 1. Activity Based

This method uses a specific activity for a flash screen.

1. Create a splash Activity and add a layout to it
2. Create Animation Files if required
3. Attach Animations with Views you want to animate
4. After a given time start the MainActivity using CountDown Timer.

**SplashActivity Layout :**

```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SplashActivity">

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintDimensionRatio="1.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:layout_editor_absoluteX="0dp"
        tools:layout_editor_absoluteY="0dp"
        tools:srcCompat="@tools:sample/backgrounds/scenic" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Splash Screen"
        android:textSize="30sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/imageView" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

**ImageView Rotate Animation**

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- will rotate the whole imageView -->
    <rotate
        android:duration = "3000"
        android:pivotX="50%"
        android:pivotY="50%"
        android:fromDegrees="0"
        android:toDegrees="360"/>

    <!-- will increase the ImageSize from 0 to expected dimensions -->
    <scale
        android:duration = "3000"
        android:pivotY="50%"
        android:pivotX="50%"
        android:fromXScale="0.0"
        android:fromYScale="0.0"
        android:toXScale="1.0"
        android:toYScale="1.0"/>

</set>
```

**TextView Rotate Animation**

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <!--  used to show TextView from a faded TextView  -->
    <alpha
        android:duration = "3000"
        android:fromAlpha="0.0"
        android:toAlpha="1.0"/>

</set>
```

**Java File to Attach Animations to Views**

```java

public class SplashActivity extends AppCompatActivity {

    private TextView textView;
    private ImageView imageView;

    Animation animationImage, animationText;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_splash);

        textView = findViewById(R.id.textView);
        imageView = findViewById(R.id.imageView);

        // load both animations in Animation Objects
        animationImage = AnimationUtils.loadAnimation(this, R.anim.image_animation);
        animationText = AnimationUtils.loadAnimation(this, R.anim.text_animation);

        imageView.setAnimation(animationImage);
        textView.setAnimation(animationText);

        // CountDownTimer for activity to show for 5000ms (5 secs.)
        new CountDownTimer(5000, 1000) {
            @Override
            public void onTick(long millisUntilFinished) {
            }

            @Override
            public void onFinish() {
                Intent intent = new Intent(SplashActivity.this, MainActivity.class);
                startActivity(intent);
                finish();
            }
        }.start();
    }
}
```

### 2. Theme Based

Using this method we don't create any new activity but a theme to use as launch screen. A custom drawable vector file can be used as background. **This method may fail to show a background drawable in some android devices**

1. Save a vector file in drawable folder to be shown as splash screen Icon.
2. Create a new drawable file with **layer-list** tag. Set vector file from 1st step as drawable
3. Create a new theme in themes.xml and set `android:windowBackground` as splash drawable created in 2nd step
4. Set theme for the MainActivity as the custom theme created in step 3
5. change the theme before setting content in mainActivity with `setTheme(R.style.AppTheme);`

**background drawable from step 2**

```xml
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@color/black"/>
    <item
        android:gravity="center"
        android:height="200dp"
        android:width="200dp"
        android:drawable="@drawable/ic_baseline_baby_changing_station_24"
        />
</layer-list>
```

**themes.xml**

```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <!-- Custom theme below -->
    <style name="Splash" parent="Theme.MaterialComponents.DayNight.NoActionBar">
        <item name="android:windowBackground">@drawable/splash_image</item>
    </style>
</resources>
```

**MainActivity.java**

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    setTheme(R.style.Theme_FeatureTest);
    setContentView(R.layout.activity_main);
```

Some delay can be added to splash screen by adding some sleep before changing theme again.

### 3. Splash Screen api

# Sending Data between Screens

### 1. Activity to Activity

While creating intent to move to another activity use `intent.putExtra()` to pass the value.

**In activity 1**

```java
Intent intent = new Intent(MainActivity.this, Activity2.class);
intent.putExtra("VALUE1", value1);
intent.putExtra("VALUE2", value2);
intent.putExtra("VALUE3", value3)
startActivity(intent);
```

**In Activity2**

```java
Intent intent = getIntent();
binding.value1.setText(intent.getStringExtra("VALUE1"));
binding.value2.setText(intent.getStringExtra("VALUE2"));
binding.value3.setText(String.valueof(intent.getIntExtra("VALUE3", 23)))
```

In case we are passing values like array or String we don't have to pass a default value but in other cases like char, int, boolean we need to pass a default value in case we don't get any value with passed tag.

### 2. Activity to Fragment

Like Data sharing between Activity to Activity we use **Intent**, we use **Bundle** to share data between Activity to Fragments.

1. Create a new instance of **Bundle** class.
2. Save value to bundle instance with `bundle.putString("TAG", value)`
3. Create the instance of fragment to which data is going to be passed.
4. Pass bundle's instance as argument to `fragObj.setArguments(bundle)`
5. Now in Fragment class get bundle using `Bundle bundle = getArguments`
6. Now one can get the passed value with `bundle.getString("TAG", "Default_value");`

**Code in Activity**

```java
String value = binding.editText.getText().toString();
Bundle bundle = new Bundle();
bundle.putString("VALUE", value);

mFragment1 frag = new mFragment1();
frag.setArguments(bundle);

FragmentTransaction transaction = manager.beginTransaction();
transaction.replace(R.id.frameLayout, frag).commit();
```

**Code in Fragment**

```java
Bundle bundle = getArguments();
assert (bundle != null);
String value = bundle.getString("VALUE", "Something");
binding.textView.setText(value);
```

### 3. Fragment to Activity

1. Create Activity Object to which we need to pass the values
2. Now create a method in Activity to receive the data from Fragment
3. In fragment call the create method and pass the data

**Code in Fragment**

```java
String value = binding.editText.getText().toString();
MainActivity mainActivity = (MainActivity) getActivity();
assert mainActivity != null;
mainActivity.getData(value);
```

**Code in Activity**

```java
@Override
protected void onCreate(Bundle savedInstanceState){...}
protected void getData(String value) {
    binding.textView.setText(value);
}
```

### 4. Fragment to Fragment

1. Create a Bundle in 1st Fragment and pass data using `bundle.putString("TAG", "something")`
2. Create instance of 2nd fragment and pass bundle as argument to `bundle.setArgument(bundle)`
3. Now in 2nd Fragment Create the bundle
4. getArguments from bundle using `bundle.getString("KEY", "Default_value")`

**Input Fragment Code**

```java
String value = binding.editText.getText().toString();
Bundle bundle = new Bundle();
bundle.putString("VALUE", value);

mFragment1 frag = new mFragment1();
frag.setArguments(bundle);

FragmentManager manager = requireActivity().getSupportFragmentManager();
FragmentTransaction transaction = manager.beginTransaction();

transaction.replace(R.id.frameLayout, frag).commit();
```

**Receiving Fragment Code**

```java
Bundle bundle = getArguments();
assert (bundle != null);
String value = bundle.getString("VALUE", "Something");
binding.textView.setText(value);
```
