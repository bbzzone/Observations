# Services

A service can perform long running operations in background. It doesn't have a user interface but it can be bound to a component. Once started, a service might continue to run for some time, even if application is put in background.

3 types of services are:-

1. **Foreground Services**

   1. A foreground service perform actions which are noticable for the user. Like an audio application would use a foreground service to play music in the. **A foreground service must need to show a notification which can't be dismissed until the application is closed**.

2. **Background Services**

   1. A background service performs an operation that isn't directly noticed by the user. For example, if an app used a service to compact its storage, that would usually be a background service.

3. **Bound Services**

   1. A bound service is started when a component of the application bound itself to it. 
   2. It is called with `bindService()` from the component like activity.
   3.  bound service offers a client-server interface that allows components to interact with the service, send requests, receive results, and even do so across processes with interprocess communication (IPC). A bound service runs only as long as another application component is bound to it. Multiple components can bind to the service at once, but when all of them unbind, the service is destroyed.

   

There is a note [here](https://developer.android.com/guide/components/services#Types-of-services:~:text=the%20manifest.-,Choosing%20between%20a%20service%20and%20a%20thread,thread%20within%20the%20service%20if%20it%20performs%20intensive%20or%20blocking%20operations.,-The%20basics) which will tell when should be use a thread or a service instead, which may clear some of confusion.

## Creating a service

To create a service one need to create a subclass of `Service`. To do some actions with service we need to `@Override` some methods.

- `onStartCommand` method will be invoked when a service is invoked with `startService(serviceName)` method. To stop the service one can use `selfStop()` or `serviceStop()`.
- `onBind` method will be invoked when a service is started with `bindService()`. This method should be implemented even if it is not required. And in case where there is no need of onBind method one can simply return `null`.
- `onCreate` this method is called even before `onBind` or `onStartCommand` method is called. It creates the service will always be called.
- `onDestroy` will be invoked when service is no longer in use. Your service should implement this to clean up any resources such as threads, registered listeners, or receivers. This is the very last call a service will receive.

### Adding Service in Manifest File

A service should be added in manifest file with a service tag inside application tag.

```xml
<application ... >
    <service android:name=".ExampleService" />
    ...
</application>
```



### Creating Standard Service Class

```java
public class ExampleService extends Service {
    private static final String TAG = "ExampleService";
    @Override
    public void onCreate() {
        super.onCreate();
        Log.d(TAG, "onCreate: Service Created");
    }

    @Nullable
    @Override
    public IBinder onBind(Intent intent) {
        Log.d(TAG, "onBind: Service Bound");
        return null;
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Log.d(TAG, "onStartCommand: Service Started");
        return super.onStartCommand(intent, flags, startId);
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        Log.d(TAG, "onDestroy: Service Destroyed");
    }
}
```

#### Starting Service(Standard)

```java
private void startService(View view) {
    Intent intent = new Intent(this, ExampleService.class);
    startService(intent);
}

private void stopService(View view) {
    Intent intent = new Intent(this, ExampleService.class);
    stopService(intent);
}
```



### Creating Bound Service

- To create a bound service, implement the `onBind()` callback method to return an `IBinder` that defines the interface for communication with the service
- Other application components can then call `bindService()` to retrieve the interface and begin calling methods on the service.
- The service lives only to serve the application component that is bound to it, so when there are no components bound to the service, the system destroys it.

**Creating Bound Service**

- To create a bound service, you must define the interface that specifies how a client can communicate with the service.
- This interface between the service and a client must be an implementation of `IBinder` and is what your service must return from the `onBind()` callback method.
- After the client receives the `IBinder`, it can begin interacting with the service through that interface.

#### BoundService

- A bound service is the server in a client-server interface.
- It allows components (such as activities) to bind to the service, send requests, receive responses, and perform interprocess communication (IPC)
- You can create a service that is both started and bound. That is, you can start a service by calling `startService()`, which allows the service to run indefinitely, and you can also allow a client to bind to the service by calling `bindService()`.
- If you do allow your service to be started and bound, then when the service has been started, the system does *not* destroy the service when all clients unbind. Instead, you must explicitly stop the service by calling `stopSelf()` or `stopService()`.

**Although you usually implement either `onBind()` *or* `onStartCommand()`, it's sometimes necessary to implement both. For example, a music player might find it useful to allow its service to run indefinitely and also provide binding. This way, an activity can start the service to play some music and the music continues to play even if the user leaves the application. Then, when the user returns to the application, the activity can bind to the service to regain control of playback.**

```java
```



## LifeCycle of Services

- **A service is created** when another component calls `startService()`. The service then runs indefinitely and must stop itself by calling `stopSelf()`. Another component can also stop the service by calling `stopService()`. When the service is stopped, the system destroys it.
- **A Bound service** is created when another component (a client) calls `bindService()`. The client then communicates with the service through an `IBinder` interface. The client can close the connection by calling `unbindService()`. Multiple clients can bind to the same service and when all of them unbind, the system destroys the service. The service does *not* need to stop itself.