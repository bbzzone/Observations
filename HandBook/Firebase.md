# Firebase

Firebase offers too many services like Realtime Database(json based), authentication, Machine Learning, FireStone Database, AppChecks etc.

## RealTimeDatabase

Add the firebase library to your project using required procedure. This is a real time database service where we save data in `json` format. We can write or read data in database using firebase libraries. Data can be added directly or through android application.

### Write Simple Data to firebase

1. Get instance of the database and use that to get a `DatabaseRefrence` to the parent.
2. Now to add values to database for different keys use `setValue` method.

```java
// Create refrence of the parent in which we need to save data
// Get parent refrence from database
FirebaseDatabase firebase = FirebaseDatabase.getInstance();
DatabaseReference reference = firebase.getReference().child("User");
binding.button.setOnClickListener(this::SendData);

// Method to write data to firebase
private void SendData(View view) {
    String userName = binding.name.getText().toString();
    String email = binding.email.getText().toString();
    String phone = binding.phone.getText().toString();

    reference.child("Name").setValue(userName);
    reference.child("Email").setValue(email);
    reference.child("Phone Num").setValue(phone);
}
```

 ### Reading Simple Data from Firebase

1. Again get refrence object for the parent whose children we want to see.
2. To get values of the keys from database we need to add a value listener to the reference.
3. We can get values from the database using snapshot.
4. We can also define another listener which will provide information for single time `addListenerForSingleValueEvent`.

```java
// Get database instance
FirebaseDatabase firebase = FirebaseDatabase.getInstance();
DatabaseReference reference = firebase.getReference().child("User");

reference.addValueEventListener(new ValueEventListener() {
    // Every time data is changed onDataChange method will execute.
    @Override
    public void onDataChange(@NonNull DataSnapshot snapshot) {
        String name = (String)snapshot.child("Name").getValue();
        binding.textView.setText(name);
    }

    @Override
    public void onCancelled(@NonNull DatabaseError error) {}
});
```



## Authenticating with Firebase

### Simple Email/Password Login

In the authentication section of firebase web interface add `Email/Password` as **Sign-in-method**. Now connect android studio project with firebase via firebase interface provided with Android Studio. After connecting the project select `custom sign in methods`

When setup is complete create a SignUp Activity and Use firebase to signup.

1. Create instance of `FirebaseAuth` class with `FirebaseAuth firebaseAuth = FirebaseAuth.getInstance();`
2. now call `createUserWithEmailAndPassword` method. (This method will create user)
3. Add a click listener to know the result of the signup process with `addOnCompleteListener`

```java
private void addUserToServer(String email, String password) {
    // createUserWithEmailAndPassword method will create account
    // Listener is to check of task is successful or not.
    firebaseAuth.createUserWithEmailAndPassword(email, password)
        .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {
                if (task.isSuccessful()) {
                    Toast.makeText(SignUpActivity.this,
                                   "Account Created Successful",
                                   Toast.LENGTH_SHORT).show();
                    finish();
                } else {
                    // If sign in fails, display a message to the user.
                    Toast.makeText(SignUpActivity.this,
                                   "Failed", Toast.LENGTH_SHORT).show();
                }
            }
        }
    );
}
```



**SignIn Operation**:

1. Create instance of `FirebaseAuth` class with `FirebaseAuth firebaseAuth = FirebaseAuth.getInstance();`
2. now call `signInWithEmailAndPassword` method. (This method will create user)
3. Add a click listener to know the result of the signup process with `addOnCompleteListener`

```java
private void UserSignIn(String email, String password) {
    firebaseAuth.signInWithEmailAndPassword(email, password)
        .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {
                if (task.isSuccessful()) {
                    Toast.makeText(MainActivity.this, "Sign in Successful",
                                   Toast.LENGTH_SHORT).show();
                    Intent intent = new Intent(MainActivity.this, MainMenu.class);
                    startActivity(intent);
                    finish();
                } else {
                    Toast.makeText(MainActivity.this, "Sign in Failed",
                                   Toast.LENGTH_SHORT).show();
                }
            }
        }
	);
}
```



#### keep user logged in

In the login activity's `onStart` method check if user is already logged in or not if yes than we can directly jump on to main content otherwise we should proceed with login. like below:-

```java
// Create instance of FirebaseAuth class
FirebaseAuth firebaseAuth = FirebaseAuth.getInstance();

@Override
protected void onCreate(Bundle savedInstanceState){...}

@Override
protected void onStart() {
    super.onStart();

    FirebaseUser user = firebaseAuth.getCurrentUser();
    if (user != null) {
        Intent intent = new Intent(MainActivity.this, MainMenu.class);
        startActivity(intent);
        finish();
    }
}
```



#### Forgot password

```java
private void Forgot(String email) {
    firebaseAuth.sendPasswordResetEmail(email)
        .addOnCompleteListener(new OnCompleteListener<Void>() {
            @Override
            public void onComplete(@NonNull Task<Void> task) {
                if (task.isSuccessful()) {
                    Toast.makeText(ForgotActivity.this,
                                   "reset mail sent",
                                   Toast.LENGTH_SHORT).show();
                }
            }
        }
	);
}
```



### OTP Login

1. Create `FirebaseAuth` instance with `FirebaseAuth.getInstance()`.
2. Bulid `PhoneAuthOptions` with `PhoneAuthOptions.newBuilder(firebaseAuth)`. 
   1. use `setPhoneNumber` on `PhoneAuthOptions.newBuilder` to add a phone number to be used for verification.
   2. `setTimeout` to set the validity of the code.
   3. `setActivity` to set the activity in which code will be verified.
   4. `setCallbacks` to set the callbacks on Authenticaion success, failure etc.
3. Create `PhoneAuthProvider.OnVerificationStateChangedCallbacks` object which will be passed to `PhoneAuthOptions` and implement `onVerificationCompleted` and `onVerificationFailed`. One may override `onCodeSent` method, which will help to get sentcode.
4. If required save the sms code sent in a variable from `onCodeSent` method.
5. Now to send the message run `PhoneAuthProvider.verifyPhoneNumber(phoneAuthOptionsObject)`. Whole above procedure was to send the code and actions to be taken when code was successfully verified or failed to verify but now we need to verify the code entered by the user and code sent.
6. Create `PhoneAuthCredential` object with `PhoneAuthProvider.getCredential(codeSent, codeUserEntered)`. Firebase will automatically check if those values match or not.
7.  Now we need to signIn with `firebaseAuth` instance we created in very 1st step. We use credential object created in previous step to Login with `firebaseAuth.signInWithCredential(credential)`.
   1. add a listener to signInWithCredential to check if verification was successful or not.
   2. implement `onComplete` method and use Task parameter to check if process was successful or a failure with `task.isSuccessful()`.

**Java Code to Send OTP**

```java
private void sendSMS(View view) {
    String phone = binding.phone.getText().toString();
    PhoneAuthOptions options = PhoneAuthOptions.newBuilder(firebaseAuth)
        .setPhoneNumber(phone)
        .setTimeout(120L, TimeUnit.SECONDS)
        .setActivity(PhoneLogin.this)
        .setCallbacks(myCallbacks)
        .build();

    PhoneAuthProvider.verifyPhoneNumber(options);
}

// Callback used in PhoneAuthOptions above
PhoneAuthProvider.OnVerificationStateChangedCallbacks myCallbacks =
    new PhoneAuthProvider.OnVerificationStateChangedCallbacks() {
    @Override
    public void onVerificationCompleted(
        @NonNull PhoneAuthCredential phoneAuthCredential) {
        Toast.makeText(PhoneLogin.this,
                       "Verification Done", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onVerificationFailed(@NonNull FirebaseException e) {
        try {
            throw e;
        } catch (FirebaseAuthInvalidCredentialsException exception) {
            Toast.makeText(PhoneLogin.this,
                           "Check your phone number and country code",
                           Toast.LENGTH_SHORT).show();
        } catch (FirebaseException fireException) {
            Toast.makeText(PhoneLogin.this,
                           "Bad Response try again", Toast.LENGTH_SHORT).show();
        }
    }

    @Override
    public void onCodeSent(@NonNull String s, @NonNull PhoneAuthProvider
                           .ForceResendingToken forceResendingToken) {
        super.onCodeSent(s, forceResendingToken);
        sentCode = s;
        Toast.makeText(PhoneLogin.this,
                       "Code Sent", Toast.LENGTH_SHORT).show();
    }
};
```

**Java code to Verify OTP**

```java
// get user entered otp
String otp = binding.otpNum.getText().toString();
// Get PhoneAuthCredentials for transaction
PhoneAuthCredential credential = PhoneAuthProvider
    .getCredential(sentCode, otp);
// Login using credentials received
firebaseAuth.signInWithCredential(credential)
    .addOnCompleteListener(new OnCompleteListener<AuthResult>() {
        @Override		// listener on verification successful
        public void onComplete(@NonNull Task<AuthResult> task) {
            if (task.isSuccessful()) {
                Toast.makeText(PhoneLogin.this,
                               "Completed", Toast.LENGTH_SHORT).show();
                Intent intent = new Intent(PhoneLogin.this, MainMenu.class);
                startActivity(intent);
                finish();
            } else {
                Toast.makeText(PhoneLogin.this,
                               "Not correct", Toast.LENGTH_SHORT).show();
            }
        }
    }
);
```



### Sign In with Google

1. Create a new `GoogleSignInOptions` object by using builder.
   1. set requestIdToken by getting its value from generated res folders or with `getString (R.string.default_web_client_id)`
   2. requestEmail will be used to give user options to select an email.
2. create a `GoogleSignInClient` with `GoogleSignIn.getClient(options, googleSignInOptionsObj)`
3. Now we have to start an implicit activity for user to select an email from list of emails available on phone.
4. Our ultimate goal here is to login with credentials for which we need `GoogleSignInAccount` to get credentials
5. Now in Intent from 3rd step get `Task<GoogleSignInAccount>` using `GoogleSignIn.getSignedInAccountFromIntent(data)`. And from this data get the `GoogleSignInAccount`
6. Now using `GoogleSignInAccount` create `AuthCredential` now use `FirebaseAuth` object to login using `signInWithCredential`

**Create GoogleSignInOptions object**

```java
GoogleSignInOptions options = new GoogleSignInOptions.Builder(GoogleSignInOptions.DEFAULT_SIGN_IN)
    //                .requestIdToken("259246650605-dve2kpfb0496i01i42sshc52ej4ntr22.apps.googleusercontent.com")
                .requestIdToken(getString(R.string.default_web_client_id))
                .requestEmail()     // this will ask user to choose an email
                .build();

// Create a signInClient
GoogleSignInClient client = GoogleSignIn.getClient(this, options);

// start intent to make user select a google account.
Intent signInIntent = client.getSignInIntent();
googleSignInResult.launch(signInIntent);
```

**SignInIntent Launcher**

```java
googleSignInResult = registerForActivityResult(
    new ActivityResultContracts.StartActivityForResult(),
    new ActivityResultCallback<ActivityResult>() {
        @Override
        public void onActivityResult(ActivityResult result) {
            int resultCode = result.getResultCode();
            Intent data = result.getData();
            if (resultCode == RESULT_OK && data != null) {
                Task<GoogleSignInAccount> task = GoogleSignIn.getSignedInAccountFromIntent(data);
                try {
                    GoogleSignInAccount account = task.getResult(ApiException.class);
                    // Custom function defined below
                    getDeviceIdToken(account);
                } catch (ApiException e) {
                    e.printStackTrace();
                }

            }
        }
    });
```

**getDeviceIdToken function**

```java
private void getDeviceIdToken(GoogleSignInAccount account) {
    AuthCredential credential = GoogleAuthProvider.getCredential(account.getIdToken(), null);
    firebaseAuth.signInWithCredential(credential)
        .addOnCompleteListener(new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {
                if (task.isSuccessful()) {
                    Toast.makeText(LogIn.this, "Login Successful", Toast.LENGTH_SHORT).show();
                    Intent intent = new Intent(LogIn.this, MainActivity.class);
                    startActivity(intent);
                    finish();
                    // FirebaseUser user = firebaseAuth.getCurrentUser();
                    // by getting user using above method we can perform
                    // many actions on user like getting email, profile image
                    // set on google account, name etc.
                } else {
                    Toast.makeText(LogIn.this, "Something went wrong", Toast.LENGTH_SHORT).show();
                }
            }
        });
}
```









## LogOut

Just a simple command will do it for us: `FirebaseAuth.getInstance().signOut();`  



## Push Notifications Firebase

1. Create a custom service class extending `FirebaseMessagingService`
2. You can override methods like `onMessageReceived` or `onNewToken`
3. Now in manifest file register your service with intent filter to set action for firebase notification.
4. After all these steps has been done. Your app is ready to receive notifications from firebase server.

```xml
<service android:name=".MyFirebaseService"
         android:exported="false">
    <intent-filter>
        <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
    </intent-filter>
</service>
<meta-data
           android:name="com.google.firebase.messaging.default_notification_icon"
           android:resource="@drawable/notification_important"/>
<meta-data
           android:name="com.google.firebase.messaging.default_notification_color"
           android:resource="@color/purple_500"
           />
```

These metadata values can be used to set Notification icon and notification color from firebase.

**Custom Service class**

```java
package com.redheadhammer.myfirebase;

import androidx.annotation.NonNull;

import com.google.firebase.messaging.FirebaseMessagingService;
import com.google.firebase.messaging.RemoteMessage;

public class MyFirebaseService extends FirebaseMessagingService {
    @Override
    public void onMessageReceived(@NonNull RemoteMessage message) {
        super.onMessageReceived(message);
    }

    @Override
    public void onNewToken(@NonNull String token) {
        super.onNewToken(token);
    }
}
```



## Firebase Storage

### Upload Images

1. get the image from the local storage to upload (Image URI)
2.  Now create an instance of current `FirebaseUser` with `firebaseAuthObject.getCurrentUser()`.  **(Not neccessary but to keep data in folders with folder name of the user-email or phone)**
3. Now to create a directory by user name or phone create a `StorageReference` object by using `FirebaseStorage.getInstance().getReference(firebaseUser.getEmail());` (This will create a branch in the storage with useremail)
4. Now create another `StorageReference` which will be the child of the storageReference created in previous step. `reference = storageReference.child("userImage");`. The value passed as child will be the name of the file being uploaded.
5. Upload the file with reference from step 4 using `reference.put(ImageUri)`
6. Add Success, Failure and Progress Listener to the upload process.
