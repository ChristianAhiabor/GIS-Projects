# Watershed Delineation of a portion of Kwahu South district of Ghana using QGIS

## Step 1: Creating a Digital Elevation Model (DEM) for your study
- The shapefile for the study area was obtained by clipping the district polygon from Ghana's administrative shapefile dataset at [GADM](https://gadm.org/download_country.html).
- The DEM was created using QGIS SRTM downloader by setting canvas extent to suit the study area.
  
## Step 2: Changing Coordinate System
- Adjust the Coordinate Reference Sytem of the DEM to a Projected Coordinate system which in this case is WGS 84/UTM zone 30N.
- To ensure accurate spatial analysis the UTM (Universal Transverse Mercator) provides better distance and area calculations than geographic coordinates (latitude/longitude).
  
## Step 3: Fill Operation
- This process is done by using Fill Sinks (Wang & Liu) tool located in Terrain Analysis-Channel section of SAGA toolbox.
- This step removes depressions or sinks in the DEM that could interfere with hydrological analysis.
- In the pop-up dialog box untick Flow direction and Watershed basins and set DEM to the created DEM and save output as *Filled Dem*.
- By unchecking Flow direction and Watershed basins, the process strictly modifies elevation without additional calculations.
  
## Step 4: Strahler Order 
- The Strahler order assigns hierarchical values to streams based on their connectivity. Higher values represent main rivers, while lower values indicate tributaries.
- The Strahler order tool is in the Terrain analysis-channel section in the SAGA toolbox.
- In the pop-up dialog box, for Elevation select Filled Dem and save output as *Stream order*.
- In properties menu of Strahler order layer modify symbology by changing render type to singleband pseudocolor, interpolation to discrete, Mode to Equal interval and Classes to 11.
  
## Step 5: Raster Calculation
- Raster calculator can be located in Raster section from QGIS menu bar.
- In raster calculator perform the expression: [Stream order] >= 6 and save output as *New Stream order*.
- This calculation filters streams based on their order, retaining only significant water channels (those with order 6 or higher).
- The result is a binary raster where 1 represents streams with Stream order >= 6 and 0 represents areas without significant streams.
  
## Step 6: Channel network operation
- This process is done by using the Channel network and Drainage Basins tool from Terrain analysis-channel section of SAGA toolbox.
- This tool extracts major drainage paths using the Filled Dem as elevation, setting the Threshold to 6, and unticking everything except for Channels ensuring only significant streams are included and save output as *Channels*.
  
## Step 7: Upslope Area Calculation
- The Upslope area tool is located in from Terrain Analysis-Hydrology section in the SAGA toolbox.
- For this operation you will be required to provide Target X and Y coordinates which should be the point where multiple main channels meet creating a watershed divide. 
- Coordinates can be made evident by right clicking on your desired point of interest and copying coordinates.
- In the upslope area dialog box, insert Target X and Y coordinates, set Elevation to Filled Dem and select Deterministic 8 as the Method.
- Save output as *Watershed*.

## Step 8: Watershed Polygonization
- The final raster output is converted into a vector polygon by using the Polygonize tool for better visualization and spatial analysis.
  
## Step 9: Clipping Channels with Watershed 
- The watershed polygon is used to clip the extracted channels, refining the final water network.
- Save output as *Water body*.

## Step 10: Export map as Image and 3D visulaization
- Insert the necessary Title, Legend, North arrow and Scale bar in Print layout view and save map as an Image.
- With the help QGIS plugin *QGIS2threejs* the map is further visualized in a 3D format. 

## Results
![Delineation(new)](https://github.com/user-attachments/assets/fd683d04-a672-4649-9d08-c4b4b6fd44a7)
![delineation](https://github.com/user-attachments/assets/8b714046-b07b-4309-94a4-71fc03d5e232)


