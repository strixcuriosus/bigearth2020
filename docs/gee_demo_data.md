For this workshop, we will be exploring a dataset of Planet's Surface Reflectance product in California in 2018.

## Collection Access

Make sure this collection import works for you:
```
var imageCollection = ee.ImageCollection("projects/sat-io/open-ca/ps4bsr");
print(imageCollection.size());
```

## What's in this Collection
This ImageCollection contains 2273 surface reflectance images. 

Planet's surface reflectance assets are atmospherically-corrected analytic imagery stored as 16-bit scaled (surface). These images have 4 bands:

- Blue: 455 - 515 nm
- Green: 500 - 590 nm
- Red: 590 - 670 nm
- NIR: 780 - 860 nm

Find more details about the Surface Reflectance (SR) product in Planet's **[imagery product spec](https://assets.planet.com/docs/combined-imagery-product-spec-april-2019.pdf)**