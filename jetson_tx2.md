OS: Ubuntu16.04 aarch64

# 1. Jetpack Install (Update?)
Jetpack download 3.2/
## Memo
I tried installing with "sudo apt -f install" without any package name several times.
I couldn't install at once.

After installing, 
```bsh
$ cd NVIDIA_CUDA-9.0_Samples/bin/aarch64/linux/release
$ ./oceanFFT
```

#2. sudo apt-get update

## Keyserver Problem.
```bsh
W: GPG error: file:/var/cuda-repo-9-0-local  Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY XXXXXXXXXXXXXXXX
W: The repository 'file:/var/cuda-repo-9-0-local  Release' is not signed.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
W: GPG error: file:/var/nv-tensorrt-repo-ga-cuda9.0-trt3.0.4-20180208  Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY XXXXXXXXXXXXXXXX
W: The repository 'file:/var/nv-tensorrt-repo-ga-cuda9.0-trt3.0.4-20180208  Release' is not signed.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```
Solution: Add a public key. [link](https://devtalk.nvidia.com/default/topic/1030831/jetpack-3-2-mdash-l4t-r28-2-production-release-for-jetson-tx1-tx2/?offset=14#5245450)
```bsh
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys XXXXXXXXXXXXXXXX
```
## lock Problem
```bsh
E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?
```
Solution: kill the process that uses apt. [link](https://askubuntu.com/questions/15433/unable-to-lock-the-administration-directory-var-lib-dpkg-is-another-process)
```bsh
$ ps aux | grep apt
$ kill process#
```


# 3. Packages


## pip
```bsh
$ sudo apt-get install python3-pip
$ pip3 install --upgrade setuptools
$ pip3 install --upgrade pip
```
Additional Packages:
```bsh
The following additional packages will be installed:
  libexpat1-dev libpython3-dev libpython3.5-dev python-pip-whl python3-dev
  python3-setuptools python3-wheel python3.5-dev
Suggested packages:
  python-setuptools-doc
The following NEW packages will be installed:
  libexpat1-dev libpython3-dev libpython3.5-dev python-pip-whl python3-dev
  python3-pip python3-setuptools python3-wheel python3.5-dev
0 upgraded, 9 newly installed, 0 to remove and 28 not upgraded.
```

After upgrade pip, I got a trouble.
```bsh
Traceback (most recent call last):
  File "/usr/bin/pip3", line 9, in <module>
    from pip import main
ImportError: cannot import name 'main'
```
Solution: Edit /use/bin/pip3 [link](https://github.com/pypa/pip/issues/5240#issuecomment-381662679)
```python
#I upgraded with pyenv, both python2 and python3, now pip2 not work and pip3 works
#After comparing pip2 and pip3, the difference is the import line

#pip2
from pip import main

#pip3
from pip._internal import main

After substitute pip2 import line with pip3 version, it works
```

## python3.6 and pip3 (python3.6)
```bsh
$ add-apt-repository ppa:jonathonf/python-3.6
$ sudo apt-get update
$ sudo apt-get install python3.6
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2
$ sudo update-alternatives --config python3
```
then select '2'.

```bsh 
$ pip3 -V
pip 10.0.1 from /home/nvidia/.local/lib/python3.6/site-packages/pip (python 3.6)
```

## virtualenv
```bsh
$ pip3 install virtualenv. 
```
Add "/home/nvidia/.local/bin" to PATH@.bashrc.

```bsh
nvidia@tegra-ubuntu:~$ mkdir envCV
nvidia@tegra-ubuntu:~$ virtualenv --no-site-packages envCV
Using base prefix '/usr'
New python executable in /home/nvidia/envCV/bin/python3
Also creating executable in /home/nvidia/envCV/bin/python
Installing setuptools, pip, wheel...done.

nvidia@tegra-ubuntu:~$ source envCV/bin/activate
(envCV) nvidia@tegra-ubuntu:~$ 
```

```bsh
(envCV) nvidia@tegra-ubuntu:~$ python -V
Python 3.5.2
(envCV) nvidia@tegra-ubuntu:~$ deactivate
nvidia@tegra-ubuntu:~$ python -V
Python 2.7.12
nvidia@tegra-ubuntu:~$ 
```

##pytorch
[ref link](https://github.com/andrewadare/jetson-tx2-pytorch)
add --user option when pip3 install
### scipy and LA libs
sudo apt install libopenblas-dev libatlas-dev liblapack-dev
sudo apt install liblapacke-dev checkinstall #For openCV

sudo apt-get install python3.6-dev libmysqlclient-dev 
pip3 install --user numpy 
pip3 install --user scipy # 20~30min

### Build tool prerequisites
pip3 install --user pyyaml
pip3 install --user scikit-build
sudo apt install ninja-build

### CMake
[CMake link](https://askubuntu.com/questions/355565/how-do-i-install-the-latest-version-of-cmake-from-the-command-line/865294#865294)
* Uninstall the default version (nothing)
sudo apt remove cmake
sudo apt purge --auto-remove cmake

```bsh
$ download lastest package from [cmake official](https://cmake.org/download/)
"Unix/Linux Source (has \n line feeds)" (cmake-3.11.3.tar.gz) worked for me.
$ tar -xzvf cmake-$version.$build.tar.gz
$ cd cmake-$version.$build/
$ ./bootstrap
$ make -j4
$ sudo make install
```
After installing, codes below show the version.
```bsh
nvidia@tegra-ubuntu:~$ cmake --version
cmake version 3.11.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```


### Install CFFI
sudo apt install python3-dev
sudo apt install libffi-dev
pip3.6 install --user cffi

### OpenCV
[reference link](https://www.pyimagesearch.com/2016/10/24/ubuntu-16-04-how-to-install-opencv/)
 I skipped CUDA and OpenCL integration, and went system-wide with the Python 3 bindings (no virtualenvs). 
 
 Install openCV dependencies.
 ```bsh
$ sudo apt-get install build-essential cmake pkg-config
$ sudo apt-get install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
$ sudo apt-get install libxvidcore-dev libx264-dev
$ sudo apt-get install libgtk-3-dev
$ sudo apt-get install libatlas-base-dev gfortran
```
Download openCV source (ver. 3.2.0)
and unzip.
```bsh
nvidia@tegra-ubuntu:~$ wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.2.0.zip
--2018-06-13 23:39:24--  https://github.com/Itseez/opencv/archive/3.2.0.zip
Resolving github.com (github.com)... 192.30.255.112, 192.30.255.113
Connecting to github.com (github.com)|192.30.255.112|:443... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://github.com/opencv/opencv/archive/3.2.0.zip [following]
--2018-06-13 23:39:30--  https://github.com/opencv/opencv/archive/3.2.0.zip
Reusing existing connection to github.com:443.
HTTP request sent, awaiting response... 302 Found
Location: https://codeload.github.com/opencv/opencv/zip/3.2.0 [following]
--2018-06-13 23:39:31--  https://codeload.github.com/opencv/opencv/zip/3.2.0
Resolving codeload.github.com (codeload.github.com)... 192.30.255.121, 192.30.255.120
Connecting to codeload.github.com (codeload.github.com)|192.30.255.121|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [application/zip]
Saving to: ‘opencv.zip’

opencv.zip              [             <=>    ]  78.23M  35.1KB/s    in 30m 14s 

2018-06-14 00:09:47 (44.2 KB/s) - ‘opencv.zip’ saved [82033498]

$ unzip opencv.zip
$ ls opencv-3.2.0
```

openCV and openCV_contrib should be same version.
```bsh
nvidia@tegra-ubuntu:~$ wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.2.0.zip
--2018-06-13 23:39:05--  https://github.com/Itseez/opencv_contrib/archive/3.2.0.zip
Resolving github.com (github.com)... 192.30.255.113, 192.30.255.112
Connecting to github.com (github.com)|192.30.255.113|:443... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://github.com/opencv/opencv_contrib/archive/3.2.0.zip [following]
--2018-06-13 23:39:06--  https://github.com/opencv/opencv_contrib/archive/3.2.0.zip
Reusing existing connection to github.com:443.
HTTP request sent, awaiting response... 302 Found
Location: https://codeload.github.com/opencv/opencv_contrib/zip/3.2.0 [following]
--2018-06-13 23:39:06--  https://codeload.github.com/opencv/opencv_contrib/zip/3.2.0
Resolving codeload.github.com (codeload.github.com)... 192.30.255.121, 192.30.255.120
Connecting to codeload.github.com (codeload.github.com)|192.30.255.121|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [application/zip]
Saving to: ‘opencv_contrib.zip’

opencv_contrib.zip      [            <=>     ]  53.39M  48.2KB/s    in 23m 18s 

2018-06-14 00:02:25 (39.1 KB/s) - ‘opencv_contrib.zip’ saved [55984686]

$ unzip opencv_contrib.zip
```

activate envCV and install numpy
```bsh
(envCV) $ pip install numpy==1.12.1
```

#### Install openCV!

make .sh file.

```bsh
(envCV) $ cd ~/opencv-3.2.0
(envCV) $ mkdir build
(envCV) $ cd build
(envCV) $ vi build.sh
``````bsh
#!/bin/bash
cmake \
    -D ENABLE_PRECOMPILED_HEADERS=OFF \
    -D WITH_OPENCL=OFF \
    -D WITH_CUDA=OFF \
    -D WITH_CUFFT=OFF \
    -D WITH_CUBLAS=OFF \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D INSTALL_C_EXAMPLES=OFF \
    -D PYTHON_EXECUTABLE=~/envCV/bin/python \
    -D BUILD_EXAMPLES=OFF ..

```
Make builder!
```bsh
(envCV) $ chmod +x build.sh
(envCV) $ ./build.sh
```

```bsh
...
--   Python 3:
--     Interpreter:                 /home/nvidia/envCV/bin/python3 (ver 3.6.5)
--     Libraries:                   /usr/lib/aarch64-linux-gnu/libpython3.6m.so (ver 3.6.5)
--     numpy:                       /home/nvidia/envCV/lib/python3.6/site-packages/numpy/core/include (ver 1.12.1)
--     packages path:               lib/python3.6/site-packages
--
...
```

Compile
```bsh
(envCV) $ make -j4
```
Install
```bsh
(envCV) $ sudo make install
(envCV) $ sudo ldconfig
```

Certicify and move cv2 file.
```bsh
(envCV) $ ls /usr/local/lib/python3.6/site-packages
cv2.cpython-36m-aarch64-linux-gnu.so
(envCV) $ mv /usr/local/lib/python3.6/site-packages/cv2.cpython-36m-aarch64-linux-gnu.so ~/envCV/lib/python3.6/site-packages/cv2.so
```

```bsh
(envCV) nvidia@tegra-ubuntu:~/envCV/lib/python3.6/site-packages$ python
Python 3.6.5 (default, May  3 2018, 10:08:28) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import cv2
>>> cv2.__version__
'3.2.0'
>>> 
```

```bsh
$ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2017 NVIDIA Corporation
Built on Sun_Nov_19_03:16:56_CST_2017
Cuda compilation tools, release 9.0, V9.0.252
$ ldconfig -p | grep dnn
```

```bsh
#.bashrc
export CUDNN_LIB_DIR=/usr/lib/aarch64-linux-gnu
export CUDNN_INCLUDE_DIR=/usr/include
```

```bsh
(envCV) $ python
>>> import os
>>> print(os.getenv("CUDNN_LIB_DIR"))
/usr/lib/aarch64-linux-gnu
```

## PyTorch 0.4.0

```bsh
(envCV) nvidia@tegra-ubuntu:~/pytorch$ git clone https://github.com/pytorch/pytorch.git
(envCV) nvidia@tegra-ubuntu:~/pytorch$ git checkout -b v0.4.0 v0.4.0
```
```bsh
(envCV) nvidia@tegra-ubuntu:~/pytorch$ git submodule update --init
(envCV) nvidia@tegra-ubuntu:~/pytorch$ pip install pyyaml
Collecting pyyaml
Installing collected packages: pyyaml
Successfully installed pyyaml-3.12
(envCV) nvidia@tegra-ubuntu:~/pytorch$ time python setup.py install --user
```

~6/13
```python
import torch
torch.backends.cudnn.is_acceptable(torch.cuda.FloatTensor(1))
```

If true returned, it means that pytorch works well.
```bsh
(envCV) $ pip install --user torchvision==0.2.1
```

pillow 5.1.0, numpy 1.14.2 pandas 0.22.0, urllib3 1.22, scipy 1.1.0, ipython 6.3.1, jupyter-client 5.2.3, jupyter-core=4.4.0, Cython 0.28.2 ...........

#### Cleanup
The postFlashTX1 repo contains some useful cleanup scripts. In addition:
```bsh
sudo apt clean
sudo apt autoremove --purge
sudo rm /usr/src/*.tbz2 ## I had 6.9 GB of zip files
sudo rm /var/cuda-repo-8.0-local/*.deb
rm ~/temp # From my CMake 3.7 install
```
The OpenCV sources can also be removed if necessary.

## Fail to open terminal
with error message below:
```bsh
Traceback (most recent call last):
  File "/usr/bin/gnome-terminal", line 9, in <module>
    from gi.repository import GLib, Gio
  File "/usr/lib/python3/dist-packages/gi/__init__.py", line 42, in <module>
    from . import _gi
ImportError: cannot import name '_gi'
Error in sys.excepthook:
Traceback (most recent call last):
  File "/usr/lib/python3/dist-packages/apport_python_hook.py", line 63, in apport_excepthook
    from apport.fileutils import likely_packaged, get_recent_crashes
  File "/usr/lib/python3/dist-packages/apport/__init__.py", line 5, in <module>
    from apport.report import Report
  File "/usr/lib/python3/dist-packages/apport/report.py", line 30, in <module>
    import apport.fileutils
  File "/usr/lib/python3/dist-packages/apport/fileutils.py", line 23, in <module>
    from apport.packaging_impl import impl as packaging
  File "/usr/lib/python3/dist-packages/apport/packaging_impl.py", line 23, in <module>
    import apt
  File "/usr/lib/python3/dist-packages/apt/__init__.py", line 23, in <module>
    import apt_pkg
ModuleNotFoundError: No module named 'apt_pkg'

Original exception was:
Traceback (most recent call last):
  File "/usr/bin/gnome-terminal", line 9, in <module>
    from gi.repository import GLib, Gio
  File "/usr/lib/python3/dist-packages/gi/__init__.py", line 42, in <module>
    from . import _gi
ImportError: cannot import name '_gi'
```
Does this error occur because I installed python3.6?    
Anyway, solution:
```bsh
$ cd /usr/lib/python3/dist-packages/gi
$ sudo cp _gi_cairo.cpython-35m-aarch64-linux-gnu.so _gi_cairo.cpython-36m-aarch64-linux-gnu.so 
$ sudo cp _gi.cpython-35m-aarch64-linux-gnu.so _gi.cpython-36m-aarch64-linux-gnu.so 
```
