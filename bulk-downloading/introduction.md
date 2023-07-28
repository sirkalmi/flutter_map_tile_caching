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

For testing purposes, check out the testing tile server included in the FMTC project: [#testing-your-application](introduction.md#testing-your-application "mention").
{% endhint %}

Square and [rectangular](regions.md#rectangle) regions are boring, but can be useful sometimes. However, FMTC goes above and beyond, and also offers both [circular](regions.md#circle) and [line-based](regions.md#line-based) regions, so now you can download just the tiles along your travel route!

Downloading is extremely efficient and fast, and uses multiple threads and isolates to achieve write speeds of hundreds of tiles per second (if the network/server speed allows). It is also simple to understand and implement:

1. [Create a region based on the user's input](regions.md)
2. [Convert that region into a downloadable region](prepare.md)
3. Start downloading that region, either in the [foreground](foreground.md) or [background](background/)
4. Listen for progress events to update your user
5. (Optionally, [control the download](control-downloads.md))

After downloading, tiles are stored in the same place as when Browse Caching, meaning that no extra setup is needed to use them in a map (other than the usual [integration.md](../usage/integration.md "mention")).

## Testing Your Application

{% hint style="success" %}
Avoid making too many costly and slow requests to your chosen tile server during development by using the basic tile server included with the FMTC project!
{% endhint %}

Since v9, a miniature tile server, intended to test and calibrate FMTC, has been included in the project.

For internal testing and development purposes, it also doubles down as a handy way to test your application without making too many costly and slow requests to your chosen tile server. When in use with the example application, it can handle over 2000 tiles/second.

It is a very simple web HTTP server written in Dart, that responds to all\* requests with a tile. There is a theoretically 90% chance that this tile will be a specific land tile, and a 10% chance that it will be a sea tile - designed to test the sea tile skipping functionality. _There are only these two tiles - it is not a full tile server._

<div>

<figure><img src="../.gitbook/assets/land.png" alt="" width="128"><figcaption><p><em>the</em> Land Tile<br>90% chance</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/sea.png" alt="" width="128"><figcaption><p><em>the</em> Sea Tile<br>10% chance</p></figcaption></figure>

</div>

To use this tile server:

{% hint style="info" %}
The tile server is hardcoded to use standard HTTP port 8080 to serve content. Other programs must not be using this port.
{% endhint %}

1. Download/compile & start the tile server (no permanent installation required)
   * On Windows\
     Download a copy of the latest 'windows-ts' artifact from GitHub Actions, and run the executable inside
   * On Linux\
     Download a copy of the latest 'linux-ts' artifact from GitHub Actions, and run the executable inside
   * On other platforms\
     Clone the [FMTC GitHub repository](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/) to your device, then use `dart run` to run '/test/tools/tile\_server/bin/tile\_server.dart' manually
2. Use the following URL to connect to it
   * From the local device (preferred): `http://localhost:8080/{z}/{x}/{y}.png`
   * From the same network: `http://<your-local-ip>:8080/{z}/{x}/{y}.png`\
     To find your local IP address, follow the [instructions for your OS here](https://www.avast.com/c-how-to-find-ip-address)
3. Control the tile server using keyboard key presses in the console window
   * `q`: Release port 8080 and quit the executable
   * UP arrow: Increase the artificial delay between request and response by 2ms
   * DOWN arrow: Decrease the artificial delay between request and response by 2ms
