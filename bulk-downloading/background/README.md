---
description: fmtc_plus_background_downloading Module
---

# 3⃣ Start In Background

{% hint style="success" %}
The [`fmtc_plus_background_downloading`](https://github.com/JaffaKetchup/fmtc\_plus\_background\_downloading) module is required to use the background bulk downloading functionality.

Note this functionality is only available on Android.

See the [#fmtc\_plus\_background\_downloading-installation-and-setup](../../get-started/additional-setup.md#fmtc\_plus\_background\_downloading-installation-and-setup "mention") instructions to add this module.
{% endhint %}

{% hint style="info" %}
You should read about the [limitations and tradeoffs of background downloading](limitations.md) before you use it.
{% endhint %}

{% hint style="warning" %}
Before using FMTC, especially to bulk download, ensure you comply with the appropriate restrictions and terms of service set by your tile server. Failure to do so may lead to any punishment, at the tile server's discretion.

This library and/or the creator(s) are not responsible for any violations you make using this package.

***

Some common tile servers' ToS are listed below:

* [OpenStreetMap](https://operations.osmfoundation.org/policies/tiles)
* [Mapbox](https://www.mapbox.com/legal/tos)
* [Thunderforest](https://www.thunderforest.com/terms/)
* [Stadia Maps](https://stadiamaps.com/terms-of-service/)

For testing purposes, check out the testing tile server included in the FMTC project: [#testing-your-application](../introduction.md#testing-your-application "mention").
{% endhint %}

```dart
FMTC.instance('storeName').download.startBackground();
```

{% embed url="https://pub.dev/documentation/fmtc_plus_background_downloading/latest/fmtc_plus_background_downloading/FMTCBackgroundDownloadingModule/startBackground.html" %}

## Additional Preparation

You should also wrap your application's root widget (such as a `Scaffold`) with the [`FMTCBackgroundDownload`](https://pub.dev/documentation/flutter\_map\_tile\_caching/5.0.0-dev.6/fmtc\_advanced/FMTCBackgroundDownload-class.html) widget.

This is designed to stop the app from terminating when it is taken off the widget tree, such as when the user closes the application. It is safe to leave there even when not downloading: it is intelligent enough to only keep the application alive if there is an ongoing background download.
