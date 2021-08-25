

#Orbits and Sensor Motion

The image data are collected from moving platforms (satellites or aircraft). The motion of the platform, together with the imaging geometry of the sensor, determines the spatio-temporal resolution of the data. To get an idea for how these design choices interact to produce the wonderful imagery in Earth Engine, examine [the orbit of the Aqua satellite](http://svs.gsfc.nasa.gov/vis/a000000/a003300/a003348/aquacomp720.mp4) for a selected day in 2013.

Load and display MODIS (Aqua) sensor zenith angle for imagery collected on September 1, 2013:

```javascript
var aquaImage = ee.Image(myd09.filterDate('2013-09-01').first());
// Zoom to global level.
Map.setCenter(81.04, 0, 3);
// Display the sensor-zenith angle of the Aqua imagery.
var szParams = {bands: 'SensorZenith', min: 0, max: 70*100};
Map.addLayer(aquaImage, szParams, 'Aqua sensor-zenith angle');
```

To understand where those visualization parameters come from, expand the 'Layers' section on [this page](https://lpdaac.usgs.gov/dataset_discovery/modis/modis_products_table/mod09ga).

We've stored some satellite positions from September 1, 2013 in a comma-delimited file, which is stored as an asset at this address: /users/book/etc. Accessing that asset give you access to a FeatureCollection of points:

```javascript
var aquaOrbit = ee.FeatureCollection('ft:1ESvPygQ76WvVflKMN2nc14sS2wwtzqv3j2ueTqg');
```

Display     the points by [adding them to the map](https://developers.google.com/earth-engine/feature_collections_visualizing). (If you have other layers displayed from the previous sections, either comment the Map.addLayer() lines, or add **false** as a fourth argument to Map.addLayer(), so that they will be turned off by default.) Zoom the map to a global view:

```javascript
Map.addLayer(aquaOrbit, {color: 'FF0000'}, 'Aqua Positions');
```

Compare this orbit, and the swath of imagery, to a [Landsat orbit](http://svs.gsfc.nasa.gov/vis/a010000/a011400/a011481/G2014-016_LDCM_orbit_MASTER_ipod_lg.m4v) from the same day. To explore the difference, color the landsat imagery blue:

```javascript
// Load Landsat ETM+ data directly, filter to one day.
var landsat7 = ee.ImageCollection('LANDSAT/LE7')
		.filterDate('2013-09-01', '2013-09-02');
// Display the images by specifying one band and a single color palette.
Map.addLayer(landsat7, {bands: 'B1', palette: 'blue'}, 'Landsat 7 scenes');
```