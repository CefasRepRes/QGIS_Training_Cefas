# QGIS Training module 2 – Map creation and visualisation 

---

## 1. Introduction 
In this tutorial, you will use QGIS to create a map to help plan a fisheries survey. You will plot station locations as points in QGIS, learn how to install new plugins, add contextual basemaps and ICES rectangles and create and export new maps. For Windows 10 users, there is a QGIS (currently 3.2 and higher version) available to install from the Cefas Software Centre. In this module, you are going to:
* Create points
* 	Plugin installation
* 	Adding basemaps
* 	Map composer
* 	Exporting a map output

To access data for this module, please contact us at gissupport@cefas.co.uk and we will share the data with you and a link to a supplementary tutorial video.

The data folder contains the following:

**Data add table with below** 
* 	CarhelmarWesternEngChannelSOL_andPLE_FSO_stn_posns.csv
 
1. “AreaStratum”- area where the survey was conducted
1. “Prime Station”- station ID
1. “Latitude”- Y coordinate in WGS 84 (EPSG 4326)
1. “Longitude”- X coordinate in WGS 84 (EPSG 4326)

You will need the internet access for this module, since we will install a QGIS plugin that will be donwloaded from the online repository.

## 2. Map creation and visualisation
### 2.1. Open QGIS Project
Open QGIS Desktop and navigate to Settings --> Options --> CRS and click on Prompt for CRS. As opposed to the earlier versions of QGIS, in QGIS 3 the ‘on the fly’ (OTF) option is enabled at all times.
### 2.2. Create survey points
Open Data Source Manager (CTRL+L) or click on ![image](https://user-images.githubusercontent.com/47147296/79881216-d8224f80-83e8-11ea-9340-9323ede451fc.png) and select Delimited Text. In File Name navigate to ‘data ‘folder and click on CarhelmarWesternEngChannelSOL_andPLE_FSP_stn_posns.csv as file. Choose Layer Name and in Geometry Definition X field as Longitude and Y field as Latitude. Geometry CRS is selected to WGS84 (EPSG: 4326) and click Add, Close (screenshot below).  This layer is only virtual. In order to save it go Right click on it in the table of contents (‘Layers’ Window) and Export             -->Save Features As. In Format, ensue that ESRI Shapefile is selected. In File Name browse to the ‘data’ folder location and chose name ‘surveyPoints.shp’ This will be saved as a shapefile and loaded to your map document. You can remove the original layer (Right click- Remove Layer).

![image](https://user-images.githubusercontent.com/47147296/79881491-2899ad00-83e9-11ea-9ca7-f3c3982e23f4.png)

### 2.3. Installations of plugins
In the top bar navigate to Plugins --> Manage and Install Plugins. In the ‘All’ tab type in QuickMapServices and then click on Install plugin. A new globe icon will appear in the tab panel for the QuickMapServices plugin as shown below (If you get any errors while installing the plugins, try to close your QGIS project and re-open it again. Go straight to Manage and Install Plugins and repeat the steps above to install the plugin):

![image](https://user-images.githubusercontent.com/47147296/79881892-b70e2e80-83e9-11ea-9c06-ce18ec26c403.png)

Click on the globe icon for QuickMapService and select Settings --> More services --> Get contributed pack. This will load all the QuickMapService basemaps available. After these were installed click on the globe icon again. There are going to be numerous basemaps available to load. You can experiment by left clicking on them. For the purpose of this exercise select ‘ESRI OCEAN’ to get bathymetry context for the survey points.

### 2.4. Save project
A shortcut CTRL+S to save the project or go to Project --> Save as and save the project in your working directory.

### 2.5. Add ICES Statistical Areas
Open Data Source Manager (CTRL+L) --> Vector and in the file navigate to the data folder in your working area and select 'GeodataShapefiles_ICES_Rectangles_UK.shp' and click Add.

### 2.6. Symbology ICES Rectangles
To change the symbology, right click on the GeodataShapefiles_ICES_Rectangles_UK.shp                              
Properties --> Symbology --> Simple Fill --> Fill colour --> Transparent fill to show only an outline of the ICES rectangles as shown below.

![image](https://user-images.githubusercontent.com/47147296/79882329-50d5db80-83ea-11ea-937a-9a0e6b66175d.png)

### 2.7. Change CRS (Coordinate Reference System)
To change the on-the-fly projection, go to the EPSG:4326 button in the right-hand corner- Project Properties|CRS (a screenshot below). At the moment, the projection is in the WGS84 coordinate reference system (unique 4326 created by EPSG*). Since we are working on a small local scale and to preserve distances, we are going to change the projection to the British National Grid (EPSG:27700). After opening Project Properties|CRS, type in ‘British National Grid’ in the Filter window, select it and click Apply --> OK. Check how the shape of the ICES Rectangles and especially the coast changed.

*European Petroleum Survey Group

For more information on the CRS, please visit our dedicated module [here](https://github.com/CefasRepRes/QGIS_Training_Cefas/blob/main/Module_1_Coordinate_Reference_Systems/instructions.md)

### 2.8.	Creating a map
In QGIS, the map outputs are created in a map composer. To open one navigate to Project --> New Print Layout and a window where you name the new composer is opens.In the video instructions, there is a more detailed description of the map composer, showing different functionalities. Click on ![image](https://user-images.githubusercontent.com/47147296/79882544-b2964580-83ea-11ea-9c82-2b8f4ed6b419.png) to add a new map to the layout and draw a square- size of your map. Add another one (smaller) which will represent your inset map. 

![image](https://user-images.githubusercontent.com/47147296/79882629-d0fc4100-83ea-11ea-8ad3-509b3ed4908d.png)

Click on map 1 and then on the symbol ![image](https://user-images.githubusercontent.com/47147296/79882722-eec9a600-83ea-11ea-9735-1ecbb1589a05.png) which allows you to pan and zoom the map with by scrolling your mouse. Zoom in to the area of the survey points. Then click on map 2 (inset map), then and go back to the QGIS project. Uncheck the survey points and ICES rectangles. Go back to the map composer and in the Item Properties press Update Preview. Update Preview updates the map print layout with the current visible QGIS layers but keeps the extent the same. You can also change the zoom in the Item Properties and Scale.  Then, still in Item Properties, navigate to Frame and choose the width of the map frame line.  An important step is to lock the layers for further editing which means that if you change the layers visibility/symbology etc in the QGIS project, it will not affect your map composer. To do that, check the Lock Layers as shown below. Check the Lock Layers for Map 2 and click on save.

### 2.9.	Adding grid
Click on Map1 --> Item Properties find Grids. Add a new grid with a + sign. Click on Modify grid which opens grid settings. Select the following:

![image](https://user-images.githubusercontent.com/47147296/79882876-27697f80-83eb-11ea-9186-05970f79afd8.png)


Click on Line Style --> Configure Symbol -->Simple Line and in Stroke style select ‘No Pen’. This will remove grid lines which would clash with the visibility of the ICES rectangles. Go back to the grid properties and select the following parameters about the grid labels. You can play around with the settings to see what each of them does.

![image](https://user-images.githubusercontent.com/47147296/79883033-55e75a80-83eb-11ea-8505-9fb945f39ef8.png)

### 2.10.	Extent overview
To add an extent overview to the inset map firstly highlight Map2 in the Items window. In the Item Properties find Overviews and add a new overview with the + sign and select Map frame to ‘Map 1’. You can change the symbology of the extent square by clicking Frame style --> Configure symbol --> Simple Fill. In Fill colour select ‘Transparent fill’ and in the Stroke style ‘Solid Line’.

![image](https://user-images.githubusercontent.com/47147296/79883235-921abb00-83eb-11ea-83c6-5269b9d64717.png)

### 2.11.	Legend and scale 
Add Item --> Add legend and draw a legend in the print layout. In Legend Items unclick ‘Auto update’ and click on the legend- highlight them. The legend item can be removed by the – sign and added by the + sign. Double clicking on the item opens an Item text in which you can change the layer name and you can leave ‘Title’ blank. To add a scale bar, go back to Add Item --> Add a scale bar  and draw a scale bar on the Map 1. Then you can change the properties as below to adjust the scale:

![image](https://user-images.githubusercontent.com/47147296/79883393-c42c1d00-83eb-11ea-9c37-8cc58014fe2a.png)

### 2.12.	Add text label
Add Item --> Add label and draw it under the scale bar. In the Main Properties of the label, type in ‘CRS: British National Grid (27700)’.

### 2.13.	North Arrow 
To add a north arrow, Add Item --> Add image and draw a rectangle in the corner of the map. Then navigate to Picture properties and Search directories. You can select one of the north arrow images and change the colour.  

### 2.14.	Export a map
Layout --> Export as image (other options-PDF (raster and vector formats)). Save edits of your map composer.

### 2.15.	Multiple map composers/layouts
For the single QGIS project, you can have multiple map printing composers. To create new map composers, open and manage the existing ones go to the QGIS project: Project -- > Layout Manager. Here you can duplicate your existing layouts, rename, delete or create new ones from scratch. For more information on the map composer/layout functionality, please watch the video which you can find in the ‘Instructions’ folder of this module.

Congratulations, you just finished Cefas QGIS Training Module 2 🥇🥇

---

## 3. Auhtors and acknowledgement

**Author:** Rose Nicholson and Lenka Fronkova

**Contact:** gissupport@cefas.co.uk
