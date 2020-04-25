# How to run jupyterlab on Raspberry Pi remotely and use on your browser
Assumed jupyterlab is setup on raspberry pi

open putty on laptop
- enter ip address and port as 22
terminal will be opened
- enter raspberry username and password
- python3 -m jupyterlab --no-browser --port=8889
on laptop open cmd window and type
- ssh -N -f -L localhost:8888:localhost:8889 username@your_remote_host_name
- enter password
on browser type localhost:8889 and enter same password again
