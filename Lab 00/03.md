# Image and Image Collection

#### Images

**Images** are **Raster** objects composed of:

- Bands, or layers with a unique:
  - Name
  - Data type
  - Scale
  - Mask
  - Projection

Additionally, each image has a set of metadata stored as a set of properties. You are able to create images from constants, lists or other objects. In the code editor 'docs', you'll find numerous processes you can apply to images. 

Ensure that you do not confuse an individual image with an image collection, which is a set of images grouped together, most often as a time series. For those familiar with remote sensing terminology, this is the same thing as a `stack`.

#### Image Collection

Let's analyze the code below, which is an established method of extracting one individual image from an image collection. You can copy and paste this code snippet into the code editor to follow along.

On the first line, we see that we are creating a JavaScript variable named `first`, and then using `ee` in front of `ImageCollection`, which signifies we are requesting information from GEE. The data we are importing ('COPERNICUS/S2_SR') is the Sentinel-2 MSI: MultiSpectral Instrument, Level-2A, with more information found in the dataset [documentation](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR?hl=en#description). 

The next four steps further refine the extraction of an image from an image collection. 

1. `.filterBounds` filters data to the area specified, in this case a geometry Point that was created within GEE.
2. `.filterDate` filters between the two dates specified (filtering down to images collected in 2019)
3. `.sort` organizes the images in descending order based upon the perentage of cloudy pixels (this is an attribute of the image, which can be found in the 'Image Properties' tab in the dataset documentation) 
4. `.first` is a JavaScript method of choosing the first image in the list of sorted images

As a result, we can now use the JavaScript variable 'first' to visualize the image. 

`Map.centerObject()` centers the map on the image, and the number is the amount of zoom. The higher that value is, the more zoomed in the image is - you'll likely have to adjust via trial-and-error to find the best fit. 

`Map.addLayer()` adds the visualization layer to the map. Image/image collections will each have a unique naming convention of their bands, so you will have to reference the documentation. GEE uses Red-Green-Blue ordering (as opposed to the popular Computer Vision framework, OpenCV, which uses a Blue-Green-Red convention). `min` and `max` are the values that normalize the value of each pixel to the conventional 0-255 color scale. In this case, although the maximum value of a pixel in all three of those bands is 2000, for visualization purposes GEE will normalize that to 255, the max value in a standard 8-bit image. 

There is a comprehensive [guide](https://developers.google.com/earth-engine/guides/image_visualization) to working on visualization with different types of imagery that goes quite in-depth on working with different types of imagery. It is a worthwhile read, and covers some interesting topics such as false-color composites, mosaicking and single-band visualization. Work with some of the code-snippets to understand how to build visualizations for different sets of imagery. 

```js
var first = ee.ImageCollection('COPERNICUS/S2_SR')
                .filterBounds(ee.Geometry.Point(-70.48, 43.3631))
                .filterDate('2019-01-01', '2019-12-31')
                .sort('CLOUDY_PIXEL_PERCENTAGE')
                .first();
Map.centerObject(first, 11);
Map.addLayer(first, {bands: ['B4', 'B3', 'B2'], min: 0, max: 2000}, 'first');
```

#### Sensed versus Derived Imagery

One additional note: GEE providesa rich suite of datasets, and while many of them are traditional sensed imagery, others are derived datasets. For instance, the *Global Map of Oil Palm Plantations* [dataset](https://developers.google.com/earth-engine/datasets/catalog/BIOPAMA_GlobalOilPalm_v1) provides is derived from analysis on the Sentinel composite imagery. If you look at the 'Bands', there are only three values, which refer to categories of palm plantations. Datasets such as these will have different methods for visualizing the data or working as a mosaic.



