Working with the same ImageCollection from before, we can demonstrate filtering by location, time, and metadata

## Load the collection 
see how many images it contains:
```
var imageCollection = ee.ImageCollection("projects/sat-io/open-ca/ps4bsr");
print(imageCollection.size())
```

## Filter to a region of interest

You can draw polygons direcly on the map or create them in the code editor:

```
var geometry = ee.Geometry.Polygon(
    [[[-121.60537095765662, 39.81212205030285],
      [-121.60537095765662, 39.779412655667514],
      [-121.55902238587927, 39.779412655667514],
      [-121.55902238587927, 39.81212205030285]]], null, false)

Map.centerObject(geometry, 12)
Map.addLayer(geometry, {color: '8c1515'})
``` 

Filter the collection by region:
```
var filteredCollection = imageCollection.filterBounds(geometry);
print("Region filtered:", filteredCollection.size());
```

## Filter location and by time
Chain a date filter:
```
var filteredCollection = imageCollection
.filterBounds(geometry)
.filterDate('2018-11-01', '2018-11-15');

print("Region and date filtered:", filteredCollection.size());
```

Try to filter on medadata like cloud cover!