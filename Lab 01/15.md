#Temporal Resolution

Temporal resolution refers to the *revisit time*, or temporal *cadence* of a particular sensor’s image stream. Think of this as the frequency of pixels in a time series at a given location. 

**MODIS**. MODIS (either Terra or Aqua) produces imagery at approximately daily cadence. To see the time series of images at a location, you can print() the ImageCollection, filtered to your area and date range of interest. For example, to see the MODIS images in 2011:

```javascript
// Filter the MODIS mosaics to one year.   
var modisSeries = myd09.filterDate('2011-01-01', '2011-12-31');      
// Print the filtered  MODIS ImageCollection.   
print('MODIS series:', modisSeries);  
```

Expand the features property of the printed ImageCollection to see a List of all the images in the collection. Observe that the date of each image is part of the filename. Note the daily cadence. Observe that each MODIS image is a global mosaic, so there's no need to filter by location.

**Landsat**. Landsats (5 and later) produce imagery at 16-day cadence. TM and MSS are on the same satellite (Landsat 5), so it suffices to print the TM series to see the temporal resolution. Unlike MODIS, data from these sensors is produced on a scene basis, so to see a time series, it's necessary to filter by location in addition to     time:

```javascript
// Filter to get a year's worth of TM scenes.
var tmSeries = tm
  .filterBounds(Map.getCenter())
  .filterDate('2011-01-01', '2011-12-31');
// Print the filtered TM ImageCollection. 
print('TM series:', tmSeries);
```

Again expand the features property of the printed ImageCollection. Note that a [careful parsing of the TM image IDs](http://landsat.usgs.gov/naming_conventions_scene_identifiers.php) indicates the day of year (DOY) on which the image was collected. A slightly more cumbersome method involves expanding each Image in the list, expanding its properties and looking for the 'DATE_ACQUIRED' property. 

To make this into a nicer list of dates, [map()](https://en.wikipedia.org/wiki/Map_(higher-order_function)) a function over the ImageCollection. First define a function to get a Date from the metadata of each image, using the system properties:

```javascript
var getDate = function(image) {
 // Note that you need to cast the argument
 var time = ee.Image(image).get('system:time_start');
 // Return the time (in milliseconds since Jan 1, 1970) as a Date
 return ee.Date(time);
};
```

Turn the ImageCollection into a List and[ map() the function](https://developers.google.com/earth-engine/getstarted#mapping-what-to-do-instead-of-a-for-loop) over it:

```javascript
var dates = tmSeries.toList(100).map(getDate);
print(dates);
```

 



 

