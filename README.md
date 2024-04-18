# MOHID_SOIL_TOOL
Processing tool for EMBRAPA soil texture raster and determination of van Genuchten parameters

  MOHID Land is an open source hydrological model, programmed in Fortran, physically based, spatially distributed and able to modeling all different phases of the hydrological cycle. The partial differential equations of conservation of mass and momentum are solved using the finite volume approach, where all properties are calculated inside the volume and the velocities are calculated in the faces [1].
  
  The soil is discretized in a 3D domain, where its upper limit is the topography and the lower limit is defined by the user. Between these limits the soil is defined in vertical horizons, which may have different hydraulic characteristics and thicknesses. MOHID Land calculates water retention in the soil according to the van Genuchten-Mualem model, which depends on the following hydraulic properties: θs which is the saturated water content; θr which is the residual water content; α which is related to the inverse of the air intake; n is a measure of pore size distribution; and Ksat is the saturated conductivity [2].
  
  Establishing the values of all the hydraulic properties described above, for each type of soil included in a watershed and for each defined horizon is a costly task, which demands research and technical knowledge from the modeler, thus constituting a challenge for hydrological modeling. Considering the complexity in obtaining soil hydraulic properties, the model based on Artificial Neural Networks, Rosetta, was developed [3, 4, 5]. This model uses physical parameters that are easier to obtain, in order to estimate the hydraulic properties of the soil: percentages of sand, silt and clay; apparent soil density; volumetric soil water content at 33 kPa; and volumetric soil water content at 1500 kPa,. The Rosetta has a web interface [6], API in R [7] and API in Python [8].
  
  The Brazilian Agricultural Research Corporation (EMBRAPA) is responsible for mapping the types of soil present in the national territory and in different properties, making several raster and shapefile geospatial products available for download on the portal http://geoinfo.cnps.embrapa.br /maps/. Thus, the input parameters of the Rosetta model (sand, clay, silt and density) are estimated by EMBRAPA from sampling throughout the national territory, and are then interpolated through statistical procedures and spatialized in 90m pixels, at different depths (0 -5, 5-15, 15-30, 30-60, 60-100 and 100-200 cm) [9, 10].
  
  So, through exhaustive geoprocessing procedures, for each type of soil, it is possible to extract data on sand, silt, clay and soil density from EMBRAPA products, insert them into one of the Rosetta versions, and finally build the ASCII files, which will effectively be implemented in MOHID Land. In this context of time-consuming, repetitive and exhaustive data processing procedures and construction of MOHID Land files, the MOHID SOIL TOOL application is justified.
  
  Therefore, MOHID SOIL TOOL can be described as a tool developed for the Windows 10/11 x64 operating system, with a graphical interface, functions programmed in the Python 3 language and which has the purpose of: (i) importing and processing the testural parameters of the soil, made available by EMBRAPA; (ii) calculate the hydraulic properties for each type of soil present in the user's watershed, via the rosetta-soil API in Python; (iii) build and export the input ASCII file for the MOHID Land hydrological model, in addition to accessory files. This tool aims to make the processing and preparation of input data for MOHID Land more agile and intuitive, saving time in the development of the hydrological model.



Referências

[1] Mohid wiki (2023). Equations in Mohid Land. Disponível em: <http://wiki.mohid.com/index.php?title=Equations_in_Mohid_Land>. Acesso em 04 de setembro de 2023.

[2] Mohid wiki (2023). Module Porous Media. Disponível em: <http://wiki.mohid.com/index.php?title=Module_PorousMedia>. Acesso em 04 de setembro de 2023.

[3] M. G. Schaap, F. J. Leij and M.T. Van Genuchten. 2001. ROSETTA: a computer program for estimating soil hydraulic parameters with hierarchical pedotransfer functions. Journal of Hydrology 251(3-4): 163-176. doi: 10.1016/S0022-1694(01)00466-8

[4] M. G. Schaap, A. Nemes, and M.T. van Genuchten. 2004. Comparison of Models for Indirect Estimation of Water Retention and Available Water in Surface Soils. Vadose Zone Journal 3(4): 1455-1463. doi: 10.2136/vzj2004.1455

[5] Y. Zhang and M. G. Schaap. 2017. Weighted recalibration of the Rosetta pedotransfer model with improved estimates of hydraulic parameter distributions and summary statistics (Rosetta3). Journal of Hydrology 547: 39-53. doi: 10.1016/j.jhydrol.2017.01.004

[6] Rosetta 2023. Estimate unsaturated soil hydraulic parameters from soil characterization data. Disponível em: < https://www.handbook60.org/rosetta/>. Acesso em 05 de setembro de 2023.

[7] D. Beaudette, R. Reid and T. Skaggs. 2022. ROSETTA Model API. Disponível em: < http://ncss-tech.github.io/AQP/soilDB/ROSETTA-API.html>. Acesso em 05 de setembro de 2023.

[8] M. Schaap and Y. Zhang. 2016. Implementação do modelo de função de pedotransferência Rosetta para previsão de parâmetros hidráulicos de solos não saturados. Disponível em: <https://github.com/usda-ars-ussl/rosetta-soil>. Acesso em 05 de setembro de 2023.

[9] G. M. Vasques, M. R. Coelho, R. O. Dart, L. C. Cintra, and J. F. M. Baca. Soil Clay, Silt and Sand Content Maps for Brazil at 0-5, 5-15, 15-30, 30-60, 60-100 and 100-200 cm Depth Intervals with 90 m Spatial Resolution, Embrapa Solos, Rio de Janeiro, Brazil, 2021.

[10] G. M. Vasques, M. R. Coelho, R. O. Dart, L. C. Cintra, and J. F. M. Baca. Soil Bulk Density Maps for Brazil at 0-5, 5-15, 15-30, 30-60, 60-100 and 100-200 cm Depth Intervals with 90 m Spatial Resolution, Embrapa Solos, Rio de Janeiro, Brazil, 2021.

