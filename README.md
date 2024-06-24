# MOHID SOIL TOOL (MST) User Manual

## Table of Contents
1. [Introduction](#introduction)
2. [Detailed Description of MOHID SOIL TOOL](#detailed-description-of-mohid-soil-tool)
3. [System Requirements](#system-requirements)
4. [Installation](#installation)
5. [Setting File Paths](#setting-file-paths)
6. [Download Data from Embrapa](#download-data-from-embrapa)
7. [Program Features](#program-features)
   - [File Processing](#file-processing)
   - [Parameter Calculation](#parameter-calculation)
   - [Multiplication Factor Processing](#multiplication-factor-processing)
   - [File Export](#file-export)
8. [User Interface Overview](#user-interface-overview)
9. [Troubleshooting](#troubleshooting)
10. [Usage Guidelines](#usage-guidelines)
11. [Conclusion](#conclusion)

## Introduction
Welcome to the Soil Analysis Program. This software, known as the MOHID SOIL TOOL (MST), is designed to process soil texture data and estimate hydraulic soil parameters for hydrological modeling. Developed using Python 3, MST features a graphical user interface (GUI) and is compatible with Windows 10/11 x64 operating systems. The executable version of MST can be accessed from the GitHub repository at [MOHID SOIL TOOL](https://github.com/dhiegosales/MOHID_SOIL_TOOL), ensuring accessibility and ease of use. MST was specifically developed to support hydrological studies by providing precise soil parameter inputs required for models like MOHID-Land (Sales et al., 2024).


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

![MOHID SOIL TOOL Algorithm](https://github.com/dhiegosales/MOHID_SOIL_TOOL/blob/main/Algorithm_v.2.0.0.png)

[Back to Top](#mohid-soil-tool-mst-user-manual)

## System Requirements
- **Operating System:** Windows 10/11 x64
- **Software Requirements:** Executable available for download, no additional installation required.

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Installation
**Downloading the Executable:**
1. Access the [download link](https://github.com/dhiegosales/MOHID_SOIL_TOOL/releases/download/v2.0.0/MOHID_SOIL_TOOL_version2_0_0.zip).
2. Extract the executable files to a folder of your choice.

**Initial Setup:**
- No software installation is required. Simply run the downloaded file (`MOHID_SOIL_TOOL.exe`).

[Back to Top](#mohid-soil-tool-mst-user-manual)

## Setting File Paths
Open the software and configure paths to shapefiles and rasters according to your data sources. For downloading necessary shapefiles and raster data from Embrapa, use the following links:

- **Shapefiles:**
  - For your watershed, provide the specific shapefile.
  - Soil Type Shapefiles:
    - Use either [Brasil Soil Type](http://geoinfo.cnps.embrapa.br/layers/geonode%3Abrasil_solos_5m_20201104) or [Rio de Janeiro Soil Type](http://geoinfo.cnps.embrapa.br/layers/geonode%3Asolos_lat_long_wgs84) for soil type data.

- **Raster Data:**
  - **Bulk Density:**
    - [Download Raster Data](http://geoinfo.cnps.embrapa.br/maps/3499)
    - **Layers:**
      - [0-5cm](http://geoinfo.cnps.embrapa.br/documents/3487)
      - [5-15cm](http://geoinfo.cnps.embrapa.br/documents/3489)
      - [15-30cm](http://geoinfo.cnps.embrapa.br/documents/3491)
      - [30-60cm](http://geoinfo.cnps.embrapa.br/documents/3493)
      - [60-100cm](http://geoinfo.cnps.embrapa.br/documents/3495)
      - [100-200cm](http://geoinfo.cnps.embrapa.br/documents/3497)

  - **Silt:**
    - [Download Raster Data](http://geoinfo.cnps.embrapa.br/maps/3370)
    - **Layers:**
      - [0-5cm](http://geoinfo.cnps.embrapa.br/documents/3358)
      - [5-15cm](http://geoinfo.cnps.embrapa.br/documents/3360)
      - [15-30cm](http://geoinfo.cnps.embrapa.br/documents/3362)
      - [30-60cm](http://geoinfo.cnps.embrapa.br/documents/3364)
      - [60-100cm](http://geoinfo.cnps.embrapa.br/documents/3366)
      - [100-200cm](http://geoinfo.cnps.embrapa.br/documents/3368)

  - **Sand:**
    - [Download Raster Data](http://geoinfo.cnps.embrapa.br/maps/3291)
    - **Layers:**
      - [0-5cm](http://geoinfo.cnps.embrapa.br/documents/3319)
      - [5-15cm](http://geoinfo.cnps.embrapa.br/documents/3321)
      - [15-30cm](http://geoinfo.cnps.embrapa.br/documents/3323)
      - [30-60cm](http://geoinfo.cnps.embrapa.br/documents/3325)
      - [60-100cm](http://geoinfo.cnps.embrapa.br/documents/3327)
      - [100-200cm](http://geoinfo.cnps.embrapa.br/documents/3329)

  - **Clay:**
    - [Download Raster Data](http://geoinfo.cnps.embrapa.br/maps/3290)
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
The MOHID SOIL TOOL is a powerful utility for hydrological studies, providing accurate soil parameter calculations necessary for advanced modeling. By following this manual, users can efficiently operate the tool and enhance their hydrological analysis.

For any issues or further assistance, please contact Dhiego da Silva Sales at [dhiego.sales@outlook.com](mailto:dhiego.sales@outlook.com).

[Back to Top](#mohid-soil-tool-mst-user-manual)
