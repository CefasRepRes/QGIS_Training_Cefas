
# QGIS training module 5 - Raster in QGIS 

---

## 1. Introduction

In this tutorial, QGIS is used to display raster files and perform basic analysis. For more information on how to install QGIS, please visit the intriduction page of this GitHub repository. This tutotrial covers:

- Loading raster files

- Manipulating raster files in preparation for display and analysis

- Symbolising raster files

- Performing basic raster analysis

- Creating contour vector files from rasters

To access data for this module, please contact us at gissupport@cefas.co.uk and we will share the data with you.
  
The data folder contains the following:

|Natue of Data| Name | Source | Citation | Licence | Source Link | Data Processing |Date accessed 
| --- |  --- | --- | --- | --- | --- | --- | --- |
| Bathymetry | tm5390_20140729mb.tif tm5490_20140729mb.tif tm5491_20140729mb.tif tm5492_20140729mb.tif|	Environment Agency | © Environment Agency copyright and/or database right 2019. All rights reserved. | OGL*| https://data.gov.uk/dataset/52b3a813-69c6-4b6f-8684-fd0bdc4aa71b/multibeam-bathymetry | No | 2019
| EUNIS Habitat Classification  |	C20191101_CombinedMap_9_6_6_bng_clip.tif | Joint Nature Conservation Committee (JNCC) | Contains JNCC data © copyright and database right 2019. | OGL* | https://hub.jncc.gov.uk/assets/2048c042-5d68-46c6-8021-31d177b00ac4 | Re projected and clipped specifically for the module | 2019
| Sea Surface Temperature | sst.mon.anom.nc | National Oceanic and Atmospheric Administration (NOAA) Physical Sciences Laboratory | Kaplan SST V2 data provided by the NOAA/OAR/ESRL PSL, Boulder, Colorado, USA | No Usage Restrictions | https://psl.noaa.gov/data/gridded/data.kaplan_sst.html | No | 2019
| Area of Interest | AreaOfInterest.shp | Cefas | **Adding a disclaimer- using for the purposes of this module?** | **Training Module Purposes only** | **MDR Record to be added** | Information in the source link| N/A
| Rasters for calculation | raster01.tif raster02.tif | Cefas | **Adding a disclaimer- using for the purposes of this module?** | **Training Module Purposes only** | **MDR Record to be added** | Information in the source link | N/A

*OGL- Open Government Licene: http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/

---

## 2. Raster Basics

This section of the module explores how to load raster datasets, and how to create secondary products, using virtual raster and merging, to simplify raster use.

## 2.1. Add Raster Data

Open QGIS and set the coordinate system to British National Grid – EPSG 27700.
-- From the main toolbar menu, select Project > Properties. 
-- On the left panel of the dialogue box, click CRS. 
-- In Filter, type British National Grid, and in Coordinate reference systems of the world select OSGB 1936 / British National Grid EPSG: 27700. Click Apply then OK to close the dialogue.
Note that if British National Grid has been used before it will appear in the box under **Recently used coordinate reference systems**.

![image](https://user-images.githubusercontent.com/47147296/98470224-33c4f680-21dc-11eb-8ff2-ef201e2d11f8.png)

**Raster data can be added via several different methods, e.g.:**

1. From the toolbar, select Layer/Add Layer/Add Raster Layer

2. Click on the ‘Open Data Source Manager’ icon ![image](https://user-images.githubusercontent.com/47147296/98470279-7daddc80-21dc-11eb-9037-d3ff35d7aec6.png)  

3. Drag & drop, or double-click data layer, in the Browser pane: ![image](https://user-images.githubusercontent.com/47147296/98470288-89999e80-21dc-11eb-9962-1ca6a546b8a0.png)

For this exercise, from the main toolbar menu, select Layer > Add Layer > Add Raster Layer, which opens the Data Source Manager dialogue box. In Source type, the File radio button should be selected. Under Source, click the ellipsis button ![image](https://user-images.githubusercontent.com/47147296/98470321-bfd71e00-21dc-11eb-81d8-ff9fbe489348.png) and navigate to the Bathymetry folder, then: 

1. Select all four .tif files by holding Ctrl and left clicking the .tif files

2. Click Open in the bottom right corner of the explorer window

3. Click Add in the Data Source Manager, and then click Close

The bathymetry rasters are located along the Suffolk coast, including at the Cefas site, and should look something like the image below.

![image](https://user-images.githubusercontent.com/47147296/98470363-ff056f00-21dc-11eb-8fcb-aa22a5868db4.png)

**Save QGIS Document**

From the main toolbar menu, choose Project > Save > browse to the the Module6_Raster folder and name the file ‘Raster’, choosing to Save as type QGIS files (*.qgs).

## 2.2. Display Multiple Rasters – Virtual Raster

Working with multiple raster files in one document is sub-optimal: to make this more efficient, a Virtual Raster can be created. A Virtual Raster, as known as a Catalog, is a composite file (.vrt) that shows all the rasters together as one file whilst retaining the original raster files. The advantages are that the same symbology is set across all rasters, and a vrt file is created, rather than a new raster file (which can be very large when stored on disk). We will create a virtual raster from the four bathymetry rasters that were added in the previous step.

**Create Virtual Raster:**

1. Select Raster > Miscellaneous > Build Virtual Raster

2. In the dialogue box, click the ellipsis button ![image](https://user-images.githubusercontent.com/47147296/98470321-bfd71e00-21dc-11eb-81d8-ff9fbe489348.png) and under ‘Input layers’ and select the four bathymetry layers > OK

3. Uncheck ‘Place each input file into a separate band’

4. Expand 'Advanced parameters', and use the drop-down to change Resampling algorithm to Bilinear (which is better suited to continuous data). Leave the other parameters unchanged

5. Below the Advanced parameters box, click the ellipsis button under ‘Virtual’, select Save to File, and save in the Bathymetry folder with the name Bathy_Coastal_Multibeam_2014

![image](https://user-images.githubusercontent.com/47147296/98470462-ac788280-21dd-11eb-9578-7a4adff8c680.png)

6. Click Run to execute the tool and click Close when the process is complete. The virtual raster should be automatically added to the document. 

The virtual raster shows a single layer with a continuous symbology.
To ensure that the symbology displays the full range of values, the settings may need to be changed. To do this: 

--	Right click the vrt layer in the Browser pane and select Properties;
--	Select Symbology from the left pane of the Layer Properties dialogue window
--	Expand the Min/Max Value Settings box, check that the Min/Max radio button is checked, and use the drop-down to change Accuracy to ‘Actual (slower)’.
--	Click Apply and OK to close the Layer Properties dialog

The symbology should now show the minimum and maximum values.


![image](https://user-images.githubusercontent.com/47147296/98470513-f7929580-21dd-11eb-8ceb-a80c8990953a.png)

Turn off the vrt file and save the QGIS document, but keep it open.

## 2.3. Display Multiple Rasters – Merge


Multiple rasters can be merged into one new raster file, for example when two or more rasters need to be combined for analysis. This is the equivalent of the Mosaic to New Raster tool in ArcGIS.
The tool requires that the input rasters have the same coordinate reference system, number of bands, and bit depth. Input rasters can have different spatial resolutions, and the resolution used will be the resolution of the first raster in the list. This is unless the resolution is specified in the tool settings. 

**Create a merged raster:**

1. From the main toolbar select Raster > Miscellaneous > Merge

2. In the dialogue box, under Input layers, select the four original bathymetry rasters > OK

3. As before, uncheck ‘Place each input file into a separate band’

4. In Advanced parameters, in the box under ‘Assign specified “nodata” value to output’, type in the value  9999

5. Below the Advanced parameters box, click the ellipsis button ![image](https://user-images.githubusercontent.com/47147296/98470321-bfd71e00-21dc-11eb-81d8-ff9fbe489348.png) next to the box under ‘Merged’, select Save to File and save to the Bathymetry folder, with the filename Bathy_Coastal_Multibeam_2014_Merge, choosing to Save as type ‘TIF files (*.tif)

6. Click Save

The tool’s settings can be seen in the DGAL/OGR Console Call box near the bottom of the Merge dialogue. These settings can be found [here](https://gdal.org/programs/gdal_merge.html), but in later versions of QGIS the Console Call box is not editable. However, additional parameters can be added using Additional command-line parameters [optional] (at the bottom of the expanded **Advanced parameters** box). To set the resolution (pixel size) in Additional command-line parameters, type -ps 0.5 0.5. This sets the resolution to 0.5 m. 

![image](https://user-images.githubusercontent.com/47147296/98470699-56a4da00-21df-11eb-92ae-58fceaa0dbb2.png)

A closer look at the image below shows the parameters in the console call that are set in the dialogue box. 

![image](https://user-images.githubusercontent.com/47147296/98470710-6b816d80-21df-11eb-9656-05b62cbaaa94.png)

The table below shows the relationship between the parameters in the console call and the parameters in the merge dialogue box.

| Console Call     |	Merge Dialogue Box |
| ---              | :-----------------: |
| -m gdal_merge    |	Merge tool         |
|-a_nodata -9999   |	No data            |
|-ot Float32       |	Output data type   | 
| -of GTiff  	     |  Format             |
| -ps 0.5 0.5	     | Pixel Size/ Resolution) |
| -o C:/Users/RH19/Desktop/Module6_Raster/bathymetry/Bathy_Coastal_Multibeam_2014_Merge_ps_setting.tif | Merged (out filename)| 
| --optfile C:/Users/RH19/AppData/Local/Temp/processing_a09bea31f604460092b72f922ad56746/e853b23508634a19bf986ecfc0a44df0/mergeInputFiles.txt |	Input Layers |

7. Click Run to execute the tool and click Close when the process is complete. The Merge raster should be automatically added to the document. 
Right click the merged raster layer and in Layer Properties select Symbology. Under Min/Max Value settings set Accuracy to Actual (slower) > OK.
Save and close the Raster QGIS document.

## 2.4. Convert NetCDF to Raster

Although NetCDF data can be displayed, they cannot be used in analysis. To do this, NetCDF files need to be converted into raster files. 
There are several highly functional QGIS plugins available that will read in NetCDF files. The problem is that these plugins are not normally kept up to date with the latest version of QGIS. If a plugin is seen as useful, an older version of QGIS may have to be installed to get the plugin to work. For this reason, a native method to create a raster from a NetCDF file is shown, rather than showing the functionality of a plugin(s).

1. Open a new QGIS document

2. Use the Browser pane to navigate to the ‘NC_export’ subfolder of the Data folder for this module, and locate the sst.mon.anom.nc file. This NetCDF file is shown as a raster ![image](https://user-images.githubusercontent.com/47147296/98470945-c10a4a00-21e0-11eb-9d4a-8ddbb39c31dd.png). drag and drop this raster into the Layers pane. The NetCDF file is now added as a raster layer. The data layer shows sea surface temperature anomalies.

3. Note that, where a NetCDF file has a more than one time slice, there will be an arrow sign on the left of the NetCDF file in the Browser pane. This can be opened, and the time slice of choice can be added. In the Layers pane, if a question mark symbol appears at the end of the name, click on the question mark, and select the projection, in this case WGS84

The projection is in WGS84, but the longitude is 0 to 360 rather than the standard -180 to +180. (Although not necessary for this exercise, if you wish to change the raster to -180 to +180, from the main toolbar select Raster > Projections > Warp (Reproject). In the dialogue box Input layer: sst_mon_anom.tif (tif saved earlier in this step); Source CRS: Project CRS: EPSG:4326 – WGS 84; Target CRS: Project CRS: EPSG:4326 – WGS 84; Resampling method to use: Bilinear; Additional command-line parameters: -wo SOURCE_EXTRA=1000 --config CENTER_LONG 0, Reprojected: navigate to the NC_export folder and save the file as sst_mon_anom_centre_0.tif. Click the Run button.)

4. To export as a raster, right click the raster layer in the Layers pane, and select Export > Save As. In the Save Raster Layer as… dialogue box, choose Format: GeoTIFF; File name: navigate to the NC_export folder, name it sst_mon_anom.tif, and check that the CRS is EPSG:4326 – WGS 84. 

![image](https://user-images.githubusercontent.com/47147296/98470986-2100f080-21e1-11eb-9434-e30090369066.png)

5. Click Ok to save as a raster. The raster should have been automatically added to the document. Check that the raster has been added and close the QGIS document without saving.

6. **Display as Mesh Layer:** In addition to the above, QGIS can display a NetCDF in a native format by adding the file as, for example, a Mesh file. A mesh layer can be added in the same manner as any other layer, e.g., from the main toolbar: Layer > Add Layer > Add Mesh Layer. For a NetCDF file to be successfully loaded the file’s variables need to be in a certain order, namely, longitude, latitude, and time.

---

## 3. Raster symbology

This section shows how to symbolise raster datasets, depending on the type of data you are displaying.  There are two possibilities:
-	Continuous data – i.e. data that can be measured on a scale, the values of which have a continuous transition between one cell and the next (e.g. sea surface temperature; bathymetry; topography).
-	Unique (or categorical) data – i.e. data that contain discrete categories or classes within well-defined boundaries (e.g. seabed habitats; land use).

## 3.1. Continuous Data

Open the Raster map file from earlier in this module from section 2. If the document does not contain the virtual raster created earlier in Section 2.2, please add the file. Right click the vrt layer, select Properties and select Symbology. In the Layer Properties dialogue box change the Render type to ‘Singleband pseudocolor’; from the drop-down next to Color Ramp select Blues. The darkest blue needs to be set to the deepest values. If this is not the case by default, click the Color Ramp drop-down again and click Invert Color Ramp.

![image](https://user-images.githubusercontent.com/47147296/98471129-227ee880-21e2-11eb-8592-2a7a018c83a5.png)

The vrt layer should now be symbolised with a light to dark blue colour ramp.

![image](https://user-images.githubusercontent.com/47147296/98471134-36c2e580-21e2-11eb-83fa-e71feb2f1844.png)

Save the Raster QGIS document.

## 3.2. Unique Data

Open the Raster QGIS document if it is not already open and turn off all layers.

**Clip Raster**

Rasters can be clipped to an area of interest. This can be done, for instance, to speed up analysis by processing just a subset of a larger dataset, or for presentation purposes.
There are two options for achieving this:

1.	Setting the coordinates of the desired spatial extent: Clip Raster by Extent.
2.	Using another file to set the area to be clipped: Clip Raster by Mask Layer.

Both tools can be found under the main menu item Raster > Extraction.
For this example, a raster showing EUNIS Level 3 habitat areas will be added to the Raster.qgs document, then clipped and symbolised.

**Load Raster and Mask Layers**

1. Click the Open Data Source Manager button ![image](https://user-images.githubusercontent.com/47147296/98471198-84d7e900-21e2-11eb-89c8-64bdc9031b9f.png) from the toolbar.

2. In the left panel click Raster and load the following raster file from the EUNIS subfolder in your workspace for this module: C20191101_CombinedMap_9_6_6_bng_clip.tif.

While in the Open Data Source Manager dialogue, load the area of interest polygon vector layer:

3. Select Vector from the left panel, navigate to your workspace and, from the AreaOfInterest folder, select AreaOfInterest.shp, and click the Add button.

4. Close the Data Source Manager dialogue.

Turn on the raster and area of interest, if required, and turn off all other layers.


### 3.2.1. Clip Raster by Mask Layer 

1.	From the toolbar, select Raster > Extraction > Clip Raster by Mask Layer.
2.	In the dialogue box set the Input layer to the EUNIS tif file, and the Mask layer to the vector AreaOfInterest shapefile.

![image](https://user-images.githubusercontent.com/47147296/98471247-df714500-21e2-11eb-8c2b-09a267074ab1.png)


3.	Scroll down the dialogue box to Clipped (mask), click the ellipsis button ![image](https://user-images.githubusercontent.com/47147296/98470321-bfd71e00-21dc-11eb-81d8-ff9fbe489348.png), select Save to File, navigate to the EUNIS folder and name the clipped raster C20191101_CombinedMap_9_6_6_bng_clip_aoi.tif, choosing TIF files (*.tif) for ‘Save as type’.  
4.	Click Run and close the dialogue box when completed.

The result is the EUNIS raster clipped to the area of interest.

![image](https://user-images.githubusercontent.com/47147296/98471293-1f382c80-21e3-11eb-8a7a-2747cf9669d5.png)

### 3.2.2. Symbolise raster

1. Right click the raster created in Step 3.2.1., choose Properties and, in the Layer Properties dialogue box, select Symbology. Under **Band Rendering**, for Render type, select Paletted/Unique values and, at the bottom of the **Band Rendering box**, click the Classify button. This should add all of the unique values and assign a default colour. Both the colour and label can be changed by double clicking on the colour symbol or label text.

![image](https://user-images.githubusercontent.com/47147296/98471336-61fa0480-21e3-11eb-9bdb-d6fc298d1677.png)

Change the labels to reflect the EUNIS Level 3 classifications, from the table below. 

| Value | Label |
| ----- | ----- |
| 1     |  A2.4 |
| 3     | A5.2  |
| 4     | Na    |

2. Click Apply and then OK. The unique values should be symbolised.

![image](https://user-images.githubusercontent.com/47147296/98471394-c6b55f00-21e3-11eb-8699-f207cc9eb45b.png)

3. Save and close the Raster QGIS document.

## 4. Raster Basic Analysis

This section demonstrates basic raster analysis using the Raster Calculator.

### 4.1.  Raster Calculator

Rasters can be the basis of powerful spatial analysis. All rasters in the analysis need to be aligned and there must be spatial overlap between the raster datasets involved.
Open a new QGIS document and, as with Step 2.1, change the project’s coordinate system to British National Grid (EPSG:27700). Add both raster layers from the Calculation folder in your workspace for this module.
Save the QGIS document in the Calculation folder with the name Calculation.qgs.

### 4.2. Overview of the Raster Calculator

Most raster spatial analysis can be undertaken in the Raster Calculator, which can be opened from the main toolbar – select Raster > Raster Calculator.
Calculations are made at cell level, in that every calculation is performed on every cell and on the spatially-correspondent cells from other rasters.
Rasters can be added to the Raster Calculator Expression by simply double-clicking from the rasters listed in the Raster Bands window of the Raster Calculator dialogue. The output raster is created using the Result Layer settings for Output layer and Output format.

Run the calculations for the following simple examples and check the results as described. After checking the calculations turn on only the input rasters and progress to the next calculation. 

### 4.3. Addition

In this example, add 0.5 to the value of every cell:

1.	In Raster Bands double-click raster1@1 to add it to Raster Calculator Expression.  
2.	From Operators click the plus sign, click in the Raster Calculator Expression and type 0.5. The Raster Calculator Expression will show “raster1@1” + 0.5
3.	Click the ellipsis next to Output layer, navigate to the Calculation folder and save the output as raster01_addition.tif > OK.

![image](https://user-images.githubusercontent.com/47147296/98471456-4e02d280-21e4-11eb-8750-4044722ad5e5.png)

4.	To check the results, use the Identify Features tool ![image](https://user-images.githubusercontent.com/47147296/98471466-5ce98500-21e4-11eb-8945-f198fe5e39a4.png) and, in the tool, change Mode to Layer Selection. Click on the rasters, and in the pop-up box click Identify All from the list. This will show the values for that cell from each of the input rasters and the resultant output raster. As you can see from the image below, for Band 1 raster01 = 1, and raster01_addition = 1.5.

![image](https://user-images.githubusercontent.com/47147296/98471475-712d8200-21e4-11eb-92a7-9bf18c345241.png)

### 4.4. Multiplication 

Following the same procedures as for step 4.3.

1.	Raster Calculator Expression: “raster1@1” * 2
2.	Output layer: browse to Calculation folder and name raster01_double.tif

### 4.5. Substract

1.	Raster Calculator Expression: “raster1@1” – “raster2@1”
2.	Output layer: browse to Calculation folder and name raster01_subtract_raster02.tif

### 4.6. Manipulate multiple input layers

1.	Raster Calculator Expression: “raster1@1” * “raster2@1”
2.	Output layer: browse to Calculation folder and name raster01_multiply_raster02.tif
Save the QGIS document, but keep it open.

---

## 5. Raster to Vector

Raster data can be converted to vector data – this may be necessary for certain types of analysis, or for display purposes.  The example shown here is the conversion of a raster bathymetry layer to contours.  If you’ve closed your Calculation.qgs document, reopen it now and turn off all layers.
1.	Add the merged bathymetry raster you created previously (Bathy_Coastal_Multibeam_2014_Merge.tif).
2.	From the main toolbar menu, choose Raster > Extraction > Contour... to open the Contour dialogue window.
3.	For the Input layer, use the dropdown arrow to select the merged raster. 
4.	Under ‘Interval between contour lines’, type the value 1.0 in the box to set the interval between contour lines and, under ‘Attribute name’, change the field name if required (but the default name given is ELEV).

5.	To save the output, click the ellipsis button ![image](https://user-images.githubusercontent.com/47147296/98470321-bfd71e00-21dc-11eb-81d8-ff9fbe489348.png) to the right of the Contours box, browse to the Bathymetry folder, name the file Bathymetry_Coastal_Multibeam_2014_Merge_Contour_1m and choose to save as a shapefile [Save as type: ‘SHP files (*.shp)’] .

![image](https://user-images.githubusercontent.com/47147296/98471536-e8631600-21e4-11eb-926c-ed4e3419c7ef.png)

6.	Click Run, and then Close when the tool has completed.
The contour lines should look something like the image below.  You can change the symbology if you wish, to make the contour colours more distinctive.

![image](https://user-images.githubusercontent.com/47147296/98471548-f9138c00-21e4-11eb-87db-90c836bbf15a.png)

Close the QGIS document – it is not necessary to save it.

## 6. Conclusion

You have now completed this module, and should be able to:
-	Load raster files
-	Manipulate raster files to be ready for display and analysis
-	Symbolise raster files
-	Perform basic raster analysis
-	Create contour vector files from rasters


## 7. Additional Resources

https://gdal.org/programs/
https://gdal.org/programs/gdalbuildvrt.html#gdalbuildvrt
https://docs.qgis.org/3.10/en/docs/training_manual/rasters/index.html
https://psl.noaa.gov/data/gridded/data.kaplan_sst.html#detail
https://environment.data.gov.uk/DefraDataDownload/?Mode=survey
https://jncc.gov.uk/our-work/marine-habitat-data-product-eunis-level-3-combined-map/
https://www.ordnancesurvey.co.uk/opendatadownload/products.html


## 8. Acknowledgement

### 8.1. Authors

**Tutorial content and instructions:**
Richard Harrod (richard.harrod@cefas.co.uk)

**Markdown:**
Lenka Fronkova (lenka.fronkova@cefas.co.uk)

### 8.2. Data Resources
Datasets not listed in the table were created specifically for this module by Cefas.










