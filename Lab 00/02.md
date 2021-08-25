# Data and Methods

## Core Components of Google Earth Engine 

Google Earth Engine starts with an introduction of data structures and the operations you can use to analyze your data structures. To work effectively with GEE, it is essential that you understand these core components and how to complete basic operations with each of them. 

[Intro to Data](https://developers.google.com/earth-engine/guides)

- [`Image`](https://developers.google.com/earth-engine/guides/image_overview)
  - Raster Image, a fundamental data type within Earth Engine
- [`ImageCollection`](https://developers.google.com/earth-engine/guides/ic_creating)
  - A "stack" or sequence of images with the same attributes
- [`Geometry`](https://developers.google.com/earth-engine/guides/geometries)
  - Vector data either built within Earth Engine or imported
- [`Feature`](https://developers.google.com/earth-engine/guides/features)
  -  `Geometry` with specific attributes.
- [`FeatureCollection`](https://developers.google.com/earth-engine/guides/feature_collections)
  - Set of features that share a similar theme
- [`Reducer`](https://developers.google.com/earth-engine/guides/reducers_intro)
  - A method used to compute statistics or perform aggregations on the data over space, time, bands, arrays, and other data structures.
- [`Join`](https://developers.google.com/earth-engine/guides/joins_intro)
  - A method to combine datasets (`Image` or `Feature` collections) based on time, location, or another specified attribute 
- [`Array`](https://developers.google.com/earth-engine/guides/arrays_intro)
  - A flexible (albeit sometimes inefficient) data structure that can be used for multi-dimensional analyses.

