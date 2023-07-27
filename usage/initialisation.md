# Initialisation

{% hint style="warning" %}
Before using FMTC, especially to bulk download, ensure you comply with the appropriate restrictions and terms of service set by your tile server. Failure to do so may lead to any punishment, at the tile server's discretion.

This library and/or the creator(s) are not responsible for any violations you make using this package.

***

Some common tile servers' ToS are listed below:

* [OpenStreetMap](https://operations.osmfoundation.org/policies/tiles)
* [Mapbox](https://www.mapbox.com/legal/tos)
* [Thunderforest](https://www.thunderforest.com/terms/)
* [Stadia Maps](https://stadiamaps.com/terms-of-service/)

For testing purposes, check out the testing tile server included in the FMTC project: [#testing-your-application](../bulk-downloading/introduction.md#testing-your-application "mention").
{% endhint %}

The main basis of this package is the `FlutterMapTileCaching` object, which exposes the majority of FMTC's APIs (through `FMTC.instance`), and also contains most of the state needed to connect and communicate with the underlying systems.

Therefore, it must be asynchronously initialised on every app startup, usually in the `main` method that runs directly after the Flutter environment starts.

<pre class="language-dart" data-title="main.dart"><code class="lang-dart">import 'package:flutter/widgets.dart';
import 'package:flutter_map_tile_caching/flutter_map_tile_caching.dart';

Future&#x3C;void> main() async {
    <a data-footnote-ref href="#user-content-fn-1">WidgetsFlutterBinding.ensureInitialized();</a>   
    
<strong>    await FlutterMapTileCaching.initialise();
</strong><strong>    //FMTC.instance;
</strong>    
    // Run your app and do all of that other stuff
}
</code></pre>

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/FlutterMapTileCaching/initialise.html" %}

{% hint style="success" %}
`FMTC` is a shorthand type alias for `FlutterMapTileCaching`.

Prefer using the shorthand version for conciseness, except where extra clarity is required.
{% endhint %}

{% hint style="danger" %}
You must call `initialise()` before trying to use `instance`. Failure to do so will throw a `StateError`.
{% endhint %}

## Initialisation Safety

{% hint style="info" %}
In summary, in the extremely unlikely event of database corruption, FMTC can recover automatically (in most circumstances), with minimal data loss, given enough fatal app crashes - corruption cannot be caught in any other way.
{% endhint %}

Whilst it is (almost) impossible for one of the underlying [Isar](https://isar.dev/) databases to become corrupted during normal usage, or even due to a bug, it can happen if the database file is modified manually.

In this case, it is currently impossible to avoid a fatal crash during initialisation, as the database reader/parser crashes all Dart threads & isolates without warning. Please see this issue I opened:

{% embed url="https://github.com/isar/isar/issues/1011" %}

However, FMTC has a workaround.

By using a basic temporary text file, the IDs/filenames of successfully opened databases can be recorded. Once all databases have been opened, the file is deleted, meaning that the safety system will not intervene on the next app launch. However, if a database open attempt crashes the app, the file will not be deleted, and it will contain the list of safe databases.

Because the order in which databases are opened is determinate (alphabetical), the app can open every database one by one, (metaphorically) crossing it off the list. When there are no more safe databases, but more database files, the next database is deleted instead of being opened. The initialisation then continues as normal, still using the file appropriatley.

Therefore, one fatal crash is enough to detect one faulty database, and delete it, allowing the app to initialise normally on the next launch.

If there are multiple corrupted databases (`n`), one fatal crash is needed per database, so the app will successfully open after `n + 1`.

All of this means that FMTC can usually recover from a database corruption with minimal data loss. However, if the database filenames/IDs are also changed, the behaviour is unspecified, especially if the initialisation file already exists.

[^1]: A Flutter method required to prevent a fatal error from occurring on app launch.
