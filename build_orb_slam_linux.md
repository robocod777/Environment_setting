# before starting
Try using ORB SLAM.
[ORB SLAM2](https://github.com/raulmur/ORB_SLAM2)


# Environment
$ lsb_release -a
Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.5 LTS
Release:	16.04
Codename:	xenial

```bsh
$ python -V
Python 2.7.12
$ python3 -V
Python 3.5.2
$ python
>> import cv2
>> cv2.__version__
3.4.0
```

# Dependencies

```bsh
$ sudo apt-get install libglew-dev 
Unpacking libglew-dev:amd64 (1.13.0-2) ...
Setting up libglew-dev:amd64 (1.13.0-2) ...

$ sudo apt-get install cmake
Reading package lists... Done
Building dependency tree       
Reading state information... Done
cmake is already the newest version (3.5.1-1ubuntu3).
0 upgraded, 0 newly installed, 0 to remove and 13 not upgraded.

$ sudo apt-get install libpython2.7-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
libpython2.7-dev is already the newest version (2.7.12-1ubuntu0~16.04.3).
libpython2.7-dev set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 13 not upgraded.


$ sudo apt-get install ffmpeg libavcodec-dev libavutil-dev libavformat-dev libswscale-dev
libavcodec-dev is already the newest version (7:2.8.15-0ubuntu0.16.04.1).
libavformat-dev is already the newest version (7:2.8.15-0ubuntu0.16.04.1).
libavutil-dev is already the newest version (7:2.8.15-0ubuntu0.16.04.1).
libavutil-dev set to manually installed.
libswscale-dev is already the newest version (7:2.8.15-0ubuntu0.16.04.1).
The following additional packages will be installed:
  libavdevice-ffmpeg56
Unpacking libavdevice-ffmpeg56:amd64 (7:2.8.15-0ubuntu0.16.04.1) ...
Selecting previously unselected package ffmpeg.
Preparing to unpack .../ffmpeg_7%3a2.8.15-0ubuntu0.16.04.1_amd64.deb ...
Unpacking ffmpeg (7:2.8.15-0ubuntu0.16.04.1) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up libavdevice-ffmpeg56:amd64 (7:2.8.15-0ubuntu0.16.04.1) ...
Setting up ffmpeg (7:2.8.15-0ubuntu0.16.04.1) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...

$ sudo apt-get install libdc1394-22-dev libraw1394-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
libraw1394-dev is already the newest version (2.1.1-2).
libraw1394-dev set to manually installed.
libdc1394-22-dev is already the newest version (2.2.4-1).
0 upgraded, 0 newly installed, 0 to remove and 13 not upgraded.

$ sudo apt-get install libjpeg-dev libpng12-dev libtiff5-dev libopenexr-dev
5-dev libopenexr-dev 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
libjpeg-dev is already the newest version (8c-2ubuntu8).
libopenexr-dev is already the newest version (2.2.0-10ubuntu2).
libopenexr-dev set to manually installed.
libpng12-dev is already the newest version (1.2.54-1ubuntu1.1).
libtiff5-dev is already the newest version (4.0.6-1ubuntu0.4).
0 upgraded, 0 newly installed, 0 to remove and 13 not upgraded.
```


# Install Pangolin
[Pangolin](https://github.com/stevenlovegrove/Pangolin)

## Install OpenGL
Sometimes, OpenGL crashes with nvidia-* stuffs. 
[Refernce(askubuntu)](https://askubuntu.com/questions/893922/ubuntu-16-04-gives-x-error-of-failed-request-badvalue-integer-parameter-out-o/896248#896248)<br>

We may need to purge some nvidia things in order to install opengl.

```bsh
$ sudo apt purge nvidia-367 nvidia-opencl-icd-375 nvidia-375 nvidia-prime nvidia-settings
$ sudo apt-get install --reinstall xserver-xorg-video-intel libgl1-mesa-glx libgl1-mesa-dri xserver-xorg-core
```

## Install LIBUVC
$ mkdir ~/libuvc_src && cd ~/libuvc_src
$ git clone git://github.com/ktossell/libuvc.git
$ cd libuvc
$ mkdir build && cd build
$ cmake ..
$ make
$ sudo make install

## Install openCV
[openCV: Installation in Linux (official)](https://docs.opencv.org/3.4.1/d7/d9f/tutorial_linux_install.html)
[How to install openCV by mr demura](http://demura.net/misc/14118.html)

```bsh
$ cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=~/opencv/opencv_contrib/modules  -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D WITH_VTK=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D ENABLE_FAST_MATH=1 -D WITH_CUBLAS=1 -D WITH_OPENGL=ON -D WITH_CUDA=OFF ..
```

## Install Pangolin
It took 2~3 minutes.
```bsh
$ mkdir ~/pangolin_src && cd ~/pangolin_src
$ git clone https://github.com/stevenlovegrove/Pangolin.git
$ cd Pangolin
$ mkdir build && cd build
$ cmake ..
$ cmake --build .
$ sudo make install
```

## Instal Eigen3
It took more than 2 hours.
[Eigen lib(official)](http://eigen.tuxfamily.org/dox/GettingStarted.html)

```bsh
$ mkdir ~/eigen_src && cd ~/eigen_src
$ wget http://bitbucket.org/eigen/eigen/get/3.3.4.tar.gz
$ tar -zxf 3.3.4.tar.gz
$ cd eigen-eigen-5a0156e40feb
$ mkdir build
$ cd build
$ cmake ..
$ make check 
$ sudo make install
```
after make check
```bsh
Test project /home/joon/eigen_ws/eigen-eigen-5a0156e40feb/build
...
        Start 480: bdcsvd_9
480/801 Test #480: bdcsvd_9 .........................***Exception: Other  0.15 sec
        Start 481: bdcsvd_2
...

        Start 571: sparse_basic_6
571/801 Test #571: sparse_basic_6 ...................***Exception: Other  0.57 sec
...
        Start 678: boostmultiprec_10
678/801 Test #678: boostmultiprec_10 ................   Passed    0.96 sec
...
        Start 745: sparse_extra_3
745/801 Test #745: sparse_extra_3 ...................***Exception: Other  0.18 sec
        Start 746: openglsupport
746/801 Test #746: openglsupport ....................***Exception: Other  0.27 sec
...
        Start 795: cxx11_tensor_io
795/801 Test #795: cxx11_tensor_io ..................***Exception: SegFault  0.15 sec
99% tests passed, 6 tests failed out of 801

Label Time Summary:
Official       = 544.54 sec (678 tests)
Unsupported    = 103.18 sec (110 tests)

Total Test time (real) = 802.99 sec

The following tests FAILED:
	418 - schur_complex_2 (OTHER_FAULT)
	480 - bdcsvd_9 (OTHER_FAULT)
	571 - sparse_basic_6 (OTHER_FAULT)
	745 - sparse_extra_3 (OTHER_FAULT)
	746 - openglsupport (OTHER_FAULT)
	795 - cxx11_tensor_io (SEGFAULT)
```

2nd trial:
```bsh
Label Time Summary:
Official       = 566.48 sec (678 tests)
Unsupported    =  73.09 sec (110 tests)

Total Test time (real) = 794.31 sec

The following tests FAILED:
	480 - bdcsvd_9 (OTHER_FAULT)
	745 - sparse_extra_3 (OTHER_FAULT)
	746 - openglsupport (OTHER_FAULT)
	795 - cxx11_tensor_io (SEGFAULT)
```
3rd trial:
```bsh
The following tests FAILED:
	480 - bdcsvd_9 (OTHER_FAULT)
	678 - boostmultiprec_10 (OTHER_FAULT)
	745 - sparse_extra_3 (OTHER_FAULT)
	746 - openglsupport (OTHER_FAULT)
	795 - cxx11_tensor_io (SEGFAULT)
```

### Trouble shooting
Symptoms: Freeze at Login Screen. Cannto input P/W.<br>

Grub -> Advanced Boot -> Recovery Mode -> Terminal mode.
```bsh
$ sudo apt-get update
$ sudo apt-get install xserver-xorg-input-evdev
$ sudo reboot
# sudo apt-get install xserver-xorg-input-all
# sudo apt-get install ubuntu-desktop
# sudo apt-get install ubuntu-minimal
# sudo apt-get install xorg xerver-xorg
# sudo apt-get install xserver-xorg-video-intel
```



## Install g2o
[g2o github](https://github.com/RainerKuemmerle/g2o)
```bsh
$ sudo apt update
$ sudo apt install libsuitesparse-dev - qtdeclarative5-dev - qt5-qmake - libqglviewer-dev
$ mkdir ~/g2o_src && cd ~/g2o_src
$ git clone https://github.com/RainerKuemmerle/g2o.git
$ cd g2o
$ mkdir build && cd build
$ cmake ..
$ make -j 4
$ sudo make install
```

## Install DBoW2
[DBoW2(github)](https://github.com/dorian3d/DBoW2)

```bsh
$ sudo apt-get install libboost-dev
$ mkdir ~/DBoW2_ws
$ cd ~/DBoW2_ws
$ git clone https://github.com/dorian3d/DBoW2.git
$ cd DBoW2
$ mkdir build && cd build
$ cmake ..
$ make
$ sudo make install
```

## Install ROS
Please refer the official site.
I installed kinetic.

## Install ORB-SLAM2

```bsh
$ mkdir ~/orb_slam2_src && cd orb_slam2_ws
$ git clone https://github.com/raulmur/ORB_SLAM2.git ORB_SLAM2
$ cd ORB_SLAM2
$ chmod +x build.sh
$ ./build.sh
```

## Download sample data.
[TUM link](https://vision.in.tum.de/data/datasets/rgbd-dataset/download)
```bsh
$ mkdir ~/orb_slam2_src/dataset && cd ~/orb_slam2_src/dataset
$ wget https://vision.in.tum.de/rgbd/dataset/freiburg1/rgbd_dataset_freiburg1_xyz.tgz
$ tar -zxf rgbd_dataset_freiburg1_xyz.tgz
$ ./Examples/Monocular/mono_tum Vocabulary/ORBvoc.txt Examples/Monocular/TUM1.yaml ../dataset/rgbd_dataset_freiburg1_xyz 
```
