# Current Setup
## Setup for Python 3.7.6, Cuda 10.1 and Tensorflow 2.1

In case of using Windows you might want to use prebuilt libraries, so getting the configuration right seems sometimes to be an issue.
This is a working configuration on my machine, as for a python-tensorflow-cuda-cudnn-keras stack.

* Install pyton tutorial: 
  * https://www.pytorials.com/python-download-install-windows/
* 64-bit version.
  * https://www.python.org/ftp/python/3.7.6/python-3.7.6-amd64.exe

* Install Cuda 10.1 (No special nvidia account required)
  * https://developer.nvidia.com/cuda-toolkit-archive
* Install CuDNN 7.6.5 for Cuda 10.1 (Developer account required)
  * https://developer.nvidia.com/rdp/cudnn-download
* Install Tensorflow 2.1
  * `pip3 install tensorflow-gpu==2.1`
  * `pip3 install tensorboard==2.1`
* Install Keras
  * `pip3 install keras==2.3.1`
* Install Pydot (if you use pydot for exporting graphs)
  * `pip3 install pydot`
* Install Jupyter-Notebook-stuff    
  * `pip3 install jupyter`
  * `pip3 install jupyter_contrib_nbextensions`
  * `pip3 install autopep8`
* sometimes, there is a dll missing, `msvcp140_1.dll` 
  * in case of this errormessage 
    * ImportError: Could not find the DLL(s) 'msvcp140_1.dll'. TensorFlow requires that these DLLs be installed in a directory that is named in your %PATH% environment variable. You may install these DLLs by downloading "Microsoft C++ Redistributable for Visual Studio 2015, 2017 and 2019" for your platform from this URL: https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads
  * you might need to download and install:
    * https://support.microsoft.com/de-de/help/2977003/the-latest-supported-visual-c-downloads
    * https://aka.ms/vs/16/release/vc_redist.x64.exe
    
# Older Setup
## Setup for Python 3.6, Cuda 10.0 and Tensorflow 1.14

Because python for windows uses prebuilt libraries, the setup might seem overly complicated, because of compatibility issues.
I use Python 3.6.4.

* Install pyton tutorial: 
  * https://www.pytorials.com/python-download-install-windows/
* 64-bit version.
  * https://www.python.org/ftp/python/3.6.4/python-3.6.4-amd64.exe

* Install Cuda 10.0 (No special nvidia account required)
  * https://developer.nvidia.com/cuda-10.0-download-archive
* Install CuDNN 7.6.4 for Cuda 10.0 (Developer account required)
  * https://developer.nvidia.com/rdp/cudnn-archive
* Install Tensorflow 1.14
  * `pip3 install tensorflow-gpu==1.14`
  * `pip3 install tensorboard==1.14`
* Install Keras 2.3.1
  * `pip3 install keras==2.3.1`
* Install Jupyter-Notebook-stuff    
  * `pip3 install jupyter`
  * `pip3 install jupyter_contrib_nbextensions`
  * `pip3 install autopep8`


