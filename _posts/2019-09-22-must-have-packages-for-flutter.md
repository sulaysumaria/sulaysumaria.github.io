---
layout: post
title: "Must have packages for Flutter"
categories: [Flutter]
permalink: /must-have-packages-for-flutter
---

Flutter makes it real easy to develop apps with many features out of the box. But there are some great dependencies that you must depend on. Here is a list of a few of them with the purpose of each and a sample code.

All of this plugins support both Android and iOS.

## connectivity <span style="font-size: 17px;"><a href="https://pub.dev/packages/connectivity" target="_blank">Link</a></span>

This plugin allows Flutter apps to discover network connectivity and configure themselves accordingly. It can distinguish between cellular vs WiFi connection. This plugin works for iOS and Android.

```dart
var connectivityResult = await (Connectivity().checkConnectivity());
if (connectivityResult == ConnectivityResult.mobile) {
  // I am connected to a mobile network.
} else if (connectivityResult == ConnectivityResult.wifi) {
  // I am connected to a wifi network.
}
```

## url_launcher <span style="font-size: 17px;"><a href="https://pub.dev/packages/url_launcher" target="_blank">Link</a></span>

A Flutter plugin for launching a URL in the mobile platform. Urls include not only `http` and `https` but also `mailto`, `tel` and `sms`. This package also has a method named `canLaunch()` which you can use to check whether device can launch that kind of url. For ex, Some tablets might not handle `tel` or `sms` urls.

```dart
_launchURL() async {
  const url = 'https://flutter.dev';
  if (await canLaunch(url)) {
    await launch(url);
  } else {
    throw 'Could not launch $url';
  }
}
```

## dio <span style="font-size: 17px;"><a href="https://pub.dev/packages/dio" target="_blank">Link</a></span>

A powerful Http client for Dart, which supports Interceptors, Global configuration, FormData, Request Cancellation, File downloading, Timeout etc.

```dart
void getHttp() async {
  try {
    Response response = await Dio().get("http://www.google.com");
    print(response);
  } catch (e) {
    print(e);
  }
}
```

## device_info <span style="font-size: 17px;"><a href="https://pub.dev/packages/device_info" target="_blank">Link</a></span>

Get current device information from within the Flutter application.

```dart
DeviceInfoPlugin deviceInfo = DeviceInfoPlugin();
AndroidDeviceInfo androidInfo = await deviceInfo.androidInfo;
print('Running on ${androidInfo.model}');  // e.g. "Moto G (4)"

IosDeviceInfo iosInfo = await deviceInfo.iosInfo;
print('Running on ${iosInfo.utsname.machine}');  // e.g. "iPod7,1"
```

## shared_preferences <span style="font-size: 17px;"><a href="https://pub.dev/packages/shared_preferences" target="_blank">Link</a></span>

Wraps NSUserDefaults (on iOS) and SharedPreferences (on Android), providing a persistent store for simple data.

```dart
SharedPreferences prefs = await SharedPreferences.getInstance();
int counter = (prefs.getInt('counter') ?? 0) + 1;
print('Pressed $counter times.');
await prefs.setInt('counter', counter);
```

## file_picker <span style="font-size: 17px;"><a href="https://pub.dev/packages/file_picker" target="_blank">Link</a></span>

A package that allows you to use a native file explorer to pick single or multiple absolute file paths, with extensions filtering support.

```dart
String filePath;

// Will let you pick one file path, from all extensions
filePath = await FilePicker.getFilePath(type: FileType.ANY);

// Will filter and only let you pick files with svg extension
filePath = await FilePicker.getFilePath(type: FileType.CUSTOM, fileExtension: 'svg')
```

## path_provider <span style="font-size: 17px;"><a href="https://pub.dev/packages/path_provider" target="_blank">Link</a></span>

A Flutter plugin for finding commonly used locations on the filesystem. Supports iOS and Android.

```dart
Directory tempDir = await getTemporaryDirectory();
String tempPath = tempDir.path;

Directory appDocDir = await getApplicationDocumentsDirectory();
String appDocPath = appDocDir.path;
```

## dynamic_theme <span style="font-size: 17px;"><a href="https://pub.dev/packages/dynamic_theme" target="_blank">Link</a></span>

This packages manages changing your theme during runtime and persiting that theme.

```dart
void changeBrightness() {
    DynamicTheme.of(context).setBrightness(
        Theme.of(context).brightness == Brightness.dark? Brightness.light: Brightness.dark,
    );
}

void changeColor() {
    DynamicTheme.of(context).setThemeData(new ThemeData(
        primaryColor: Theme.of(context).primaryColor == Colors.indigo? Colors.red: Colors.indigo
    ));
}
```

## flutter_advanced_networkimage <span style="font-size: 17px;"><a href="https://pub.dev/packages/flutter_advanced_networkimage" target="_blank">Link</a></span>

An advanced image provider provides caching and retrying for flutter app, with zoomable widget and transition to image widget.

```dart
Image(
  image: AdvancedNetworkImage(
    url,
    header: header,
    useDiskCache: true,
    cacheRule: CacheRule(maxAge: const Duration(days: 7)),
  ),
  fit: BoxFit.cover,
)
```

There are a ton more plugins and this list will keep getting updated as I use them.
