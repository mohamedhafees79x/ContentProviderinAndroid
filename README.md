
# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the text create your own content providers to get contacts details.
Developed by: Mohamed Hafees R
Registeration Number: 212225230175
*/
```

MAIN_ACTIVIT.JAVA
```
package com.example.contactproviderapp;

import android.app.Activity;
import android.os.Bundle;
import android.content.ContentValues;
import android.database.Cursor;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends Activity {

    EditText etName, etPhone;
    Button btnAdd, btnView;
    TextView tvResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        etName = findViewById(R.id.etName);
        etPhone = findViewById(R.id.etPhone);

        btnAdd = findViewById(R.id.btnAdd);
        btnView = findViewById(R.id.btnView);

        tvResult = findViewById(R.id.tvResult);

        // Add Contact
        btnAdd.setOnClickListener(v -> {

            String name = etName.getText().toString();
            String phone = etPhone.getText().toString();

            ContentValues values = new ContentValues();

            values.put(DatabaseHelper.NAME, name);
            values.put(DatabaseHelper.PHONE, phone);

            getContentResolver().insert(
                    ContactProvider.CONTENT_URI,
                    values
            );

            Toast.makeText(
                    MainActivity.this,
                    "Contact Added Successfully",
                    Toast.LENGTH_SHORT
            ).show();

            etName.setText("");
            etPhone.setText("");
        });

        // View Contacts
        btnView.setOnClickListener(v -> {

            Cursor cursor = getContentResolver().query(
                    ContactProvider.CONTENT_URI,
                    null,
                    null,
                    null,
                    null
            );

            StringBuilder result = new StringBuilder();

            if (cursor != null) {

                while (cursor.moveToNext()) {

                    String name = cursor.getString(
                            cursor.getColumnIndexOrThrow(
                                    DatabaseHelper.NAME
                            )
                    );

                    String phone = cursor.getString(
                            cursor.getColumnIndexOrThrow(
                                    DatabaseHelper.PHONE
                            )
                    );

                    result.append("Name: ")
                            .append(name)
                            .append("\n");

                    result.append("Phone: ")
                            .append(phone)
                            .append("\n\n");
                }

                cursor.close();
            }

            tvResult.setText(result.toString());
        });
    }
}
```
MAIN_ACTIVITY.XML
```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <!-- Title -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Contact Provider"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:padding="16dp" />

    <!-- Name Input -->
    <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Name"
        android:inputType="textPersonName" />

    <!-- Phone Input -->
    <EditText
        android:id="@+id/etPhone"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Phone Number"
        android:inputType="phone" />

    <!-- Add Contact Button -->
    <Button
        android:id="@+id/btnAdd"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Add Contact" />

    <!-- View Contacts Button -->
    <Button
        android:id="@+id/btnView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="View Contacts" />

    <!-- Display Contacts -->
    <TextView
        android:id="@+id/tvResult"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:padding="20dp"
        android:textSize="18sp" />

</LinearLayout>

```
ANDROIDMANIFEST.XML
```
<?xml version="1.0" encoding="utf-8"?>

<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="ContactProviderApp"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.ContactProviderApp">

        <activity
            android:name=".MainActivity"
            android:exported="true">

            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category
                    android:name="android.intent.category.LAUNCHER" />
            </intent-filter>

        </activity>

        <provider
            android:name=".ContactProvider"
            android:authorities="com.example.contactproviderapp.provider"
            android:exported="true" />

    </application>

</manifest>
```



## OUTPUT
<img width="1917" height="1076" alt="628884976-8f417679-797f-40e3-9a5d-643f395e5029" src="https://github.com/user-attachments/assets/10777e5b-ec3d-4bf4-833f-69dfeed009ca" />
<img width="1917" height="1078" alt="628885122-175cd339-4cbb-41e5-b6eb-33fb26d4b27f" src="https://github.com/user-attachments/assets/46fab898-890a-4749-b2da-7cefa5d8fe8a" />




## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
