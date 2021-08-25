# Spatial Resolution

In the present context, spatial resolution means pixel size. In practice, spatial resolution depends on the projection of the sensor's instantaneous field of view (IFOV) on the ground and how a set of radiometric measurements are resampled into a regular grid. To see the difference in spatial resolution resulting from different sensors, visualize data at different scales from different sensors.

*an image comparing spectral resolution that sets the reader up for what to expect in the following code would be helpful* 

**MODIS**. There are two Moderate Resolution Imaging Spectro-Radiometers ([MODIS](http://modis.gsfc.nasa.gov/)) aboard the [Terra](http://terra.nasa.gov/) and [Aqua](http://aqua.nasa.gov/) satellites. Different MODIS [bands](http://modis.gsfc.nasa.gov/about/specifications.php) produce data at different spatial resolutions. For the visible bands, the lowest common resolution is 500 meters (red and NIR are 250 meters). Data from the MODIS platforms are used to produce a large number of data sets having daily, weekly, 16-day, monthly, and annual data sets. Outside this lab, you can find a list of MODIS land products [here](https://lpdaac.usgs.gov/dataset_discovery/modis/modis_products_table). 

Search for '[MYD09GA](https://lpdaac.usgs.gov/dataset_discovery/modis/modis_products_table/myd09ga_v006)' and import '*MYD09GA.006 Aqua Surface Reflectance Daily Global 1km and 500m*'. Name the import myd09. 

Zoom the map to SFO airport:

```javascript
// Define a region of interest as a point at SFO airport.
var sfoPoint = ee.Geometry.Point(-122.3774, 37.6194);

// Center the map at that point.

Map.centerObject(sfoPoint, 16);
```

To display a false-color MODIS image, select an image acquired by the Aqua MODIS sensor and display it for SFO:

```javascript
// Get a surface reflectance image from the MODIS MYD09GA collection.
var modisImage = ee.Image(myd09.filterDate('2017-07-01').first());
// Use these MODIS bands for red, green, blue, respectively.
var modisBands = ['sur_refl_b01', 'sur_refl_b04', 'sur_refl_b03'];
// Define visualization parameters for MODIS.
var modisVis = {bands: modisBands, min: 0, max: 3000};
// Add the MODIS image to the ma
Map.addLayer(modisImage, modisVis, 'MODIS');
```

Note the size of pixels with respect to objects on the ground. (It may help to turn on the satellite basemap to see high-resolution data for comparison.) Print the size of the pixels (in meters) with:

```javascript
// Get the scale of the data from the first band's projection:
var modisScale = modisImage.select('sur_refl_b01')
  .projection().nominalScale();
print('MODIS scale:', modisScale);
```

It's also worth noting that these MYD09 data are surface reflectance scaled by 10000 (not TOA reflectance), meaning that clever NASA scientists have done a fancy atmospheric correction for you!

**MSS**. Multi-spectral scanners ([MSS](https://landsat.gsfc.nasa.gov/multispectral-scanner-system)) were flown aboard Landsats 1-5. MSS data have a spatial resolution of 60 meters.

Search for 'landsat 5 mss' and import the result called *'USGS Landsat 5 MSS Collection 1 Tier 2 Raw Scenes'*. Name the import mss.

To visualize MSS data over SFO, for a relatively less cloudy image, use:

```javascript
// Filter MSS imagery by location, date and cloudiness.   
var mssImage = ee.Image(mss     
                        .filterBounds(Map.getCenter())     
                        .filterDate('2011-05-01',  '2011-10-01')     
                        .sort('CLOUD_COVER')     
                        //  Get the least cloudy image.     
                        .first());  
// Display the MSS image as a color-IR composite.
Map.addLayer(mssImage, {bands: ['B3', 'B2', 'B1'], min: 0, max: 200}, 'MSS');
```

Check the scale (in meters) as previously:

```javascript
// Get the scale of the MSS data from its projection:
var mssScale = mssImage.select('B1')
  .projection().nominalScale();
print('MSS scale:', mssScale);
```

**TM**. The Thematic Mapper ([TM](https://landsat.gsfc.nasa.gov/landsat-4-5/tm)) was flown aboard Landsats 4-5. (It was succeeded by the Enhanced Thematic Mapper ([ETM+](https://landsat.gsfc.nasa.gov/about/enhanced-thematic-mapper)) aboard Landsat 7 and the Operational Land Imager ([OLI](https://landsat.gsfc.nasa.gov/landsat-8/operational-land-imager)) / Thermal Infrared Sensor ([TIRS](https://landsat.gsfc.nasa.gov/landsat-8/thermal-infrared-sensor-tirs)) sensors aboard Landsat 8.) TM data have a spatial resolution of 30 meters.

Search for 'landsat 5 toa' and import the first result (which should be '*USGS Landsat 5 TM Collection 1 Tier 1 TOA Reflectance*'. Name the import tm.

To visualize TM data over SFO, for approximately the same time as the MODIS image, use:

```javascript
// Filter TM imagery by location, date and cloudiness.
var tmImage = ee.Image(tm
  .filterBounds(Map.getCenter())
  .filterDate('2011-05-01', '2011-10-01')
  .sort('CLOUD_COVER')
  .first());
// Display the TM image as a color-IR composite.
Map.addLayer(tmImage, {bands: ['B4', 'B3', 'B2'], min: 0, max: 0.4}, 'TM'); 
```

For some hints about why the TM data is not the same date as the MSS data, see [this page](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-5?qt-science_support_page_related_con=0#qt-science_support_page_related_con).

Check the scale (in meters) as previously:

```javascript
// Get the scale of the TM data from its projection:
var tmScale = tmImage.select('B1')
  .projection().nominalScale();
print('TM scale:', tmScale);
```

**NAIP**. The National Agriculture Imagery Program ([NAIP](http://www.fsa.usda.gov/programs-and-services/aerial-photography/imagery-programs/naip-imagery/)) is an effort to acquire imagery over the continental US on a 3-year rotation using airborne sensors. The imagery has a spatial resolution of 1-2 meters. 

Search for 'naip' and import the data set for *'NAIP: National Agriculture Imagery Program'*. Name the import naip. Since NAIP imagery is distributed as quarters of Digital Ortho Quads at irregular cadence, load everything from the most recent year in the acquisition cycle (2012) over the study area and [mosaic()](https://developers.google.com/earth-engine/guides/ic_composite_mosaic) it:

```javascript
// Get NAIP images for the study period and region of interest.
var naipImages = naip.filterDate('2012-01-01', '2012-12-31')
  .filterBounds(Map.getCenter());

// Mosaic adjacent images into a single image.
var naipImage = naipImages.mosaic();
// Display the NAIP mosaic as a color-IR composite.
Map.addLayer(naipImage, {bands: ['N', 'R', 'G']}, 'NAIP');

```

Check the scale by getting the first image from the mosaic (a mosaic doesn't know what its projection is, since the mosaicked images might all have different projections), getting its projection, and getting its scale (meters):

```javascript
// Get the NAIP resolution from the first image in the mosaic.
var naipScale = ee.Image(naipImages.first()).projection().nominalScale();
print('NAIP scale:', naipScale);
```

