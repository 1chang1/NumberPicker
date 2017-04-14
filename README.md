NumberPicker 
============

[![Build Status](https://travis-ci.org/travijuu/NumberPicker.svg?branch=master)](https://travis-ci.org/travijuu/NumberPicker) [![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.github.travijuu/numberpicker/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.github.travijuu/numberpicker)

A simple customizable NumberPicker for Android.

<img src="https://raw.githubusercontent.com/travijuu/NumberPicker/master/images/numberpicker.png" width=450/>

Download
--------

Download [the latest JAR][2] or grab via Gradle:
```groovy
compile 'com.travijuu.numberpicker:numberpicker:1.0.6'
```
or Maven:
```xml
<dependency>
  <groupId>com.github.travijuu</groupId>
  <artifactId>numberpicker</artifactId>
  <version>1.0.6</version>
  <type>aar</type>
</dependency>
```

Usage
-----

Add NumberPicker component in your XML layout

*activity_main.xml*

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    xmlns:numberpicker="http://schemas.android.com/apk/res-auto"
    tools:context="com.travijuu.numberpicker.sample.MainActivity">

    <com.travijuu.numberpicker.library.NumberPicker
        android:id="@+id/number_picker"
        android:layout_width="130dp"
        android:layout_height="40dp"
        numberpicker:min="0"
        numberpicker:max="10"
        numberpicker:value="-5"
        numberpicker:unit="1"
        numberpicker:custom_layout="@layout/number_picker_custom_layout"
        numberpicker:focusable="false" />

</LinearLayout>

```

if you want to customize your NumberPicker layout you can create your own.

**IMPORTANT!** This layout should contains at least 3 items with given Ids:
- Button (@+id/increment)
- Button (@+id/decrement)
- TextView (@+id/display)

Note: You can see an example layout in both sample and library modules.

Example XML layout:

```xml
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="130dp"
    android:layout_height="40dp"
    android:orientation="horizontal"
    android:background="@android:color/white">

    <Button
        android:layout_width="30dp"
        android:layout_height="match_parent"
        android:padding="0dp"
        android:textColor="@android:color/black"
        android:background="@null"
        android:id="@+id/decrement"
        android:textStyle="bold"
        android:text="—"/>

    <TextView
        android:layout_width="70dp"
        android:background="@android:color/white"
        android:layout_height="match_parent"
        android:text="1"
        android:textColor="@android:color/black"
        android:inputType="number"
        android:id="@+id/display"
        android:gravity="center"
        />
    <Button
        android:layout_width="30dp"
        android:layout_height="match_parent"
        android:padding="0dp"
        android:textSize="25sp"
        android:textColor="@android:color/black"
        android:background="@null"
        android:id="@+id/increment"
        android:text="+"/>
</LinearLayout>
```

**Another way to setup NumberPicker:**

*MainActivity.java*

```java
import com.travijuu.numberpicker.library.NumberPicker;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        NumberPicker numberPicker = (NumberPicker) findViewById(R.id.number_picker);
        numberPicker.setMax(15);
        numberPicker.setMin(5);
        numberPicker.setUnit(2);
        numberPicker.setValue(10);
    }
}

```

Here is the list of functions.

Getters/Setters
--------
- setMin(int value)
- getMin()
- setMax(int value)
- getMax()
- setUnit(int value)
- getUnit()
- setValue(int value)
- getValue()
- setActionEnabled(ActionEnum action, boolean enabled)
- setDisplayFocusable(boolean focusable)

Useful functions
--------
- increment()
- increment(int unit)
- decrement()
- decrement(int unit)

Listeners
---------
- setLimitExceededListener(LimitExceededListener limitExceededListener)

**LimitExceededListener** is triggered when you try to set lower or higher than the given min/max limits

```java
public class DefaultLimitExceededListener implements LimitExceededListener {

    public void limitExceeded(int limit, int exceededValue) {

        String message = String.format("NumberPicker cannot set to %d because the limit is %d.", exceededValue, limit);
        Log.v(this.getClass().getSimpleName(), message);
    }
}
```

- setValueChangedListener(ValueChangedListener valueChangedListener)

**ValueChangedListener** is triggered when the NumberPicker is incremented or decremented.

*Note:* `setValue`method will not trigger this listener.

```java
public class DefaultValueChangedListener implements ValueChangedListener {

    public void valueChanged(int value, ActionEnum action) {

        String actionText = action == ActionEnum.INCREMENT ? "incremented" : "decremented";
        String message = String.format("NumberPicker is %s to %d", actionText, value);
        Log.v(this.getClass().getSimpleName(), message);
    }
}
```

- setOnEditorActionListener(OnEditorActionListener onEditorActionListener)

**OnEditorActionListener** is triggered when you click "**done**" button on keyboard after you edit current value.

*Note:* "**done**" button can be changed on xml so this listener should be overrided according to new IME option. 
