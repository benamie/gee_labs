# Reducer

Up until this point, we have been talking about objects: Images, Features and Geometries. Reducers are a method of aggregating data for analysis. For instance, we could take an Image Collection and use `reducer` to find the average value at each pixel, resulting in a single layer. Or we could reduce an image to a set of regions, grouping similar data together to create a simplifed map. The applications of Reducer are endless, and can be applied to both Images and Features. There are different functions for different object types, and Reducer can be both combined and sequenced to create a chain of analysis. From the documentation, the code chunk below   creates the variable `collection` which is a collection that is filtered to the year 2016 and defined to a specific point. The variable `extrema` then reduces the dataset to identify the minimum and maximum value at that specific point for every band.

```javascript
// Load and filter the Sentinel-2 image collection.
var collection = ee.ImageCollection('COPERNICUS/S2')
    .filterDate('2016-01-01', '2016-12-31')
    .filterBounds(ee.Geometry.Point([-81.31, 29.90]));
// Reduce the collection.
var extrema = collection.reduce(ee.Reducer.minMax());
```

If you print `extrema` in the console, you can see that the result is 32 separate 'bands', which represents the minimum and maximum value for all 16 bands in the Sentinel data. In the screenshot below, you can expand the first 'band', which identifies the attributes of the minimum value of Band 1. 

![Screen Shot 2021-08-21 at 2.34.40 PM](./im3.png)

There are hundreds of different operations for using Reducer, with the functions listed on the left hand table under 'Docs'. Certain functions will only work with specific object types, but follow along with the Reducer [documentation](https://developers.google.com/earth-engine/guides/reducers_intro) to get a better understanding of how to aggregate data and extract meaningful results. Getting familiar with Reducer is an essential component to working with Google Earth Engine. 

![Screen Shot 2021-08-21 at 2.31.01 PM](./im4.png)

## 