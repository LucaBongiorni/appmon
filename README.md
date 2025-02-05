Welcome to AppMon!
==================

This project was only possible because of **Ole André Vadla Ravnås** and I dedicate it to him.


Follow him on [**GitHub**](https://github.com/oleavr), [**Twitter**](https://twitter.com/oleavr)

_TL;DR_
AppMon is an automated framework for monitoring and tampering system API calls of native iOS and Android apps (upcoming). It is based on [**Frida**](http://www.frida.re). You may call it the [**GreaseMonkey**](https://en.wikipedia.org/wiki/Greasemonkey) for native mobile apps. ;-)

----------

Motivation
-------------

Being a big fan of the Sysinternals Suite (acquired by Microsoft) and the recent spike in the number of mobile app releases we see an increase in Mobile app security assessments and the lack of toolset for doing it easily and thoroughly, easily, became the motivation for this idea. 

AppMon is my vision is to make become the iOS/Android equivalent of the this project [**apimonitor**](http://www.rohitab.com/apimonitor) and [**GreaseMonkey**](https://en.wikipedia.org/wiki/Greasemonkey). This should become a useful tool for the mobile penetration testers to not only monitor the app’s overall activity and focus on things that seem suspicious, as a starting point but also use pre-defined user-scripts to modify the app’s functionality/logic in the runtime e.g. spoofing the DeviceID, spoofing the GPS co-ordinates, faking In-App purchases etc. 

And as the tool matures, with time (i.e. as I get more spare time) we can have even more refinement as to add pattern detection into this monitoring where we can tag/classify the data (e.g. PII etc.) 

Dynamic instrumentation of native mobile apps is not something new to us, there are tools, available since 2011, to do one or the other thing. But the tools I have used so far are not as flexible as it is to do with Frida i.e. extending the capabilities and adding new features is very hard and cumbersome process with similar alternatives. And more over most of them are very tightly bound to a specific version of the mobile OS.

So far I have grouped the methods of interesting classes into logical categories of APIs that I’m going to intercept/manipulate into e.g.
> **Categories:**
> - Disk I/O (R/W)
> - Network (HTTP GET, POST etc.)
> - Crypto (HMAC, Hash function, block ciphers, X.509 certs etc.)
> - XML/JSON
> - KeyChain
> - Database (e.g. SQLite)
> - WebView
> - UserDefaults (SharedPreferences equiv.) & more.

In the current release, we have the ability to hook both the Apple’s CoreFoundation API’s as well as the Objective-C methods (even if its done in a Swift app via the bridging header). Swift support is not yet available in frida-gum and hence we'll have to wait until then. All I want to from you all is to watch the Video Demo (link above), take a look at the source-code and then provide your feedbacks/comments/suggestions/rants. And also it would be really helpful if you can provide me and missing feature you would like to see in the tool.

Setup & Install
-----------------
> Tested on:
> - **Host**: MacOS X 10.11
> - **Target Device**: iPhone 5S (iOS 8.1) _(other devices, OS is supported as long as Frida supports it)_

Setup Host Environment
```
$ sudo -H pip install argparse frida flask termcolor
```

Setup Target Device

> - Follow the instructions to install Frida on the target device i.e. the iOS device, as mentioned in the [**Official Frida Docs**](http://www.frida.re/docs/ios/#with-jailbreak)
> - Do the smoke-test as mentioned in the [**Official Frida Docs**](http://www.frida.re/docs/ios/#with-jailbreak) and make sure everything is working as expected.

Usage
-------------

####AppMon Sniffer
```
usage: appmon.py [-h] [-a APP_NAME] [-p PLATFORM] [-s SCRIPT_PATH]
                 [-o OUTPUT_DIR] [-ls LIST_APPS] [-v]

optional arguments:
  -h, --help      show this help message and exit
  -a APP_NAME     Process Name; Accepts "Twitter" for iOS;
                  "com.twitter.android" for Android; "Twitter" for MacOS X
  -p PLATFORM     Platform Type; Accepts "ios", "android" or "mac"
  -s SCRIPT_PATH  Path to agent script file; Can be relative/absolute path for
                  a file or directory; Multiple scripts in a directory shall
                  be merged; Needs "-a APP_NAME"
  -o OUTPUT_DIR   (Optional) Path to store any dumps/logs; Accepts
                  relative/absolute paths
  -ls LIST_APPS   Optional; Accepts 1 or 0; Lists running Apps on target
                  device; Needs "-p PLATFORM"
  -v              show program's version number and exit
```
-----
####AppMon Intruder
```
usage: appintruder.py [-h] [-a APP_NAME] [-p PLATFORM] [-ls LIST_APPS]
                      [-s SCRIPT_PATH] [-v]

optional arguments:
  -h, --help      show this help message and exit
  -a APP_NAME     Process Identifier; Accepts "Twitter" for iOS;
                  "com.twitter.android" for Android; "Twitter" for MacOS X
  -p PLATFORM     Platform Type; Accepts "ios", "android" or "mac"
  -ls LIST_APPS   Optional; Accepts 1 or 0; Lists running Apps on target
                  device; Needs "-p PLATFORM"
  -s SCRIPT_PATH  Path to agent script file; Can be relative/absolute path for
                  a file or directory; Multiple scripts in a directory shall
                  be merged; Needs "-a APP_NAME"
  -v              show program's version number and exit
```
----------


Screenshots
-------------------


![Screenshot#1](https://raw.githubusercontent.com/dpnishant/appmon/master/screenshots/1.png?raw=true "Screenshot#1")



![Screenshot#2](https://raw.githubusercontent.com/dpnishant/appmon/master/screenshots/2.png?raw=true "Screenshot#2")



![Screenshot#3](https://raw.githubusercontent.com/dpnishant/appmon/master/screenshots/3.png?raw=true "Screenshot#3")



![Screenshot#4](https://raw.githubusercontent.com/dpnishant/appmon/master/screenshots/4.png?raw=true "Screenshot#4")


Video(s)
------------------

###TouchID Bypass using AppMon Intruder

[![TouchID Bypass using AppMon Intruder](https://img.youtube.com/vi/ECnkgz3jnPM/0.jpg)](https://youtu.be/ECnkgz3jnPM)
