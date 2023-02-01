# Adding Kernels to Jupyter notebook and Jupyterlab
On a Jupyter notebook, there is an optoin to chose which kernel to run for the notebook. It also appeares similar option but with icons when creating a new notebook.

<img src="images\kernel_selection1.png"></img>

<img src="images\kernel_selection2.png"></img>

To make your new python environment available in this optoin do following..

Open file explorer
 - go to C:\Users\[user name]\AppData\Roaming\jupyter\kernels\
 <img src="images\kernel_folders.png"></img>
 - add a new folder (example. youtube envrioment which I just installed)
 - copy kernel.json and png logos from existing kernel folder
 - edit kernel.json
   - edit the path to python in new environment
   - edit the display name
     ```
     {
      "argv": [
       "C:\\miniconda3\\envs\\youtube\\python.exe",
       "-m",
       "ipykernel_launcher",
       "-f",
       "{connection_file}"
      ],
      "display_name": "youtbue",
      "language": "python",
      "metadata": {
       "debugger": true
      }
     }
     ```
   - edit the logo if you want differnt style for your environment  
   
     <img src="images\kernel_folder.png"></img>


## Making QGIS available in Juypyter kernels list
this example is for QGIS installed with OSGEO4W setup and you have jupyter-lab installed (maybe with other python environmet)

Go to C:\OSGeo4W
 - copy OSGeo4W.bat as OSGeo4W_python_qgis.bat and open it in edit mode

go to C:\OSGeo4W\bin and open python-qgis.bat in edit mode and copy the content

 - paste at last row of OSGeo4W_python_qgis.bat (edit mode) and save

the bat file content will be looked like this
```
@echo off
rem this bat file is to use in argv parameter of Jupyter kernel.json file.

rem Root OSGEO4W home dir to the same directory this script exists in
call "%~dp0\bin\o4w_env.bat"

rem List available o4w programs
rem but only if osgeo4w called without parameters
cd bin

@echo off
call "%~dp0\o4w_env.bat"
@echo off
path %OSGEO4W_ROOT%\apps\qgis\bin;%PATH%
set QGIS_PREFIX_PATH=%OSGEO4W_ROOT:\=/%/apps/qgis
set GDAL_FILENAME_IS_UTF8=YES
rem Set VSI cache to be used as buffer, see #6448
set VSI_CACHE=TRUE
set VSI_CACHE_SIZE=1000000
set QT_PLUGIN_PATH=%OSGEO4W_ROOT%\apps\qgis\qtplugins;%OSGEO4W_ROOT%\apps\qt5\plugins
set PYTHONPATH=%OSGEO4W_ROOT%\apps\qgis\python;%PYTHONPATH%
python %*
```

from command line
 - C:\OSGeo4W\apps\Python39\python -m pip install ipykernel
 - OR install ipykernel from OSGEO4W setup UI

Go to C:\Users\Kyaw\AppData\Roaming\jupyter\kernels
 - copy an existing kernel folder and paste and rename as QGIS

in side the folder edit kernel.json as follow
```
{
 "argv": [
  "C:\\OSGeo4W\\OSGeo4W_python_qgis.bat",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "QGIS(Py3.9)",
 "language": "python"
}
```
 - save it

when you create a new notebook you see a list of available kernels like below

 <img src="images\kernel_selection3.png"></img>

### test if it works
open new note book with QGIS python as kernel

type ```from qgis.core import *`` in a cell and run. if no error, you succeeded
