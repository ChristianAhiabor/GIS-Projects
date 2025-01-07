# Creating Deforestation and Afforestation Maps Using ArcGIS

## Step 1: Download Image Data
1.	Source Data:
  - Visit [Copernicus Data Space](https://browser.dataspace.copernicus.eu/) to download Sentinel-2 imagery for your study area for the years 2020 and 2024. 
  - Ensure to select bands suitable for NDVI calculation, typically Band 4 (Red) and Band 8 (Near-Infrared).
2.  Study area was clipped from Ghana's administrative shapefile which was obtained from [GAdM](https://gadm.org/download_country.html) 

## Step 2: Create NDVI Maps
1.	Open ArcMap.
2.	Load Sentinel-2 imagery for both 2020 and 2024.
3.	Use the Raster Calculator from the Spatial Analyst toolbox to calculate NDVI: Formula: Float (Band 8 - Band 4)) / Float (Band 8 + Band 4)
4.	Save the results as separate raster layers (e.g., NDVI_2020 and NDVI_2024).

## Step 3: Classify NDVI Values
1.	Right-click on the NDVI rasters (NDVI_2020 and NDVI_2024) and open Layer Properties.
2.	Go to the Symbology tab and classify the NDVI values into two classes: 
  - Class 1: Vegetation (NDVI >= threshold value, eg. 0.25).
  - Class 2: No Vegetation (NDVI <= threshold value).
    
## Step 4: Reclassify NDVI Rasters
1.	Use the Reclassify tool (Spatial Analyst Tools > Reclass > Reclassify) to reclassify NDVI values into two categories: 
  - Vegetation (1).
  - No Vegetation (-1).
2.	Save the outputs as Reclass_2020 and Reclass_2024.

## Step 5: Convert Raster to Polygon
1.	Use the Raster to Polygon tool to convert the reclassified rasters to polygons.
2.	Ensure to select the Simplify polygons option for cleaner results.
3.	Save outputs as Poly_2020 and Poly_2024.

## Step 6: Dissolve Polygons
1.	Use the Dissolve tool to simplify polygons based on the Gridcode field.
2.	Save outputs as Dissolve_2020 and Dissolve_2024.

## Step 7: Add Fields for Class and Area
1.	Open the attribute table for the dissolved polygons (Dissolve_2020 and Dissolve_2024).
2.	Add two new fields: 
  - Class: Set values as, *Vegetation for Grid code = 1* and *No Vegetation for Grid code = -1*.
  - Area: Use Calculate Geometry to compute area in square kilometres.

## Step 8: Intersect Polygons
1.	Use the Intersect tool to combine the polygons for 2020 and 2024.
2.	Save the output as Intersect_Polygons.

## Step 9: Add Fields for Change Analysis
1.	Open the attribute table of Intersect_Polygons.
2.	Add two new fields: 
  - Change: Use the Field Calculator to concatenate Class_2020 and Class_2024 (e.g., Vegetation to No Vegetation).
  - Area Change: Use Calculate Geometry to compute the areas.

## Step 10: Visualize Changes
1.	Open the Layer Properties for the intersected polygons.
2.	Under the Symbology tab, select Unique Values. 
  - Use the Change field to display transitions such as: *Vegetation to No Vegetation*, *No Vegetation to Vegetation*, *Vegetation to vegetation*, and *No vegetation to No vegetation*.
3.	Customize the colours and symbology as desired.

## Export data
1.  Open attribute table of Intersect_polygons and select fields of *Vegetation to No Vegetation* and  *No Vegetation to Vegetation* and export data as a new shapefile.
2.  Save output as Change(2020-2024).
3.  Change label of *Vegetation to No Vegetation* to *Deforestation* and *No Vegetation to Vegetation* to *Afforestation*
4.  Customize the colours and symbology as desired.

## Export Map
1.  Insert title, north arrow, legend and scale bar in Layout view and Export map to desired format.

## Results
![Deforest Afforest2](https://github.com/user-attachments/assets/92d6ecb9-ac2f-4cc5-bdc0-81133cd2efbb)

