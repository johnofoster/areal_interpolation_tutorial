# Areal Interpolation Tutorial

In this Jupyter Notebook tutorial we will look at two of the areal interpolation methods that are made possible by PySal's Tobler package.
* What is areal interpolation?
* What is a Jupyter Notebook etc?
* What will we do?



# Getting Started

## Access a Remote Copy of the Tutorial

### Option 1: Binder

If you wish to access an interactive copy of this tutorial please follow these instructions:

1. Click  on [this link](https://mybinder.org/v2/gh/johnofoster/areal_interpolation_tutorial/HEAD) and the tutorial's Binder splash page will open. 
2. While it's loading, you can access a non-interactive preview of the notebook (`areal_interp_tutorial.ipynb`)through nbviewer, but it shouldn't take too long to start up.
3. After loading, a JupyterLab session will launch in your browser. This session will use the environment created for the tutorial so all of the dependencies should work just fine.
4. In the File Browser pane on the left, double-click `areal_interp_tutorial.ipynb` to open the tutorial notebook.
5. With the tutorial now open as an interactive Jupyter notebook you can run and modify each code cell in order to see the output.


### Option 2: Carleton University Department of Geography and Environmental Studies Open Source GIS Tutorials Page

As previously mentioned, this tutorial was created as a student project for a Carleton University geomatics course. It has been converted to a MediaWiki page and uploaded [at this link](https://dges.carleton.ca/CUOSGwiki/index.php/Areal_Interpolation_in_Python_using_Tobler).


## Install a Local Copy of the Tutorial

If you have git installed:

1. Open a terminal window
2. Change the current working directory to the location where you want the tutorial to reside
3. Clone the repo by running:
```$ git clone https://github.com/johnofoster/areal_interpolation_tutorial```

Otherwise, simply download the zip file of the tutorial from [this link](https://github.com/johnofoster/areal_interpolation_tutorial/archive/refs/heads/main.zip) and unzip it into a suitable working directory on your computer.

### Create Environment

This tutorial uses Python 3.9, Conda, JupyterLab, and a number of Python packages.

If you don't already have an Anaconda distribution then you can find it [here](https://www.anaconda.com/products/individual). For a very lightweight alternative to Anaconda that only contains Conda, Python, and a few essential packages then check out Miniconda [here](https://docs.conda.io/en/latest/miniconda.html). After installing either please follow these instructions:

1. Open a terminal window
2. Change the current working directory to tutorial's directory
3. Create the environment by running: `$ conda env create -- file environment.yml`
4. It might take a while to build the environment so go grab a cup of your favorite beverage.

This will create a Conda environment containing the necessary packages to run this tutorial.

### Open the Tutorial

Now that you have downloaded the tutorial files and created the Conda environment please follow these instructions to launch it:

1. Open a terminal window
2. Change the current working directory to the tutorial's directory
3. Activate the environment: `$ conda activate areal_interp_env`
4. Launch JupyterLab: `$ Jupyter Lab`
5. In the File Browser pane on the left, double-click `areal_interp_tutorial.ipynb` to open the tutorial notebook.
6. With the tutorial now open as an interactive Jupyter notebook you can run and modify each code cell in order to see the output.


### Remove the Tutorial

Once you are done with tutorial you might want to remove it. Simply delete the directory you placed it in and then remove the Conda environment by running the following in the terminal: `$ conda env remove --name areal_interp_env`.



## Tutorial Data

The data for this tutorial has been preprocessed for your convenience and can be found in `data/`. All of this data comes from free and open sources. Links to the source geometry and attributes can be found below along with notes regarding the processing.

| a                   | Geometry source                                                                                                                                                                  | Geometry transformations                                                                                       | Attributes source                                                                                                                                                                                                                                          | Attributes transformations                                                                                                                          |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Census Tracts       | [StatCan 2016 Census - Census Tracts Cartographic Boundary File](https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-2016-eng.cfm)                   | Extracted the census tracts falling within the City of Ottawa boundary and reprojected to WGS 84 UTM 18N       | [StatCan 2016 Census: Census metropolitan areas (CMAs), tracted census agglomerations (CAs) and census tracts (CTs)](https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/download-telecharger/comp/page_dl-tc.cfm?Lang=E&)              | Extracted the 'Population, 2016' data ('member ID 1') for the City of Ottawa census tracts and joined them to the census tracts geometry            |
| Dissemination Areas | [StatCan 2016 Census - Dissemination Areas Cartographic Boundary File](https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-2016-eng.cfm)             | Extracted the dissemination areas falling within the City of Ottawa boundary and reprojected to WGS 84 UTM 18N | [Canada, provinces, territories, census divisions (CDs), census subdivisions (CSDs) and dissemination areas (DAs) - Ontario only](https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/download-telecharger/comp/page_dl-tc.cfm?Lang=E&) | Extracted the 'Population, 2016' data ('member ID 1) for the City of Ottawa dissemination areas and joined them to the dissemination areas geometry |
| Neighborhoods       | [Ottawa Neighbourhood Study (ONS) - Neighbourhood Boundaries Gen 2](https://open.ottawa.ca/datasets/ottawa::ottawa-neighbourhood-study-ons-neighbourhood-boundaries-gen-2/about) | Reprojected to WGS 84 UTM 18N                                                                                  | [Ottawa Neighbourhood Study (ONS) - Neighbourhood Boundaries Gen 2](https://open.ottawa.ca/datasets/ottawa::ottawa-neighbourhood-study-ons-neighbourhood-boundaries-gen-2/about)                                                                           | Extracted the neighbourhood names ('NAMES') and estimated population fields ('POPEST')                                                              |
| Landcover           | [Government of Canada - 2015 Land Cover of Canada](https://open.canada.ca/data/en/dataset/4e615eae-b90c-420b-adee-2ca35896caf6)                                                  | Clipped to the City of Ottawa's extent                                                                         |                                                                                                                                                                                                                                                            |                                                                                                                                                     |
| Zoning              | [City of Ottawa - Zoning](https://data1-esrica-ncr.opendata.arcgis.com/datasets/esrica-ncr::city-of-ottawa-zoning/about?layer=3)                                                 | Reprojected to WGS 84 UTM 18N                                                                                  | [City of Ottawa - Zoning](https://data1-esrica-ncr.opendata.arcgis.com/datasets/esrica-ncr::city-of-ottawa-zoning/about?layer=3)                                                                                                                           | Extracted the main zones                                                                                                                            |
| Synthetic Points    | John Foster (tutorial author)                                                                                                                                                    |                                                                                                                |                                                                                                                                                                                                                                                            |                                                                                                                                                     |
