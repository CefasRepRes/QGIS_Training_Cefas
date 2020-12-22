# QGIS Training module 3 – Digitisation

---
## 1. Introduction
This QGIS module focuses on data digitisation and creation of new shapefiles. The instructions are written for QGIS 3.2 version and above. At the end of this module you will be able to do the following: 

Adding new layers to QGIS project
* Create bookmarks
* Geo-referencing
* Create new points, polygons and lines

To access data for this module, please contact us at gissupport@cefas.co.uk and we will share the data with you and a link to a supplementary tutorial video.

|Natue of Data| Name | Source | Citation | Licence | Source Link | Data Processing |Date accessed 
| --- |  --- | --- | --- | --- | --- | --- | --- |
|Non-georeferenced screenshot|Survey.tif|Cefas|Please note that the data/ dataset is fictional and has been created solely for the purposes of training and must only be used for this training module. Resemblance or links to any person or natural entity directly or indirectly is purely coincidental.|Training Module Purposes only|http://mdrviewer/#/View/20993|Information in the source link|N/A|
|World coastline|coastline.shp|NOAA|COPYINGv3 and COPYING.LESSERv3|GNU Lesser General Public License (LGPL)**|https://shoreline.noaa.gov/data/datasheets/wvs.html|No, Only level 1 f used (full resolution)|2020|

---

## 2. Digitisation
### 2.1. Open Blank QGIS Project
Navigate to the Windows Taskbar and type in 'QGIS'-  double click to open 'QGIS Desktop' 

### 2.2. Add coastline shapefile
**Data Source Manager (CTRL+L)** and click on **Vector** ![image](https://user-images.githubusercontent.com/47147296/80387215-4a3edc80-88a0-11ea-9f51-28ed9c221e76.png) this will allow you to add a shapefile (vector layer). In the **file name** navigate to the place where you saved the data (hereafter the data folder) and add coastline.shp, click **"Add and Close"**.

### 2.3. Create Bookmark for Cornwall
Zoom to the area of Cornwall (below): Then go to **View** --> **New Bookmark** and type a name of the bookmark in the Spatial Bookmarks Panel. If you change the zoom, you can apply the bookmark zoom by: left-click on the bookmark (highlights) and click on ![image](https://user-images.githubusercontent.com/47147296/80385196-af450300-889d-11ea-92fc-768486286a6a.png)

![image](https://user-images.githubusercontent.com/47147296/80385251-c126a600-889d-11ea-81b8-6346d3e39c92.png)

### 2.4. Activate Georeferencer GDAL Plugin
**Plugins** --> **Manage and Install Plugins** and type in Georeferencer GDAL. Check the box 
next to the plugin and **Close**. This plugin will appear under Raster tab at the top of the QGIS 
project.

![image](https://user-images.githubusercontent.com/47147296/80385433-f59a6200-889d-11ea-9f81-19ef5400ca80.png)

### 2.5. Open Georeferencer GDAL tool
**Raster** --> **Georeferencer GDAL**. A new georeferencing window will pop up. Load raster Survey image by clicking on **Open Raster**:
![image](https://user-images.githubusercontent.com/47147296/80385619-309c9580-889e-11ea-9f04-595213eea16d.png)

### 2.6. Goreferencing
Click ![image](https://user-images.githubusercontent.com/47147296/80385740-59bd2600-889e-11ea-8521-e67daaaa608b.png) to add ground control points. Navigate to locations in the screenshot below (red points), click on the location of red points in a map and the panel (Enter Map Coordinates) where you can insert coorindates appears. In the **Enter Map Coordinates panel**, select  **From map canvas** which will navigate you back to the Europe shapefile. Use the bookmark created to zoom to Cornwall and pick the same spot as in the georeferencer. In theory, you need at least 3 evenly distributed control points for georeferencing. In this case, we added 4 points in order for the Survey.png to better align with the coastline. The GCP table becomes populated with the X and Y coordinates from the shapefile (see below). The accuracy of the georeferenced image is the highest around the GCPs. If the GCPs are clusstered in one part of the image, the position, distances and angles of the areas without the GCPs will be inaccurate.

![image](https://user-images.githubusercontent.com/47147296/101461918-73921180-3933-11eb-9fe0-207a533691e2.png)

![image](https://user-images.githubusercontent.com/47147296/80385946-a6a0fc80-889e-11ea-9c2b-717e081ca4ab.png)

![image](https://user-images.githubusercontent.com/47147296/80386014-ba4c6300-889e-11ea-8663-d617faf26fe7.png)

In the Georeferencer panel go to **Settings** --> **Transformation Settings** and fill the settings with the parameters below and save raster to your working folder. Then press **Start Georeferening** ![image](https://user-images.githubusercontent.com/47147296/80386145-e0720300-889e-11ea-989d-559998de11b8.png). After setting-up your georeferencing settings, you will see that the residual pixels are calculated. This shows how well your control points match the referencing surface. If some of them seem too high, this is most likely due to human error and you should consider changing them or remove them from the georeferencing. After georeferencing is finished, the new layer will be added to QGIS project.

![image](https://user-images.githubusercontent.com/47147296/101460260-46446400-3931-11eb-8773-312cde4f8519.png)

There are different transformation types and recommendations on which transformation could be used in specific circumstances (more information in [Available Transformation Algorithms](https://docs.qgis.org/3.4/en/docs/user_manual/plugins/core_plugins/plugins_georeferencer.html). However, you will need to experiment with the transformation types taking into consideration the quality of the input data and the GCPs in a way that the value of the residual pixels is as small as possible. 

### 2.7. Transparency
To check how accurate the georeferencing was, we can change the transparency of the georeferenced layer. Right click **survey_modified_georef.tif** --> **Properties** --> **Transparency** and change **Global Opacity** to 50%. If unsatisfied with the georeferenced layer, you can remove/add ground control points in the georeferencer panel and compute new outputs. 

### 2.8. Saving
To save your project, go to the top tab **Project** --> **Save As** and navigate to your working folder, add a new name to the exported output.

### 2.9. Digitising
We are going to create 3 types of shapefiles- points, lines and polygons. To create a shapefile, go to the top tab 
**Layer** --> **Create Layer** --> **New Shapefile** (as below).              

![image](https://user-images.githubusercontent.com/47147296/80386628-8a518f80-889f-11ea-9867-bd660775d7b5.png)

### 2.10. New Shapefile Layer
To create a new point shapefile, fill in the **File name** (save in your working folder by clicking on the three dots next to it), **Geometry type** --> **Point** and the **Coordinate Reference System** (already pre-defined for you as WGS 84). Repeat the same steps and create **surveyLines.shp** (Geometry type= Line) and **surveyPolygons** (Geometry type= Polygon).

### 2.11. Digitising points
In your table of contents, right click on **surveyPoints.shp** to highlight it. Press Toggle Editting to active the editing mode as shown below. Then click on ![image](https://user-images.githubusercontent.com/47147296/80386820-d0a6ee80-889f-11ea-96a9-d0492197e090.png) to add Point Features. Click on the point features around the coast. For each feature, you have to add a feature ID as shown below.

![image](https://user-images.githubusercontent.com/47147296/80386912-ec11f980-889f-11ea-8a1c-7625b9ef9924.png)

![image](https://user-images.githubusercontent.com/47147296/80386986-0055f680-88a0-11ea-8aa8-af41b25660f8.png)

When all the point features are digitised, press **Save Layer Edits** and **Toggle Editing** again to get out of the edit mode. Repeat the same steps for lines and polygons. When adding the last vertex of a line or polygon, left click to finish the feature and that’s when the feature attribute table opens. For more information please follow the accompanying video. At the end you should have 3 shapefiles as shown below:

![image](https://user-images.githubusercontent.com/47147296/80387136-2b404a80-88a0-11ea-8606-9edf432d2381.png)

Congratulations, you have just completed Cefas QGIS Training module 4 🥇 🥇 🥇 🥇

---

## 3. Auhtors and Contact

**Author:** Lenka Fronkova

**Contact:** gissupport@cefas.co.uk

---

## 4. Additional Resources

https://www.qgistutorials.com/en/docs/3/advanced_georeferencing.html
https://docs.qgis.org/3.10/en/docs/training_manual/forestry/stands_digitazing.html
https://docs.qgis.org/2.8/en/docs/user_manual/plugins/plugins_georeferencer.html#available-transformation-algorithms

