# Adding Kernels to Jupyter notebook and Jupyterlab
On a Jupyter notebook, there is an optoin to chose which kernel to run for the notebook. It also appeare similar option when creating a new notbook.

<img src="images\kernel_selection1.png"></img>

<img src="images\kernel_selection2.png"></img>

To make your new python environment available in this optoin do following..

Open file explorer
 - go to C:\Users\[user name]\AppData\Roaming\jupyter\kernels\
 <img src="images\kernel_folders.png"></img>
 - add a new folder (example. youtube envrioment which I just installed)
 - copy kernel.json and png logos from existing kernel folder
 <img src="images\kernel_folder.png"></img>
 - edit kernel.json
   - edit the path to python in new environment
   - edit the display name
   - edit the logo if you want differnt style for your environment  
   - 
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
