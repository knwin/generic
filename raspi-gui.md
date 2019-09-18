How to run GUI on raspberry pi if it cannot show up start up and configration does not work
boot your raspberry pi
scan IP address and find the one with the correct mac addrress
#Putty
open putty on your laptop
 - enter ip address
 - log in with raspberry admin account
#install vncserver if not done yet
sudo apt-get install realvnc-vnc-server
 - sudo raspi-config
 - interface options > VNC enabled
#turn on GUI (no matter connected to monitor or not)
sudo mount -o rw,remount \
#run vncserver
vncserver
- this will show ip address as well
#VNC viewer
open vnc viewer on your laptop
type in ip address of raspberry pi - voila!

#**** Running Jupyter notebook server on raspberry pi *****#
ref: https://jupyter-notebook.readthedocs.io/en/stable/config_overview.html
in terminal type
python3 jupyter notebook --generate-config
a jupyter_notebook_config.py will be created under home/pi/.jupyter folder
note: .jupyter is hidden folder
to edit config file
sudo leafpad /home/pi/.jupyter/jupyter_notebook_config.py
this will open leafpad text editor
add or change to c.NotebookApp.ip = '0.0.0.0'
save
python3 -m jupyterlab --no-browser
now you can access jupyterlab @ raspberrypi:8888 port on your browser