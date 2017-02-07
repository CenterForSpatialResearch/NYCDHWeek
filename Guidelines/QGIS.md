
# Mapping Data with QGIS - Part I

The purpose of this tutorial is to introduce you to the mapping platform, QGIS, and help you become familiar with the interface and its features. By completing this tutorial, you will be able to:

* Navigate most commonly used features of the QGIS user interface 
* Add shapefiles to a project
* Add a vector layer
* Upload a dataset to QGIS 
* Join datasets based on a shared identifier
* Join datasets based on a shared location
* Query a dataset based on a feature
* Create a choropleth map

## Getting Started
Download the GitHub repository for the tutorials. Using the green button [here](https://github.com/CenterForSpatialResearch/NYCDHWeek), select `Download ZIP`. You only need to do this once. The Data folder will then have all of the datasets needed for this tutorial. 

## Mapping Refugee Destinations in the United States

This mapping project is based on recent [discussions](https://www.thisamericanlife.org/radio-archives/episode/600/will-i-know-anyone-at-this-party?act=1") about Refugees in the United States, research on language maintenance and English acquisition by refugees in the [Twin Cities Metropolitan Area](http://onlinelibrary.wiley.com/doi/10.1111/j.0020-7985.2003.00262.x/full) (Fennelley and Palasz, 2003) and the shift in the early 2000's away from refugees being resettled in larger cities towards smaller and mid-sized cities. We are interested in this topic because Refugees in the US tend to speak less common languages (i.e., not English, Spanish, or Chinese), and tend to settle in small enclaves. Unlike other immigrant groups, refugees tend to have less academic and linguistic preparation before arriving in the US and because of a variety of factors, rarely have the opportunity to, or other adult learning opportunities (for more about Refugees in the US, visit [Office of Refugee Services](http://www.acf.hhs.gov/orr).

We are interested in creating a map of refugee resettlement in the United States (and at the same time exploring the QGIS interface). We have a point file for the cities refugees go when they arrive in the United States (from the [Refugee Processing Center](http://www.wrapsnet.org/Reports/InteractiveReporting/tabid/393/EnumType/Report/Default.aspx?ItemPath=/rpt_WebArrivalsReports/MX%20-%20Arrivals%20by%20Destination%20and%20Nationality)) and a polygon file for state boundaries. This map will serve as a basemap to which we can add additional information and layers in order to better understand refugee resettlement in the United States.

## Setting up QGIS

1. Download QGIS [here](http://www.qgis.org/en/site/forusers/download.html)
	1. On a PC, this is straightforward. Simply Click on the 'QGIS standalone installer' and follow the prompts. 
	2. On a Mac, you will be taken to the KyngChaos page.
	![kingchaos](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/qdown.png)
	3. Something like this will download
	![download](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/qgisdownload.png)
	4. You MUST install the items IN ORDER. They are numbered. It is very important to follow the numbers. 
	5. Finally, follow all of the prompts for all of the packages. 

**Launch** QGIS. Your new blank map project will look like this:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/01_OpenQGIS.png)

Begin to familiarize yourself with the interface by hovering over the icons to see what they say. You can also refer to this [brief description](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Resources/QGIS_InterfaceDescription.md) of the elements of the interface for more information. 

## Adding Layers

Maps in QGIS are based on data layers. This system allows you to analyze datasets with respect to each other. We will use two layers with different information. The basemap is polygons representing states in the US. 

First we will add a basemap of the United States. 
1. Go to the Data/cb2014 folder. This folder contains all the files QGIS needs to make an outline of the United States. 

	1. You'll notice a number of different file extensions. Do NOT delete, move or rename these files.
	
	2. These **files must stay together** in the same folder otherwise QGIS will not be able to load the layer.
		* .shp - The main file that stores the feature geometry (required).
		* .shx - The index file that stores the index of the feature geometry (required).
		* .dbf - The dBASE table that stores the attribute information of features (required).
		* .sbn and .sbx - The files that store the spatial index of features (these might get corrupted, see note at the end of this tutorial).
		* .prj - The file that stores the coordinate system information.
		* For more information on these extensions and others see [this explanation by ESRI](http://webhelp.esri.com/arcgisdesktop/9.2/index.cfm?TopicName=Shapefile_file_extensions).
		
		
2. In the browser (on the left side of the QGIS window), navigate to where you saved the Data/cb2014 layer. For me, that is here. It may be somewhere else for you. 
![layer](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/browserpanel.png)

3. Click on the `Add Vector Layer` button to add the data. 
![vector](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_Adding_Layers_Vector.png)
	1. Add the `cb_2014_us_state.shp` file. Even though we only add this file to the map, QGIS still references the other files (.shx,.dbf,.sbn,.prj). 
		1. The selected layer will be added in default colors. 
3. This map looks strange because it is in the wrong Coordinate Reference System (CRS). We need to change the projection. Here's a [simple tool](http://projectionwizard.org/) to help you pick a CRS if you ever don't know which one to pick. 
	1. Double click on the layer to change to CRS. We want "North America Lambert Conformal Conic (EPSG: 102009)" (North America Albert would have been OK, too)
	![image](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/CRS.png)
	2. Click on the Render box in the lower right hand. Also change this to "North America Lambert Conformal Conic (EPSG: 102009)"
	![image](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/projection.png)
5. Moving Alaska and Hawaii is beyond the scope of this tutorial. 

6. Add the cities layer. 
	1. Add Delimited Text layer
	![Delimited](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/Delimited.png)
	2. Find the city_latlong.csv file
	3. Select the 'csv' button and make sure that the latitude and longitude columns are the correct ones.
	4. If you can't see the points or only see one point, double click on the layer and go to General to make sure that it is the same projection as the map (North America Lambert Conformal Conic (EPSG: 102009)).
	5. If you still can't see them, click on the zoom full magnifying glass (with three arrows pointing outwards), and then zoom back in to the lower 48 states.

7. Moving Layers

	1. Click and drag the states layer on top of the cities layer. The cities points are no longer visible because they are behind the states polygons. 

8. It might be easier to look at if we use state outlines rather than filled polygons. To do this, we must change the **style** of the data layer. 

	1. Double click on the layer name.
	2. The properties box will appear, select the 'Style' tab on the left
	3. Click on Fill > Simple Fill
	4. Select Fill > Transparent and Border > Solid Line
	5. Select 'OK' to exit the menu

**Save** your QGIS project by selecting `Project` > `Save`. Name your project Refugee_Cities.qgs and save it in the folder you are using for this tutorial. QGIS projects are saved as .qgs files. It is important to note that the data layers are not saved with it the map project but are rather linked to the project.


We are ready to answer a few questions: 

* How many states have populations of greater than two million people? 
* How many states received more than 300 refugees in 2014? 
* How many states with fewer than ten million people received greater than 300 refugees in 2014?

## Set Up


We already mapped the locations of refugee resettlement in the United States as well as state polygons. We have tabular data available for population at the state level from the [United States Census](https://www.census.gov/) in the state_pop.csv file. The city data also has the number of Refugees per city. We will use these two datasets to answer questions about population and refugee resettlement. In the next tutorial, we will use more detailed information about the cities, including income and infrastructure.


In order to answer these questions we’ll first select just those cities which have populations of more than two million. Then we will export that as a separate layer. 


### Import population information

Now we will add the table containing population by state which we will join to the state polygons. *QGIS can read several types of tabular data formats, including .csv and .xls files. Our total population file is saved an .csv file (note QGIS cannot read .xlsx files).*

1. Upload Tabular Data
	
	1. Click on the Add Vector Layer button 
	
	2. Add the state_pop.csv file. (Note: we realize it is a little bit confusing that we use the `Add vector layer` button in order to add tabular data to our map project however this is somewhat a product of the fact that QGIS is open source).
	![CSV](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_Adding_Layers_Vector.png)
	
	3. State_pop should appear in the Layers menu. *Because it is just a table and does not have any geometry, it will not show up in the map view.*
	
	4. Open its attribute table to see the fields that it contains before we join it to our state polygons. 
	
	5. Make a note of the columns (or fields) it contains. 
	
	6. This dataset has been pre-cleaned, and the column names have been reformatted. See the tutorial on DATACLEANING for more details.

2. Perform a Table Join *A table join allows GIS users to combine tabular data with vector data based on an identical field in their attribute tables.*

	1. **Right-click** 2014_Census_State in the layer menu and select `Open Attribute Table`. This describes the data associated with each feature in the feature class.
	![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/attribtable.png)
	
	2. To join attributes from a table to a shapefile the two data sets must share a common attribute field. 
	
	3. Review the fields in the attribute table for the 2014_Census_State layer, they are: 
	
		* STATEFP
		* STATENS
		* AFFGEOID
		* GEOID
		* STUSPS
		* NAME
		* LSAD
		* ALAND
		* AWATER

**Note that NAME is identical to stateName**, and each is unique -- no two states have the same name. This unique field that is common to both datasets is what allows us to join the tabular population data to the vector file describing the geometry of those countries. 

We always start the join on the file that we are joining to. We are joining the population estimates table to the state boundary shapefile. 


1. Open the Properties for the 2014_Census_State layer.

2. Navigate to “Joins” in the left hand menu. 

3. Click the “+” icon. 

4. Make the following selections in the dialogue box.
	![Attribute](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/vectorjoin.png)

	1. join layer = state_pop
	
	2. join field = stateName
	
	3. target field = NAME which matches the join field in the 2014_Census_State layer.
	
	4. **Click** `OK` to close the join dialogue. 
	
	5. **Click** `OK` to close the layer properties menu. 
	
5. Open the attribute table for the countries shapefile. A new field has been joined to the right hand side of the table: state_pop_population
IMPORTANT!! This joined data is not permanently associated with its attribute table. The relationship only exists within this QGIS project. If we added the cb_2014_us_state layer to another QGIS project the fields we joined from the population estimates would not be there. To permanently incorporate the join, we must save a new version of the shapefile.

6. **Right-click** on the 2014_Census_State layer and select Save.

7. Select `ESRI Shapefile` as the format, and save your file in the same folder as the project folder as stateboundaries_pop.shp. 

This new layer will then be added to the map and will contain the  joined data.

## Attribute Tables and Data Querying

Now that we have assembled these data layers we can begin to ask a few simple questions about the data. We will accomplish this by querying the attribute fields of our two vector layers, the populated places and the countries. To do this we will select features using Select by Attributes. 

There are multiple routes to select features within a dataset. We will follow one, but you may see other ways. We want to select just those states with an estimated population of greater than two million.

1. Open the stateboundaries_pop attribute table and select select features using an expression
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/selectfeature.png)

2. Make sure the header is correct - we want to select features from the stateboundaries_pop layer.

3. If you click on any of the terms in the central box a description of it will appear on the right. We will combine the field name with other operators to build an expression on the left side.
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/selectfeaturesscreen.png)

4. Expand `Fields and Values` and select 'state_pop'
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/selectstatepop.png)

5. **Double-click**  on `state_pop` and it will appear in the expression box on the right. 

6. Open Operators and double-click on the greater than symbol (>). Type in 2000000. Your expression should now look like the following:
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/greaterthan.png)

7. **Click** `Select`. Some of the populated_places points should turn yellow. At the bottom left corner of your QGIS project the footer will show how many features were selected (36).
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/selected.png)

8. Save those 36 states as a separate shapefile, just like we did for the cb_2014_us_state layer after we joined the population estimates to it. 

9. **Right-Click** in on the stateboundaries_pop layer, **select** Save As. 

10. Select Save only selected features, and save the shapefile as selectedlayers.shp. This will then be added to our map as a new layer. 

11. To see the new layer, clear your selection by clicking the Deselect features from all layers button.
![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/18_Deselect.png)

## Refugees per state

Now we need to create a layer that will tell us how many refugees went to each state. Our city_latlong file has the number of individuals in it. To count the number of individuals per state, we will join the city_latlong to stateboundaries_pop based on their shared location, and then sum the 'Individuals' column.

1. Select the stateboundaries_pop layer

2. Select Vector > Data Management Tools > Join Attributes by Location
![Attributes](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/joinbylocation.png)

3. In the Dialogue box, select the following options
![Attributes](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/joinlocation_attributes.png)

4. Save as citystaterefugees.shp and click 'OK'

5. Open the attribute table for the citystaterefugees layer. You should see a SUMIndividuals column. This represents the sum of individuals across all the cities in that state. (Don't worry about the NULL values - it just means there aren't any cities in that state where refugees are settled). 

6. Order by number of refugees per state by clicking on the SUMIndividual column header.

7. What state received the most refugees? 

8. Click on that row (by clicking on the number on the far left). Move the attribute table out of the way so you can see the map again. That state should be highlighted. You can select multiple rows by holding the "Command" button and clicking on the rows you are interested in.

9. Close the attribute table and 'Deselect Features' from 'All layers'
![features](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/deselect.png)

10. Select the `select features using an expression` tool. We will again select by expression in order to select the states with greater than 300 refugees. Use the expression builder as we did above to select the states. Your expression should read:  `"SUMIndividuals"  > 300`

The footer bar of the map will indicate that 14 features were selected. 

Use this selection to identify which states have recieved more than 300 refugees but have a total population of fewer than ten million people. Use the expression builder to figure out which 6 states have these two characteristics. *Hint: You will need to use 'AND'*

11. SAVE your project

## Creating a map

Now that we have calculated information about the number refugees in each state, we can represent that in different ways in the map. We will make a chloropleth map to represent refugees by state. We will then go over cartographic conventions adding a legend and scale bar to the map and exporting as a PDF. 

We will create a choropleth map for refugee population by state, where each state will be colored according to the number of refugees who settled there in 2014. 

1. **Open** the properties for the citystaterefugees layer and navigate to the Style tab.

2. Select Graduated Symbols from the dropdown at the top.
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/graduated.png)

3. Select SUMIndividuals as the Column on which we will color the map. 

4. To change the color of the entire state polygon, we need to change the symbol from an outline to a filled polygon.

5. Click the Change button next to Symbol and select “simple fill.” 

6. Next  break up the data into classes (ranges of values) and classify the colors for the choropleth map according to these. 

	1. Change the mode to Natural Breaks (jenks), and the number of classes to 8.
	
	2. **Click** `Classify`. Your properties menu will now look like the one below. 
	![Attribute](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/jenks.png)

	3. Click `Apply`. The country polygons will change on the map. 
	
7. Some states stayed the same color as the base color. These states do not have any relevant data. That is, no refugees were resettled there in 2014.



## Designing a map
In order to present this map, we will now compose a map layout and become familiar with the QGIS map composer. The map composer allows you to add a legend, north arrow and scale bar to the map as well as to export our work as a PDF. 

1. Open a new map composer 
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/composer.png)

2. To add a new map to the composer select the add new map button. 

3. Then click once and drag a rectangle over the area on the page that you would like the map to occupy. *Whatever is showing in your QGIS map project window is what will appear in the new map.*
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/composenewmap.png)

4. Add a legend. 

	1. Select 'Add New Legend'. 
	![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/addlegend.png)

	2. Again click to draw a rectangle where you would like to place the legend. An unformatted legend that matches the information from the Layers panel will appear. 
	
	3. Use the options in the Item Properties tab to change which layers are represented in the legend and to change the labeling of the layers in the legend.
	
	4. Select the 'Item Properties' Tab
	
	5. Unselect 'Auto Update'
	![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/itemproperties.png)

	6. Remove Unnecessary layers with the '-' button
	
	7. Change the layer names by clicking the “legend item properties” button
	![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/customlegend.png)

5. Add a scale bar

	1. Select Add new scale bar button. 
	
	2. Again you will be able to change the properties of the scale bar, including the style, number of segments and size. 
	![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/scalebar.png)

6. Add text boxes

	1. Add a title for the map 
	
	2. Add abbreviated citations for our data sources. 
	
	3. Click the add new label button then use the Main properties field to add the text, and use the Font button to change the text size and font. 
	![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/textlabel.png)

7. use one of the export options circled in blue above to save the map composition as an image file, PDF, or SVG. 
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/saveas.png)

______________________________________________________________________________________________________________

This tutorial was prepared by Michelle McSweeney for the NYCDH Week. It is based on the tutorial written by Dare Brawley, for *Mapping for the Urban Humanities* taught in Summer 2016 also by the [Center for Spatial Research](http://c4sr.columbia.edu).




