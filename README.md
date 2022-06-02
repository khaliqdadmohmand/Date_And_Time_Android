# Android Java Pick Date And Time 
How to pick date and time using edittext in android studio java project.
Android provides controls for the user to pick a time or pick a date as ready-to-use dialogs. 
Each picker provides controls for selecting each part of the time (hour, minute, AM/PM) or date (month, day, year). 
Using these pickers helps ensure that your users can pick a time or date that is valid, formatted correctly, and adjusted to the user's locale.

[![Watch Tutorial](https://img.youtube.com/vi/cxEb4IafzZU/0.jpg)](https://www.youtube.com/watch?v=cxEb4IafzZU)

# Creating a Time Picker EditText

xml
```
<EditText
        android:id="@+id/time_picker"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="50dp"
        android:drawableRight="@android:drawable/ic_menu_recent_history"
        android:clickable="false"
        android:cursorVisible="false"
        android:focusable="false"
        android:focusableInTouchMode="false"
        android:hint="select time" />
```

Java

```
private void selectTime(){
        Calendar currentTime = Calendar.getInstance();
        int hour = currentTime.get(Calendar.HOUR_OF_DAY);
        int minut = currentTime.get(Calendar.MINUTE);
        TimePickerDialog timePickerDialog;
        timePickerDialog = new TimePickerDialog(MainActivity.this, new TimePickerDialog.OnTimeSetListener() {
            @Override
            public void onTimeSet(TimePicker view, int hour, int minut) {
                currentTime.set(Calendar.HOUR_OF_DAY,hour);
                currentTime.set(Calendar.MINUTE,minut);

                String myFormat = "HH:mm:ss";
                SimpleDateFormat dateFormat = new SimpleDateFormat(myFormat, Locale.US);
                timePicker.setText(dateFormat.format(currentTime.getTime()));

            }
        },hour,minut,true);
        timePickerDialog.setTitle("Select Time");
        timePickerDialog.show();
    }
 ```
 
 # Creating a Date Picker EditText

xml

```
<EditText
        android:id="@+id/date_picker"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:drawableRight="@android:drawable/ic_menu_my_calendar"
        android:clickable="false"
        android:cursorVisible="false"
        android:focusable="false"
        android:focusableInTouchMode="false"
        android:hint="select date" />
```


Java

```
private void selectDate(){
        DatePickerDialog.OnDateSetListener date = new DatePickerDialog.OnDateSetListener() {
            @Override
            public void onDateSet(DatePicker view, int year, int month, int day) {
                myCalendar.set(Calendar.YEAR,year);
                myCalendar.set(Calendar.MONTH, month);
                myCalendar.set(Calendar.DAY_OF_MONTH,day);

                datePciker.setText(updateDate());
            }
        };

        datePciker.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                new DatePickerDialog(MainActivity.this, date, myCalendar.get(Calendar.YEAR),myCalendar.get(Calendar.MONTH),myCalendar.get(Calendar.DAY_OF_MONTH)).show();

            }
        });
    }

    private String updateDate(){
        String myFormat = "yyyy-MM-dd";
        SimpleDateFormat dateFormat = new SimpleDateFormat(myFormat, Locale.US);
        return  dateFormat.format(myCalendar.getTime());
    }
  ```


