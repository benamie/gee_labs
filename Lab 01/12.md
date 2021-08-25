# Digital Image Visualization

You've learned about how an image stores pixel data in each band as DNs and how the pixels are organized spatially. When you add an image to the map, Earth Engine handles the spatial display for you by recognizing the projection and putting all the pixels in the right place. However, you must specify how to stretch the DNs to make an 8-bit display image (e.g. the min and max visualization parameters). Specifying min and max applies (where DN' is the displayed value):

* DN' = (DN - min) * 255 / (max - min)

To apply a [gamma correction](https://en.wikipedia.org/wiki/Gamma_correction) (DN' = DN𝛾), use:

```javascript
// Display gamma stretches of the input image.
Map.addLayer(image.visualize({gamma: 0.5}), {}, 'gamma = 0.5');
Map.addLayer(image.visualize({gamma: 1.5}), {}, 'gamma = 1.5');
```

Note that gamma is supplied as an argument to [image.visualize()](https://developers.google.com/earth-engine/apidocs/ee-image-visualize) so that you can click on the map to see the difference in pixel values (try it!). It's possible to specify gamma, min and max to achieve other unique visualizations.

1. To apply a [histogram equalization](https://en.wikipedia.org/wiki/Histogram_equalization) stretch, use the [sldStyle() method](https://devsite.googleplex.com/earth-engine/image_visualization#styled-layer-descriptors):

```javascript
// Define a RasterSymbolizer element with '_enhance_' for a placeholder.
var histogram_sld =
  '<RasterSymbolizer>' +
    '<ContrastEnhancement><Histogram/></ContrastEnhancement>' +
    '<ChannelSelection>' +
      '<RedChannel>' +
        '<SourceChannelName>R</SourceChannelName>' +
      '</RedChannel>' +
      '<GreenChannel>' +
        '<SourceChannelName>G</SourceChannelName>' +
      '</GreenChannel>' +
      '<BlueChannel>' +
        '<SourceChannelName>B</SourceChannelName>' +
      '</BlueChannel>' +
    '</ChannelSelection>' +
  '</RasterSymbolizer>';

// Display the image with a histogram equalization stretch.
Map.addLayer(image.sldStyle(histogram_sld), {}, 'Equalized');
```

The [sldStyle() method](https://devsite.googleplex.com/earth-engine/image_visualization#styled-layer-descriptors) requires image statistics to be computed in a region (to determine the histogram)