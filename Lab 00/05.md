# Features 

## Features

At the most basic definition, a Feature in GEE is an object which stores a `geometry` property (`Point`, `Line`, `Polygon`) along with it's associated properties. GEE uses the GeoJSON format to store and transmit these features. In the previous video, we saw how to build geometries within Google Earth Engine, a feature adds meaningful information to it. This would be a good section to review working with dictionaries with JavaScript.

Let's say we created an individual point, which we want to associate with data that we collected. The first line establishes the variable `point`, which is then used as the `geometry` to create a `feature`. The curly braces represent a JavaScript dictionary, which creates Key:Value pairs, which in our case is the type of tree and a measurement of the size. this new variable, `treeFeature`, now contains geographic information along with attribute data about that point. 

```javascript
// geometry created from within GEE
var point = ee.Geometry.Point([-79.68, 42.06]);
// Create a Feature from the geometry
var treeFeature = ee.Feature(point, {type: 'Pine', size: 15});
```

Obviously this is just one point, but JavaScript and GEE engine provide functionality for bringing different data sources together and automatically associating geometries with attribute data. This can be done within GEE or outside, depending on your preferences.  

## Feature Collections

Just like the relationship between images and image collections, Feature Collections are Features that can be grouped together for ease of use and analysis. They can be different types and combinations of geometry, as well as associated tabular data. The code segment from the documentation consolidates the operations discussed earlier. Each line has an interior layer which creates the geometry (`ee.Geometry.---()` ), which is then associated with attribute data (information within the {} ) and then converted to a Feature. This variable is a JavaScript`list`, which contains three separate features.  This is then converted to a Feature Collection with the command `ee.FeatureCollection(features)`

```javascript
// Make a list of Features.
var features = [
  ee.Feature(ee.Geometry.Rectangle(30.01, 59.80, 30.59, 60.15), {name: 'Voronoi'}),
  ee.Feature(ee.Geometry.Point(-73.96, 40.781), {name: 'Thiessen'}),
  ee.Feature(ee.Geometry.Point(6.4806, 50.8012), {name: 'Dirichlet'})
];

// Create a FeatureCollection from the list and print it.
var fromList = ee.FeatureCollection(features);
print(fromList);
```

If you take this code block and run it in Google Earth Engine, you can see the information that is contained within the FeatureCollection, which has three elements (Features) and two columns (the `index` and the `properties`). By clicking on the dropdown next to each one, you can see that the first feature is a Polygon that has the name of 'Voronoi'.

![Screen Shot 2021-08-21 at 1.19.21 PM](./im2.png)

Once you have information in a Feature Collection, you can filter it to find specific information, such as the name of an object or based on the size of a polygon, or provide aggregated analysis. The [documentation](https://developers.google.com/earth-engine/guides/features) on working with Feature Collections  is comprehensive, and provides many ideas on how to use them efficiently in in your analysis. 