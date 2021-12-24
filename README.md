# Areal Interpolation in Python Using Tobler - A Jupyter Notebook Tutorial

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/johnofoster/areal_interpolation_tutorial/HEAD)

## Introduction

Areal interpolation is the process where the attributes of one set of polygons are interpolated to a different set of polygons. There are many applications for this process, for example, the interpolation of census data from census tracts to neighborhoods, or the interpolation of aggregated environment data from one set of geographic boundaries to another.

Tobler, a component of the [Python Spatial Analysis Library](https://pysal.org/) (PySAL) is a package of Python functions designed to perform and support areal interpolation. Visit Tobler's [website](https://pysal.org/tobler/index.html) and [github page](https://github.com/pysal/tobler) for the official documentation.

In this Jupyter notebook tutorial we will use Tobler to perform two different methods of areal interpolation on two different scales of source data. In Part 1 we will use areal weighted and dasymetric methods to interpolate 2016 Canadian census data from Ottawa census tracts and dissemination areas to Ottawa neighborhoods. In part 2 we will do same but with synthetic population data instead of real data. By using this synthetic dataset we will know exactly what the results should be and thus more accurately assess the effect of the methods and scale.

The intended audience of this tutorial are students who have some prior experience using Python, JupyterLab, Jupyter Notebooks, Pandas, and GeoPandas. That being said, the code should work as-is, providing all students with the opportunity to follow along through the steps of the analysis. If you are new to Jupyter notebooks and need help running code cells or performing other basic operations then check out [Project Jupyter's introductory tutorials](https://jupyter.org/try). I have included links to the different packages' documentation throughout the tutorial and feel free to insert or split cells at any point in order to inspect any intermediate data.

> **Disclaimer:** The tutorial and all related documents have been created as a school assignment for Carleton University's GEOM 4008 – Advanced Topics in Geographic Information Systems course. Please forgive any errors, whether simple typographic ones or more critical errors in logic or syntax. Whether you happened upon this document through its [github repository](https://github.com/johnofoster/areal_interpolation_tutorial) or Carleton University's [Open Source GIS Tutorials](https://dges.carleton.ca/CUOSGwiki/index.php/Main_Page) page and want to propose any changes, feel free to submit a pull request to this tutorial's github repository or find me at my [Twitter account](https://twitter.com/FrothyFoster).

## Getting Started

There are a couple of different ways to access this tutorial. If you wish to interact with it by editing and running the code then the simplest method is through Binder. This service will allow you to run the tutorial notebook in JupyterLab without needing to download anything or creating an environment. Alternatively, you can download the files from the github repository, set up the environment, and run the notebook locally. If a static copy of the tutorial is all you want then feel free to check it out at Carleton University's Open Source GIS Tutorials page. Here are the instructions for these three options:

### Option 1: Non-Interactive Copy

As mentioned, this tutorial was created as a student project for a Carleton University geomatics course. It has been converted to a MediaWiki page and uploaded [here](https://dges.carleton.ca/CUOSGwiki/index.php/Areal_Interpolation_in_Python_Using_Tobler).


### Option 2: Run the Tutorial Through Binder 

Please follow these instructions if you want to use an online interactive copy of the tutorial:

1. Open [this link](https://mybinder.org/v2/gh/johnofoster/areal_interpolation_tutorial/HEAD) in a new tab to access a Binder copy of the tutorial repository. 
2. While the Binder service is loading, you can access a non-interactive preview of the notebook (`areal_interp_tutorial.ipynb`) through nbviewer at the bottom of the page.
3. After loading, a JupyterLab session will launch in your browser. This session will use the tutorial environment so all dependencies should work.
4. In the File Browser pane on the left, double-click `areal_interp_tutorial.ipynb` to open the tutorial notebook.
5. With the tutorial now open as an interactive Jupyter notebook you can run and modify each code cell and any output.


### Option 3: Install a Local Copy of the Tutorial

Please follow these instructions if you want to use a local interactive copy of the tutorial:

#### Step 1: Download the Files

If you have git installed:

1. Open a terminal window
2. Change the current working directory to the location where you want the tutorial to reside
3. Clone the repo by running:
```$ git clone https://github.com/johnofoster/areal_interpolation_tutorial```

Otherwise, simply download the zip file of the tutorial from [this link](https://github.com/johnofoster/areal_interpolation_tutorial/archive/refs/heads/main.zip) and unzip it into a suitable working directory on your computer.

#### Step 2: Create Environment

This tutorial uses Python 3.9, Conda, JupyterLab, and a number of Python packages.

If you don't already have an Anaconda distribution then you can find it [here](https://www.anaconda.com/products/individual). For a very lightweight alternative to Anaconda that only contains Conda, Python, and a few essential packages then check out Miniconda [here](https://docs.conda.io/en/latest/miniconda.html). After installing either please follow these instructions:

1. Open a terminal window
2. Change the current working directory to tutorial's directory
3. Create the environment by running: `$ conda env create -- file environment.yml`
4. It might take a while to build the environment so go grab a cup of your favorite beverage.

This will create a Conda environment containing the necessary packages to run this tutorial.

#### Step 3: Open the Tutorial

Now that you have downloaded the tutorial files and created the Conda environment please follow these instructions to launch it:

1. Open a terminal window
2. Change the current working directory to the tutorial's directory
3. Activate the environment: `$ conda activate areal_interp_env`
4. Start a local JupyterLab session in your web browser: `$ Jupyter Lab`
5. In the File Browser pane on the left, double-click `areal_interp_tutorial.ipynb` to open the tutorial notebook.
6. With the tutorial now open you can run and modify each code cell in order to see the output.


#### Step 4: Remove the Tutorial

Once you are done with tutorial you might want to remove it. Simply delete the directory you placed it in and then remove the Conda environment by running the following terminal command: `$ conda env remove --name areal_interp_env`.


### Data Sources

The data for this tutorial has been preprocessed for your convenience and can be found in `data/`. All of this data comes from free and open sources. Links to the original geometry and attributes can be found below along with notes regarding the preprocessing that was performed.

|  	| Geometry source 	| Geometry transformations 	| Attributes source 	| Attributes transformations 	|
|---	|---	|---	|---	|---	|
| Census Tracts 	| [StatCan 2016 Census - Census Tracts Cartographic Boundary File](https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-2016-eng.cfm) 	| Extracted the census tracts falling within the City of Ottawa boundary and reprojected to WGS 84 UTM 18N 	| [StatCan 2016 Census: Census metropolitan areas (CMAs), tracted census agglomerations (CAs) and census tracts (CTs)](https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/download-telecharger/comp/page_dl-tc.cfm?Lang=E&) 	| Extracted the 'Population, 2016' data ('member ID 1') for the City of Ottawa census tracts and joined them to the census tracts geometry 	|
| Dissemination Areas 	| [StatCan 2016 Census - Dissemination Areas Cartographic Boundary File](https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-2016-eng.cfm) 	| Extracted the dissemination areas falling within the City of Ottawa boundary and reprojected to WGS 84 UTM 18N 	| [Canada, provinces, territories, census divisions (CDs), census subdivisions (CSDs) and dissemination areas (DAs) - Ontario only](https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/download-telecharger/comp/page_dl-tc.cfm?Lang=E&) 	| Extracted the 'Population, 2016' data ('member ID 1) for the City of Ottawa dissemination areas and joined them to the dissemination areas geometry 	|
| Neighborhoods 	| [Ottawa Neighbourhood Study (ONS) - Neighbourhood Boundaries Gen 2](https://open.ottawa.ca/datasets/ottawa::ottawa-neighbourhood-study-ons-neighbourhood-boundaries-gen-2/about) 	| Reprojected to WGS 84 UTM 18N 	| [Ottawa Neighbourhood Study (ONS) - Neighbourhood Boundaries Gen 2](https://open.ottawa.ca/datasets/ottawa::ottawa-neighbourhood-study-ons-neighbourhood-boundaries-gen-2/about) 	| Extracted the neighbourhood names ('NAMES') and estimated population fields ('POPEST') 	|
| Landcover 	| [Government of Canada - 2015 Land Cover of Canada](https://open.canada.ca/data/en/dataset/4e615eae-b90c-420b-adee-2ca35896caf6) 	| Clipped to the City of Ottawa's extent 	|  	|  	|
| Zoning 	| [City of Ottawa - Zoning](https://data1-esrica-ncr.opendata.arcgis.com/datasets/esrica-ncr::city-of-ottawa-zoning/about?layer=3) 	| Reprojected to WGS 84 UTM 18N 	| [City of Ottawa - Zoning](https://data1-esrica-ncr.opendata.arcgis.com/datasets/esrica-ncr::city-of-ottawa-zoning/about?layer=3) 	| Extracted the main zones 	|
| Synthetic Points 	| John Foster (tutorial author) 	|  	|  	|  	|
