# QGIS Training Module 4 - Coordinate Reference Systems

---

## 1. Introduction

In this module we introduce the concept of coordinate reference systems (CRS). We introduce geographic and projected coordinate systems and discuss the difficulties with transferring the locations from a curved surface (3D) to a flat surface (2D). In the second part of this module we present a tutorial introducing the basics of working with CRS in QGIS, setting coordinate systems and projecting data. 

---

## 2. Coordinate Reference System basics

A coordinate system ensures that objects and data are accurately and consistently mapped. There are, however, a lot of different coordinate systems of various types. Choosing the right one is crucial to ensuring that maps, calculations and measurements are correct. Applying a coordinate system to the Earth is not a straightforward endeavour. Before we can apply a CRS, a number of steps need to be taken. Thankfully, mathematicians and geodesists have been doing this for years.  
One of the difficulties with applying a CRS to the Earth is that the planet is not a uniform sphere, nor is the surface smooth. The Earth is wider at the equator than at the poles, and topography, bathymetry, and factors such as changing ocean height mean that the surface of the Earth is lumpy and irregular. 

**Geoid**

The geoid (Figure 1) is a mathematical approximation of the shape of the Earth. This approximation is based on the impacts of gravity on the Earth’s surface, determining its shape. The geoid is less lumpy than the Earth. The geoid is a model of global mean sea level used to measure elevation.

![](https://user-images.githubusercontent.com/47147296/92700772-1f34c100-f347-11ea-99ef-21ab1be1e141.png)

*Figure 1. Geoid.* 



**Ellipsoid/Spheroid**

An ellipsoid or spheroid (Figure 2) is a smooth 3D object that describes the size and shape of the Earth allowing us to assign coordinates to a location. These coordinates are represented by latitude and longitude. Latitude and longitude are angles measured in degrees from the centre of the Earth to a point on the Earth’s surface. Latitude and longitude can describe any location, but we cannot accurately measure area or distance using just these coordinates.

![Figure 2. Example ellipsoid with lines of latitude and longitude. ](https://user-images.githubusercontent.com/47147296/92700856-38d60880-f347-11ea-9931-0473bab4953f.png)

*Figure 2. Example ellipsoid with lines of latitude and longitude.*

**Datum**

Mapping objects or locations on the Earth’s surface requires a datum (Figure 3). A datum defines the way in which the ellipsoid fits to the geoid. The ellipsoid approximates the shape of the Earth and the datum defines the position of the ellipsoid relative to the centre of the Earth. The datum provides the location from which to measure latitude and longitude; it determines the ‘starting point’.

![Figure 3. Example of how an ellipsoid is fit to the geoid to create a datum.](https://user-images.githubusercontent.com/47147296/92700889-425f7080-f347-11ea-8399-56a54a9222d3.png)

*Figure 3. Example of how an ellipsoid is fit to the geoid to create a datum.*

The datum is the basis of a geographic coordinate system (GCS). The most common datum used is WGS84 (World Geodetic System developed in 1984), which is described as the ‘best fit’ for the whole world, with the least overall distortions. Local datums can be used to minimise distortions over a smaller area, and most countries and areas have specific datums which increase location accuracy for that specific area. 

**Projections**

A projection is a mathematical transformation of the measurements of the round datum to a flat surface (Figure 4). **Projections define how a 3D object is transformed to a 2D surface.**  A GCS uses degrees as they measure angles, whereas a PCS uses linear measurements such as feet and metres as it is measuring the distance from a known point on a Cartesian plane. 

![Figure 4.   Example of a cartesian coordinate system.](https://user-images.githubusercontent.com/47147296/92700935-4ee3c900-f347-11ea-9949-2030fe9bd57d.png)

*Figure 4.   Example of a Cartesian coordinate system.*

**How does this all fit together?**

In order to better understand how these elements affect a coordinate reference system, we can look at the  British National Grid (BNG) as an example here:

![](https://user-images.githubusercontent.com/47147296/92700974-5c994e80-f347-11ea-9c7f-ff4f3dc95458.png)




### 2.1. Geographic vs Projected Coordinate Systems    


#### 2.1.1. Geographic coordinate systems 
 
**A geographic coordinate system (GCS)** enables us to define a location using degrees represented by a grid. The North-South direction is measured by latitude lines that run parallel to the equator. The east-west direction is measured by longitude lines. These run from pole to pole and are called meridians. A point on the Earth’s surface is referenced by its longitude and latitude, measured in degrees, referring to the angle from the centre of the Earth to that point. 

![Figure 5. Example of how geographic coordinates are calculated.  				](https://user-images.githubusercontent.com/47147296/92701010-67ec7a00-f347-11ea-9027-90b689dff381.png)

*Figure 5. Example of how geographic coordinates are calculated.*

The line of 0 latitude is the equator, latitude values are measured relative to the equator ranging from 90 at the north pole to -90 at the south pole. The line of 0 longitude is called the Prime Meridian and it passes through Greenwich, England. Longitude values are measured relative to the prime meridian, ranging from 0° to 180 when travelling east and 0° to -180 when travelling west. Latitude and longitude can be expressed as either decimal degrees or degrees, minutes, and seconds. 

![Figure 6. Example of latitude and longitude coordinates of a geographic coordinate system.](https://user-images.githubusercontent.com/47147296/92701048-7175e200-f347-11ea-89a8-6b438fc4fd7b.png)

*Figure 6. Example of latitude and longitude coordinates of a geographic coordinate system.*

#### 2.1.2. Projected coordinate systems

A projected coordinate system (PCS) is a flattened version of a geographic coordinate system. Unlike a GCS, grid lines are parallel and consistent, and coordinates are given in linear units such as feet or metres. Locations are defined by x and y coordinates on a grid, with the origin at the centre of that grid given the coordinates 0, 0 (where x = 0 and y = 0). All locations are referred to in relation to the origin (0, 0) with x and y values being either positive or negative depending on their location relative to the origin. X coordinates to the right of the origin will be positive, x coordinates to the left will be negative. Y coordinates above the origin will be positive and y coordinates below will be negative.

![Figure 7. Cartesian coordinate system](https://user-images.githubusercontent.com/47147296/92701083-7aff4a00-f347-11ea-8cc2-cd7a30444289.png)

*Figure 7. Cartesian coordinate system*

When projecting a 3D grid to a 2D grid (flattening) there will always be a distortion of the grid’s proportions. This means the distance, area, angle, or shape of an object being projected will also be distorted. By choosing the correct PCS for a specific area, the proportions of these objects can be preserved, ensuring measurements, calculations and analysis will be more accurate.

##### 2.1.2.1. Problems with projections
 
Any time a projection is used, area, shape, angle and distance, or a combination of these will be distorted. To perform measurements and analysis of your geospatial data most accurately, the correct projection needs to be used. Choosing a projection is extremely important and the projection you use is dependent on location and the aspects of your data’s spatial attributes that you want to preserve. For example, if your work focuses on measuring distance between points, you should use a map projection that provides high accuracy for distances. As a result of choosing this projection, it is likely that other parameters such as area and shape will be distorted and therefore inaccurate.

Projections can be grouped by the property that they best preserve: 

**Conformal Projections** are used when preserving shape and angular relationships is important. These are most accurate for small areas as angular relationships and shapes become less reliable over long distances. This type of projection will result in distortion of the area of objects, making area calculations incorrect. An example of a conformal projection is the World Mercator projection (Figure 8). This is most apparent in the Mercator projection as Greenland is shown to be similar in size to Africa, when Africa is in fact roughly 14 times larger. 

![Figure 8. ESRI Ocean basemap with the World Mercator projection applied. ](https://user-images.githubusercontent.com/47147296/92701123-8488b200-f347-11ea-8c75-921f4f8631c1.png)

*Figure 8. ESRI Ocean basemap with the World Mercator projection applied.*

**Equidistant Projections** or Azimuthal projections show true distances, but only from the centre of the projection or along a set of lines. This means an equidistant map centred in London shows the correct distance between London and any other point on the map but does not show the correct distance between other points. The distortions that make the map accurate for London will mean the map is inaccurate for measuring area, angle, or distances between other locations. A common example of an equidistant projection is the Plate Carrée Equidistant Cylindrical projection (Figure 9).  

![Figure 9. ESRI Ocean basemap with the Plate Carrée equidistant cylindrical projection applied. ](https://user-images.githubusercontent.com/47147296/92701155-8d798380-f347-11ea-9872-6bf0e19d6032.png)

*Figure 9. ESRI Ocean basemap with the Plate Carrée equidistant cylindrical projection applied.*

**Equal-area Projections** portray areas on a map with the same proportional relationship to the areas on Earth they represent. This type of projection is most suitable when measuring area and extent. When dealing with large areas, equal-area projections result in distortions in angular conformity while smaller areas will be less likely to distort angular measurements. Examples of equal-area projections are Alber’s equal area, Lambert’s equal area and the Mollweide projections (Figure 10). 

![Figure 10.  ESRI Ocean basemap with the Mollweide projection applied. ](https://user-images.githubusercontent.com/47147296/92701189-98341880-f347-11ea-91b6-50aa9ff52b88.png)

*Figure 10.  ESRI Ocean basemap with the Mollweide projection applied.*

### 2.2 Changing between Coordinate Reference Systems

**Transformation**
A transformation is a mathematical method that converts coordinates in one geographic coordinate system to another geographic coordinate system. A transformation is necessary when changing between coordinate systems based on different datums. An example of this is the transformation of British data from the WGS 84 to the OSGB 36, from the World Geodetic System 1984 datum to the Ordnance Survey of Great Britain 1936 datum.  

**Projection**
Projections take data in a geographic coordinate system (degrees) and changes it to a projected coordinate system (metres). Projections use a mathematical calculation to convert the coordinate system used on the 3D surface of a GCS to the 2D grid of a projected coordinate system. If projecting from a GCS to a PCS that is based on a different geographic datum, a transformation must first be performed. 

![Figure 10. Earth represented using geographic and projected coordinate systems. ](https://user-images.githubusercontent.com/47147296/92701257-aa15bb80-f347-11ea-88b9-464df138df6f.png)

*Figure 10. Earth represented using geographic and projected coordinate systems.*


---




## 3. Working with Coordinate Reference Systems in QGIS

### 3.1. Data and video instructions

To access data for this module, please contact us at gissupport@cefas.co.uk and we will share the data with you.
  
The data folder contains the following:

|Natue of Data| Name | Source | Citation | Licence | Source Link | Data Processing |Date accessed 
| --- |  --- | --- | --- | --- | --- | --- | --- |
|Bathymetry|Bathymetry.tif|GEBCO|Imagery reproduced from the GEBCO_2019 Grid, GEBCO Compilation Group (2019) GEBCO 2019 Grid (doi:10.5285/836f016a-33be-6ddc-e053-6c86abc0788e)||https://www.gebco.net/data_and_products/gridded_bathymetry_data/|Public Domain|https://www.gebco.net/data_and_products/gridded_bathymetry_data/|No|2020|
|Ports in the UK| UK_Ports.shp| Nautical Geospatial Intelligence Agency |World Port Index Shapefile| |Public Domain  |Subset for the UK |Subset for the UK| 2020|
|World Boundaries| world_boundaries.shp | Natural Earth | Made with Natural Earth. Free vector and raster map data @ naturalearthdata.com. | Public Domain | https://www.naturalearthdata.com/downloads/50m-cultural-vectors/50m-admin-0-countries-2/ | No|2020|

---

#### 1. Start a new project

Open QGIS and start a new project by going to **Project > New**. Save this project in your desired workspace by clicking **Project > Save As**, this will save your work as a QGIS project file. When saving work to this project file, all layers in your workspace will be saved. This allows you to return to projects at a later date with all previous edits and the up to date version of your layers.   

#### 2.	Coordinate reference system settings

General CRS settings in QGIS can be found in **Setting > Options > CRS**. This is where you can choose what happens to layers and projects when opening QGIS. 

![](https://user-images.githubusercontent.com/47147296/92701298-b568e700-f347-11ea-9cd2-48adaa2068a5.png)

#### 3. Setting Project CRS

Your project CRS can be set in QGIS in **Project > Properties > CRS** or by clicking the icon in the bottom right corner. The project CRS determines how your data is displayed on your QGIS map canvas. By default, the QGIS sets the project CRS as WGS 84 (ESPG:4326).

QGIS uses “On the fly” transformations, meaning that all layers loaded into your project are automatically transformed and projected into the CRS of your project. Therefore, despite the layer’s original CRS, all layers will be rendered into the correct position with respect to each other. As a result, when layers are saved with a new projection, they appear in the map pane in the same position, this is because they are being automatically reprojected to the project CRS. 
 
![](https://user-images.githubusercontent.com/47147296/92701325-bf8ae580-f347-11ea-9f66-46f2ea12e63d.png)

 
#### 4. Set Layer CRS

The layer Coordinate Reference System can be set by right-clicking on the layer and selecting **Set CRS > Set Layer CRS** and searching your chosen CRS and applying. This will change the CRS of the layer while you are working with it in QGIS; however, this does not change the CRS of the shapefile itself, just the properties of the layer. 

**Part 2: Reprojecting vector data**

If data does not share the same CRS, it is necessary to reproject it. Projection is often the first step in geospatial analysis before other measurements and calculations can be made. Using the correct projection ensures your analysis is as accurate as possible.

#### 1. Load vector data

Open QGIS Desktop and load the world shapefile by opening the data source manager and selecting *world_boundaries.shp* from wherever you have saved it. 

![](https://user-images.githubusercontent.com/47147296/92701358-c9ace400-f347-11ea-93c9-20fde6763885.png)


You will now see the shapefile in the main panel and in the layer panel on the left of the screen. 

![](https://user-images.githubusercontent.com/47147296/92701389-d29db580-f347-11ea-9a3a-4c8e97d47c89.png)


#### 2. View layer properties

To view this layer’s properties and see which CRS this layer is using, you can double click, or right click on the layer in the layer panel and select *Properties*. In the properties go to *Source* and you will see the geometry and CRS. In this case, the shapefile is set in the WGS 84 geographic coordinate system.


![](https://user-images.githubusercontent.com/47147296/92701416-dcbfb400-f347-11ea-8867-dd41c9767fc3.png)


Back on the main screen, we can see the coordinates of a location by moving the mouse around and reading the coordinates at the bottom of the screen, these coordinates are in degrees. As a GCS represents a 3D object and a computer screen can only display objects in 2D, QGIS is forced to choose a projection and defaults to WGS 84 Pseudo-Mercator, the same projection as used by Google Maps. 

#### 3. Change CRS

One way of visualising this data in a projected system of your choice is to change the project CRS. To do this, click the icon in the bottom right hand corner, or select **Project > Properties > CRS** and select a projected coordinate system from the list. One of the easiest ways to select a CRS is by searching by its EPSG code. In this example, we will project to the Lambert Azimuthal Equal-Area projection for Europe (EPSG: 3035). 

When doing this, multiple transformations options are available. Select the first option, notice there is a column which indicates the accuracy of this transformation, in this case we are transforming this data to within an accuracy of 1 metre. Choosing the most accurate transformation is crucial when undertaking small scale spatial analyses and calculations, for broader scale work or when producing maps without performing analysis, a transformation with lower accuracy can be chosen. 

![](https://user-images.githubusercontent.com/47147296/92701447-e6e1b280-f347-11ea-86b8-c75fc2b55155.png)


Your shapefile should now look like this. We can see here the distortion created by the projection at the higher longitudes. This projection is most accurate for calculating area in Europe but would be unsuitable for measuring angles or distance. It would also be inaccurate at measuring area outside of Europe.

![](https://user-images.githubusercontent.com/47147296/92701471-f103b100-f347-11ea-8032-6fd656a362a6.png)


You will be able to see now that the coordinates displayed at the bottom of the screen are in linear units. To find which unit of measurement is used with this projection we can check in **Properties > Information**. 

However, this has just changed the way the shapefile is displayed, it has not been permanently reprojected. To properly reproject this we will need save a copy of this shapefile in the correct CRS. 

#### 4. Save reprojected layer

To do this, right click on the layer in the layer panel and click **Export > Save Feature As**. Under the format dropdown menu choose ‘ESRI Shapefile’ and choose the name and location for the file to be saved next to ‘File name’. Next choose the CRS you want the shapefile to be saved in, for this, again choose Lambert Azimuthal Equal Area (EPSG: 3035) and click ‘Ok’ at the bottom of the page.

![](https://user-images.githubusercontent.com/47147296/92701510-fbbe4600-f347-11ea-8f8e-725088479c01.png)


This has saved a version of this shapefile in our chosen projected coordinate system. You can check to see if this has worked by opening a new QGIS application and loading this newly generated shapefile into it. Your shapefile should look as it does above and the project CRS should automatically change to EPSG: 3035. 

#### 5 Reproject layer

Alternatively, QGIS has a tool for reprojecting vector data. Go to **Vector > Data Management Tools > Reproject Layer**, select your input layer and choose your target CRS. By clicking ‘Run’, a temporary layer will be added to your QGIS project in your chosen CRS. This will still need to be exported to be saved but will save with your chosen CRS.

![](https://user-images.githubusercontent.com/47147296/92701543-0547ae00-f348-11ea-960c-8338a7dd6433.png)


To save this layer without exporting later, we can click where the arrow points to choose where to save this newly reprojected layer. 

**Part 3: Reprojecting raster data**

#### 1. Load raster data

Open a new QGIS project by selecting **Project > New** and select whether you want to save your current project. Load *‘Bathymetry.tif’* from wherever your data is saved.

![](https://user-images.githubusercontent.com/47147296/92701577-11337000-f348-11ea-944a-4bfdc497802b.png)


#### 2. Save reprojected raster

The current CRS of this layer can be viewed in the layer’s properties. This should be the WGS 84 geographic coordinate system. We are going to reproject this layer from WGS 84 to the Lambert Azimuthal Equal Area projection. One way of doing this is the same way as we did with the vector layers in the previous tutorial. 

To do this, right click on the layer in the layer panel and click **Export > Save Feature As**. Under the format dropdown menu choose ‘GeoTIFF’ and choose the name and location for the file to be saved next to ‘File name’. Next choose the CRS you want the shapefile to be saved in, for this, again choose Lambert Azimuthal Equal Area (EPSG: 3035) and click ‘Ok’ at the bottom of the page.

![](https://user-images.githubusercontent.com/47147296/92701615-1c869b80-f348-11ea-9edc-0eda871ee8c8.png)


#### 3. Reproject raster

The second option for reprojecting raster data gives more options about the method used for reprojecting the data. This is done by clicking **Raster > Projections > Warp (Reproject)** selecting the raster layer you wish to reproject and setting a target CRS.

![](https://user-images.githubusercontent.com/47147296/92701643-25776d00-f348-11ea-80a5-10c818ecad97.png)


Within this tool there are options for different resampling methods, this determines the method for changing the value of a cell due to changes in the raster grid when reprojecting. 	For more information on raster resampling and which method is best to use: <https://gisgeography.com/raster-resampling/>. 

This tool will generate a new raster layer with the new CRS which will need to be saved to your specified folder. Alternatively, you can choose to save the output raster to your chosen folder within the tool. 

![](https://user-images.githubusercontent.com/47147296/92701671-2f00d500-f348-11ea-98f0-a808cbdd52af.png)


**Part 4: Generating coordinates**

Sometimes when point data is reprojected we want to store the coordinates of these points in the layer’s attribute table. However, when reprojecting, the coordinates change. This part of the tutorial will show you how to add the new coordinates to your shapefile’s attribute table. 

#### 1.	Load point data

In a new QGIS project (Project > New) load the ‘UK_Ports.shp’ shapefile from the data folder. This is a point shapefile showing the location of ports in the UK. This shapefile is in the WGS 84 geographic coordinate system, with latitude and longitude in columns in the layer’s attribute table. 

![](https://user-images.githubusercontent.com/47147296/92701708-3922d380-f348-11ea-9966-93a86933c6c9.png)


#### 2.	Reproject layer

Project this layer to the British National Grid coordinate system (EPSG:27700) using one of the methods used in Part 2 of this module. You will be asked to choose a transformation when reprojecting from WGS 84 to the British National Grid. Choose the first option with an accuracy of 1m. If you get the following error message: *'This transformation requires the grid file “OSTN15_NTv2_OSGBtoETRS.gsb”, which is not available for use on the system'*, follow this link for [instructions on installing the necessary files](https://github.com/CefasRepRes/QGIS_Training_Cefas/Module_1_Coordinate_Reference_Systems/BNG_Transformation.pdf).

![](https://user-images.githubusercontent.com/47147296/92701740-4344d200-f348-11ea-8e84-56981146de18.png)

 
Once you have successfully reprojected your layer to BNG, in the layer information (**Properties > Information**) you will then see that this layer is using metres as the unit of measurements, as opposed to degrees used in a GCS. BNG also measures latitude as Northing and longitude as Easting, so we will need to add these coordinates to the attribute table. 

#### 3.	Open attribute table and enable editing

Open the layers attribute table and click the pencil ![image](https://user-images.githubusercontent.com/47147296/101175751-73e19280-363d-11eb-947b-c7bbd9325855.png) in the top left of the attribute table tab, this enables allows you to edit the table (***1***). Next, open the field calculator (***2**) ![image](https://user-images.githubusercontent.com/47147296/101175919-adb29900-363d-11eb-91c7-e9fdeb1c43d7.png) so we can generate the northing and easting coordinates. 
 
![](https://user-images.githubusercontent.com/47147296/92701770-4cce3a00-f348-11ea-88c2-07745349df56.png)


#### 4.	Generate easting and northing coordinates

Within the field calculator, add a new column named “easting” in the ‘Output field name’ (**1**). Change the output field type to Decimal number (real) (**2**). The Output field length (***3**) and precision determine the maximum size of the value in that field and the number of values after the decimal. 

![](https://user-images.githubusercontent.com/47147296/92701797-5788cf00-f348-11ea-9a5f-3c0ce19a6de7.png)

 
In the field calculator (***4**) type the expression ***x($geometry)** this expression will return the X coordinate value of each point in the layer CRS. As our layer is in the BNG coordinate system, this value will be the easting value in metres. Click OK. This will add a column table with the easting values. 

Repeat the process, name the column “northing” and change the expression to ***y($geometry)**. We will now have easting and northing coordinates for each point in our UK ports vector layer.


![](https://user-images.githubusercontent.com/47147296/92701831-61aacd80-f348-11ea-90fb-f2554802542c.png)

---

## 4. Conclusion

The module is now complete!🥇🥇🥇🥇

This module has introduced you to the theory of coordinate reference systems and given you some experience of working with coordinate reference systems in QGIS. You have been introduced to the methods used to assign coordinates and map spatial data. We have covered the difference between geographic and projected coordinate systems and discussed the inherent issues that come with projecting spatial data. 

---

## 5. Additional Resources

https://docs.qgis.org/3.4/en/docs/user_manual/working_with_projections/working_with_projections.html

https://docs.qgis.org/2.8/en/docs/gentle_gis_introduction/coordinate_reference_systems.html

https://www.youtube.com/watch?v=Z41Dt7_R180

https://www.earthdatascience.org/courses/earth-analytics/spatial-data-r/intro-to-coordinate-reference-systems/

---

## 6. Author and Contact

**Author:** William Procter

**Contact:** gissupport@cefas.co.uk

