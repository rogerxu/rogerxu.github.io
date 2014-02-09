---
layout: post
title: Android Development
---

## Android Overview

### Android Features

* Android Application Framework
* Dalvik virtual machine
* Integrated browser
* Optimized graphics
* SQLite
* Media Support
* GSM Telephony
* Bluetooth, EDGE, 3G, WiFi
* Camera, GPS, Compass and accelerometer
* Rich development environment

### Android Architecture

* Application
* Application Framework
* Libraries
* Android Runtime
* Dalvik Virtual Machine
* Linux Kernel


## Installation

### Android SDK

[Android developer site](http://developer.android.com/sdk/index.html)

    android-sdk-<machine-platform>

#### Device Emulator

### Android Development Tools

### ADT Eclipse Plugin

Eclipse Help > Install New Software

    https://dl-ssl.google.com/android/eclipse/

Android applications are typically developed with the Eclipse IDE.


## Android Application Components

* Activity
* Service - background execution without user interface
* Content Provider - manages shared application data
* Broadcast Receiver - listens for and react to system-wide broadcast announcements

### Activity

Activity is the presentation layer of your application.

`android.app.Activity`

#### Activity States

* Running/Resumed
* Paused
* Stopped

#### Activity Lifecycle Callback Methods

    onCreate()

Initialization - create views, bind data to lists

    onStart()

Called when the activity is becoming visible the user.

    onResume()

Called when the activity will start interacting with the user. At this point your activity is at the top of the activity stack, with user input going to it.

    onPause()

Called when the system is about to start resuming a previous activity. Implementations of this method must be very quick because the next activity will not be resumed until this method returns.

    onSaveInstanceState()

Save the instance state in a Bundle in case the Activity is destroyed due to lack of system resources and needs to be re-created again.

    onStop()


    onDestroy()


#### View and ViewGroup

 The user interface in Android is made up of Views and View Groups arranged in a hierarchy.

 The View class - widget

 The ViewGroup class - layout

Two ways to build UI

* Declaratively in XML files
* Programmatically

### Intents

An Intent is a asynchronous message which activate components and acts as "glue between components".

* The called component may or may not be a part of the current application (loose coupling)
* An intent may carry additional data
* `startActivity(Intent intent)`
* Intents may be created as implicit or explicit intent

#### Explicit intents

#### Implicit intents

#### Intent filters

    <intent-filter>
        <actiion android:name="" />
        <category android:name="" />
        <data android:mimeType="" />
    </intent-filter>

## Project Structure

    android-app
    |-- src
        |-- demo.android.helloandroid
            |-- HelloAndroidActiviti.java
    |-- gen
    |-- assets
    |-- res
        |-- drawable-hdpi
            |-- ic_launcher.png
        |-- drawable-ldpi
            |-- ic_launcher.png
        |-- drawable-mdpi
            |-- ic_launcher.png
        |-- drawable-xhdpi
        |-- layout
            |-- activity_hello_android.xml
        |-- menu
        |-- values
            |-- strings.xml
            |-- styles.xml
    |-- AndroidManifest.xml
    |-- ic_launcher-web.png
    |-- proguard-project.txt
    |-- project.properties


### Auto-generated Files

#### gen/R.java

#### default.properties

#### proguard.cfg

### Manifest


## Building an Android applications

## Android Layouts

* FrameLayout
* LinearLayout
* RelativeLayout
* TableLayout
* GridLayout

### Text Controls

* TextView
* EditText
* AutoCompleteTextView
* MultiAutoCompleteView

### Button Controls

* Button
* ImageButton
* ToggleButton
* CheckBox
* RadioButton

### List Controls

* ListView

### Grid Controls

* GridView


* ProgressBar
* Spinner

### Menu

* Options Menu
* Context Menu
* Sub Menu

### Dialog

* AlertDialog
* ProgressDialog
* DatePicker
* TimePickerDialog
* Custom Dialog

## Adapters

Adapters are bridging classes that bind data to views.

AdapterView

* ArrayAdapter
* SimpleCursorAdapter

## Handling User Events

### Event Listeners

* onClick()
* onLongClick()
* onFocusChange()
* onKey()
* onTouch()
* onCreateContextMenu()

### Event Handlers

    Activity.dispatchTouchEvent(MotionEvent)

    ViewGroup.onInterceptTouchEvent(MotionEvent)

    ViewParent.requestDisallowInterceptTouchEvent(boolean)

### Touch Mode

### Handling Focus

    isFocusable()
    setFocusable()
    isFocusableInTouchMode()
    setFocusableInTouchMode()


## Debugging

### ADT

LogCat

### ADB (Android Debug Bridge)

adb acts as a middleman between a device and your development system.

    <sdk>/platform-tools/adb.exe

Copying files

Upload

    adb push <local file path> <remote file path>

Download

    adb pull <remote file path> <local file path>

Install

    adb install <apk file path>

### DDMS - Dalvik Debug Virtual Machine

* Monitoring Thread Activity
* Prompting Garbage Collection
* Monitoring Heap Activity
* Monitoring Memory Allocation
* Stopping a Process
* Browsing in the File System
* Working with Emulator Control
* Simulating Incoming Voice calls
* Simulating Incoming SMS Messages
* Working with Application Logging
* Taking Screen Captures of Screen

## Threads and Services

Application - process
process made of several threads

One UI thread per process

code run in UI thread must be nimble

Service in background

### Services

Services are perfect for long-running processes that do not require use interaction.

The other application can bind to the service to interact with it and even perform interprocess communications (IPC).

#### Bound Services

    onCreate()
    onStartCommand()
    onBind()
    stopSelf()


#### Starting a Service

    Intent intent = new Intent(this, HelloService.class);
    startService(intent);

#### IntentService



### Threads and Handlers


### AsyncTask

### Notifications and Alert Dialogs

### Broadcast Receivers


## SQLite Database

## Hardware Interfaces

### Android Telephony

### SMS

### Bluetooth

### Network connectivity

### Wi-Fi

### Device Sensor

### Monitoring Battery

## Location Service


