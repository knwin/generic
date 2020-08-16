# How to solve no signal on your monitor after first time OS installed in SD card.
https://www.raspberrypi.org/forums/viewtopic.php?t=34061&fbclid=IwAR35HONvDZvdruf6JJi4LQvdg5IM6bNW-FTdeFZtOe1DOmjm12q4UMDBnvc

The Pi outputs a relatively weak HDMI signal. Some devices may not immediately notice the Pi's HDMI or may not do the negotiation.
Setting the hdmi_force_hotplug=1 makes sure the Pi believes the monitor/TV is really there.
You might also need to set config_hdmi_boost=4 or even higher (up to 9) if your display needs a stronger signal.
If the display is a computer monitor, use hdmi_group=1 and if it is an older TV, try hdmi_group=2.
Do not set hdmi_safe=1 as that overrides many of the previous options.
Using a shorter or better quality HDMI cable might help.
Make sure your Pi's power supply delivers 1A and not 500mA.
If you see a problem with the red colour - either absent, or interference - then try a boost. However it might simply be that the display requires a stronger signal than the Pi can give.

# Hwo to access via putty
- sudo raspi-config
- interfacing option > enable SSH
- scan the ip with ip scanner or ifconfig on pi

open putty
- add ip address

# How to run GUI on raspberry pi 
This is for the case when GUI does show up start up no matter how many time you have choosen GUI option in configuration file.
- boot your raspberry pi
- on your laptop, scan IP address and find the one with the correct mac addrress
- open putty on your laptop
  - enter ip address
  - log in with raspberry admin account
  - install vncserver if not done yet: sudo apt-get install realvnc-vnc-server
  - VNC enable as follow
    - sudo raspi-config
    - interface options > VNC enabled
## turn on GUI (no matter connected to monitor or not)
- sudo mount -o rw,remount \
## run vncserver
- vncserver
this will show ip address as well
## VNC viewer
open vnc viewer on your laptop
## Schedule task
- crontab -e
will open crontab file in nano editor. Add following for some task at boot and some at specific hour

use `m h  dom mon dow   command` for time setting

`@reboot python3 -m jupyterlab --no-browser --port=8889`

`@reboot vncserver`

`0 15 * * * python3 /home/pi/JupyterNoteBooks/DMH/DMH_riverlevel_scraping_daily.$`


# How to install PIP
you will not have pip in the raspbarian OS. So you need to install it first for adding moudles later

`sudo apt install python3-pip`

now you have pip and install other module as follow
`sudo python3 -m pip install yourmoudule`

type in ip address of raspberry pi with port 1, example 192.168.1.100:1 - voila!

## Running Jupyter notebook server on raspberry pi 
ref: https://jupyter-notebook.readthedocs.io/en/stable/config_overview.html

in terminal type
- python3 jupyter notebook --generate-config
a jupyter_notebook_config.py will be created under home/pi/.jupyter folder

note: .jupyter is hidden folder

to edit config file
- sudo leafpad /home/pi/.jupyter/jupyter_notebook_config.py
this will open leafpad text editor

add or change to c.NotebookApp.ip = '0.0.0.0'

save and type
- python3 -m jupyterlab --no-browser

now you can access jupyterlab @ raspberrypi:8888 port on your browser

# Geopandas installation fail due to fiona module problem
install gdal dev `sudo apt-get install libgdal-dev`, then install geopandas

# PyPrj installation fail
install from git hub `pip install git+https://github.com/jswhit/pyproj.git`

if git is not installed `sudo apt-get install git`
