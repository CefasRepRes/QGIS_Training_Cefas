# QGIS Training Module 3 – Data Visualisation and Query 

---

## 1. Introduction

This QGIS module focuses on data visualisation and querying. The instructions are written for Q-GIS 3.2 version and above.  In this module, you will learn the following:
* 	Create points
* 	Labelling
* 	Data query
* 	Symbology and Data Visualisation
* 	Count the number of points in a polygon
* 	Creating new fields in attribute table

To access data for this module, please contact us at gissupport@cefas.co.uk and we will share the data with you and a link to a supplementary tutorial video.

The data folder contains the following:

**add data table**

1. training_data_vms.csv with fields:
*  speed- fishing speed
*  gear – fishing gear
*  d_harbour – departure harbour
*  r_harbour – return harbour
*  d_date – departure date
*  r_date – return date
*  catch- kg of fish caught
*  lon-easting
*  lat- northing

**source:** fictional- created for the purposes of this module



**source:** https://www.eea.europa.eu/data-and-maps/data/eea-coastline-for-analysis-2

1. Scottish Marine Protected Areas (MPAs) - mpa_scotland.shp

**source**: OSPAR (https://www.ospar.org/work-areas/bdc/marine-protected-areas)

---

## 2. Data Visusalisation and Query

### 2.1. Open QGIS Project
Navigate to the folder where you saved your data and double click on Module2_Data_Visualisation_and_Querying.qgs. The QGISs project contains UK/Irish coastline, MPAs and major Scottish towns shapefiles.

### 2.2. Create VMS points from a csv file
Open **Data Source Manager (CTRL+L)** or click on ![image](https://user-images.githubusercontent.com/47147296/80372253-2624d080-888b-11ea-8133-d22c2c63a21b.png) and select 'Delimited Text'. In File Name navigate to the place where you saved the data (hereafter the data folder) and click on 'training_data_vms.csv' file. Choose **Layer Name** and in **Geometry Definition** 'X' field as lon and 'Y' field as lat. Geometry CRS is selected as 'OSGB 1936 /British National Grid' (EPSG: 27700). Click Add and Close.  This layer is only virtual. In order to save it go Right click on it in the table of contents (TBO)--> **Save As**. In File Name browse to the data folder location and chose name ‘vms.shp’ This will be exported as a shapefile and loaded to your map document after clicking **OK**. You can remove the original layer (Right click- remove).

### 2.3. Create Labels
Right click on **towns_scotland** --> **Properties** --> **Labels** --> **Show labels for this layer** and select the town name column:

![image](https://user-images.githubusercontent.com/47147296/80371235-77cc5b80-8889-11ea-8545-ccfb75d6cfe9.png)

Place the labels below the points: **Placement** --> **Offset from point** --> **Apply and OK**.
![image](https://user-images.githubusercontent.com/47147296/80371323-a1858280-8889-11ea-84e1-79595021497f.png)

### 2.4. Change the style of VMS points and querying
Right click on **vms** in the table of contents --> **Properties** --> **Symbology**, where you can change colour or size of the points. Then click on **Source** --> **Query Builder** and try to type in a query which selects **(Task 1):** only the points that depart from Aberdeen and Inverness, have speed between 2-4 and gear type is Boat Dredges (DRB).

_(Hint: by left-clicking on the field and then click All, you will get all the attribute values that are present in the field. The result is at the end of this module with more SQL examples.)_

![image](https://user-images.githubusercontent.com/47147296/80371516-ee695900-8889-11ea-8a21-cb21a64ab032.png)

You can explore the result of which VMS points belong to the specific ports and use different SQL statements and see how they change the output. More SQL tasks below with answers at the end. For the purpose of this module, however, we are going to use all the data. Therefore, you can remove the statement from the **Query Builder** and click **Apply and OK**.

**Task 2:**
Select all the data points where the ships fished between 1st January 2015 and 15th February  2015 and they landed in Mallaig.
_(Hint: by left-clicking on the field and then click All, you will get all the attribute values that are present in the field. The result is at the end of this module with more SQL examples.)_

### 2.5. Count the number of points within MCZ
Click on the **Vector** in the tob panel --> **Analysis Tool** --> **Count points in polygon**

![image](https://user-images.githubusercontent.com/47147296/80371928-98e17c00-888a-11ea-8d88-d294772a8386.png)

Add the following fields and save the new shapefile in your data folder. Uncheck ‘Open output file after running algorithm’:

![image](https://user-images.githubusercontent.com/47147296/80372031-c1697600-888a-11ea-933a-b0d6f2a80406.png)

### 2.6. Add mpa_scotland_vms.shp
**CTRL+L** and click on **Vector** ![image](https://user-images.githubusercontent.com/47147296/80372176-0392b780-888b-11ea-8618-9b3fbb71b7ca.png). In the file section, navigate to the place where you saved the output from 2.5 and add it, by clicking on mpa_scotland_vms.shp. Cick **Add and Close**.

### 2.7. Open attribute table and add a new field
Right click on **mpa_scotland_vms** --> **Open Attribute Table** -->**Edit mode** ![image](https://user-images.githubusercontent.com/47147296/80374150-1eb2f680-888e-11ea-854d-359ddc9f4357.png)           
Open **Field calculator**  ![image](https://user-images.githubusercontent.com/47147296/80374237-4a35e100-888e-11ea-9292-8f0bac0c37c5.png) and type in the following field:

![image](https://user-images.githubusercontent.com/47147296/80374313-65085580-888e-11ea-9543-d0f3bd95fe68.png)

Click the **Editing tool** ![image](https://user-images.githubusercontent.com/47147296/80374150-1eb2f680-888e-11ea-854d-359ddc9f4357.png) again to navigate out of the editing session and click **Save edits**.
We calculated fishing effort per MPA as each point has temporal resolution of 2 hours (number of points per MPA * 2).

### 2.8. Change symbology of MPAs
Right click **mpa_scotland_vms** --> **Properties** --> **Symbology** --> **Graduated**. Pick 'effort_h' column and click on **Classify** and **Apply and OK**. You can also change the colour ramp by clicking on the box and choosing a colour of your choice.

![image](https://user-images.githubusercontent.com/47147296/80372836-0b069080-888c-11ea-97dd-f9a831effce7.png)

![image](https://user-images.githubusercontent.com/47147296/80372888-240f4180-888c-11ea-9ad3-02fd60a63178.png)

This step visually differentiates MPAs from each other depending on the fishing effort that occurs in them. You can use hte **Identify tool** ![image](https://user-images.githubusercontent.com/47147296/80372991-4c973b80-888c-11ea-8098-21d3048198b1.png) to find out how much fishing effort is in a specific MPA. For the identify tool to work, you must highlight mpa_scotland_vms layer in the table of contents first (right click).

Following the same steps than in the part 2.4, you can complte **Task 3:**
Select MPAs that have effort greater or equal to 100 and their STATUS is proposed. The result is in the answers.

Congratulations, you just completed Cefas QGIS Training Module 3 🥇 🥇 🥇 

---

## 3. Task answers

**Task 1**

![image](https://user-images.githubusercontent.com/47147296/80373635-43f33500-888d-11ea-9eb8-b5b8c64d41ff.png)

**Task 2**

![image](https://user-images.githubusercontent.com/47147296/80373724-68e7a800-888d-11ea-97ee-322c401c7c63.png)

**Task 3**

![image](https://user-images.githubusercontent.com/47147296/80373497-11e1d300-888d-11ea-99e8-546dc0e0ce85.png)

---

## 4. Additional Resources

https://docs.qgis.org/3.10/en/docs/training_manual/basic_map/symbology.html#basic-ty

https://www.qgistutorials.com/en/docs/3/basic_vector_styling.html

---

## 5. Author and Contact

**Author:** Lenka Fronkova

**Contact:** gissupport@cefas.co.uk
