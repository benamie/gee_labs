# Data and Algorithms

## Core Components of Google Earth Engine 

Google Earth Engine starts with an introduction of data structures and the operations you can use to analyze your data structures. To work effectively with GEE, it is essential that you understand these core components and how to complete basic operations with each of them. 

[Intro to Data](https://developers.google.com/earth-engine/guides)

- [`Image`](https://developers.google.com/earth-engine/guides/image_overview)
  - Fundamental raster data type in Earth Engine.
- [`ImageCollection`](https://developers.google.com/earth-engine/guides/ic_creating)
  - Stack or time-series of images.
- [`Geometry`](https://developers.google.com/earth-engine/guides/geometries)
  - Fundamental vector data type in Earth Engine.
- [`Feature`](https://developers.google.com/earth-engine/guides/features)
  -  `Geometry` with specific attributes.
- [`FeatureCollection`](https://developers.google.com/earth-engine/guides/feature_collections)
  - Set of features.
- [`Reducer`](https://developers.google.com/earth-engine/guides/reducers_intro)
  - Object used to compute statistics or perform aggregations
- [`Join`](https://developers.google.com/earth-engine/guides/joins_intro)
  - Combine datasets (`Image` or `Feature` collections) based on time, location, or an attribute property.
- [`Array`](https://developers.google.com/earth-engine/guides/arrays_intro)
  - Multi-dimensional analyses.

## Image and Image Collection

There are two most fundamental data structures within Earth Engine, which work in conjunction with each other: images and features. 

#### Images

**Images** are **Raster** objects composed of:

- Bands, or layers with a unique:
  - Name
  - Data type
  - Scale
  - Mask
  - Projection

Additionally, each image has a set of metadata stored as a set of properties. You are able to create images from constants, lists or other objects. In the code editor 'docs', you'll find numerous processes you can apply to images. 

Ensure that you do not confuse an individual image with an image collection, which is a set of images grouped together, often as a time series. For those familiar with remote sensing terminology, a `stack` is comparable terminology. 

#### Image Collection

- Explanation  of extracting an image from an image collection 

```js
var first = ee.ImageCollection('COPERNICUS/S2_SR')
                .filterBounds(ee.Geometry.Point(-70.48, 43.3631))
                .filterDate('2019-01-01', '2019-12-31')
                .sort('CLOUDY_PIXEL_PERCENTAGE')
                .first();
Map.centerObject(first, 11);
Map.addLayer(first, {bands: ['B4', 'B3', 'B2'], min: 0, max: 2000}, 'first');
```

* Include discussion about sensed vs. derived datasets 

**Features**

- Vector objects

- Composed of:

  - Geometry (points, lines, polygons)
  - Dictionary of properties

- Feature Collection

  - Numerous features