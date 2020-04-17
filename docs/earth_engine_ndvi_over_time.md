# Band Math
Since these images have visible and NIR bands, we can calculate the [Normalized Difference Vegetation Index (NDVI)](https://earthobservatory.nasa.gov/features/MeasuringVegetation/measuring_vegetation_2.php) to visualize vegetation density patterns.

How might vegetation density be relevant to wildland fire monitoring, prediction, and prevention?

## Calculating NDVI
We can take a normalized difference in the NIR and red bands like this:
```
var img = imageCollection.first();
var nir = img.select('b4');
var red = img.select('b3');
var ndvi = nir.subtract(red).divide(nir.add(red)).rename('NDVI');
print(ndvi)
```

This results in a new image with an NDVI band. 

You can get the median NDVI of that image like this:
```
print(ndvi.reduceRegion({reducer: ee.Reducer.median(), scale: 30}));
```

Visualizing the NDVI band:
```
var visParams = {min: 0, max: 1};
Map.addLayer(ndvi, visParams, "ndvi");
```

There's a builtin `normalizedDifference` function we can use:
```
var ndvi2 = img.normalizedDifference(['b4', 'b3']).rename('NDVI');
print(ndvi2.reduceRegion({reducer: ee.Reducer.median(), scale: 30}));
```

## NDVI on the whole collection
Above we showed how to get NDVI for one image. Let's calculate NDVI for the whole collection:

```
function addNDVI(image) {
  return image.addBands(image.normalizedDifference(['b4', 'b3']).rename('NDVI'));
}

var ndviCol = imageCollection.map(addNDVI).select('NDVI');
```

Visually inspect the new collection on the Map:

```
Map.addLayer(ndviCol.first(), visParams, "ndvi2");
```

### Timeseries

Add a geometry to your map before running this chart generation snippet:

```
print(ui.Chart.image.seriesByRegion(ndviCol, [geometry], ee.Reducer.mean(), 'NDVI', 30, 'system:time_start'))
```

you can replace the single `[geometry]` array with an array of multiple geometries to get per-region line graphs!
