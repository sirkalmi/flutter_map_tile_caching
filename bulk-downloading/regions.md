# 1⃣ Create A Region

Regions (`BaseRegion`s) are geographical areas that do not yet have any of the necessary extra information to start a download (like `DownloadableRegion`s).

The [example-application.md](../get-started/example-application.md "mention") contains a great way you might want to allow your users to choose a region to download, and it shows how to use Provider to share a created region and the number of approximate tiles it has to a download screen.

## Types Of Region

{% tabs %}
{% tab title="Rectangle" %}
The most basic type of region, defined by two North West and South East coordinates that create a `LatLngBounds`.

```dart
final region = RectangleRegion(
    LatLngBounds(
        LatLng(), // North West
        LatLng(), // South East
    ),
);
```

This is usually all you get from most apps, so why not give your user a unique experience with some of our other region types...
{% endtab %}

{% tab title="Circle" %}
A more advanced type of region, defined by a center coordinate and radius (in kilometers).

Many cities are circular, so this could be used to download a planned tourist adventure, for example.

```dart
final region = CircleRegion(
    LatLng(), // Center
    0, // KM Radius
);
```

If you have two coordinates, one center, and one on the edge of the circle you want, you can use ['latlong2's `Distance.distance()`](https://pub.dev/documentation/latlong2/latest/latlong2/Distance/distance.html) method, as below:

```dart
final region = CircleRegion(
    LatLng(), // Center
    const Distance(roundResult: false).distance(
        LatLng(), // Center
        LatLng(), // Edge Coord
    ) / 1000; // Convert to KM
);
```
{% endtab %}

{% tab title="Line-based" %}
The most advanced type of region, defined by a list of coordinates and radius (in meters).

This could be used to download tiles along a planned travel route, for example hiking or long-distance driving. Import coordinates from a routing engine, or from a GPX/KML file for maximum integration!

```dart
final region = LineRegion(
    [LatLng(), LatLng(), ...], // List of coordinates
    0, // Radius in meters
);
```

{% hint style="warning" %}
This type of region may temporarily consume more memory when generating tiles that the other regions.
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Custom polygons, skewed parallelograms (rectangles with a 3rd control point), and rotated rectangles are not yet supported as regions, but some may be able to be imitated by a Line-based region.
{% endhint %}

After you've created your region, you can convert it to a drawable polygon (below), or [convert it to a `DownloadableRegion`](prepare.md) ready for downloading.

## Converting To Drawable Polygons

All `BaseRegions` can be drawn on a map with minimal effort from you or the user, using `toDrawable()`.

Internally, this uses the `toOutline(s)` method to generate the points forming the `Polygon`, then it places this/these polygons into a `PolygonLayer`.
