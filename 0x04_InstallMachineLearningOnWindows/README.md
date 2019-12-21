# Setup for Python 3.5, Cuda 10.0 and Tensorflow 1.15


Because python for windows uses prebuilt libraries, the setup might seem overly complicated, because of compatibility issues.
I use Python 3.5 but should consider using 3.6.

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
    
