# Creating an NDVI Map of Kwahu South District in ArcGIS

1.	Download Required Data:
- Kwahu South District Shapefile: The shapefile was obtained by clipping the district polygon from Ghana's administrative shapefile dataset at [GADM](https://gadm.org/download_country.html).
-	Sentinel-2 Image Data: Download Bands 4 (Red) and 8 (Near-Infrared) image data of the study area from the [Copernicus Data Space Browser](https://browser.dataspace.copernicus.eu/).

2.	Open ArcMap and Set Workspace:
-	Launch ArcMap and choose a blank workspace.
-	Set your workspace environment to a folder where your files are stored.

3.	Import Data:
-	Add the Kwahu South District shapefile to your workspace using the "Add Data" button.
-	Import Sentinel-2 Band 4 and Band 8 image files in GeoTIFF format.

4.	Perform NDVI Calculation:
-	Open the Raster Calculator from the Spatial Analyst Tools toolbox.
-	Use the formula for NDVI: NDVI = Float(Band 8 - Band 4) / Float(Band 8 + Band 4)
-	This calculates the NDVI values for the entire Sentinel-2 image.

5.	Extract NDVI for Kwahu South District:
-	Use the Extract by Mask tool in the Spatial Analyst Tools toolbox.
-	Input the NDVI layer as the raster and the Kwahu South District shapefile as the mask layer.
-	The output will be the NDVI clipped to the boundaries of the Kwahu South District.

6.	Classify NDVI Values:
-	In the Table of Contents, right-click the extracted NDVI layer and select Properties.
-	Navigate to the Symbology tab.
-	Select Classified and choose to classify the NDVI into six classes.
-	Adjust the Color Ramp to reflect vegetation health.

7.	Label the Classes:
-	Modify the labels for each class to represent the NDVI ranges.
-	Apply the changes.

8.	Export the NDVI Map:
-	Use the Export Map option to save the final NDVI map as an image or PDF.

Tips:
-	Ensure all data are in the same coordinate system before analysis.
-	Preprocess the Sentinel-2 images to remove clouds if necessary.
-	Use descriptive file names for outputs to maintain organization.


# Results
![Kwahu South](https://github.com/user-attachments/assets/5c5c6324-1036-4482-a8f8-8724f5e2679d)

