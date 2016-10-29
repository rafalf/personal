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
### Step 2: Install Android SDK tool packadge
[Go to this site] (https://developer.android.com/studio/index.html) and install the command line tool. Set _ANDROID_HOME_ environment variable as your Android SDK path. Additionally add the _tool_ and _platform-tools_ folders to your path variable.
Go 
### Step 3: Install Intel Hardware Accelerated Execution Manager, Android Tools and API
Look inside Android SDK folder and start up SDK Manager.exe. Select all Tools, any top level API checkbox (one or all) that you want to use (makesure greater than 17), click on HAXM Installer in extras section and install it. Be patient, it'll take some time to complete this task. Make sure that you have plent of free space on your drive if you decide to install all APIs. Once installed go to the _SDK\extras\intel\Hardware_Accelerated_Execution_Manager_ and execute _intelhaxm-android.exe_.
To troubleshot and resolve any issues related to HAXM [this post will help](http://stackoverflow.com/questions/26355645/error-in-launching-avd-with-amd-processor)
### Step 4: Create Android virtual device
Again, look inside Android SDK folder, and start up AVD Manager.exe. It'll launch AVD manager.
Click on Create button and create a device of your choice. 


&nbsp;
