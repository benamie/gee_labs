# Spectral Resolution

Spectral resolution refers to the number and width of spectral bands in which the sensor takes measurements. You can think of the width of spectral bands as the wavelength intervals for each band. A sensor that measures radiance in multiple bands is called a *multispectral* sensor (generally 3-10 bands), while a sensor with many bands (possibly hundreds) is called a *hyperspectral* sensor (these are not hard and fast definitions). For example, compare the [multi-spectral OLI](http://landsat.gsfc.nasa.gov/?p=5779) aboard Landsat 8 to [Hyperion](https://eo1.usgs.gov/sensors/hyperioncoverage), a hyperspectral sensor aboard the [EO-1 satellite](https://eo1.usgs.gov/).

*Would be helpful to have a image of spectral resolution here* 

There is an easy way to check the number of bands in Earth Engine, but no way to get an understanding of the relative *spectral response* of the bands, where spectral response is a function measured in the laboratory to characterize the detector. 

To see the number of bands in an image, use:

```javascript
// Get the MODIS band names as a List
var modisBands = modisImage.bandNames();
// Print the list.
print('MODIS bands:', modisBands);
// Print the length of the list.
print('Length of the bands list:', modisBands.length());
```

It's worth noting that only some of those bands contain radiometric data. Lots of them have other information, like quality control data. So the band listing isn't necessarily an indicator of spectral resolution,     but can inform your investigation of the spectral resolution of the dataset. Try printing the bands from some of the other sensors to get a sense of spectral resolution.