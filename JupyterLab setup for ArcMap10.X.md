# How to setup Jupyter for Arcgis 10.x
(here ArcGIS 10.8 as example, change to actural version)
## 1. create a virtual environment as follow..
+ open cmd.exe as adminstrator
 + cd python27\arcgis10.8
 + python -m pip install virtualenv
 + python -m virtualenv venv\jupyter
 + cd venv\jupyter\scripts
 + python -m pip install jupyter
 + python -m pip install jupyterlab
 + install any module you want to install here

## 2. link to Arcpy and numpy modules

Although you have installed jupyter, you cannot import arcpy module yet. Do following steps

(ref: https:\\notesfromthelifeboat.com\post\arcpy-virtualenv\)

open command prompt (cmd.exe) as adminstrator
+ cd c:\Python27\ArcGIS10.8
+ mkdir arcpy_includes
+ cd arcpy_includes
+ from windows explorer goto c:\Python27\ArcGIS10.8\Lib\site-packages\
  - copy Desktop10.8.pth and
    - paste into c:\Python27\ArcGIS10.8\arcpy_includes 
    - panste into c:\Python27\ArcGIS10.8\venv\jupyter\Lib\site-packages 
+ in command propt, form acrpy_includes type following command and run
  - mklink/D numpy c:\Python27\ArcGIS10.8\Lib\site-packages\numpy 

## 3. Prepare for Jupyter lab
+ if not installed in step 1, install jupyter lab: _C:\Python27\ArcGIS10.8\venv\jupyter\Scripts\python -m pip install jupyterlab_ 
+ copy C:\Python27\ArcGIS10.8\venv\jupyter\Scripts\activate.bat as jupyterlab_activate.bat in the same folder
+ edit jupyterlab_activate.bat with notepad or notepad++
  + add _set "PYTHONPATH=C:\Python27\ArcGIS10.8\Lib\site-packages"_ at second line
  + add _jupyter-lab.exe_ at the end of file
  + 
<img src="images\jupyterlab.bat.PNG"></img>
## 4. Create a widnows short cut for Jupyter lab
+ create a shortcut by right click over jupyterlab_activate.bat file and select shortcut to desktop
+ open properties of the _short cut_
  + add path for home folder for jupyter notebooks in _"Start in"_ e.g _C:\jupyter_notebooks\ArcGIS_
<img src="images\jupyterlab-shortcut.PNG"></img>  
  Now you double click the short cut and juputer lab will open

type __import arcpy__ in new cell of new notebook

if no error, you are ready for ArcGIS on Jupyter environment
