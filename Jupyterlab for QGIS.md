# Jupyterlab for QGIS

Use OSGEO installer to install qgis and python modules

### Find python directory for qgis
from QGIS python console check sys.path to see where python is installed.

usually OSGEO4W/apps/PythonXX

### Make a bat file
In the python directory copy *python-qgis.bat* as *python-qgis-jupyterlab.bat* and **open in text editor**. 

Remark the **"%PYTHONHOME%\python" %** and add **"call jupyter-lab"** after last line

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
    rem "%PYTHONHOME%\python" %*
    call jupyter-lab
and save.

### Install jupyterlab
in OSGEO4W folder right click on *OSGeo4W.bat* and select **Run as Administrator**

type **pip install jupyterlab**

### Run Jupyterlab
type python-qgis-jupyterlab.bat in OSGeo4W shell

### Test QGIS module
Open new notebook and add

**from qgis.core import* **
run, if no error, you are fine
