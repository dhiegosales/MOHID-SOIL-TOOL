## Version Information
This manual applies to **MOHID SOIL TOOL [version 4.0.0]**.  <br><br>
The previous manual version, **MOHID SOIL TOOL [Versions 2.0.0 and 3.0.0]**, can be accessed [here](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/v2.0.0_and_v3.0.0_User_Manual.md).  

## Table of Contents
1. [Introduction](#introduction)
2. [System Requirements](#system-requirements)
4. [Installation](#installation)
6. [Detailed Description of MOHID SOIL TOOL](#detailed-description-of-mohid-soil-tool)
   - [Integration with MOHID-Land](#integration-with-mohid-land)
   - [Main Features and Workflow](#main-features-and-workflow)
7. [User Interface Overview](#user-interface-overview)
9. [Troubleshooting](#troubleshooting)
10. [Usage Guidelines](#usage-guidelines)
11. [Field Auto-Filling](#field-auto-filling)
12. [Download Data from Embrapa](#download-data-from-embrapa)
13. [Conclusion](#conclusion)
14. [Citation](#citation)

## Introduction
Welcome to the Soil Analysis Program. This software, known as the MOHID SOIL TOOL (MST), is designed to process soil texture data and estimate hydraulic soil parameters for hydrological modeling. Developed using Python 3, MST features a graphical user interface (GUI) and is compatible with Windows 10/11 x64 operating systems. The executable version of MST can be accessed from the GitHub repository at [MOHID SOIL TOOL](https://github.com/dhiegosales/MOHID_SOIL_TOOL), ensuring accessibility and ease of use. MST was specifically developed to support hydrological studies by providing precise soil parameter inputs required for models like MOHID-Land.

[Back to Top](#table-of-contents)


## System Requirements
- **Operating System:** Windows 10/11 x64
- **Software Requirements:** Executable available for download, no additional installation required.

[Back to Top](#table-of-contents)

## Installation
**Downloading the Executable:**
1. Access the [download link](https://github.com/dhiegosales/MOHID-SOIL-TOOL/releases/download/v4.0.0/MOHID_SOIL_TOOL_version4_0_0.zip).
2. Extract the executable files to a folder of your choice.

**Initial Setup:**
- No software installation is required. Simply run the downloaded file (`MOHID_SOIL_TOOL.exe`).

[Back to Top](#table-of-contents)

## Detailed Description of MOHID SOIL TOOL

### Integration with MOHID-Land
MOHID-Land is a hydrological modeling system utilizing the finite volume method to solve mass and momentum conservation equations. It includes horizontal and vertical discretization, drainage network derivation from elevation data, and uses Darcy's Law and Richards Equation for water movement calculations. MOHID-Land requires soil hydraulic parameters (such as Ksat, θs, θr, α, and n) estimated from soil attributes using pedotransfer functions like Rosetta's. MST calculates these parameters and formats them for seamless integration into MOHID-Land.

### Main Features and Workflow
**a) Data Import**
- **Importing Files:** Users import watershed shapefiles (*.shp) and soil texture rasters (sand, silt, clay, bulk density *.tif).
   - Watershed shapefile: user study area
   - Soil type map:
      - MOHID GRID: The user can provide the path to the .dat file generated by MOHID-Land for the project's topography. Note that large grid domains may result in long processing times, possibly hours.
      - USER: The user can import their own shapefile containing soil type polygons. In this case, the user must specify the column in the 'Attribute Table' that contains the soil type data.
      - EMBRAPA: MST allows high-resolution options for Rio de Janeiro or Brazil soil type shapefiles, extending the application nationwide. If the user’s study area is not fully contained within the Rio de Janeiro map, the Brazil map should be used.
   - Horizon rasters: the user can load up to 6 Embrapa horizon files, including:
      - Brazil sand raster (provided by Embrapa)
      - Brazil silt raster (provided by Embrapa)
      - Brazil clay raster (provided by Embrapa)
      - Density raster (provided by Embrapa)
        
**b) Processing Input Files:** The tool clips soil type shapefiles using the watershed shapefile as a mask and calculates percentages of sand, silt, clay, and density for each soil polygon within the watershed folowuing these steps:
   - Processing Shapefiles:
     - The program reads and processes shapefiles for soil data.
     - Performs reprojection of shapefiles to EPSG:5880.
     - Clips soil maps based on user-defined watershed boundaries.
     - Dissolves soil types within the watershed. If MOHID grid, it is not performed.
   - Processing raster:
      - Extract quantitative data for each soil property: sand, silt, clay, and density using clipped shapefile. The raster data is clustering by mean, median, max or min statistics.
      - Sum sand, silt and clay.
      - Calculating the percentage of sand, silt and clay.
      - Soil Texture Classification:
         - Soil texture classification is now integrated, allowing the program to automatically determine the texture class of each soil in the watershed.
         - The classification results are included in both the Excel report and the attributes table of the exported Shapefile, providing better soil data analysis.
         - **Soil Texture Triangle:** Below is the soil texture triangle used in the program for classification:

  ![Soil Texture Triangle](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/Textural_Triangle_for_Soil_Classification.png)
           
**c) Soil Compaction Assessment:** 

This module aims to simulate soil compaction, a crucial process that influences various physical and chemical properties of the soil, such as its density, porosity, and water retention capacity. The simulation is conducted by reading data from a table that contains information about the soil and assigning a 'Density Multiplier' that represents the desired level of compaction.

Upon initiating the simulation, the system reads the table and sets a default value of 1 for the 'Density Multiplier,' indicating no compaction. This value can be adjusted based on the specific conditions of the soil being modeled. After reading the data, applying the multiplier allows the system to calculate the new density of the soil, reflecting the effects of compaction. This step is essential, as variations in density simulate the impact of compaction, which can influence soil permeability, nutrient availability, and structural stability in engineering projects.

**d) Rosetta Hydraulic Parameter Estiamtion:** Utilizing Rosetta API, MST estimates hydraulic properties using the Rosetta API (compatible with versions 1, 2, or 3) based on EMBRAPA texture data.

**e) Rosetta Hydraulic Parameters Calibration:** Users adjust VGM parameters (θr, θs, α, n, Ksat) by multiplying each with a user-defined factor. This feature enhances model sensitivity and reliability across diverse hydrological scenarios.

**f) Data Export**
- **Exporting Files:** MST exports processed data in ASCII format for MOHID-Land, shapefiles with clipped soil types, and Excel spreadsheets containing calculated percentages and parameter values.

### Operational Algorithm
The operational algorithm ensures precise processing from data importation to final export, supporting robust scientific analysis and streamlining workflows for water resource studies.

![image](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/v.4.0.0_Algorithm.jpg?raw=true)

[Back to Top](#table-of-contents)

## User Interface Overview
The MST interface is divided into several sections and contains numerous buttons and options, enabling step-by-step progress through the data processing workflow.

![MST GUI](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/v4.0.0_GUI.png)

**Menus and Options:**
- **Help:** A help menu is available with a 'Instructions', 'Troblueshooting' and  'About' option to assist user in MOHID Soil Tool using.
- **Import Files:** Users can browse and load their watershed and soil type shapefiles, as well as select the horizons for data processing (1 to 6 horizons). A Help menu is available to assist user to provide Soil type map from differents sources. For each horizon there is a specific window to get paths.
- **Process Files:** Options for clustering raster data into each soil type polygon using mean, median, max, or min statistics are available. A radio button is available for chosing these statistics.
- **Soil Compaction Assesment:** A Help menu is available to assist user to simulate compaction. This block have two buttons:<br>
   - Read Table:
      - This button is used to read the data from the table and assign a value to the 'Density Multiplier' field for simulating compaction.
      - The default compaction field is set to 1, which represents 'no compaction.
      - Click this button to start reading the table and applying the corresponding values.
      - **IMPORTANT: Once the 'Read Table' button is enabled, you can consult the results table at each subsequent step as the other functions are performed. This allows you to see the changes in real-time***.
   - Multiply:
      - After reading the table, use this button to multiply the density factor values by the value that was previously assigned.
      - Attention: You only need to click this button if there are changes in the compaction field. If there are no changes in the table, there is no need to click 'Multiply'.
      - This step is important to calculate the new density considering the desired compaction.
      - Click this button after reading the table to perform the necessary calculations.
- **Rosetta Hydraulic Soil Parameter Estiamtion:** A radio button is available for Users select the version of Rosetta to be used for hydraulic parameter calculation. Than the 'calculate' button is resonsable for consulting ROsetta API in order to calculate hydraulic paramteres.
- **Roseta Hydraulic Parameters Calibration:** Fields to adjust each VGM parameter are provided. Then a 'Multiply' buttun is available to perfirme the multiplying operation.
- **Export Files:** Users can specify the file name and browse directory for export, along with the output file format (shapefile, excel report, MOHID ASCII).

[Back to Top](#table-of-contents)


## Troubleshooting
- If the program closes unexpectedly or freezes, please check the following:<br>
a) Ensure that the input file names are correct.<br>
b) Verify that none of the input files are corrupted (we recommend testing all files in a GIS software like QGIS).<br>
c) Ensure no file in the export directory is not open with the same name as the one you are trying to save.<br><br>
If so, close the file before saving again. If the program fails to open, check the following:<br>
a) Make sure your antivirus is not blocking the program. If necessary, disable the antivirus while running the MOHID SOIL TOOL.<br><br>
If the exported shapefile is only partially filled (incorrect size), verify the following:<br>
a) Ensure that the user-provided shapefile (study area) is fully contained within the provided soil type map shapefile.<br><br>

[Back to Top](#table-of-contents)

## Usage Guidelines
- Always start by importing the watershed shapefile and corresponding soil type shapefiles.
- Follow the process step-by-step: import files, process data, calculate parameters, adjust factors, and export results.
- Regularly update the software from the GitHub repository to ensure compatibility and access to new features.

[Back to Top](#table-of-contents)


## Field Auto-Filling

### Description
This function is designed to automatically fill the fields in graphical user interface (GUI) windows based on the last execution of the program. If the `inputFileNames.txt` file is not found in the current directory, the fields are initialized as empty or with default values. If the file exists, the values contained within it are read and used to populate the corresponding fields in the interface.

This approach facilitates the continuity of work, allowing parameters and files used in the previous execution to be automatically reused.

#### Function Logic
1. **File Existence Check**: The program checks if the `inputFileNames.txt` file exists in the current directory.
2. **Field Initialization**: If the file is not found, the fields are initialized as empty or with default values.
3. **Reading Values**: If the file is found, its values are read and used to fill the GUI fields.
4. **Parameters**: The filled parameters include input file paths (such as shapefiles or other necessary data), and user configurations from the previous execution.
5. **File Update/Creation**: Every time the program closes, this file is updated if it exists or created in the executable folder if not already present.

[Back to Top](#table-of-contents)

## Download Data from Embrapa
Open the software and configure paths to shapefiles and rasters according to your data sources. For downloading necessary shapefiles and raster data from Embrapa, use the following links:

- [GEOINFO EMBRAPA](https://geoinfo.dados.embrapa.br/#/)

**Note:** These are external links to the official Embrapa website. They may eventually stop functioning if the site structure changes. Please verify if the Embrapa website is operational and if the links have changed their address before attempting to download the data.

- **Shapefiles:**
  - Soil Type Shapefiles:
    - Use either [Brasil Soil Type](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/1688) or [Rio de Janeiro Soil Type](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/4762) for soil type data.

- **Raster Data:**
  - **Bulk Density:**
    - **Layers:**
      - [0-5cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2959)
      - [5-15cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2961)
      - [15-30cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2969)
      - [30-60cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2972)
      - [60-100cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2974)
      - [100-200cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2975)

  - **Silt:**
    - **Layers:**
      - [0-5cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2751)
      - [5-15cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2787)
      - [15-30cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2756)
      - [30-60cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2795)
      - [60-100cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2796)
      - [100-200cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2797)

  - **Sand:**
    - **Layers:**
      - [0-5cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2610)
      - [5-15cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2611)
      - [15-30cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2612)
      - [30-60cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2613)
      - [60-100cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2638)
      - [100-200cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2639)

  - **Clay:**
    - **Layers:**
      - [0-5cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2708)
      - [5-15cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2709)
      - [15-30cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2711)
      - [30-60cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2724)
      - [60-100cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2739)
      - [100-200cm](https://geoinfo.dados.embrapa.br/catalogue/#/dataset/2740)

[Back to Top](#table-of-contents)

## Conclusion
MOHID SOIL TOOL (MST) Version 4.0.0 offers a comprehensive solution for calculating and adjusting soil hydraulic parameters, a crucial step in hydrological modeling using MOHID-Land. It can also simulate compaction conditions by modifying density values. Its intuitive interface, robust data processing capabilities, and seamless integration with the Rosetta API ensure accurate parameterization for diverse hydrological scenarios.

[Back to Top](#table-of-contents)

## Citation
If you use this software, please cite it as follows:

Sales, D. S.; Lugon Junior, J.; Costa, D. A.; Silva Neto, A. J. (2024). MOHID SOIL TOOL - Computational Tool for Determining Soil Water Percolation Parameters (Version 4.0.0) [Computer software]. https://github.com/dhiegosales/MOHID-SOIL-TOOL. Accessed xx xxx xxxx.

For any issues or further assistance, please contact Dhiego da Silva Sales at [dhiego.sales@outlook.com](mailto:dhiego.sales@outlook.com).

[Back to Top](#table-of-contents)
