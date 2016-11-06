---
layout: post
title:  "Appium: How to configure Appium and Android emulator for testing web apps on Chrome browser with Python"
date:   2016-10-20
desc: "How to configure Appium and Android emulator for testing web apps on Chrome browser with Python"
keywords: "appium, python, webdriver"
categories: [Automation]
tags: [Appium, Automation, Python, Android]
published: true
---


Appium is an open source test automation framework for use with native, hybrid and mobile web apps. The aim of this post is to install Android emulator & Appium on Windows and get it running web app tests on Chrome. By the end of this post, we'll go through all steps required to get the tools installed that the Python test included in this post can be run to test briefly whether the Facebook home page is loaded or not in the browser.

&nbsp;

## INSTALL APPIUM AND ANDROID VIRTUAL DEVICE

&nbsp;

### Step 1: Install JAVA
Download the latest JDK, install it and set _JAVA_HOME_. Add _bin_ directory to your PATH variable.  

### Step 2: Install Android SDK tool package  
[Go to the android developer site](https://developer.android.com/studio/index.html) and install the command line tool. Set _ANDROID_HOME_ environment variable as your Android SDK path. Additionally add the _tool_ and _platform-tools_ folders to your path variable.  

### Step 3: Install Intel Hardware Accelerated Execution Manager, Android Tools and API  
Look inside Android SDK folder and start up SDK Manager.exe. Select all Tools, any top level API checkbox (one or all) that you want to use (make sure greater than 17), click on HAXM Installer in the extras section and install it. Be patient, it'll take some time to complete this task. Make sure that you have plenty of free space on your drive if you decide to install all APIs. Once installed go to the _SDK\extras\intel\Hardware_Accelerated_Execution_Manager_ and execute _intelhaxm-android.exe_.
To troubleshoot and resolve any issues related to HAXM [this stackoverflow post will help](http://stackoverflow.com/questions/26355645/error-in-launching-avd-with-amd-processor)  

### Step 4: Create Android virtual device  
Again, look inside Android SDK folder, and start up AVD Manager.exe. It'll launch AVD manager.  
Click on Create button and create a device of your choice. Once created start it up!


![alt text](http://testprojects.co/static/img/postimg/android.png "Android Virtual Device")

Open admin cmd prompt and run `adb devices` to print a list of attached emulators/devices.  
Your emulator should be listed.

&nbsp;

### Step 5: Install Chrome  
[Download chrome .apk for android](http://www.apkmirror.com/uploads/?q=chrome) (e.g. x86 - v.47 [link](http://www.apkmirror.com/apk/google-inc/chrome/chrome-47-0-2526-83-release/))  
Open admin cmd prompt and run the following command to install the .apk on your device:  

```
adb install com.android.chrome_47.0.2526.83-252608310_minAPI16(x86)(nodpi).apk 
```
Check if Chrome is installed on your emulator.

### Step 6: Check if uiautomatorviewer is working
Open admin cmd prompt and run `uiautomatorviewer`. It's a tool that lets you inspect the UI of an application. For more details, check [this page](https://nishantverma.gitbooks.io/appium-for-android/content/exploring_uiautomatorviewer/) out.

Your device is all set! Now, it's time to install Appium ...

### Step 7: Install Node and npm tools
[Download node](https://nodejs.org/en/download/) and install.  
Open admin cmd prompt and run the command  

```
npm install -g appium
```

Now, to start Appium server simply run the command `appium`

### Step 8: Install Python client
Install Python client ([source on github](https://github.com/appium/python-client)) from PyPi: `pip install Appium-Python-Client`  
If you have it correctly set up, you should be able to run [this quick Python test](https://github.com/appium/python-client/blob/master/test/functional/android/chrome_tests.py). You can also jump straight to Step 9 and run fb tests.


### Step 9: Run fb test

Run both tests:

```
#!/usr/bin/env python

# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import unittest
import time
from appium import webdriver
from selenium.webdriver.support.ui import WebDriverWait
from selenium.common.exceptions import TimeoutException
from appium.webdriver.common.touch_action import TouchAction


class FbChrome(unittest.TestCase):
    def setUp(self):
        
        desired_caps = {
            'platformName': 'Android',
            'platformVersion': '5.1.1',
            'deviceName': 'Android Emulator',
            'browserName': 'Chrome'
        }
        self.driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)
        
    def tearDown(self):
        self.driver.quit()

    def test_pass(self):
        self.driver.get('http://www.facebook.com')

        try:
            el = WebDriverWait(self.driver, 10).until(
                lambda y: self.driver.find_element_by_id('u_0_2'), message='login panel did not appear')
            el.send_keys('incorrect')
        except TimeoutException as e:
            self.fail(e)

    def test_fail(self):
        self.driver.get('http://www.facebook.com')

        try:
            el = WebDriverWait(self.driver, 2).until(
                lambda y: self.driver.find_element_by_id('incorrectID'), message='login panel did not appear')
        except TimeoutException as e:
            self.fail(e)

if __name__ == "__main__":
    suite = unittest.TestLoader().loadTestsFromTestCase(FbChrome)
    unittest.TextTestRunner(verbosity=2).run(suite)

```



&nbsp;


### 10: Extras! Troubleshooting Android

There will be times where you will need to troubleshoot Appium and Android. When it happens, `adb` comes handy to get Android logs e.g. to post an issue on github. First, we need to clean the logs by executing `adb -c`, followed by `adb logcat` to take the logs.

__Happy testing!!__





