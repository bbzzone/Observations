# Notifications

**NOTE:-** Setting flag mutable or immutable is necessary if targeting android S. 

## Local Notifications

1. **Create Notification Channel** with `NotificationChannel` which will take a custom String value to set `ChannelID`, a String for `ChannelName` and Importance of Notification.
2. **Create Notification Manager** with `getSystemService(NOTIFICATION_SERVICE)`.
3. Attach the notification manager with notification channel with `manager.createNotificationChannel(channel)`
4. Now we need to **create an instance of notification builder** with `Notification.Builder` class.
5. use the `Notification.Builder` class's instance to set icon, title, text etc. for the notification.
6. Now to **show the notification** we need to create a `NotificationManagerCompat`. 
7. Finally we need to notify the compat object from step 6 that we have a notification to show and will pass the Notificatoin from builder object.



```java
NotificationChannel notificationChannel = new NotificationChannel(CHANNEL_ID,
                "local Notification", NotificationManager.IMPORTANCE_DEFAULT);

NotificationManager manager = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
manager.createNotificationChannel(notificationChannel);

Notification.Builder builder = new Notification.Builder(MainActivity.this, CHANNEL_ID);
builder.setSmallIcon(R.drawable.ic_launcher_foreground);
builder.setContentTitle("Title of Notification");
builder.setContentText("This is content of the notification");

NotificationManagerCompat compat = NotificationManagerCompat.from(this);
compat.notify(1, builder.build());
```



## Repeated Notification

There is nothing special in tihs type of notification except these follows a time frame to pop. These are no different than local Notifications except we have to attach a period or time to them. This type of notification uses a **BroadcastReceiver** 

1. Create a new class extending `BroadCastReceiver` and build the notification there in `onReceive` method.
2. Define a receiver for activity in the manifest file.
3. Create an instance of calendar in Activity to define the data and time to show notification.
4. Create an `PendingIntent` for broadcasts with `PendingIntent.getBroadcast`.
5. Now as it is a repeating notification we need to define the frequency which can be done with `AlarmManager` class.



**Custom Receiver Class (NotificationReceiver)** 

```java
public class NotificationReceiver extends BroadcastReceiver {

        final String CHANNEL_ID = "RepeatedChannel";

        @Override
        public void onReceive(Context context, Intent intent) {
            NotificationChannel notificationChannel = new NotificationChannel(CHANNEL_ID,
                    "local Notification", NotificationManager.IMPORTANCE_DEFAULT);

            NotificationManager manager = (NotificationManager) context.
                getSystemService(NOTIFICATION_SERVICE);
            manager.createNotificationChannel(notificationChannel);

            Notification.Builder builder = new Notification.Builder(context, CHANNEL_ID);
            builder.setSmallIcon(R.drawable.ic_launcher_foreground);
            builder.setContentTitle("Title of Repeated Notification");
            builder.setContentText("This is content of the repeated notification");

            NotificationManagerCompat compat = NotificationManagerCompat.from(context);
            compat.notify(1, builder.build());
    }
}
```



**Define Receiver in Manifest**

In Application tag define the receiver class `<receiver android:name=".NotificationReceiver"/>` 

**Java code for Activity for 3rd to 5th step**

```java
// Calendar object to set datetime of notification.
Calendar calendar = Calendar.getInstance();
calendar.set(Calendar.HOUR_OF_DAY, 22);
calendar.set(Calendar.MINUTE, 41);
calendar.set(Calendar.SECOND, 0);

Intent intent = new Intent(getApplicationContext(), NotificationReceiver.class);

// Pending Intent to get broadcasts
PendingIntent pendingIntent = PendingIntent.getBroadcast(getApplicationContext(),
                                                         100, intent, PendingIntent.FLAG_IMMUTABLE);

// AlarmManger to set repetition period.
AlarmManager alarmManager = (AlarmManager) getSystemService(ALARM_SERVICE);
alarmManager.setRepeating(AlarmManager.RTC_WAKEUP, calendar.getTimeInMillis(),
                          AlarmManager.INTERVAL_DAY, pendingIntent);
```



## Notification Procedures

### Adding Click Feature to Notification

1. Just create a `PendingIntent` 
2. Attach the pending intent to `Notification.Builder` while building the notification i.e. in localNotification attach the PendingIntent with `setContentIntent(pendingIntent)`.

**Clicking Feature on Local Notification**

```java
// Intent to start on clicking notification
Intent intent = new Intent(MainActivity.this, MainActivity.class);
PendingIntent pendingIntent = PendingIntent.getActivity(this, 0,
                                    intent, PendingIntent.FLAG_IMMUTABLE);

NotificationChannel channel = new NotificationChannel(CLICKABLE_CHANNEL, "Clickable"
                                  , NotificationManager.IMPORTANCE_DEFAULT);

NotificationManager manager = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
manager.createNotificationChannel(channel);

Notification.Builder notification = new Notification.Builder(this,
                                                             CLICKABLE_CHANNEL)
    .setSmallIcon(R.drawable.ic_launcher_foreground)
    .setContentTitle("Clickable")
    .setContentText("Click Me and See Magic")
    .setContentIntent(pendingIntent)
    .setAutoCancel(true);

NotificationManagerCompat compat = NotificationManagerCompat.from(this);
compat.notify(0, notification.build());
```

### Adding custom actions to the notification

1. To add custom action buttons in the Notification we need to define actions which will be triggered on pressing these buttons.
2. We also need to add those buttons to the notification builder as an action which can be created with `Notification.Action.Builder`.
3. Than we need to attach created action with the notification builder object with `addAction`.



**Adding Actions to the Notification buttons**

```java
// Toast Button in notification
// String to show in toast message (data transfer to receiver)
String dataToShare = "This is shared data";
Intent intent1 = new Intent(MainActivity.this, ToastReceiver.class);
intent1.putExtra("TOAST", dataToShare);
PendingIntent pendingIntent1 = PendingIntent.getBroadcast(this, 321, intent1,
                                                          PendingIntent.FLAG_IMMUTABLE);
// Create Notification Actions to add actions to notification
Notification.Action action = new Notification.Action.Builder(
    Icon.createWithResource(this, 
                            R.drawable.ic_launcher_foreground)
    , "Toast", pendingIntent1)
    .build();



Intent intent2 = new Intent(MainActivity.this, DismissNotification.class);
PendingIntent dismissNote = PendingIntent.getBroadcast(this,
                                                       322, intent2, PendingIntent.FLAG_IMMUTABLE);
// Create Notification Actions to add actions to notification
Notification.Action actionDismiss = new Notification.Action.Builder(
    Icon.createWithResource(this, R.drawable.ic_launcher_foreground),
    "Dismiss", dismissNote).build();
```



**Toast Broadcast Receiver Class**

```java
public class ToastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String dataReceived = intent.getStringExtra("TOAST");
        Toast.makeText(context, dataReceived, Toast.LENGTH_LONG).show();
    }
}
```



**Dismiss Broadcast Receiver Class**

```java
public class DismissNotification extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        NotificationManagerCompat compat = NotificationManagerCompat.from(context);
        // cancel the notification with id == 0.
        compat.cancel(0);
    }
}
```



### Adding BigPictures/BigText in Notification

**For BigPictures Bitmaps will work So we need to create bitmaps to show Image in Notification**

This is a oneliner solution `.setStyle(new Notification.BigTextStyle().bigText(text))`. 

```java
NotificationChannel channel = new NotificationChannel(
    SCROLLABLE_ID,
    "Scrollable",
    NotificationManager.IMPORTANCE_DEFAULT
);

Bitmap image = BitmapFactory.decodeResource(getResources(), R.drawable.user1);
String text = "The black brown fox jumps over the lazy dog but the dog " +
    "was god so beating him at jumping was not an easy task So " +
    "in the end dog wins the game and fox goes home to watch pogo";

NotificationManager manager = (NotificationManager)
    getSystemService(NOTIFICATION_SERVICE);
manager.createNotificationChannel(channel);

Notification.Builder notification = new Notification
    .Builder(this, SCROLLABLE_ID);
notification.setContentTitle("My Notification")
    .setSmallIcon(R.drawable.ic_launcher_foreground)
    .setContentText("This is the notification")
    .setLargeIcon(image) // to set the large notification icon.
    .setStyle(new Notification.BigTextStyle().bigText(text))
    .setStyle(new Notification.BigPictureStyle().bigPicture(image));

NotificationManagerCompat compat = NotificationManagerCompat.from(this);
compat.notify(12, notification.build());
```

**Note :- Either BigPicture or BigText should be used at a single time otherwise latter defined will be shown only**.



## Push Notifications

These type of notifications are server based notifications which can be sent to millions at a given time.

There are many service providers for Push Notification including **Firebase Cloud Messaging, One Signal and Amazon SNS**. 