---
layout: single
title:  "iOS Release"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/3d92750f-8975-4085-8730-0aa085f3724e)

<br>

As Apple App Developer, Actually as a hybrid platform app developer using Flutter and Dart, there are a lot of barriers to distribute an app. I've distributed about 5 apps since 2020 but, distribution doesn't get easy. I was planning to write some summary how to deploy on App Store and here it is.

### Disclaimer
 You definately need a Mac to deploy on App Store. You need to build an app with XCode. It's necessary. Also, Apple Developer account is needed. Also, I am using Flutter, Dart and Android Studio so, it may be a slightly different from deploy only with Swift. XCode part will be same, I guess. <br>
 Also, check if your XCode app is up to date. You may need to install the older versions of iOS simulators.

### Before Deployment
 After developing all your codes, algorithms and UI/UX, you need to first test it on other format of simulators. App Store Connect requires 3 different Screenshot size. 6.7 inch, 6.5 inch, 5.1 inch. Each are  **iPhone 15 pro Max, iPhone 11 pro Max, iPhone 8 plus**. There may be some overflow of text or other kinds of errors. You may find those bugs first. <br> 
<br>
 Second, open the terminal inside Android Studio. Then enter `flutter clean`. It removes other unnecessary files and rebuilds your app. There will be a lot of wiggly underlines but, don't worry. Just type `flutter build ios`. It may take time.<br>
 
### Actual Deployment
 After cleaning and building with ios, find directory named **Runner.xcworkspace**. It is the crucial part of running your app inside XCode. Right click on that directory and find **Flutter > Open iOS/macOS module in XCode**. It may open with XCode app.<br>
 If you turn your app inside XCode, it start processing file. You need to wait for that process is finished. If it's over check the following instructions. <br><br>
 `XCode > Product > Destination > Any iOS Device` <br>
 `XCode > Product > Scheme > choose scheme > Runnner` <br>
 `XCode > Product > Archive` <br><br>

 Also, check **signing & capabilites** and make it to *signed*.

### After Deployment
If *Actual Deployment* is finished, you may see pop-ups. Go follow those steps and if it's done, go to *App Store Connect*. Make your app, write some required parts. For the app build, the button will show. Choose the version you've build and upload it to App Store Connect.<br>
<br>
That's it. It's the simplist way of deploying Dart/Flutter app through android studio and XCode. Of course, there are a lot of **issues** and **rejections** waiting ahead. Don't be frightened. Everybody gone thorugh those problems!



