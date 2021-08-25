# Resampling and ReProjection

Earth Engine makes every effort to handle projection and scale so that you don't have to. However, there are occasions where an understanding of projections is important to get the output you need. As an example, it's time to demystify the [reproject()](https://developers.google.com/earth-engine/apidocs/ee-image-reproject) calls in the previous examples. Earth Engine requests inputs to your computations in the projection and scale of the output. The map attached to the playground has a [Maps Mercator projection](http://epsg.io/3857). The scale is determined from the map's zoom level. When you add something to this map, Earth Engine secretly reprojects the input data to Mercator, resampling (with nearest neighbor) to screen resolution pixels based on the map's zoom level, then does all the computations with the reprojected, resampled imagery. In the previous examples, the reproject() calls force the computations to be done at the resolution of the input pixels: 1 meter.

Re-run the edge detection code with and without the reprojection (Comment out all previous Map.addLayer() calls except for the original one)

```javascript
// Zoom all the way in.
Map.centerObject(point, 21);
// Display edges computed on a reprojected image.
Map.addLayer(image.convolve(laplacianKernel), {min: 0, max: 255}, 
  'Edges with little screen pixels');
// Display edges computed on the image at native resolution.
Map.addLayer(edges, {min: 0, max: 255}, 
  'Edges with 1 meter pixels'); 
```

What's happening here is that the projection specified in reproject() propagates backwards to the input, forcing all the computations to be performed in that projection. If you don't specify, the computations are performed in the projection and scale of the map (Mercator) at screen resolution.

You can control how Earth Engine resamples the input with [resample()](https://developers.google.com/earth-engine/guides/resample). By default, all resampling is done with the nearest neighbor. To change that, call resample() on the *inputs*. Compare the input image,     resampled to screen resolution with a bilinear and bicubic resampling:

```javascript
// Resample the image with bilinear instead of the nearest neighbor.
var bilinearResampled = image.resample('bilinear');
Map.addLayer(bilinearResampled, {}, 'input image, bilinear resampling');
// Resample the image with bicubic instead of the nearest neighbor.
var bicubicResampled = image.resample('bicubic');
Map.addLayer(bicubicResampled, {}, 'input image, bicubic resampling');
```

Try zooming in and out, comparing to the input image resampled with the nearest with nearest neighbor (i.e. without resample() called on it).

Note: ***You should rarely, if ever, have to use\*** **reproject() *and\*** **resample()**. Do not use reproject() or resample() resample unless necessary. They are only used here for demonstration purposes.