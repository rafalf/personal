---
layout: post
title:  "Appium: How to configure Appium for web apps on Android emulator running Safari with Python"
date:   2016-10-20
desc: "How to configure appium for testing web apps on Safari with Python"
keywords: "appium, python, webdriver"
categories: [Automation]
tags: [Appium, Automation, Python]
published: true
---


Appium is an open source test automation framework for use with native, hybrid and mobile web apps. The aim of this post is to install Appium on Windows and get it running web app tests on Safari with Python. A short example of Python script will be provided at the very end of this post to test Facebook home page.

&nbsp;

## INSTALL APPIUM AND ANDROID VIRTUAL DEVICE

&nbsp;

### Step 1: Install JAVA
Download the latest JDK, install it and set _JAVA_HOME_. Add _bin_ directory to your PATH variable.  

### Step 2: Install Android SDK tool package  
[Go to this site](https://developer.android.com/studio/index.html) and install the command line tool. Set _ANDROID_HOME_ environment variable as your Android SDK path. Additionally add the _tool_ and _platform-tools_ folders to your path variable.  

### Step 3: Install Intel Hardware Accelerated Execution Manager, Android Tools and API  
Look inside Android SDK folder and start up SDK Manager.exe. Select all Tools, any top level API checkbox (one or all) that you want to use (make sure greater than 17), click on HAXM Installer in the extras section and install it. Be patient, it'll take some time to complete this task. Make sure that you have plenty of free space on your drive if you decide to install all APIs. Once installed go to the _SDK\extras\intel\Hardware_Accelerated_Execution_Manager_ and execute _intelhaxm-android.exe_.
To troubleshot and resolve any issues related to HAXM [this post will help](http://stackoverflow.com/questions/26355645/error-in-launching-avd-with-amd-processor)  

### Step 4: Create Android virtual device  
Again, look inside Android SDK folder, and start up AVD Manager.exe. It'll launch AVD manager.  
Click on Create button and create a device of your choice. Once created start it up!


![alt text](http://testprojects.co/static/img/postimg/android.png "Android Virtual Device")

Open admin cmd prompt and run `adb devices` to print a list of attached emulators/devices.  
Your emulator should be listed.

&nbsp;

### Step 5: Install Chrome  
[Download](http://www.apkmirror.com/uploads/?q=chrome) .apk for your device (e.g. x86 - .47 [link](http://www.apkmirror.com/apk/google-inc/chrome/chrome-47-0-2526-83-release/) )  
Open admin cmd prompt and run the following command to install the .apk on your device:  

```
adb install nameofyourapk.apk 
```
Check if Chrome is installed on your emulator.

### Step 6: Check if uiautomatorviewer is working
Open admin cmd prompt and run `uiautomatorviewer`. It's a tool that lets you inspect the UI of an application. For more details, check [this page](https://nishantverma.gitbooks.io/appium-for-android/content/exploring_uiautomatorviewer/) out.

Your device is all set! Now, it's time to install Appium ...

### Step 7: Install Node and npm tools
[Download](https://nodejs.org/en/download/) and install.
Open admin cmd prompt and run the command  

```
npm install -g appium
```

Now, to start Appium server simply run the command `appium`

### Step 8: Install Python client
Install Python client ([source on github](https://github.com/appium/python-client)) from PyPi: `pip install Appium-Python-Client`  
If you have it correctly set up, you should be able to run [this quick test](https://github.com/appium/python-client/blob/master/test/functional/android/chrome_tests.py)







&nbsp;
