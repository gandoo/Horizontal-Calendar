# Horizontal Calendar

[![Download](https://api.bintray.com/packages/mulham-raee/maven/horizontal-calendar/images/download.svg) ](https://bintray.com/mulham-raee/maven/horizontal-calendar/_latestVersion)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

A material horizontal calendar view for Android based on `RecyclerView`.

![demo](/art/demo.gif)

## Installation

The library is hosted on jcenter, add this to your **build.gradle**:

```gradle
repositories {
      jcenter()
    }
    
dependencies {
      compile 'devs.mulham.horizontalcalendar:horizontalcalendar:1.2.5'
    }
```

## Prerequisites

The minimum API level supported by this library is **API 14 (ICE_CREAM_SANDWICH)**.

## Usage

- Add `HorizontalCalendarView` to your layout file, for example:

```xml
<android.support.design.widget.AppBarLayout>
		............ 
		
        <devs.mulham.horizontalcalendar.HorizontalCalendarView
            android:id="@+id/calendarView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@color/colorPrimary"
            app:textColorSelected="#FFFF"/>
            
</android.support.design.widget.AppBarLayout>
```

- In your Activity or Fragment, define your **start** and **end** dates to set the range of the calendar:

```java
/* end after 1 month from now */
Calendar endDate = Calendar.getInstance();
endDate.add(Calendar.MONTH, 1);

/* start before 1 month from now */
Calendar startDate = Calendar.getInstance();
startDate.add(Calendar.MONTH, -1);
```

- Then setup `HorizontalCalendar` in your **Activity** through its Builder: 

```java
HorizontalCalendar horizontalCalendar = new HorizontalCalendar.Builder(this, R.id.calendarView)
                .startDate(startDate.getTime())
                .endDate(endDate.getTime())
                .datesNumberOnScreen(5)
                .build();
```

- Or if you are using a **Fragment**:

```java
HorizontalCalendar horizontalCalendar = new HorizontalCalendar.Builder(rootView, R.id.calendarView)
	...................
```

- To listen to date change events you need to set a listener:

```java
horizontalCalendar.setCalendarListener(new HorizontalCalendarListener() {
            @Override
            public void onDateSelected(Date date, int position) {
                //do something
            }
        });
```

- You can also listen to **scroll** and **long press** events by overriding each perspective method within **HorizontalCalendarListener**:

```java
horizontalCalendar.setCalendarListener(new HorizontalCalendarListener() {
            @Override
            public void onDateSelected(Date date, int position) {

            }

            @Override
            public void onCalendarScroll(HorizontalCalendarView calendarView, 
            int dx, int dy) {
                
            }

            @Override
            public boolean onDateLongClicked(Date date, int position) {
                return true;
            }
        });
```

## Customization

- You can customize it directly inside your **layout**:

```xml
<devs.mulham.horizontalcalendar.HorizontalCalendarView
            android:id="@+id/calendarView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@color/colorPrimary"
            app:textColorNormal="#bababa"
            app:textColorSelected="#FFFF"
            app:selectorColor="#c62828"   // default to colorAccent.
            app:selectedDateBackground="@drawable/myDrwable"/>
```

- Or you can do it programmatically in your **Activity** or **Fragment** using `HorizontalCalendar.Builder`:

```java
HorizontalCalendar horizontalCalendar = new HorizontalCalendar.Builder(this, R.id.calendarView)
                .startDate(Date startDate)
                .endDate(Date endDate)
                .datesNumberOnScreen(int number)   // Number of Dates cells shown on screen (default to 5).
                .configure()    // starts configuration.
                    .formatTopText(String dateFormat)       // default to "MMM".
                    .formatMiddleText(String dateFormat)    // default to "dd".
                    .formatBottomText(String dateFormat)    // default to "EEE".
                    .showTopText(boolean show)              // show or hide TopText (default to true).
                    .showBottomText(boolean show)           // show or hide BottomText (default to true).
                    .textColor(int normalColor, int selectedColor)    // default to (Color.LTGRAY, Color.WHITE).
                    .selectedDateBackground(Drawable background)      // set selected date cell background.
                    .selectorColor(int color)               // set selection indicator bar's color (default to colorAccent).
                .end()          // ends configuration.
                .defaultSelectedDate(Date date)    // Date to be seleceted at start (default to current day `new Date()`).
                .build();
```

#### More Customizations

```java
builder.configure()
           .textSize(float topTextSize, float middleTextSize, float bottomTextSize)
           .sizeTopText(float size)
           .sizeMiddleText(float size)
           .sizeBottomText(float size)
           .colorTextTop(int normalColor, int selectedColor)
           .colorTextMiddle(int normalColor, int selectedColor)
           .colorTextBottom(int normalColor, int selectedColor)
       .end()
```

## Features

- Disable specific dates with `HorizontalCalendarPredicate`, a unique style for disabled dates can be specified as well with `CalendarItemStyle`:
```java
builder.disableDates(new HorizontalCalendarPredicate() {
                           @Override
                           public boolean test(Date date) {
                               return false;    // return true if this date should be disabled, false otherwise.
                           }
       
                           @Override
                           public CalendarItemStyle style() {
                               return null;     // create and return a new Style for disabled dates, or null if no styling needed.
                           }
                       })
```

- Select a specific **Date** programmatically with the option whether to play the animation or not:
```java
horizontalCalendar.selectDate(Date date, boolean immediate); // set immediate to false to ignore animation.
	// or simply
horizontalCalendar.goToday(boolean immediate);
```

- Check if two dates' **days** are equal:
```java
horizontalCalendar.isDatesDaysEquals(Date date1, Date date2);
```

- Check if a date is contained in the Calendar:
```java
horizontalCalendar.contains(Date date);
```

## Contributing

Contributions are welcome, feel free to submit a pull request.

## License

> Copyright 2017  Mulham Raee
> 
> Licensed under the Apache License, Version 2.0 (the "License");
> you may not use this file except in compliance with the License.
> You may obtain a copy of the License at
       http://www.apache.org/licenses/LICENSE-2.0

> Unless required by applicable law or agreed to in writing, software
> distributed under the License is distributed on an "AS IS" BASIS,
> WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
> See the [License](/LICENSE) for the specific language governing
> permissions and limitations under the License.
