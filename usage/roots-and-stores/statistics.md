---
description: Applies to Roots & Stores
---

# Statistics

You can retrieve statistics about your Roots and Stores. For Roots, you can view the number of cached tiles, the total file size of your cached tiles, and which Stores are available within the Root.



For Stores, you can retrieve the number of cached tiles, the size of the cached tiles, as well as statistics related tile access during browsing such as how many tiles were retrieved, either successfully or unsuccessfully.

```dart
FlutterMapTileCaching.instance.rootDirectory.stats; // Roots
FlutterMapTileCaching.instance('storeName').stats; // Stores
```

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/RootStats-class.html" %}

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/StoreStats-class.html" %}

## Watching For Changes

```dart
FMTC.instance.rootDirectory.stats.watchChanges(); // Roots
FMTC.instance('storeName').stats.watchChanges(); // Stores
```

It is possible to watch for changes in structures, which can be useful to create dynamic UIs (using `StreamBuilder`s) that consume the other statistics. There are lots of customization options to increase efficiency and reduce junk/useless rebuilds.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/RootStats/watchChanges.html" %}

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/StoreStats/watchChanges.html" %}
