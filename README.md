## Version Information
This manual applies to **MOHID SOIL TOOL [version 4.0.0 or above]**.  <br><br>
The previous manual version, **MOHID SOIL TOOL [Versions 2.0.0 and 3.0.0]**, can be accessed [here](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/v2.0.0_and_v3.0.0_User_Manual.md).  

## Table of Contents
1. [Presentation](#presentation)
2. [Introduction](#introduction)
3. [System Requirements](#system-requirements)
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
14. [References](#references)
15. [Citation](#citation)

## Presentation
Welcome to the Soil Analysis Program. This software, known as the MOHID SOIL TOOL (MST), is designed to process soil texture data and estimate hydraulic soil parameters for hydrological modeling. Developed using Python 3, MST features a graphical user interface (GUI) and is compatible with Windows 10/11 x64 operating systems. The executable version of MST can be accessed from the GitHub repository at [MOHID SOIL TOOL](https://github.com/dhiegosales/MOHID_SOIL_TOOL), ensuring accessibility and ease of use. MST was specifically developed to support hydrological studies by providing precise soil parameter inputs required for models like MOHID-Land.

[Back to Top](#table-of-contents)

## Introduction
MOHID Land is an open-source hydrological model, programmed in Fortran, based on physical principles, spatially distributed, and capable of simulating the various phases of the hydrological cycle. The partial differential equations for mass conservation are solved using the finite volume approach, where each cell has a defined volume, all its properties are homogeneous within, and the velocities are homogeneous on the faces of the volume [1].

The soil is discretized in a 3D domain, where the upper boundary is the topography, and the lower boundary is defined by the user. Between these boundaries, the soil is defined in vertical horizons, which may have different hydraulic properties and thicknesses. MOHID Land calculates soil water retention using the van Genuchten model, which depends on the following hydraulic properties: 𝜃𝑠, the saturated water content; 𝜃𝑟, the residual water content; 𝛼, related to the inverse of the air entry pressure; 𝑛, a measure of pore size distribution; and 𝐾𝑠𝑎𝑡, the saturated hydraulic conductivity [2].

Establishing the values for all these hydraulic properties for each soil type within a watershed and for each defined horizon is a labor-intensive task that requires research and technical expertise from the modeler, making it a significant challenge in hydrological modeling. Given the complexity of obtaining soil hydraulic properties, the Artificial Neural Network-based model Rosetta was developed [3, 4, 5]. This model uses more easily obtainable physical parameters to estimate the soil's hydraulic properties, such as the percentages of sand, silt, and clay; soil bulk density; volumetric water content at 33 kPa; and volumetric water content at 1500 kPa. It features a web interface [6], an R API [7], and a Python API [8].

The Brazilian Agricultural Research Corporation (EMBRAPA) is responsible for mapping the soil types across the country and their various properties, providing several geospatial products in raster and shapefile formats for download on the portal http://geoinfo.dados.embrapa.br. The input parameters for the Rosetta model (sand, clay, silt, and bulk density) are estimated by EMBRAPA from nationwide sampling, then interpolated using statistical procedures and spatialized into 90m resolution pixels at various depths (0-5, 5-15, 15-30, 30-60, 60-100, and 100-200 cm) [9, 10].

Through exhaustive geoprocessing procedures, data on sand, silt, clay, and bulk density can be extracted from EMBRAPA's products for each soil type, input into one of the Rosetta versions, and used to create ASCII files, which are then implemented in MOHID Land. Given the time-consuming, repetitive, and exhaustive nature of data processing and file creation for MOHID Land, the application of the MOHID SOIL TOOL is fully justified.

The MOHID SOIL TOOL is a Windows 10/11 x64-based graphical interface tool developed in Python 3, designed to streamline the preparation of data for the MOHID Land hydrological model. It follows a comprehensive process, starting with the import and preprocessing of soil physical parameters provided by EMBRAPA. The tool then simulates soil compaction and calculates the hydraulic properties for each soil type within the user's watershed using the Rosetta-soil Python API. Additionally, it adjusts Van Genuchten-Mualem (VGM) parameters and constructs the necessary ASCII input files for the MOHID Land model, along with any accessory files. This approach makes the entire process more efficient and intuitive, significantly saving time in the development of hydrological models.

[Back to Top](#table-of-contents)

## System Requirements
- **Operating System:** Windows 10/11 x64
- **Software Requirements:** Executable available for download, no additional installation required.

[Back to Top](#table-of-contents)

## Installation
**Downloading the Executable:**
1. Access the [download link](https://github.com/dhiegosales/MOHID-SOIL-TOOL/releases/download/v4.1.0/MOHID_SOIL_TOOL_version4_1_0.zip).
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
   - Layers raster: the user can load up to 6 Embrapa layer files, including:
      - Brazil sand raster (provided by Embrapa)
      - Brazil silt raster (provided by Embrapa)
      - Brazil clay raster (provided by Embrapa)
      - Density raster (provided by Embrapa)
   - *The tool is versatile and flexible, allowing the incorporation of any available raster data from both global and local sources into the study.
        
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

![image](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/v4.0.1_and_above_Algorithm.jpg)

[Back to Top](#table-of-contents)

## User Interface Overview
The MST interface is divided into several sections and contains numerous buttons and options, enabling step-by-step progress through the data processing workflow.

![MST GUI](https://github.com/dhiegosales/MOHID-SOIL-TOOL/blob/main/v4.0.1_and_above_GUI.png)

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

Alternatively, the input data and the results obtained by the MOHID Soil Tool (MST) can be accessed in the dataset created by da Silva Sales, D. (2025): Supplementary Soil Dataset for Enhancing River Flow Predictions in MOHID-Land Through Integration of Gridded Soil Data and Hydraulic Parameters Using the MOHID Soil Tool (1.1.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.14914611. This dataset incorporates soil data from EMBRAPA, which were used in the paper "Enhancing River Flow Predictions in MOHID-Land Through Integration of Gridded Soil Data and Hydraulic Parameters Using the MOHID Soil Tool."

[Back to Top](#table-of-contents)

## Conclusion
MOHID SOIL TOOL (MST) Version 4.0.0 and above offers a comprehensive solution for calculating and adjusting soil hydraulic parameters, a crucial step in hydrological modeling using MOHID-Land. It can also simulate compaction conditions by modifying density values. Its intuitive interface, robust data processing capabilities, and seamless integration with the Rosetta API ensure accurate parameterization for diverse hydrological scenarios.

[Back to Top](#table-of-contents)

## References
[1] Mohid wiki (2023). Equations in Mohid Land. Disponível em: 
<http://wiki.mohid.com/index.php?title=Equations_in_Mohid_Land>. Acesso em 04 
de setembro de 2023.

[2] Mohid wiki (2023). Module Porous Media. Disponível em: 
<http://wiki.mohid.com/index.php?title=Module_PorousMedia>. Acesso em 04 de 
setembro de 2023.

[3] M. G. Schaap, F. J. Leij and M.T. Van Genuchten. 2001. ROSETTA: a computer 
program for estimating soil hydraulic parameters with hierarchical pedotransfer 
functions. Journal of Hydrology 251(3-4): 163-176. doi: 10.1016/S0022-
1694(01)00466-8

[4] M. G. Schaap, A. Nemes, and M.T. van Genuchten. 2004. Comparison of Models 
for Indirect Estimation of Water Retention and Available Water in Surface Soils. 
Vadose Zone Journal 3(4): 1455-1463. doi: 10.2136/vzj2004.1455

[5] Y. Zhang and M. G. Schaap. 2017. Weighted recalibration of the Rosetta 
pedotransfer model with improved estimates of hydraulic parameter distributions and 
summary statistics (Rosetta3). Journal of Hydrology 547: 39-53. 
doi: 10.1016/j.jhydrol.2017.01.004

[6] Rosetta 2023. Estimate unsaturated soil hydraulic parameters from soil 
characterization data. Disponível em: < https://www.handbook60.org/rosetta/>. 
Acesso em 05 de setembro de 2023.

[7] D. Beaudette, R. Reid and T. Skaggs. 2022. ROSETTA Model API. Disponível 
em: < http://ncss-tech.github.io/AQP/soilDB/ROSETTA-API.html>. Acesso em 05 de 
setembro de 2023.

[8] M. Schaap and Y. Zhang. 2016. Implementação do modelo de função de 
pedotransferência Rosetta para previsão de parâmetros hidráulicos de solos não 
saturados. Disponível em: <https://github.com/usda-ars-ussl/rosetta-soil>. Acesso 
em 05 de setembro de 2023.

[9] G. M. Vasques, M. R. Coelho, R. O. Dart, L. C. Cintra, and J. F. M. Baca. Soil 
Clay, Silt and Sand Content Maps for Brazil at 0-5, 5-15, 15-30, 30-60, 60-100 and 
100-200 cm Depth Intervals with 90 m Spatial Resolution, Embrapa Solos, Rio de 
Janeiro, Brazil, 2021.

[10] G. M. Vasques, M. R. Coelho, R. O. Dart, L. C. Cintra, and J. F. M. Baca. Soil 
Bulk Density Maps for Brazil at 0-5, 5-15, 15-30, 30-60, 60-100 and 100-200 cm 
Depth Intervals with 90 m Spatial Resolution, Embrapa Solos, Rio de Janeiro, Brazil, 
2021.

[Back to Top](#table-of-contents)
## Citation
If you use this software, please cite it as follows:

Sales, D. S.; Lugon Junior, J.; Costa, D. A.; Silva Neto, A. J. (2024). MOHID SOIL TOOL - Computational Tool for Determining Soil Water Percolation Parameters (Version 4.1.0) [Computer software]. https://github.com/dhiegosales/MOHID-SOIL-TOOL. Accessed xx xxx xxxx.

For any issues or further assistance, please contact Dhiego da Silva Sales at [dhiego.sales@outlook.com](mailto:dhiego.sales@outlook.com).

[Back to Top](#table-of-contents)
