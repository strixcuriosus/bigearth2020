We can visualize Planet's iamagery on the Earth Engine Map.

## Get the dataset
First, make sure to import this ImageCollection:

```
var imageCollection = ee.ImageCollection("projects/sat-io/open-ca/ps4bsr");
```

## Show an image
Now, let's set up some visualization params
```
var visualBands = ["b3","b2","b1];
var falseColorBands = ["b4","b3","b2"];

// try changing these
var visParams = {
  "opacity":1,
  "bands": visualBands,
  "min":0,
  "max":10000
};
```

Get the first image from the collection, and center the Map around it.

```
var firstImage = imageCollection.first();
Map.centerObject(imageCollection.first(), 12)
```

Add the image as a Map layer using the image id to name the layer.

```
var imageId = firstImage.id().getInfo()
print(imageId)
Map.addLayer(firstImage, visParams, imageId)
```

## Change the parameters
Look at the per-band min and max values in the image:
```
print(firstImage.reduceRegion({reducer: ee.Reducer.minMax(), scale: 30}));
```

Try changing the visParams in the code editor or in the "Layers" settings on the Map UI.

Inspect the image to see available metadata.

Clip the image to an area of interest.