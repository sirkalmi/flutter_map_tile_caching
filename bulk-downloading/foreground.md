# 3⃣ Start In Foreground

{% hint style="warning" %}
Before using FMTC, especially to bulk download, ensure you comply with the appropriate restrictions and terms of service set by your tile server. Failure to do so may lead to any punishment, at the tile server's discretion.

This library and/or the creator(s) are not responsible for any violations you make using this package.

***

Some common tile servers' ToS are listed below:

* [OpenStreetMap](https://operations.osmfoundation.org/policies/tiles)
* [Mapbox](https://www.mapbox.com/legal/tos)
* [Thunderforest](https://www.thunderforest.com/terms/)
* [Stadia Maps](https://stadiamaps.com/terms-of-service/)

For testing purposes, check out the testing tile server included in the FMTC project: [#testing-your-application](introduction.md#testing-your-application "mention").
{% endhint %}

Finally! Now you can start downloading the region. There's many customization options available, so we recommend reading through the API documentation for the `startForeground` method.

```dart
FMTC.instance('storeName').download.startForeground(
    region: downloadableRegion,
    // Many more options available!
).listen((evt) {});
```

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/DownloadManagement/startForeground.html" %}

{% hint style="success" %}
You should always monitor the progress of the download.

This is done by listening to the stream returned by the `startForeground` method. The `DownloadProgress` object contains enough information to create a complex UI to keep the user fully informed.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/DownloadProgress-class.html" %}
{% endhint %}

## Multiple Simultaneous Downloads

{% hint style="warning" %}
It is not recommended to start more than one download simultaneously, as it places extra strain on the device and may cause each download to progress slower than it otherwise would. It may also cause Isar to crash in some circumstances.

Avoid doing this unless it is a necessity.
{% endhint %}

It is possible to start and control multiple downloads simultaneously, as they are all isolated from each other. Simply pass through a unique `Object` to the `instanceId` of all methods. Keep track of this 'key' yourself, and it can be used to control its respective download.

An individual download has the ability to multi-thread without starting multiple downloads.
