

# PreLab: Getting Started

## Overview

The purpose of this lab is to introduce some of the functionality and structure of Google Earth Engine (GEE) before we get into the practical labs. This tutorial will provide a brief introduction to the GEE Javascript  interface (the Code Editor) and using GEE resources. At the completion of the lab, you will be able to access GEE imagery, upload your own assets, and explore the metadata for a given feature. 

 **Learning Outcomes:** 

- Understand the value of using GEE
- Get acquainted with the GEE Resources
- Understand the major data types and their associated methods

## Setting up an Account

To begin, ensure you sign-up for the Google Earth Engine [here](https://signup.earthengine.google.com). Registration is free and straightforward, but it takes approximately 24 hours to be approved to use the code editor. While waiting, let's get familiar with the Google Earth Engine. The video below is a quick introduction to Google Earth Engine to get you familiar with the resources available. 

[Video](https://www.youtube.com/watch?v=Ypo28T6wPbQ)

####  Resource Links

* Google Earth Engine [link](https://earthengine.google.com)
* Code Editor [Map](https://developers.google.com/earth-engine/guides/playground?hl=en)
* [Datasets](https://developers.google.com/earth-engine/datasets/)
* [Case Studies](https://earthengine.google.com/case_studies/)
* Google Earth Engine [Blog](https://medium.com/google-earth)
* [Video](https://developers.google.com/earth-engine/tutorials/tutorials) tutorials on using GEE (from the Earth Engine Users' Summit)

## Getting Set Up

Google Earth Engine allows you to work with your own data. You are able to import raster imagery, vector imagery and tabular data and then incorporate those assets into your analysis. This is process is automatically linked to the Google Drive account that signed up for GEE. If you are not familiar with Google Drive, there is a '[Getting Started Guide](https://support.google.com/a/users/answer/9282958?hl=en)' that goes over the basics of setting up and organizing your Google Drive account. We will not be covering Google Cloud Platform Storage in this course. Below are some helpful links to documentation on working with external data. 

* [Managing Assets](https://developers.google.com/earth-engine/guides/asset_manager)
* [Import Raster](https://developers.google.com/earth-engine/guides/image_upload)
* [Import Vector / Tabular Data](https://developers.google.com/earth-engine/guides/table_upload)
  * Note that GEE only supports Shapefiles and .csv files
* [Exporting Data](https://developers.google.com/earth-engine/guides/exporting)

## Understanding Google Earth Engine

It is important to understand the basics of how Google Earth Engine works. The Developer's [overview](https://developers.google.com/earth-engine/guides/concepts_overview) provides much more detail on the intricacies of how GEE processes data on the Google Cloud Platform, but in the simplest terms, there are two sides to the process - the `client` side and `server` side. When you open your web browser and begin to work in the code editor, that is considered the `client` side. You can write JavaScript code in the editor and the code will be processed within your browser. The code below simply creates a variables `x` and `y`, adds them together as the variable `z` and prints the result, which shows up in the console of the code editor. Even though the code is written in the GEE editor, it plays no role in the execution of this code - your browser executes it. 

```javascript
var x = 1; var y = 2;
var z = x + y;
print(z)
```

To begin using GEE effectively, we have to tell GEE what we need it to do. Let's say we want to import an image collection. In the snippet below, you can see that there is an `ee` before the `ImageCollection` constructor. In simple terms, this signals to Earth Engine that we will be using its resources. Without that indicator, GEE will cede operations to the browser to process the JavaScript. 

```javascript
var sentinelCollection = ee.ImageCollection('COPERNICUS/S2_SR');
```

Over time, you will gain experience understanding the role of working with JavaScript on the `client` side and the `server` side, but the main point in this section is that when programming, we will be building 'packages' that explicitly define what we need GEE to do.

An extension of this topic is listed [here](https://developers.google.com/earth-engine/guides/client_server), along with discussions of programming specific topics (ie, mapping instead of looping). 

## JavaScript

The intent of this course is not to teach the intricacies of programming within JavaScript. JavaScript is the core language for web development, and you will likely find that many of the tutorials and resources you find will not be directly relevant to the type of JavaScript that you will need to work in Earth Engine (ie, working with React, JQuery, dynamic app development, etc). JavaScript was chosen because it is an extremely popular language (~97% of websites use it in some fashion) and as an object-oriented language, it is well-suited to pair objects (in this case, imagery provided by Google Earth Engine) with methods (such as using the `reduce` function to summarize the analytical information from a processed image). 

There are some excellent resources that will assist your understanding of working with JavaScript. One helpful tutorial is [Javascript.info](https://javascript.info), which provides a thorough overview of working with JavaScript. In this tutorial, focus on part I, as part II and III are focused on web development. 

[W3Schools](https://www.w3schools.com/js/default.asp) provides good information on each individual component of working with JavaScript. For instance, if you see the word `var` and wanted more information on it, W3Schools has some helpful definitions and code snippets that will be of use. 

Finally, [JavaScript & JQuery](http://www.javascriptbook.com) is an excellent, well-designed book that goes through the fundamentals of working with JavaScript and provides helpful illustrations and use cases. The second half of the book is outside the scope of this course, but if you did want to extend your skillset, this book is a great starting point. 

