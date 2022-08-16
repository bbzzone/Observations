# Broadcast Receivers

There are many system events which need to be notices like `Change in Connectivity, Reboot, Time Change and way more than that`. Each event is observed by system. There are apps which needs to work on these events like Clock app. If app is set to alarm at 12:00 than app needs to be active at 12:00 but app can't know what time it is if it is not active for the whole time. So for an action to be triggered at some random condition app needs to be notified else it has to run forever to know when the event occured. That's where Broadcast receivers come in. Considering the example of alarm application, Android system creates Broadcasts for change in time.  When it is 12:00 it will create a broadcast and than it will check which apps are subscribed to receive the broadcast for that particular event. For instance alarm app will be subscribed for that particular event. Than it will notify the application that it is 12:00 and than app will call the `Broadcast Receiver` and it will trigger the actions defined in Broadcast receiver class defined in manifest.



## Creating Static Receiver

This receiver is also an implicit receiver as it uses action to specify the receiver.

1. Create a subClass of BroadCast receiver.
2. Implement `onReceived` method in the custom class.
3. In `onReceived` method write the actions to be triggered when `Broadcast` is received.
4. Now add the receiver in xml file.

**Receiver in XML File**

```xml
<receiver android:name=".ExampleBroadCastReceiver"
          android:exported="false">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
    </intent-filter>
</receiver>
```

Actions defined in intent filter will trigger the Broadcast Receiver, though **CONNECTIVITY_CHANGE** is deprecated since API 24 (Nougat), it will still work below Nougat. But apps above 24 will not receive this Broadcast if the receiver is defined in `Manifest` file.

**A Receiver register using Manifest file is called static Receiver and other one is called Dynamic Receiver which we define in the code file itself**.



## Difference between Implicit and Explicit Receiver

Implicit Broadcasts are broadcast where whichever components sends the broadcast doesn't specifies broadcast receiver directly by its class name instead it just specifies an action like in above receiver. These Receivers doesn't necessarily need to define an action. These are used in activity to activity. These are also defined using Intents but we need to specify the receiver class.



**Static Broadcasts are broadcast which are registered in manifest file and will keep listening even if application is closed and Dynamic Broadcasts are ones which are specified in Java class files and will unregister when **. 

## Implicit Broadcast Recivers

### Creating Dyanmic  Receiver

1. Create a sub-class of `BroadcastReceiver`.
2. implement `onReceive` and write necessary actions to be taken on receiving the Broadcast
3. Create object of the class in Activity and register it in `onStart` method
4. Create an `IntentFilter` class object and specify actions to register for.
5. `unRegisterReceiver` in `onStop` method.
6. It is not necessary to unregister receiver in `onStop` but if you don't want to keep it active while application is in background than it should be unregistered in `onStop` otherwise `onDestroy`.  

**ExampleBroadcastReceiver**

```java
public class ExampleBroadCastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        boolean noConnect = intent.getBooleanExtra(
                ConnectivityManager.EXTRA_NO_CONNECTIVITY
                , false);
        if (noConnect) {
            Toast.makeText(context, "No Connectivity"
                    , Toast.LENGTH_LONG).show();
        } else {
            Toast.makeText(context, "Connectivity "
                    , Toast.LENGTH_LONG).show();
        }
    }
}
```

**Receiver in MainActivity**

```java
public class MainActivity extends AppCompatActivity {
    ExampleBroadCastReceiver receiver;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        receiver = new ExampleBroadCastReceiver();
    }

    @Override
    protected void onStart() {
        super.onStart();
        // Create filter to register actions
        IntentFilter intentFilter = new IntentFilter(
                ConnectivityManager.CONNECTIVITY_ACTION
        );
        registerReceiver(receiver, intentFilter);
    }

    @Override
    protected void onStop() {
        super.onStop();
        unregisterReceiver(receiver);
    }
}
```



### Sending Custom Broadcasts

Custom broadcast can be sent using `sendBroadcast()` method. But before that we need to create a Broadcast with the help of an Intent. Such type of Broadcasts can be used to communicate between 2 apps.

- Create an Intent with an action, Action name should be unique as it is going to be used for receiver.
- put data in the intent. Finally use `sendBroadcast` to send the data.

```java
// this function can create a broadcast and will send it.
private void SendBroad(View view) {
    Intent intent = new Intent("MY_BROADCAST");
    String text = editText.getText().toString();
    intent.putExtra("MY_PASSED_TEXT", text);
    sendBroadcast(intent);
}
```

Now receiving the custom sent broadcast.

- Create a `Custom Receiver class` extending BroadcastReceiver.
- Register the receiver in MainActivity or whichever activity we are going to use it in 

**Custom Receiver class**

```java
public class ExampleBroadCastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if ("MY_BROADCAST".equals(intent.getAction())) {
            String receivedText = intent.getStringExtra("" +
                    "MY_PASSED_TEXT");
            Toast.makeText(context, 
                           "Receiver: " + receivedText,
                           Toast.LENGTH_SHORT).show();
        }
    }
}
```

**Registering the Receiver in Activity**

```java
public class MainActivity extends AppCompatActivity {
    ExampleBroadCastReceiver receiver;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        receiver = new ExampleBroadCastReceiver();
        IntentFilter filter = new IntentFilter("MY_BROADCAST");
        registerReceiver(receiver, filter);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(receiver);
    }
}
```

- Notice Receiver in above class is defined in `onCreate` and `onDestroy`, it is because if the receiver was defined in `onStart` or `onStop` it would not work when app is in background. So if one wants receiver to work only when it is focused than we need to register and unregister in `onStart` and `onStop`. 
- [This video](https://www.youtube.com/watch?v=qNocH6Angt0) is a good example of how one app can receive data from other app with the help of broadcast receivers.

## Explicit Broadcast Receiver

These type of receivers need to specifies in Manifest file but we don't need to specify the actions.

### Creating Explicit receiver

1. Create a custom Receiver class extending `BroadcastReceiver` and specify actions to be taken when receiving the broadcast. 
2. Create an intent and pass arguments as Context and Broadcast class.
3. than send broadcast with `sendBroadcast` method passing intent we created above.
4. Add the receiver in Manifest file as `<receiver android:name=".ExampleBroadCastReceiver"/>`. No need to specify actions.

**Custom Broadcast class**

```java
public class ExampleBroadCastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
            Toast.makeText(context, "Receiver: ", Toast.LENGTH_SHORT).show();
    }
}
```

**Send broadcast with below code**

```java
Intent intent = new Intent(MainActivity.this, ExampleBroadCastReceiver.class);
sendBroadcast(intent);
```

We can also specify an action with intent by using below approach instead of above to create intent.

```java
Intent intent = new Intent("MY_ACTION");
intent.setClass(MainActivity.this,
                ExampleBroadCastReceiver.class);
sendBroadcast(intent);
```

By using above approach we can specify an action with the intent which can be used to trigger different events if we are triggering same BroadcastReceiver from multiple activities by passing different action name like below receiver

```java
public class ExampleBroadCastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if ("MY_ACTION".equals(intent.getAction())) {
            Toast.makeText(context, "Received",
                    Toast.LENGTH_SHORT).show();
        } else if ("YOUR_ACTION".equals(intent.getAction())) {
            Toast.makeText(context, "Activity2",
                    Toast.LENGTH_SHORT).show();
        }
        else {
            Toast.makeText(context,
                    "ACTION NOT RECEIVED",
                    Toast.LENGTH_SHORT).show();
        }
    }
}
```



## To check apps with given Broadcast Receiver

Create an instance of Package Manger and run `queryBroadcastReceivers` with a given intent action.

```java
Intent intent = new Intent("MY_ACTIONS");
PackageManger packagemanager = getPackageManager();

List<ResolveInfo> infoList = packagemanager.queryBroadcastReceivers(intent, 0);

// Loop on list
for (ResolveInfo info: infoList) {
    String packageName = info.activityInfo.packageName;
    String receivername = info.activityInfo.name;
}
```

This list will create a list of all apps which have a registered "MY_ACTIONS" broadcast receiver.



## Send a broadcast to multiple apps

Before jumping in this one should know alternative way of sending broadcasts with `ComponentName` class.

```java
Intent intent = new Intent("MY_ACTION");
Component comp = new Component("packageNameOfAppToSendBroadcastTo",
                              "broadcastReceiverClassName");
intent.setComponent(comp);
sendBroadcast(intent);
```

Now to send broadcast to all apps which are registered for a given action.

```java
Intent intent = new Intent("MY_ACTIONS");
PackageManger packagemanager = getPackageManager();

List<ResolveInfo> infoList = packagemanager.queryBroadcastReceivers(intent, 0);

for (ResolveInfo info: infoList) {
    String packageName = info.activityInfo.packageName;
    String receiverName = info.activityInfo.name;
    Component comp = new Component(packageName,
                              receiverName);
}
```
