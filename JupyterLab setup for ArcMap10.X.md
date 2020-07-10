# How to setup Jupyter for Arcgis 10.x

+ open cmd.exe as adminstrator
 + cd python27\arcgis10.7
 + python -m pip install virtualenv
 + python -m virtualenv venv\jupyter
 + cd venv\jyputer
 + python -m pip install jupyter
 + python -m pip install jupyter-lab
 + install any module you want to install here

## link to Arcpy and numpy modules

Although you have installed jupyter, you cannot import arcpy module yet. Do following steps

(ref: https:\\notesfromthelifeboat.com\post\arcpy-virtualenv\)

open cmd.exe as adminstrator
+ cd c:\Python27\ArcGIS10.7
+ mkdir arcpy_includes
+ cd arcpy_includes
+ copyp c:\Python27\ArcGIS10.7\Lib\site-packages\Desktop10.7.pth  OR _you can just copy from windows explorer_
+ mklink\D numpy c:\Python27\ArcGIS10.7\Lib\site-packages\numpy 

## Prepare for Jupyter lab
+ copy C:\Python27\ArcGIS10.7\venv\jupyter\Scripts\activate.bat as jupyterlab_activate.bat
+ edit jupyterlab_activate.bat
  + add _jupyter-lab.exe_ at the end of file

## Create a widnows short cut for Jupyter lab
+ create a shortcut by right click over jupyterlab_lab.bat file and select shortcut to desktop
+ open properties of the _short cut_
  + add path for home folder for jupyter notebooks in _"Start in"_
  + e.g C:\WingPy_scripts\jupyter_notebooks\ArcGIS
  
  Now you double click the short cut and juputer lab will open

type __import arcpy__

if no error, you are ready for ArcGIS on Jupyter environment