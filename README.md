# MOHID SOIL TOOL (MST) User Manual

## Version Information
This manual applies to **MOHID SOIL TOOL [versions 2.0.0 and above]**.  <br><br>
The previous version, **MOHID SOIL TOOL [Version 1.0.0]**, is also available for download [here](https://github.com/dhiegosales/MOHID_SOIL_TOOL/releases/tag/v1.0.0).  
The previous version, **MOHID SOIL TOOL [Version 2.0.0]**, is also available for download [here](https://github.com/dhiegosales/MOHID_SOIL_TOOL/releases/tag/v2.0.0).

## Table of Contents
1. [Introduction](#introduction)
2. [Detailed Description of MOHID SOIL TOOL](#detailed-description-of-mohid-soil-tool)
   - [Integration with MOHID-Land](#integration-with-mohid-land)
   - [Main Features and Workflow](#main-features-and-workflow)
3. [System Requirements](#system-requirements)
4. [Installation](#installation)
5. [Download Data from Embrapa](#download-data-from-embrapa)
6. [Program Features](#program-features)
   - [File Processing](#file-processing)
   - [Parameter Calculation](#parameter-calculation)
   - [Multiplication Factor Processing](#multiplication-factor-processing)
   - [File Export](#file-export)
7. [User Interface Overview](#user-interface-overview)
8. [Troubleshooting](#troubleshooting)
9. [Usage Guidelines](#usage-guidelines)
10. [Conclusion](#conclusion)
11. [Citation](#citation)

## Introduction
Welcome to the Soil Analysis Program. This software, known as the MOHID SOIL TOOL (MST), is designed to process soil texture data and estimate hydraulic soil parameters for hydrological modeling. Developed using Python 3, MST features a graphical user interface (GUI) and is compatible with Windows 10/11 x64 operating systems. The executable version of MST can be accessed from the GitHub repository at [MOHID SOIL TOOL](https://github.com/dhiegosales/MOHID_SOIL_TOOL), ensuring accessibility and ease of use. MST was specifically developed to support hydrological studies by providing precise soil parameter inputs required for models like MOHID-Land.


[Back to Top](#mohid-soil-tool-mst-user-manual)

## Detailed Description of MOHID SOIL TOOL

### Integration with MOHID-Land
MOHID-Land is a hydrological modeling system utilizing the finite volume method to solve mass and momentum conservation equations. It includes horizontal and vertical discretization, drainage network derivation from elevation data, and uses Darcy's Law and Richards Equation for water movement calculations. MOHID-Land requires soil hydraulic parameters (such as Ksat, θs, θr, α, and n) estimated from soil attributes using pedotransfer functions like Rosetta's. MST calculates these parameters and formats them for seamless integration into MOHID-Land.

### Main Features and Workflow
**a) Data Import and Processing**
- **Importing Files:** Users import watershed shapefiles (*.shp) and soil texture rasters (sand, silt, clay, bulk density *.tif). MST allows high-resolution options for Rio de Janeiro or Brazil soil type shapefiles, extending the application nationwide.
- **Processing Input Files:** The tool clips soil type shapefiles using the watershed shapefile as a mask and calculates percentages of sand, silt, clay, and density for each soil polygon within the watershed.

**b) Hydraulic Property Calculation**
- **Utilizing Rosetta API:** MST estimates hydraulic properties using the Rosetta API (compatible with versions 1, 2, or 3) based on EMBRAPA texture data.

**c) VGM Parameter Adjustment**
- **Parameters Calibration:** Users adjust VGM parameters (θr, θs, α, n, Ksat) by multiplying each with a user-defined factor. This feature enhances model sensitivity and reliability across diverse hydrological scenarios.

**d) Data Export**
- **Exporting Files:** MST exports processed data in ASCII format for MOHID-Land, shapefiles with clipped soil types, and Excel spreadsheets containing calculated percentages and parameter values.

### Operational Algorithm
The operational algorithm ensures precise processing from data importation to final export, supporting robust scientific analysis and streamlining workflows for water resource studies.

![MOHID SOIL TOOL Algorithm](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/Algorithm_v.2.0.0_v.3.0.0.png)

[Back to Top](#mohid-soil-tool-mst-user-manual)

## System Requirements
- **Operating System:** Windows 10/11 x64
- **Software Requirements:** Executable available for download, no additional installation required.

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Installation
**Downloading the Executable:**
1. Access the [download link](https://github.com/dhiegosales/MOHID_SOIL_TOOL/releases/download/v3.0.0/MOHID_SOIL_TOOL_version3_0_0.zip).
2. Extract the executable files to a folder of your choice.

**Initial Setup:**
- No software installation is required. Simply run the downloaded file (`MOHID_SOIL_TOOL.exe`).

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Download Data from Embrapa
Open the software and configure paths to shapefiles and rasters according to your data sources. For downloading necessary shapefiles and raster data from Embrapa, use the following links:

- **Shapefiles:**
  - For your watershed, provide the specific shapefile.
  - Soil Type Shapefiles:
    - Use either [Brasil Soil Type](http://geoinfo.cnps.embrapa.br/layers/geonode%3Abrasil_solos_5m_20201104) or [Rio de Janeiro Soil Type](http://geoinfo.cnps.embrapa.br/layers/geonode%3Asolos_lat_long_wgs84) for soil type data.

- **Raster Data:**
  - **Bulk Density:**
    - **Layers:**
      - [0-5cm](http://geoinfo.cnps.embrapa.br/documents/3487)
      - [5-15cm](http://geoinfo.cnps.embrapa.br/documents/3489)
      - [15-30cm](http://geoinfo.cnps.embrapa.br/documents/3491)
      - [30-60cm](http://geoinfo.cnps.embrapa.br/documents/3493)
      - [60-100cm](http://geoinfo.cnps.embrapa.br/documents/3495)
      - [100-200cm](http://geoinfo.cnps.embrapa.br/documents/3497)

  - **Silt:**
    - **Layers:**
      - [0-5cm](http://geoinfo.cnps.embrapa.br/documents/3358)
      - [5-15cm](http://geoinfo.cnps.embrapa.br/documents/3360)
      - [15-30cm](http://geoinfo.cnps.embrapa.br/documents/3362)
      - [30-60cm](http://geoinfo.cnps.embrapa.br/documents/3364)
      - [60-100cm](http://geoinfo.cnps.embrapa.br/documents/3366)
      - [100-200cm](http://geoinfo.cnps.embrapa.br/documents/3368)

  - **Sand:**
    - **Layers:**
      - [0-5cm](http://geoinfo.cnps.embrapa.br/documents/3319)
      - [5-15cm](http://geoinfo.cnps.embrapa.br/documents/3321)
      - [15-30cm](http://geoinfo.cnps.embrapa.br/documents/3323)
      - [30-60cm](http://geoinfo.cnps.embrapa.br/documents/3325)
      - [60-100cm](http://geoinfo.cnps.embrapa.br/documents/3327)
      - [100-200cm](http://geoinfo.cnps.embrapa.br/documents/3329)

  - **Clay:**
    - **Layers:**
      - [0-5cm](http://geoinfo.cnps.embrapa.br/documents/3292)
      - [5-15cm](http://geoinfo.cnps.embrapa.br/documents/3293)
      - [15-30cm](http://geoinfo.cnps.embrapa.br/documents/3294)
      - [30-60cm](http://geoinfo.cnps.embrapa.br/documents/3295)
      - [60-100cm](http://geoinfo.cnps.embrapa.br/documents/3296)
      - [100-200cm](http://geoinfo.cnps.embrapa.br/documents/3297)

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Program Features

### File Processing
- **Processing Shapefiles:**
  - The program reads and processes shapefiles for soil data.
  - Performs reprojection of shapefiles to EPSG:5880.
  - Clips soil maps based on user-defined watershed boundaries.
  - Dissolves soil types within the watershed.
  - Supports both Rio de Janeiro and Brazil Soil Type shapefiles available from Embrapa.

- **Processing Rasters:**
  - The program reads rasters for sand, silt, clay, and bulk density.
  - Extracts values based on the shapefiles.

### Parameter Calculation
- **Using Rosetta API:**
  - MST calculates hydraulic parameters like Ksat, θs, θr, α, and n from soil texture data using the Rosetta API.
  - Users can select Rosetta versions 1, 2, or 3 for calculations.

- **Choosing Statistics:**
  - Users can choose to calculate the mean, median, maximum, or minimum values for soil texture and density for each horizon.

### Multiplication Factor Processing
- **Adjusting Parameters:**
  - Users can adjust the VGM parameters by applying multiplication factors to θr, θs, α, n, and Ksat, enhancing model customization.

### Soil Texture Classification
- **New in Version 3.0.0:**
  - Soil texture classification is now integrated, allowing the program to automatically determine the texture class of each soil in the watershed.
  - The classification results are included in both the Excel report and the attributes table of the exported Shapefile, providing better soil data analysis.

- **Soil Texture Triangle:**
  Below is the soil texture triangle used in the program for classification:

  ![Soil Texture Triangle](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/Textural_Triangle_for_Soil_Classification.png)

### File Export
- **Export Options:**
  - MST allows exporting the results as shapefiles, Excel spreadsheets, or ASCII files compatible with MOHID-Land.
  - Results include clipped soil type shapefiles, calculated parameter values, and formatted ASCII files.

[Back to Top](#mohid-soil-tool-mst-user-manual)


## User Interface Overview
The MST interface is divided into several sections and contains numerous buttons and options, enabling step-by-step progress through the data processing workflow.

![MST GUI](https://github.com/dhiegosales/MOHID_SOIL_TOOL/blob/main/GUI.png)

**Menus and Options:**

- **Import Files:** Users can browse and load their watershed and soil type shapefiles, as well as select the horizons for data processing (1 to 6 horizons).
- **Process Files:** Options for clustering raster data into each soil type polygon using mean, median, max, or min statistics are available.
- **Rosetta API:** Users can select the version of Rosetta to be used for hydraulic parameter estimation.
- **Multiply Factor for Calibration:** Fields to adjust each VGM parameter are provided.
- **Export Files:** Users can specify the file name and directory for export, along with the output file format (shapefile, excel report, MOHID ASCII).

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Troubleshooting
- Ensure all required files (shapefiles and rasters) are correctly specified and accessible.
- Verify that the correct Rosetta version is selected and that the API is functioning.
- If calculations seem incorrect, check the multiplication factors and chosen statistics.

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Usage Guidelines
- Always start by importing the watershed shapefile and corresponding soil type shapefiles.
- Follow the process step-by-step: import files, process data, calculate parameters, adjust factors, and export results.
- Regularly update the software from the GitHub repository to ensure compatibility and access to new features.

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Conclusion
MOHID SOIL TOOL (MST) Versions 2.0.0 and 3.0.0 provide a robust solution for estimating soil hydraulic parameters essential for hydrological modeling using MOHID-Land. Its user-friendly interface, comprehensive data processing capabilities, and integration with Rosetta API ensure accurate parameterization for varied hydrological conditions.

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Citation
If you use this software, please cite it as follows:

Sales, D. S.; Lugon Junior, J.; Costa, D. A.; Silva Neto, A. J. (2024). MOHID SOIL TOOL - Computational Tool for Determining Soil Water Percolation Parameters (Version 3.0.0) [Computer software]. https://github.com/dhiegosales/MOHID-SOIL-TOOL. Accessed xx xxx xxxx.


For any issues or further assistance, please contact Dhiego da Silva Sales at [dhiego.sales@outlook.com](mailto:dhiego.sales@outlook.com).

[Back to Top](#mohid-soil-tool-mst-user-manual)
