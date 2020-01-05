# Setup for Python 3.6, Cuda 10.0 and Tensorflow 1.14


Because python for windows uses prebuilt libraries, the setup might seem overly complicated, because of compatibility issues.
I use Python 3.6.4.

* Install pyton tutorial: 
  * https://www.pytorials.com/python-download-install-windows/
* 64-bit version.
  * https://www.python.org/ftp/python/3.6.4/python-3.6.4-amd64.exe

I currently have the following working setup.

* Install Cuda 10.0 (No special nvidia account required)
  * https://developer.nvidia.com/cuda-10.0-download-archive
* Install CuDNN 7.6.4 for Cuda 10.0 (Developer account required)
  * https://developer.nvidia.com/rdp/cudnn-archive
* Install Tensorflow 1.14
  * pip3 install tensorflow-gpu==1.14
  * pip3 install tensorboard==1.14
* Install Keras 2.3.1
  * pip3 install keras==2.3.1
* Install Jupyter-Notebook-stuff    
  * pip3 install jupyter
  * pip3 install jupyter_contrib_nbextensions
  * pip3 install autopep8
    
