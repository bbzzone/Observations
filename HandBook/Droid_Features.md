# Accessing Android Features

## Sending SMS Message

Sending SMS Message requires SEND_SMS permission and for that we need to do certain steps:

1. Add permission required in Manifest file in `<uses-permission>` tag.
   1. `<uses-permission android:name="android.permission.SEND_SMS" />`
2. Create instance of `SmsManager`
3. send message with the help of instance of sms Manger using `manager.sendTextMessage()`

```java
SmsManager manager = SmsManager.getDefault();
manager.sendTextMessage(userNum, null, userMessage, null, null);	
```

userNum is the mobile number of the user and userMessage is the message you want to send.

## Sending Email

1. Create an intent with `ACTION_SEND`.
2. add data with appropriate tags.
3. create a chooser without it ndroid will not know with which activity to handle the request.
4. start the activity.

```java
String[] emails = {userAddress};
Intent intent = new Intent(Intent.ACTION_SEND);

intent.setData(Uri.parse("mailto:"));

// setting type after setting data will clear data and vice-versa.
intent.setType("text/plain");

intent.putExtra(Intent.EXTRA_EMAIL, emails);
intent.putExtra(Intent.EXTRA_SUBJECT, title);
intent.putExtra(Intent.EXTRA_TEXT, message);

/**
* chooser will give user choice to select app from which
* to send mail. 2nd parameter passed will be the title
* of the selection menu.
*/
startActivity(Intent.createChooser(intent, "email"));
```



**Approach 2**

```java
private void sendEmail(String userAddress, String title, String message)  {

    String[] emails = {userAddress};

    Uri uri = Uri.parse("mailto:")
        .buildUpon()
        .build();

    Intent emailIntent = new Intent(Intent.ACTION_SENDTO, uri);

    emailIntent.putExtra(Intent.EXTRA_EMAIL, emails);
    emailIntent.putExtra(Intent.EXTRA_SUBJECT, title);
    emailIntent.putExtra(Intent.EXTRA_TEXT, message);

    startActivity(Intent.createChooser(emailIntent, "select application: "));
}
```



## Making a Call

Add permission for `CALL_PHONE` in manifest file.

`"tel:"` is an abreviation for telephone as `"mailto:"` is for email

- We need to append telephone number with `"tel:"` like `"tel:12354363"`. 

```java
private void initCall(String phoneNum) {
    Intent intent = new Intent(Intent.ACTION_CALL);
    intent.setData(Uri.parse("tel:" + phoneNum));
    startActivity(intent);
}
```

 

## Speech To Text

Create intent with a speech recognizer.

```java
private void convert() {
    Intent intent = new Intent(RecognizerIntent.ACTION_RECOGNIZE_SPEECH);
    intent.putExtra(RecognizerIntent.EXTRA_LANGUAGE_MODEL,
                    RecognizerIntent.LANGUAGE_MODEL_FREE_FORM);
    intent.putExtra(RecognizerIntent.EXTRA_LANGUAGE, Locale.getDefault());

    startActivityForResult(intent, 123);
}
```

on receiving activity result, set the text received as text of an edittext or textView.

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    if (requestCode == 123 && resultCode == RESULT_OK && data != null) {
        ArrayList<String> arrayList = data.getStringArrayListExtra
            (RecognizerIntent.EXTRA_RESULTS);
        binding.convertedText.setText(arrayList.get(0));
    }
}
```

 

