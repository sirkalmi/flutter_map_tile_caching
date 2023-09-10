---
description: Applies to Roots & Stores
---

# Management

Root management is limited to either resetting or deleting the root. Resetting will clear all the data of the root, essentially reverting it to a newly created state.&#x20;

For Stores, more options exist. Stores have similar methods for resetting and deleting. You can also access tiles directly using the StoreManagement class, rename the store, or create a store.

```dart
FlutterMapTileCaching.instance.rootDirectory.manage; // Roots
FlutterMapTileCaching.instance('storeName').manage; // Stores

FlutterMapTileCaching.instance('storeName').manage.rename('newStoreName'); //Rename
```

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/RootManagement-class.html" %}

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/StoreManagement-class.html" %}
