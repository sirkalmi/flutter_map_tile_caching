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
