# Introduction

FMTC also provides the ability to bulk download areas of maps in one-shot, known as 'regions'.

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

Square and [rectangular](regions.md#rectangle) regions are boring, but can be useful sometimes. However, FMTC goes above and beyond, and also offers both [circular](regions.md#circle) and [line-based](regions.md#line-based) regions, so now you can download just the tiles along your travel route!

Downloading is extremely efficient and fast, and uses multiple threads and isolates to achieve write speeds of hundreds of tiles per second (if the network/server speed allows).

After downloading, tiles are stored in the same place as when Browse Caching, meaning that no extra setup is needed to use them in a map (other than the usual [integration.md](../usage/integration.md "mention")).

## 4½ Steps To Downloading

Downloading is simple: take a geographical region, add some extra information to it, then download it!

1. [Create a region based on the user's input](regions.md)
2. [Convert that region into a downloadable region](prepare.md)
3. Start downloading that region, either in the [foreground](foreground.md) or [background](background/)
4. Listen for progress events to update your user
5. (Optionally, [control the download](control-downloads.md))

## Multiple Simultaneous Downloads

{% hint style="warning" %}
It is not recommended to start more than one download simultaneously, as it places extra strain on the device and may cause each download to progress slower than it otherwise would. It may also cause Isar to crash in some circumstances.

Avoid doing this unless it is a necessity.
{% endhint %}

It is possible to start and control multiple downloads simultaneously, as they are all isolated from each other. Simply pass through a unique `Object` to the `instanceId` of all methods. Keep track of this 'key' yourself, and it can be used to control its respective download.

An individual download has the ability to multi-thread without starting multiple downloads.
