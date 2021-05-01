# LAS_Processing_Tools
 A set of tools for deriving products from LAS Pointclouds
 
 This manual has been designed with the non GIS specialist in mind. It can act as a guide for staff from other geospatial disciplines found in a geospatial office such as land survey technicians to process LiDAR data to consistent reproducible products.
Introduction
The tools in the jupyter notebook referred to in this manual are designed to facilitate the efficient processing of LAS file pointcloud data. A jupyter notebook is a web app that allows both the code and the visualisation of products. It also has markdown cells which allow explanations of the code as it is run.

Tools Contained in the Code
The code contained in this jupyter notebook performs the following functions
•	Creates a LAS dataset from the LAS files. A LAS dataset file references LAS files and any surface constraints used. 
•	Classifies the ground. One of the most valuable products from aerial LiDAR is a model of the bare earth. To create this, it is first necessary to extract all the points in the pointcloud that represent the ground. This is done in ArcGIS pro using a set of algortihms that identify ground points and attribute them as such. In the LAS specification all points classified as ground are designated class 2.
•	Creates a Digital Terrain Model (DTM). This is a raster representation of the ground surface with the pixel values representing elevation
•	Creates a Digital Surface Model (DSM). This is a raster representation of the surfaces seen by the LiDAR scanner and includes man made features such as houses as well as trees and other vegetation.
•	Creates a set of profiles along the alignment. With this function, a series of section views are created by sampling either the DSM or DTM along the cross-sections in the shapefile. This outputs an image in the notebook as well as a jpg and CSV file for each section.
•	A surface model of the vegetation height. This is created by subtracting the DTM from the DSM.

Getting Started

1.	Before starting
•	A number of the tools here are rely on the arcpy package. To run these scripts the machine will need a licenced version of ArcGIS Pro with the 3D Anlyst extension, although ArcGIS Pro doesn’t need to be running. The following workflow uses the Anaconda distribution to manage and install the various packages and create the required environment for the tools to run in. 
•	This guide assumes the user is working on a windows machine.
•	The function which extracts sections from the surface models  assumes that the las files are in a projected coordinate system and not a geographic one. If the coordinates of the LAS file are in lat, long the tool will not work.
•	To extract the cross-sections, a shape file containing the linestrings of the sections is required. This can be created in ArcGIS Pro and then exported. The code requires that the shapefile has a field (string type) called “xs_id” (see fig1).  The code will use this string id for the names of the output CSV and jpg files of the cross-sections.

2.	Downloading the files
To begin with go to this repository to download the files. https://github.com/creaton-p/LAS_Processing_Tools
Perhaps the easiest way to do this is to go to the green code button on the repository page and download the zip file to a location of your choice.

A set of sample data is also available to try the tools out on. It contains a sample pointcloud and a shapefile of cross-sections and another of a clip region. It can be downloaded from the following link. 
https://drive.google.com/drive/folders/1oWOcZGH8XyItQWyAD-vEmMEGzo5CKYn_?usp=sharing

3.	Set up the folder structure
A number of folders are utilised to hold the various datasets that go into the functions and are outputted by them . The user is free to choose how to structure these and can modify the various paths in the jupyter-notebook to reflect their own setup. The stucture that is pre-coded into the notebook is:
C:\DSM_Tools\LAS_Processing_Tools\
		Pointcloud_Data (folder to hold the LAS files and associated files)
		rasters (folder to hold the various DTMs and DSMs)
		xsections (folder contianing a .shp of linestrings which will be used as cross-sections)
		Extracted_sections (folder to hold extracted cross-section images and CSV files)
		Clip_region (folder containing a polygon shapefile to limit the processing boundaries
 		Also included in here are the extracted files from the repository (fig 5)

4.	Setup the python environment
Before running the jupyter notebook, the correct environment settings have to be created. This is where all the correct versions  of the required python modules are selected and kept together in one place so that everything works as it should when called upon by the code. The environment.yml file contains all the correct versions of the modules and python required to run the code. This manual will take the user through setting up the environment using Anaconda. Anaconda is a python distribution that greatly simplifies package management. It can be downloaded at https://www.anaconda.com/products/individual . After installing Anaconda, launch the anaconda-navigator which is a graphical user interface that makes it easy to launch applications and mange packages. From the home screen launch the CMD.exe prompt to open a terminal window.
Once in the terminal window change directory the directory where the extracted repository files are (including the environment.yml file) and then create the environment. The creation of the environment may take some time as each package will also install some dependencies.
The user is now ready to launch the jupyter notebook. This is done by typing ‘jupyter notebook’ at the command prompt. This will open the notebook in a webpage (fig 11) and the LAS_Products.ipynb can be opened by double clicking on it. 
Once the notebook is opened, instructions on the tools will be given in the markdown cells.


