# Joins and Arrays

## Join

If you have programmed in the past, joining data togetgher is likely a familiar concept. This process assicates information from one set of data with relevant data from another set on a specific attribute. Let's say you have an Image Collection of Landsat data that is filtered to the first six months of the year 2016 and a bounding box of your area of study. You also have a table of Redwood tree locations that is filtered to the same area of study, although it contains information over the past decade. You can use a Join to associate information about the trees from the Feature Collection and include it in the Image Collection, keeping only the relevant data. You now have a dataset with useful information from both the Image Collection and Feature Collection in one location. Although there are different types of joins, the process brings information together, keeping only relevant information. The [documentation](https://developers.google.com/earth-engine/guides/joins_save_all) on Joins goes over specific examples and concepts, but a crucial component is understanding the type of join you need the three most prominent within GEE are: 

* Left Join
  * Keeps all the information from the primary dataset, and only information that joins from the secondary datset
* Inner Join
  * Keeps only the information where the primary and secondary data match
* Spatial Join
  * A join based on spatial location (ie, keep only the geometry points that fall within a specified buffer)

GEE provides some unique types of joins, including 'Save-All', 'Save-Best' and 'Save-First', which are useful if you want to look at a specific area.  

## Array

Arrays are a collection of data where information is stored contiguously - matrices are a multi-dimensional array. For instance, an image might have 1024 rows and 1024 columns. Each row is an array, each column is an array, and taken together, you have a 2-dimensional array, also known as a matrix. If the image has three separate color channels, then that is a 3-dimensional array. Some of the terminology changes depending on discipline (ie, physics vs. computer science), but if you are familiar with working with matrices and arrays in programming languages such as Matlab or OpenCV, it is important to understand the role of arrays within GEE. In fact, Google Earth Engine states that working with arrays outside of the established functions that they have built is not recommended, as GEE is not specifically designed for array-based math, and will lead to unoptimized performance. There is a very informative [video](https://developers.google.com/earth-engine/guides/arrays_intro) that delves into the engineering behind Google Earth Engine, but in this course we will only be doing a limited amount with array transformations and Eigen Analysis. In many cases, you will probably be better off aggregating the specific data and then conducting array mathematics with programming frameworks geared to that context. 