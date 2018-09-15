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
        Start   1: rand
  1/801 Test   #1: rand .............................   Passed    7.09 sec
        Start   2: meta
  2/801 Test   #2: meta .............................   Passed    0.00 sec
        Start   3: numext
  3/801 Test   #3: numext ...........................   Passed    0.00 sec
        Start   4: sizeof
  4/801 Test   #4: sizeof ...........................   Passed    0.00 sec
        Start   5: dynalloc
  5/801 Test   #5: dynalloc .........................   Passed    0.01 sec
        Start   6: nomalloc_1
  6/801 Test   #6: nomalloc_1 .......................   Passed    0.00 sec
        Start   7: nomalloc_2
  7/801 Test   #7: nomalloc_2 .......................   Passed    0.00 sec
        Start   8: nomalloc_3
  8/801 Test   #8: nomalloc_3 .......................   Passed    0.00 sec
        Start   9: nomalloc_4
  9/801 Test   #9: nomalloc_4 .......................   Passed    0.00 sec
        Start  10: nomalloc_5
 10/801 Test  #10: nomalloc_5 .......................   Passed    0.00 sec
        Start  11: nomalloc_6
 11/801 Test  #11: nomalloc_6 .......................   Passed    0.00 sec
        Start  12: nomalloc_7
 12/801 Test  #12: nomalloc_7 .......................   Passed    0.00 sec
        Start  13: nomalloc_8
 13/801 Test  #13: nomalloc_8 .......................   Passed    0.00 sec
        Start  14: first_aligned
 14/801 Test  #14: first_aligned ....................   Passed    0.00 sec
        Start  15: nullary_1
 15/801 Test  #15: nullary_1 ........................   Passed    0.00 sec
        Start  16: nullary_2
 16/801 Test  #16: nullary_2 ........................   Passed    0.00 sec
        Start  17: nullary_3
 17/801 Test  #17: nullary_3 ........................   Passed    0.00 sec
        Start  18: nullary_4
 18/801 Test  #18: nullary_4 ........................   Passed    0.07 sec
        Start  19: nullary_5
 19/801 Test  #19: nullary_5 ........................   Passed    0.00 sec
        Start  20: nullary_6
 20/801 Test  #20: nullary_6 ........................   Passed    0.00 sec
        Start  21: nullary_7
 21/801 Test  #21: nullary_7 ........................   Passed    0.05 sec
        Start  22: nullary_8
 22/801 Test  #22: nullary_8 ........................   Passed    0.00 sec
        Start  23: nullary_9
 23/801 Test  #23: nullary_9 ........................   Passed    0.01 sec
        Start  24: nullary_10
 24/801 Test  #24: nullary_10 .......................   Passed    0.00 sec
        Start  25: mixingtypes_1
 25/801 Test  #25: mixingtypes_1 ....................   Passed    0.00 sec
        Start  26: mixingtypes_2
 26/801 Test  #26: mixingtypes_2 ....................   Passed    0.00 sec
        Start  27: mixingtypes_3
 27/801 Test  #27: mixingtypes_3 ....................   Passed    7.59 sec
        Start  28: mixingtypes_4
 28/801 Test  #28: mixingtypes_4 ....................   Passed    0.00 sec
        Start  29: mixingtypes_5
 29/801 Test  #29: mixingtypes_5 ....................   Passed    0.00 sec
        Start  30: mixingtypes_6
 30/801 Test  #30: mixingtypes_6 ....................   Passed    3.28 sec
        Start  31: packetmath_1
 31/801 Test  #31: packetmath_1 .....................   Passed    0.00 sec
        Start  32: packetmath_2
 32/801 Test  #32: packetmath_2 .....................   Passed    0.00 sec
        Start  33: packetmath_3
 33/801 Test  #33: packetmath_3 .....................   Passed    0.00 sec
        Start  34: packetmath_4
 34/801 Test  #34: packetmath_4 .....................   Passed    0.00 sec
        Start  35: packetmath_5
 35/801 Test  #35: packetmath_5 .....................   Passed    0.00 sec
        Start  36: unalignedassert_1
 36/801 Test  #36: unalignedassert_1 ................   Passed    0.00 sec
        Start  37: unalignedassert_2
 37/801 Test  #37: unalignedassert_2 ................   Passed    0.00 sec
        Start  38: unalignedassert_3
 38/801 Test  #38: unalignedassert_3 ................   Passed    0.00 sec
        Start  39: unalignedassert_4
 39/801 Test  #39: unalignedassert_4 ................   Passed    0.00 sec
        Start  40: vectorization_logic_1
 40/801 Test  #40: vectorization_logic_1 ............   Passed    0.00 sec
        Start  41: vectorization_logic_2
 41/801 Test  #41: vectorization_logic_2 ............   Passed    0.00 sec
        Start  42: basicstuff_2
 42/801 Test  #42: basicstuff_2 .....................   Passed    0.00 sec
        Start  43: basicstuff_1
 43/801 Test  #43: basicstuff_1 .....................   Passed    0.00 sec
        Start  44: basicstuff_3
 44/801 Test  #44: basicstuff_3 .....................   Passed    0.09 sec
        Start  45: basicstuff_4
 45/801 Test  #45: basicstuff_4 .....................   Passed    0.04 sec
        Start  46: basicstuff_5
 46/801 Test  #46: basicstuff_5 .....................   Passed    0.11 sec
        Start  47: basicstuff_6
 47/801 Test  #47: basicstuff_6 .....................   Passed    0.01 sec
        Start  48: basicstuff_7
 48/801 Test  #48: basicstuff_7 .....................   Passed    0.10 sec
        Start  49: constructor_1
 49/801 Test  #49: constructor_1 ....................   Passed    0.01 sec
        Start  50: linearstructure_1
 50/801 Test  #50: linearstructure_1 ................   Passed    0.00 sec
        Start  51: linearstructure_2
 51/801 Test  #51: linearstructure_2 ................   Passed    0.00 sec
        Start  52: linearstructure_3
 52/801 Test  #52: linearstructure_3 ................   Passed    0.00 sec
        Start  53: linearstructure_4
 53/801 Test  #53: linearstructure_4 ................   Passed    0.00 sec
        Start  54: linearstructure_5
 54/801 Test  #54: linearstructure_5 ................   Passed    0.02 sec
        Start  55: linearstructure_6
 55/801 Test  #55: linearstructure_6 ................   Passed    0.02 sec
        Start  56: linearstructure_7
 56/801 Test  #56: linearstructure_7 ................   Passed    0.02 sec
        Start  57: linearstructure_8
 57/801 Test  #57: linearstructure_8 ................   Passed    0.02 sec
        Start  58: linearstructure_9
 58/801 Test  #58: linearstructure_9 ................   Passed    0.02 sec
        Start  59: linearstructure_10
 59/801 Test  #59: linearstructure_10 ...............   Passed    0.05 sec
        Start  60: linearstructure_11
 60/801 Test  #60: linearstructure_11 ...............   Passed    0.00 sec
        Start  61: integer_types_1
 61/801 Test  #61: integer_types_1 ..................   Passed    0.00 sec
        Start  62: integer_types_2
 62/801 Test  #62: integer_types_2 ..................   Passed    0.00 sec
        Start  63: integer_types_3
 63/801 Test  #63: integer_types_3 ..................   Passed    0.00 sec
        Start  64: integer_types_4
 64/801 Test  #64: integer_types_4 ..................   Passed    0.01 sec
        Start  65: integer_types_5
 65/801 Test  #65: integer_types_5 ..................   Passed    0.00 sec
        Start  66: integer_types_6
 66/801 Test  #66: integer_types_6 ..................   Passed    0.00 sec
        Start  67: integer_types_7
 67/801 Test  #67: integer_types_7 ..................   Passed    0.00 sec
        Start  68: integer_types_8
 68/801 Test  #68: integer_types_8 ..................   Passed    0.00 sec
        Start  69: integer_types_9
 69/801 Test  #69: integer_types_9 ..................   Passed    0.00 sec
        Start  70: unalignedcount
 70/801 Test  #70: unalignedcount ...................   Passed    0.00 sec
        Start  71: exceptions
 71/801 Test  #71: exceptions .......................   Passed    0.01 sec
        Start  72: redux_1
 72/801 Test  #72: redux_1 ..........................   Passed    0.00 sec
        Start  73: redux_2
 73/801 Test  #73: redux_2 ..........................   Passed    0.00 sec
        Start  74: redux_3
 74/801 Test  #74: redux_3 ..........................   Passed    0.00 sec
        Start  75: redux_4
 75/801 Test  #75: redux_4 ..........................   Passed    0.02 sec
        Start  76: redux_5
 76/801 Test  #76: redux_5 ..........................   Passed    0.01 sec
        Start  77: redux_6
 77/801 Test  #77: redux_6 ..........................   Passed    0.01 sec
        Start  78: redux_7
 78/801 Test  #78: redux_7 ..........................   Passed    0.00 sec
        Start  79: redux_8
 79/801 Test  #79: redux_8 ..........................   Passed    0.01 sec
        Start  80: visitor_1
 80/801 Test  #80: visitor_1 ........................   Passed    0.00 sec
        Start  81: visitor_2
 81/801 Test  #81: visitor_2 ........................   Passed    0.00 sec
        Start  82: visitor_3
 82/801 Test  #82: visitor_3 ........................   Passed    0.00 sec
        Start  83: visitor_4
 83/801 Test  #83: visitor_4 ........................   Passed    0.00 sec
        Start  84: visitor_5
 84/801 Test  #84: visitor_5 ........................   Passed    0.00 sec
        Start  85: visitor_6
 85/801 Test  #85: visitor_6 ........................   Passed    0.00 sec
        Start  86: visitor_7
 86/801 Test  #86: visitor_7 ........................   Passed    0.00 sec
        Start  87: visitor_8
 87/801 Test  #87: visitor_8 ........................   Passed    0.00 sec
        Start  88: visitor_9
 88/801 Test  #88: visitor_9 ........................   Passed    0.00 sec
        Start  89: visitor_10
 89/801 Test  #89: visitor_10 .......................   Passed    0.00 sec
        Start  90: block_1
 90/801 Test  #90: block_1 ..........................   Passed    0.00 sec
        Start  91: block_2
 91/801 Test  #91: block_2 ..........................   Passed    0.00 sec
        Start  92: block_3
 92/801 Test  #92: block_3 ..........................   Passed    0.00 sec
        Start  93: block_4
 93/801 Test  #93: block_4 ..........................   Passed    0.00 sec
        Start  94: block_5
 94/801 Test  #94: block_5 ..........................   Passed    0.00 sec
        Start  95: block_6
 95/801 Test  #95: block_6 ..........................   Passed    0.00 sec
        Start  96: block_8
 96/801 Test  #96: block_8 ..........................   Passed    0.00 sec
        Start  97: block_7
 97/801 Test  #97: block_7 ..........................   Passed    0.00 sec
        Start  98: corners_1
 98/801 Test  #98: corners_1 ........................   Passed    0.00 sec
        Start  99: corners_2
 99/801 Test  #99: corners_2 ........................   Passed    0.00 sec
        Start 100: corners_3
100/801 Test #100: corners_3 ........................   Passed    0.00 sec
        Start 101: corners_4
101/801 Test #101: corners_4 ........................   Passed    0.00 sec
        Start 102: corners_5
102/801 Test #102: corners_5 ........................   Passed    0.00 sec
        Start 103: swap_1
103/801 Test #103: swap_1 ...........................   Passed    0.00 sec
        Start 104: swap_2
104/801 Test #104: swap_2 ...........................   Passed    0.00 sec
        Start 105: swap_3
105/801 Test #105: swap_3 ...........................   Passed    0.01 sec
        Start 106: swap_4
106/801 Test #106: swap_4 ...........................   Passed    0.01 sec
        Start 107: resize
107/801 Test #107: resize ...........................   Passed    0.00 sec
        Start 108: conservative_resize_1
108/801 Test #108: conservative_resize_1 ............   Passed    0.04 sec
        Start 109: conservative_resize_2
109/801 Test #109: conservative_resize_2 ............   Passed    0.04 sec
        Start 110: conservative_resize_3
110/801 Test #110: conservative_resize_3 ............   Passed    0.05 sec
        Start 111: conservative_resize_4
111/801 Test #111: conservative_resize_4 ............   Passed    0.07 sec
        Start 112: conservative_resize_5
112/801 Test #112: conservative_resize_5 ............   Passed    0.04 sec
        Start 113: conservative_resize_6
113/801 Test #113: conservative_resize_6 ............   Passed    0.04 sec
        Start 114: product_small_1
114/801 Test #114: product_small_1 ..................   Passed    0.00 sec
        Start 115: product_small_2
115/801 Test #115: product_small_2 ..................   Passed    0.01 sec
        Start 116: product_small_8
116/801 Test #116: product_small_8 ..................   Passed    0.00 sec
        Start 117: product_small_3
117/801 Test #117: product_small_3 ..................   Passed    0.00 sec
        Start 118: product_small_4
118/801 Test #118: product_small_4 ..................   Passed    0.00 sec
        Start 119: product_small_5
119/801 Test #119: product_small_5 ..................   Passed    0.00 sec
        Start 120: product_small_6
120/801 Test #120: product_small_6 ..................   Passed    0.00 sec
        Start 121: product_small_11
121/801 Test #121: product_small_11 .................   Passed    0.00 sec
        Start 122: product_small_12
122/801 Test #122: product_small_12 .................   Passed    0.00 sec
        Start 123: product_small_13
123/801 Test #123: product_small_13 .................   Passed    0.01 sec
        Start 124: product_small_21
124/801 Test #124: product_small_21 .................   Passed    0.00 sec
        Start 125: product_small_22
125/801 Test #125: product_small_22 .................   Passed    0.01 sec
        Start 126: product_small_23
126/801 Test #126: product_small_23 .................   Passed    0.01 sec
        Start 127: product_small_31
127/801 Test #127: product_small_31 .................   Passed    0.01 sec
        Start 128: product_small_32
128/801 Test #128: product_small_32 .................   Passed    0.00 sec
        Start 129: product_small_33
129/801 Test #129: product_small_33 .................   Passed    0.02 sec
        Start 130: product_small_41
130/801 Test #130: product_small_41 .................   Passed    0.01 sec
        Start 131: product_small_42
131/801 Test #131: product_small_42 .................   Passed    0.00 sec
        Start 132: product_small_43
132/801 Test #132: product_small_43 .................   Passed    0.01 sec
        Start 133: product_small_7
133/801 Test #133: product_small_7 ..................   Passed    0.00 sec
        Start 134: product_large_1
134/801 Test #134: product_large_1 ..................   Passed    0.48 sec
        Start 135: product_large_2
135/801 Test #135: product_large_2 ..................   Passed    0.95 sec
        Start 136: product_large_3
136/801 Test #136: product_large_3 ..................   Passed    1.05 sec
        Start 137: product_large_4
137/801 Test #137: product_large_4 ..................   Passed    0.35 sec
        Start 138: product_large_5
138/801 Test #138: product_large_5 ..................   Passed    0.59 sec
        Start 139: product_large_6
139/801 Test #139: product_large_6 ..................   Passed    0.02 sec
        Start 140: product_extra_1
140/801 Test #140: product_extra_1 ..................   Passed    0.19 sec
        Start 141: product_extra_2
141/801 Test #141: product_extra_2 ..................   Passed    0.16 sec
        Start 142: product_extra_3
142/801 Test #142: product_extra_3 ..................   Passed    0.10 sec
        Start 143: product_extra_4
143/801 Test #143: product_extra_4 ..................   Passed    0.20 sec
        Start 144: product_extra_5
144/801 Test #144: product_extra_5 ..................   Passed    0.00 sec
        Start 145: product_extra_6
145/801 Test #145: product_extra_6 ..................   Passed    0.01 sec
        Start 146: product_extra_7
146/801 Test #146: product_extra_7 ..................   Passed    0.00 sec
        Start 147: product_extra_8
147/801 Test #147: product_extra_8 ..................   Passed    0.00 sec
        Start 148: diagonalmatrices_1
148/801 Test #148: diagonalmatrices_1 ...............   Passed    0.00 sec
        Start 149: diagonalmatrices_2
149/801 Test #149: diagonalmatrices_2 ...............   Passed    0.00 sec
        Start 150: diagonalmatrices_3
150/801 Test #150: diagonalmatrices_3 ...............   Passed    0.00 sec
        Start 151: diagonalmatrices_4
151/801 Test #151: diagonalmatrices_4 ...............   Passed    0.00 sec
        Start 152: diagonalmatrices_5
152/801 Test #152: diagonalmatrices_5 ...............   Passed    0.00 sec
        Start 153: diagonalmatrices_6
153/801 Test #153: diagonalmatrices_6 ...............   Passed    0.04 sec
        Start 154: diagonalmatrices_7
154/801 Test #154: diagonalmatrices_7 ...............   Passed    0.03 sec
        Start 155: diagonalmatrices_8
155/801 Test #155: diagonalmatrices_8 ...............   Passed    0.04 sec
        Start 156: diagonalmatrices_9
156/801 Test #156: diagonalmatrices_9 ...............   Passed    0.03 sec
        Start 157: diagonalmatrices_10
157/801 Test #157: diagonalmatrices_10 ..............   Passed    0.00 sec
        Start 158: adjoint_1
158/801 Test #158: adjoint_1 ........................   Passed    0.00 sec
        Start 159: adjoint_2
159/801 Test #159: adjoint_2 ........................   Passed    0.00 sec
        Start 160: adjoint_3
160/801 Test #160: adjoint_3 ........................   Passed    0.00 sec
        Start 161: adjoint_4
161/801 Test #161: adjoint_4 ........................   Passed    0.02 sec
        Start 162: adjoint_5
162/801 Test #162: adjoint_5 ........................   Passed    0.03 sec
        Start 163: adjoint_6
163/801 Test #163: adjoint_6 ........................   Passed    0.02 sec
        Start 164: adjoint_8
164/801 Test #164: adjoint_8 ........................   Passed    0.00 sec
        Start 165: adjoint_9
165/801 Test #165: adjoint_9 ........................   Passed    0.00 sec
        Start 166: adjoint_10
166/801 Test #166: adjoint_10 .......................   Passed    0.00 sec
        Start 167: adjoint_11
167/801 Test #167: adjoint_11 .......................   Passed    0.00 sec
        Start 168: adjoint_12
168/801 Test #168: adjoint_12 .......................   Passed    0.00 sec
        Start 169: adjoint_7
169/801 Test #169: adjoint_7 ........................   Passed    0.00 sec
        Start 170: adjoint_13
170/801 Test #170: adjoint_13 .......................   Passed    0.00 sec
        Start 171: diagonal_1
171/801 Test #171: diagonal_1 .......................   Passed    0.01 sec
        Start 172: diagonal_2
172/801 Test #172: diagonal_2 .......................   Passed    0.04 sec
        Start 173: miscmatrices_1
173/801 Test #173: miscmatrices_1 ...................   Passed    0.00 sec
        Start 174: miscmatrices_2
174/801 Test #174: miscmatrices_2 ...................   Passed    0.00 sec
        Start 175: miscmatrices_3
175/801 Test #175: miscmatrices_3 ...................   Passed    0.00 sec
        Start 176: miscmatrices_4
176/801 Test #176: miscmatrices_4 ...................   Passed    0.00 sec
        Start 177: miscmatrices_5
177/801 Test #177: miscmatrices_5 ...................   Passed    0.00 sec
        Start 178: commainitializer
178/801 Test #178: commainitializer .................   Passed    0.00 sec
        Start 179: smallvectors
179/801 Test #179: smallvectors .....................   Passed    0.01 sec
        Start 180: mapped_matrix_1
180/801 Test #180: mapped_matrix_1 ..................   Passed    0.00 sec
        Start 181: mapped_matrix_2
181/801 Test #181: mapped_matrix_2 ..................   Passed    0.00 sec
        Start 182: mapped_matrix_3
182/801 Test #182: mapped_matrix_3 ..................   Passed    0.00 sec
        Start 183: mapped_matrix_4
183/801 Test #183: mapped_matrix_4 ..................   Passed    0.00 sec
        Start 184: mapped_matrix_5
184/801 Test #184: mapped_matrix_5 ..................   Passed    0.00 sec
        Start 185: mapped_matrix_11
185/801 Test #185: mapped_matrix_11 .................   Passed    0.00 sec
        Start 186: mapped_matrix_6
186/801 Test #186: mapped_matrix_6 ..................   Passed    0.00 sec
        Start 187: mapped_matrix_7
187/801 Test #187: mapped_matrix_7 ..................   Passed    0.00 sec
        Start 188: mapped_matrix_8
188/801 Test #188: mapped_matrix_8 ..................   Passed    0.00 sec
        Start 189: mapped_matrix_9
189/801 Test #189: mapped_matrix_9 ..................   Passed    0.00 sec
        Start 190: mapped_matrix_10
190/801 Test #190: mapped_matrix_10 .................   Passed    0.00 sec
        Start 191: mapstride_1
191/801 Test #191: mapstride_1 ......................   Passed    0.00 sec
        Start 192: mapstride_2
192/801 Test #192: mapstride_2 ......................   Passed    0.00 sec
        Start 193: mapstride_3
193/801 Test #193: mapstride_3 ......................   Passed    0.00 sec
        Start 194: mapstride_4
194/801 Test #194: mapstride_4 ......................   Passed    0.00 sec
        Start 195: mapstride_5
195/801 Test #195: mapstride_5 ......................   Passed    0.00 sec
        Start 196: mapstride_6
196/801 Test #196: mapstride_6 ......................   Passed    0.00 sec
        Start 197: mapstaticmethods_1
197/801 Test #197: mapstaticmethods_1 ...............   Passed    0.00 sec
        Start 198: mapstaticmethods_2
198/801 Test #198: mapstaticmethods_2 ...............   Passed    0.00 sec
        Start 199: mapstaticmethods_3
199/801 Test #199: mapstaticmethods_3 ...............   Passed    0.00 sec
        Start 200: mapstaticmethods_4
200/801 Test #200: mapstaticmethods_4 ...............   Passed    0.00 sec
        Start 201: mapstaticmethods_5
201/801 Test #201: mapstaticmethods_5 ...............   Passed    0.00 sec
        Start 202: mapstaticmethods_6
202/801 Test #202: mapstaticmethods_6 ...............   Passed    0.00 sec
        Start 203: mapstaticmethods_7
203/801 Test #203: mapstaticmethods_7 ...............   Passed    0.00 sec
        Start 204: mapstaticmethods_8
204/801 Test #204: mapstaticmethods_8 ...............   Passed    0.00 sec
        Start 205: array_1
205/801 Test #205: array_1 ..........................   Passed    0.00 sec
        Start 206: array_2
206/801 Test #206: array_2 ..........................   Passed    0.00 sec
        Start 207: array_3
207/801 Test #207: array_3 ..........................   Passed    0.00 sec
        Start 208: array_4
208/801 Test #208: array_4 ..........................   Passed    1.14 sec
        Start 209: array_5
209/801 Test #209: array_5 ..........................   Passed    0.45 sec
        Start 210: array_6
210/801 Test #210: array_6 ..........................   Passed    0.07 sec
        Start 211: array_for_matrix_1
211/801 Test #211: array_for_matrix_1 ...............   Passed    0.00 sec
        Start 212: array_for_matrix_2
212/801 Test #212: array_for_matrix_2 ...............   Passed    0.00 sec
        Start 213: array_for_matrix_3
213/801 Test #213: array_for_matrix_3 ...............   Passed    0.00 sec
        Start 214: array_for_matrix_4
214/801 Test #214: array_for_matrix_4 ...............   Passed    0.04 sec
        Start 215: array_for_matrix_5
215/801 Test #215: array_for_matrix_5 ...............   Passed    0.05 sec
        Start 216: array_for_matrix_6
216/801 Test #216: array_for_matrix_6 ...............   Passed    0.05 sec
        Start 217: array_for_matrix_7
217/801 Test #217: array_for_matrix_7 ...............   Passed    0.00 sec
        Start 218: array_for_matrix_8
218/801 Test #218: array_for_matrix_8 ...............   Passed    0.00 sec
        Start 219: array_replicate_1
219/801 Test #219: array_replicate_1 ................   Passed    0.00 sec
        Start 220: array_replicate_2
220/801 Test #220: array_replicate_2 ................   Passed    0.00 sec
        Start 221: array_replicate_3
221/801 Test #221: array_replicate_3 ................   Passed    0.00 sec
        Start 222: array_replicate_4
222/801 Test #222: array_replicate_4 ................   Passed    0.00 sec
        Start 223: array_replicate_5
223/801 Test #223: array_replicate_5 ................   Passed    0.00 sec
        Start 224: array_replicate_6
224/801 Test #224: array_replicate_6 ................   Passed    0.00 sec
        Start 225: array_reverse_1
225/801 Test #225: array_reverse_1 ..................   Passed    0.00 sec
        Start 226: array_reverse_2
226/801 Test #226: array_reverse_2 ..................   Passed    0.00 sec
        Start 227: array_reverse_3
227/801 Test #227: array_reverse_3 ..................   Passed    0.00 sec
        Start 228: array_reverse_4
228/801 Test #228: array_reverse_4 ..................   Passed    0.00 sec
        Start 229: array_reverse_5
229/801 Test #229: array_reverse_5 ..................   Passed    0.03 sec
        Start 230: array_reverse_6
230/801 Test #230: array_reverse_6 ..................   Passed    0.03 sec
        Start 231: array_reverse_7
231/801 Test #231: array_reverse_7 ..................   Passed    0.04 sec
        Start 232: array_reverse_8
232/801 Test #232: array_reverse_8 ..................   Passed    0.01 sec
        Start 233: array_reverse_9
233/801 Test #233: array_reverse_9 ..................   Passed    0.03 sec
        Start 234: ref_1
234/801 Test #234: ref_1 ............................   Passed    0.00 sec
        Start 235: ref_2
235/801 Test #235: ref_2 ............................   Passed    0.00 sec
        Start 236: ref_3
236/801 Test #236: ref_3 ............................   Passed    0.00 sec
        Start 237: ref_4
237/801 Test #237: ref_4 ............................   Passed    0.00 sec
        Start 238: ref_5
238/801 Test #238: ref_5 ............................   Passed    0.00 sec
        Start 239: ref_6
239/801 Test #239: ref_6 ............................   Passed    0.00 sec
        Start 240: ref_7
240/801 Test #240: ref_7 ............................   Passed    0.00 sec
        Start 241: is_same_dense
241/801 Test #241: is_same_dense ....................   Passed    0.00 sec
        Start 242: triangular_1
242/801 Test #242: triangular_1 .....................   Passed    0.00 sec
        Start 243: triangular_2
243/801 Test #243: triangular_2 .....................   Passed    0.00 sec
        Start 244: triangular_3
244/801 Test #244: triangular_3 .....................   Passed    0.00 sec
        Start 245: triangular_4
245/801 Test #245: triangular_4 .....................   Passed    0.00 sec
        Start 246: triangular_5
246/801 Test #246: triangular_5 .....................   Passed    0.01 sec
        Start 247: triangular_6
247/801 Test #247: triangular_6 .....................   Passed    0.00 sec
        Start 248: triangular_7
248/801 Test #248: triangular_7 .....................   Passed    0.00 sec
        Start 249: triangular_8
249/801 Test #249: triangular_8 .....................   Passed    0.00 sec
        Start 250: triangular_9
250/801 Test #250: triangular_9 .....................   Passed    0.00 sec
        Start 251: selfadjoint_1
251/801 Test #251: selfadjoint_1 ....................   Passed    0.00 sec
        Start 252: selfadjoint_2
252/801 Test #252: selfadjoint_2 ....................   Passed    0.00 sec
        Start 253: selfadjoint_3
253/801 Test #253: selfadjoint_3 ....................   Passed    0.00 sec
        Start 254: selfadjoint_4
254/801 Test #254: selfadjoint_4 ....................   Passed    0.08 sec
        Start 255: selfadjoint_5
255/801 Test #255: selfadjoint_5 ....................   Passed    0.02 sec
        Start 256: product_selfadjoint_1
256/801 Test #256: product_selfadjoint_1 ............   Passed    0.00 sec
        Start 257: product_selfadjoint_2
257/801 Test #257: product_selfadjoint_2 ............   Passed    0.00 sec
        Start 258: product_selfadjoint_3
258/801 Test #258: product_selfadjoint_3 ............   Passed    0.00 sec
        Start 259: product_selfadjoint_4
259/801 Test #259: product_selfadjoint_4 ............   Passed    0.01 sec
        Start 260: product_selfadjoint_5
260/801 Test #260: product_selfadjoint_5 ............   Passed    0.03 sec
        Start 261: product_selfadjoint_6
261/801 Test #261: product_selfadjoint_6 ............   Passed    0.03 sec
        Start 262: product_selfadjoint_7
262/801 Test #262: product_selfadjoint_7 ............   Passed    0.03 sec
        Start 263: product_symm_1
263/801 Test #263: product_symm_1 ...................   Passed    0.30 sec
        Start 264: product_symm_2
264/801 Test #264: product_symm_2 ...................   Passed    0.59 sec
        Start 265: product_symm_3
265/801 Test #265: product_symm_3 ...................   Passed    0.19 sec
        Start 266: product_symm_4
266/801 Test #266: product_symm_4 ...................   Passed    0.37 sec
        Start 267: product_symm_5
267/801 Test #267: product_symm_5 ...................   Passed    0.03 sec
        Start 268: product_symm_6
268/801 Test #268: product_symm_6 ...................   Passed    0.03 sec
        Start 269: product_symm_7
269/801 Test #269: product_symm_7 ...................   Passed    0.04 sec
        Start 270: product_symm_8
270/801 Test #270: product_symm_8 ...................   Passed    0.05 sec
        Start 271: product_syrk_1
271/801 Test #271: product_syrk_1 ...................   Passed    0.13 sec
        Start 272: product_syrk_2
272/801 Test #272: product_syrk_2 ...................   Passed    0.26 sec
        Start 273: product_syrk_3
273/801 Test #273: product_syrk_3 ...................   Passed    0.20 sec
        Start 274: product_syrk_4
274/801 Test #274: product_syrk_4 ...................   Passed    0.36 sec
        Start 275: product_trmv_1
275/801 Test #275: product_trmv_1 ...................   Passed    0.00 sec
        Start 276: product_trmv_2
276/801 Test #276: product_trmv_2 ...................   Passed    0.00 sec
        Start 277: product_trmv_3
277/801 Test #277: product_trmv_3 ...................   Passed    0.00 sec
        Start 278: product_trmv_4
278/801 Test #278: product_trmv_4 ...................   Passed    0.01 sec
        Start 279: product_trmv_5
279/801 Test #279: product_trmv_5 ...................   Passed    0.02 sec
        Start 280: product_trmv_6
280/801 Test #280: product_trmv_6 ...................   Passed    0.02 sec
        Start 281: product_trmm_1
281/801 Test #281: product_trmm_1 ...................   Passed    0.00 sec
        Start 282: product_trmm_11
282/801 Test #282: product_trmm_11 ..................   Passed    1.27 sec
        Start 283: product_trmm_111
283/801 Test #283: product_trmm_111 .................   Passed    0.02 sec
        Start 284: product_trmm_21
284/801 Test #284: product_trmm_21 ..................   Passed    1.61 sec
        Start 285: product_trmm_121
285/801 Test #285: product_trmm_121 .................   Passed    0.02 sec
        Start 286: product_trmm_31
286/801 Test #286: product_trmm_31 ..................   Passed    1.57 sec
        Start 287: product_trmm_131
287/801 Test #287: product_trmm_131 .................   Passed    0.04 sec
        Start 288: product_trmm_12
288/801 Test #288: product_trmm_12 ..................   Passed    3.02 sec
        Start 289: product_trmm_112
289/801 Test #289: product_trmm_112 .................   Passed    0.03 sec
        Start 290: product_trmm_22
290/801 Test #290: product_trmm_22 ..................   Passed    2.45 sec
        Start 291: product_trmm_122
291/801 Test #291: product_trmm_122 .................   Passed    0.03 sec
        Start 292: product_trmm_32
292/801 Test #292: product_trmm_32 ..................   Passed    2.92 sec
        Start 293: product_trmm_132
293/801 Test #293: product_trmm_132 .................   Passed    0.03 sec
        Start 294: product_trmm_13
294/801 Test #294: product_trmm_13 ..................   Passed    0.93 sec
        Start 295: product_trmm_113
295/801 Test #295: product_trmm_113 .................   Passed    0.02 sec
        Start 296: product_trmm_23
296/801 Test #296: product_trmm_23 ..................   Passed    0.97 sec
        Start 297: product_trmm_123
297/801 Test #297: product_trmm_123 .................   Passed    0.02 sec
        Start 298: product_trmm_33
298/801 Test #298: product_trmm_33 ..................   Passed    1.13 sec
        Start 299: product_trmm_133
299/801 Test #299: product_trmm_133 .................   Passed    0.02 sec
        Start 300: product_trmm_14
300/801 Test #300: product_trmm_14 ..................   Passed    1.66 sec
        Start 301: product_trmm_114
301/801 Test #301: product_trmm_114 .................   Passed    0.03 sec
        Start 302: product_trmm_24
302/801 Test #302: product_trmm_24 ..................   Passed    2.06 sec
        Start 303: product_trmm_124
303/801 Test #303: product_trmm_124 .................   Passed    0.03 sec
        Start 304: product_trmm_34
304/801 Test #304: product_trmm_34 ..................   Passed    1.87 sec
        Start 305: product_trmm_134
305/801 Test #305: product_trmm_134 .................   Passed    0.02 sec
        Start 306: product_trsolve_1
306/801 Test #306: product_trsolve_1 ................   Passed    0.34 sec
        Start 307: product_trsolve_2
307/801 Test #307: product_trsolve_2 ................   Passed    0.60 sec
        Start 308: product_trsolve_3
308/801 Test #308: product_trsolve_3 ................   Passed    0.26 sec
        Start 309: product_trsolve_4
309/801 Test #309: product_trsolve_4 ................   Passed    0.39 sec
        Start 310: product_trsolve_5
310/801 Test #310: product_trsolve_5 ................   Passed    0.03 sec
        Start 311: product_trsolve_6
311/801 Test #311: product_trsolve_6 ................   Passed    0.04 sec
        Start 312: product_trsolve_7
312/801 Test #312: product_trsolve_7 ................   Passed    0.06 sec
        Start 313: product_trsolve_8
313/801 Test #313: product_trsolve_8 ................   Passed    0.08 sec
        Start 314: product_trsolve_9
314/801 Test #314: product_trsolve_9 ................   Passed    0.00 sec
        Start 315: product_trsolve_10
315/801 Test #315: product_trsolve_10 ...............   Passed    0.00 sec
        Start 316: product_trsolve_11
316/801 Test #316: product_trsolve_11 ...............   Passed    0.00 sec
        Start 317: product_trsolve_12
317/801 Test #317: product_trsolve_12 ...............   Passed    0.00 sec
        Start 318: product_trsolve_13
318/801 Test #318: product_trsolve_13 ...............   Passed    0.00 sec
        Start 319: product_trsolve_14
319/801 Test #319: product_trsolve_14 ...............   Passed    0.00 sec
        Start 320: product_mmtr_1
320/801 Test #320: product_mmtr_1 ...................   Passed    0.15 sec
        Start 321: product_mmtr_2
321/801 Test #321: product_mmtr_2 ...................   Passed    0.30 sec
        Start 322: product_mmtr_3
322/801 Test #322: product_mmtr_3 ...................   Passed    0.13 sec
        Start 323: product_mmtr_4
323/801 Test #323: product_mmtr_4 ...................   Passed    0.61 sec
        Start 324: product_notemporary_1
324/801 Test #324: product_notemporary_1 ............   Passed    0.21 sec
        Start 325: product_notemporary_2
325/801 Test #325: product_notemporary_2 ............   Passed    0.43 sec
        Start 326: product_notemporary_3
326/801 Test #326: product_notemporary_3 ............   Passed    0.31 sec
        Start 327: product_notemporary_4
327/801 Test #327: product_notemporary_4 ............   Passed    0.63 sec
        Start 328: stable_norm_1
328/801 Test #328: stable_norm_1 ....................   Passed    0.00 sec
        Start 329: stable_norm_2
329/801 Test #329: stable_norm_2 ....................   Passed    0.00 sec
        Start 330: stable_norm_3
330/801 Test #330: stable_norm_3 ....................   Passed    0.01 sec
        Start 331: stable_norm_4
331/801 Test #331: stable_norm_4 ....................   Passed    0.01 sec
        Start 332: stable_norm_5
332/801 Test #332: stable_norm_5 ....................   Passed    0.03 sec
        Start 333: permutationmatrices_1
333/801 Test #333: permutationmatrices_1 ............   Passed    0.00 sec
        Start 334: permutationmatrices_2
334/801 Test #334: permutationmatrices_2 ............   Passed    0.00 sec
        Start 335: permutationmatrices_3
335/801 Test #335: permutationmatrices_3 ............   Passed    0.00 sec
        Start 336: permutationmatrices_4
336/801 Test #336: permutationmatrices_4 ............   Passed    0.00 sec
        Start 337: permutationmatrices_5
337/801 Test #337: permutationmatrices_5 ............   Passed    0.01 sec
        Start 338: permutationmatrices_6
338/801 Test #338: permutationmatrices_6 ............   Passed    0.01 sec
        Start 339: permutationmatrices_7
339/801 Test #339: permutationmatrices_7 ............   Passed    0.00 sec
        Start 340: bandmatrix
340/801 Test #340: bandmatrix .......................   Passed    0.00 sec
        Start 341: cholesky_1
341/801 Test #341: cholesky_1 .......................   Passed    0.00 sec
        Start 342: cholesky_3
342/801 Test #342: cholesky_3 .......................   Passed    0.00 sec
        Start 343: cholesky_4
343/801 Test #343: cholesky_4 .......................   Passed    0.00 sec
        Start 344: cholesky_5
344/801 Test #344: cholesky_5 .......................   Passed    0.00 sec
        Start 345: cholesky_2
345/801 Test #345: cholesky_2 .......................   Passed    2.54 sec
        Start 346: cholesky_6
346/801 Test #346: cholesky_6 .......................   Passed    1.06 sec
        Start 347: cholesky_7
347/801 Test #347: cholesky_7 .......................   Passed    0.00 sec
        Start 348: cholesky_8
348/801 Test #348: cholesky_8 .......................   Passed    0.00 sec
        Start 349: cholesky_9
349/801 Test #349: cholesky_9 .......................   Passed    0.00 sec
        Start 350: lu_1
350/801 Test #350: lu_1 .............................   Passed    0.01 sec
        Start 351: lu_2
351/801 Test #351: lu_2 .............................   Passed    0.00 sec
        Start 352: lu_3
352/801 Test #352: lu_3 .............................   Passed    0.67 sec
        Start 353: lu_4
353/801 Test #353: lu_4 .............................   Passed    0.58 sec
        Start 354: lu_5
354/801 Test #354: lu_5 .............................   Passed    3.34 sec
        Start 355: lu_6
355/801 Test #355: lu_6 .............................   Passed    5.06 sec
        Start 356: lu_7
356/801 Test #356: lu_7 .............................   Passed    0.02 sec
        Start 357: lu_9
357/801 Test #357: lu_9 .............................   Passed    0.00 sec
        Start 358: determinant_1
358/801 Test #358: determinant_1 ....................   Passed    0.00 sec
        Start 359: determinant_2
359/801 Test #359: determinant_2 ....................   Passed    0.00 sec
        Start 360: determinant_3
360/801 Test #360: determinant_3 ....................   Passed    0.00 sec
        Start 361: determinant_4
361/801 Test #361: determinant_4 ....................   Passed    0.00 sec
        Start 362: determinant_5
362/801 Test #362: determinant_5 ....................   Passed    0.00 sec
        Start 363: determinant_6
363/801 Test #363: determinant_6 ....................   Passed    0.02 sec
        Start 364: inverse_5
364/801 Test #364: inverse_5 ........................   Passed    0.58 sec
        Start 365: inverse_6
365/801 Test #365: inverse_6 ........................   Passed    0.16 sec
        Start 366: inverse_1
366/801 Test #366: inverse_1 ........................   Passed    0.00 sec
        Start 367: inverse_2
367/801 Test #367: inverse_2 ........................   Passed    0.00 sec
        Start 368: inverse_3
368/801 Test #368: inverse_3 ........................   Passed    0.00 sec
        Start 369: inverse_4
369/801 Test #369: inverse_4 ........................   Passed    0.00 sec
        Start 370: inverse_7
370/801 Test #370: inverse_7 ........................   Passed    0.00 sec
        Start 371: qr_1
371/801 Test #371: qr_1 .............................   Passed    0.06 sec
        Start 372: qr_2
372/801 Test #372: qr_2 .............................   Passed    0.04 sec
        Start 373: qr_3
373/801 Test #373: qr_3 .............................   Passed    0.00 sec
        Start 374: qr_4
374/801 Test #374: qr_4 .............................   Passed    0.00 sec
        Start 375: qr_5
375/801 Test #375: qr_5 .............................   Passed    0.00 sec
        Start 376: qr_11
376/801 Test #376: qr_11 ............................   Passed    0.00 sec
        Start 377: qr_6
377/801 Test #377: qr_6 .............................   Passed    0.01 sec
        Start 378: qr_7
378/801 Test #378: qr_7 .............................   Passed    0.01 sec
        Start 379: qr_8
379/801 Test #379: qr_8 .............................   Passed    0.01 sec
        Start 380: qr_9
380/801 Test #380: qr_9 .............................   Passed    0.00 sec
        Start 381: qr_10
381/801 Test #381: qr_10 ............................   Passed    0.00 sec
        Start 382: qr_12
382/801 Test #382: qr_12 ............................   Passed    0.00 sec
        Start 383: qr_colpivoting_1
383/801 Test #383: qr_colpivoting_1 .................   Passed    0.47 sec
        Start 384: qr_colpivoting_2
384/801 Test #384: qr_colpivoting_2 .................   Passed    1.06 sec
        Start 385: qr_colpivoting_3
385/801 Test #385: qr_colpivoting_3 .................   Passed    3.64 sec
        Start 386: qr_colpivoting_4
386/801 Test #386: qr_colpivoting_4 .................   Passed    0.00 sec
        Start 387: qr_colpivoting_5
387/801 Test #387: qr_colpivoting_5 .................   Passed    0.00 sec
        Start 388: qr_colpivoting_6
388/801 Test #388: qr_colpivoting_6 .................   Passed    0.01 sec
        Start 389: qr_colpivoting_7
389/801 Test #389: qr_colpivoting_7 .................   Passed    0.00 sec
        Start 390: qr_colpivoting_8
390/801 Test #390: qr_colpivoting_8 .................   Passed    0.00 sec
        Start 391: qr_colpivoting_9
391/801 Test #391: qr_colpivoting_9 .................   Passed    0.00 sec
        Start 392: qr_fullpivoting_1
392/801 Test #392: qr_fullpivoting_1 ................   Passed    0.06 sec
        Start 393: qr_fullpivoting_2
393/801 Test #393: qr_fullpivoting_2 ................   Passed    0.11 sec
        Start 394: qr_fullpivoting_3
394/801 Test #394: qr_fullpivoting_3 ................   Passed    0.50 sec
        Start 395: qr_fullpivoting_4
395/801 Test #395: qr_fullpivoting_4 ................   Passed    0.02 sec
        Start 396: qr_fullpivoting_5
396/801 Test #396: qr_fullpivoting_5 ................   Passed    0.00 sec
        Start 397: qr_fullpivoting_6
397/801 Test #397: qr_fullpivoting_6 ................   Passed    0.00 sec
        Start 398: qr_fullpivoting_7
398/801 Test #398: qr_fullpivoting_7 ................   Passed    0.00 sec
        Start 399: upperbidiagonalization_1
399/801 Test #399: upperbidiagonalization_1 .........   Passed    0.00 sec
        Start 400: upperbidiagonalization_2
400/801 Test #400: upperbidiagonalization_2 .........   Passed    0.00 sec
        Start 401: upperbidiagonalization_3
401/801 Test #401: upperbidiagonalization_3 .........   Passed    0.01 sec
        Start 402: upperbidiagonalization_4
402/801 Test #402: upperbidiagonalization_4 .........   Passed    0.00 sec
        Start 403: upperbidiagonalization_5
403/801 Test #403: upperbidiagonalization_5 .........   Passed    0.00 sec
        Start 404: upperbidiagonalization_6
404/801 Test #404: upperbidiagonalization_6 .........   Passed    0.00 sec
        Start 405: upperbidiagonalization_7
405/801 Test #405: upperbidiagonalization_7 .........   Passed    0.00 sec
        Start 406: hessenberg_1
406/801 Test #406: hessenberg_1 .....................   Passed    0.00 sec
        Start 407: hessenberg_2
407/801 Test #407: hessenberg_2 .....................   Passed    0.00 sec
        Start 408: hessenberg_3
408/801 Test #408: hessenberg_3 .....................   Passed    0.00 sec
        Start 409: hessenberg_4
409/801 Test #409: hessenberg_4 .....................   Passed    0.00 sec
        Start 410: hessenberg_5
410/801 Test #410: hessenberg_5 .....................   Passed    0.00 sec
        Start 411: hessenberg_6
411/801 Test #411: hessenberg_6 .....................   Passed    0.00 sec
        Start 412: schur_real_1
412/801 Test #412: schur_real_1 .....................   Passed    0.00 sec
        Start 413: schur_real_2
413/801 Test #413: schur_real_2 .....................   Passed    0.00 sec
        Start 414: schur_real_3
414/801 Test #414: schur_real_3 .....................   Passed    0.00 sec
        Start 415: schur_real_4
415/801 Test #415: schur_real_4 .....................   Passed    0.00 sec
        Start 416: schur_real_5
416/801 Test #416: schur_real_5 .....................   Passed    0.00 sec
        Start 417: schur_complex_1
417/801 Test #417: schur_complex_1 ..................   Passed    0.00 sec
        Start 418: schur_complex_2
418/801 Test #418: schur_complex_2 ..................***Exception: Other  0.18 sec
        Start 419: schur_complex_3
419/801 Test #419: schur_complex_3 ..................   Passed    0.00 sec
        Start 420: schur_complex_4
420/801 Test #420: schur_complex_4 ..................   Passed    0.00 sec
        Start 421: schur_complex_5
421/801 Test #421: schur_complex_5 ..................   Passed    0.00 sec
        Start 422: eigensolver_selfadjoint_1
422/801 Test #422: eigensolver_selfadjoint_1 ........   Passed    0.00 sec
        Start 423: eigensolver_selfadjoint_12
423/801 Test #423: eigensolver_selfadjoint_12 .......   Passed    0.00 sec
        Start 424: eigensolver_selfadjoint_13
424/801 Test #424: eigensolver_selfadjoint_13 .......   Passed    0.01 sec
        Start 425: eigensolver_selfadjoint_2
425/801 Test #425: eigensolver_selfadjoint_2 ........   Passed    0.01 sec
        Start 426: eigensolver_selfadjoint_3
426/801 Test #426: eigensolver_selfadjoint_3 ........   Passed    0.04 sec
        Start 427: eigensolver_selfadjoint_4
427/801 Test #427: eigensolver_selfadjoint_4 ........   Passed    0.14 sec
        Start 428: eigensolver_selfadjoint_5
428/801 Test #428: eigensolver_selfadjoint_5 ........   Passed    0.29 sec
        Start 429: eigensolver_selfadjoint_9
429/801 Test #429: eigensolver_selfadjoint_9 ........   Passed    0.24 sec
        Start 430: eigensolver_selfadjoint_6
430/801 Test #430: eigensolver_selfadjoint_6 ........   Passed    0.00 sec
        Start 431: eigensolver_selfadjoint_7
431/801 Test #431: eigensolver_selfadjoint_7 ........   Passed    0.00 sec
        Start 432: eigensolver_selfadjoint_8
432/801 Test #432: eigensolver_selfadjoint_8 ........   Passed    0.00 sec
        Start 433: eigensolver_generic_1
433/801 Test #433: eigensolver_generic_1 ............   Passed    0.01 sec
        Start 434: eigensolver_generic_2
434/801 Test #434: eigensolver_generic_2 ............   Passed    0.20 sec
        Start 435: eigensolver_generic_3
435/801 Test #435: eigensolver_generic_3 ............   Passed    0.00 sec
        Start 436: eigensolver_generic_4
436/801 Test #436: eigensolver_generic_4 ............   Passed    0.00 sec
        Start 437: eigensolver_generic_5
437/801 Test #437: eigensolver_generic_5 ............   Passed    0.00 sec
        Start 438: eigensolver_complex_1
438/801 Test #438: eigensolver_complex_1 ............   Passed    0.02 sec
        Start 439: eigensolver_complex_2
439/801 Test #439: eigensolver_complex_2 ............   Passed    0.65 sec
        Start 440: eigensolver_complex_3
440/801 Test #440: eigensolver_complex_3 ............   Passed    0.00 sec
        Start 441: eigensolver_complex_4
441/801 Test #441: eigensolver_complex_4 ............   Passed    0.01 sec
        Start 442: eigensolver_complex_5
442/801 Test #442: eigensolver_complex_5 ............   Passed    0.00 sec
        Start 443: real_qz_1
443/801 Test #443: real_qz_1 ........................   Passed    0.00 sec
        Start 444: real_qz_2
444/801 Test #444: real_qz_2 ........................   Passed    0.11 sec
        Start 445: real_qz_3
445/801 Test #445: real_qz_3 ........................   Passed    0.00 sec
        Start 446: real_qz_4
446/801 Test #446: real_qz_4 ........................   Passed    0.00 sec
        Start 447: eigensolver_generalized_real_1
447/801 Test #447: eigensolver_generalized_real_1 ...   Passed    0.00 sec
        Start 448: eigensolver_generalized_real_2
448/801 Test #448: eigensolver_generalized_real_2 ...   Passed    0.32 sec
        Start 449: eigensolver_generalized_real_3
449/801 Test #449: eigensolver_generalized_real_3 ...   Passed    0.00 sec
        Start 450: eigensolver_generalized_real_4
450/801 Test #450: eigensolver_generalized_real_4 ...   Passed    0.00 sec
        Start 451: jacobi_1
451/801 Test #451: jacobi_1 .........................   Passed    0.00 sec
        Start 452: jacobi_2
452/801 Test #452: jacobi_2 .........................   Passed    0.00 sec
        Start 453: jacobi_3
453/801 Test #453: jacobi_3 .........................   Passed    0.00 sec
        Start 454: jacobi_4
454/801 Test #454: jacobi_4 .........................   Passed    0.00 sec
        Start 455: jacobi_5
455/801 Test #455: jacobi_5 .........................   Passed    0.01 sec
        Start 456: jacobi_6
456/801 Test #456: jacobi_6 .........................   Passed    0.00 sec
        Start 457: jacobisvd_3
457/801 Test #457: jacobisvd_3 ......................   Passed    0.01 sec
        Start 458: jacobisvd_4
458/801 Test #458: jacobisvd_4 ......................   Passed    0.01 sec
        Start 459: jacobisvd_7
459/801 Test #459: jacobisvd_7 ......................   Passed   24.78 sec
        Start 460: jacobisvd_8
460/801 Test #460: jacobisvd_8 ......................   Passed   63.59 sec
        Start 461: jacobisvd_11
461/801 Test #461: jacobisvd_11 .....................   Passed    0.01 sec
        Start 462: jacobisvd_12
462/801 Test #462: jacobisvd_12 .....................   Passed    0.01 sec
        Start 463: jacobisvd_5
463/801 Test #463: jacobisvd_5 ......................   Passed    0.01 sec
        Start 464: jacobisvd_6
464/801 Test #464: jacobisvd_6 ......................   Passed    0.01 sec
        Start 465: jacobisvd_10
465/801 Test #465: jacobisvd_10 .....................   Passed    0.16 sec
        Start 466: jacobisvd_13
466/801 Test #466: jacobisvd_13 .....................   Passed    0.00 sec
        Start 467: jacobisvd_1
467/801 Test #467: jacobisvd_1 ......................   Passed    0.00 sec
        Start 468: jacobisvd_9
468/801 Test #468: jacobisvd_9 ......................   Passed    0.00 sec
        Start 469: jacobisvd_2
469/801 Test #469: jacobisvd_2 ......................   Passed    0.02 sec
        Start 470: bdcsvd_3
470/801 Test #470: bdcsvd_3 .........................   Passed    0.00 sec
        Start 471: bdcsvd_4
471/801 Test #471: bdcsvd_4 .........................   Passed    0.00 sec
        Start 472: bdcsvd_7
472/801 Test #472: bdcsvd_7 .........................   Passed   19.59 sec
        Start 473: bdcsvd_8
473/801 Test #473: bdcsvd_8 .........................   Passed   99.59 sec
        Start 474: bdcsvd_101
474/801 Test #474: bdcsvd_101 .......................   Passed    0.01 sec
        Start 475: bdcsvd_102
475/801 Test #475: bdcsvd_102 .......................   Passed    0.01 sec
        Start 476: bdcsvd_5
476/801 Test #476: bdcsvd_5 .........................   Passed    0.01 sec
        Start 477: bdcsvd_6
477/801 Test #477: bdcsvd_6 .........................   Passed    0.07 sec
        Start 478: bdcsvd_10
478/801 Test #478: bdcsvd_10 ........................   Passed   20.31 sec
        Start 479: bdcsvd_1
479/801 Test #479: bdcsvd_1 .........................   Passed    0.00 sec
        Start 480: bdcsvd_9
480/801 Test #480: bdcsvd_9 .........................***Exception: Other  0.15 sec
        Start 481: bdcsvd_2
481/801 Test #481: bdcsvd_2 .........................   Passed    0.02 sec
        Start 482: householder_1
482/801 Test #482: householder_1 ....................   Passed    0.00 sec
        Start 483: householder_2
483/801 Test #483: householder_2 ....................   Passed    0.00 sec
        Start 484: householder_3
484/801 Test #484: householder_3 ....................   Passed    0.00 sec
        Start 485: householder_4
485/801 Test #485: householder_4 ....................   Passed    0.00 sec
        Start 486: householder_5
486/801 Test #486: householder_5 ....................   Passed    0.81 sec
        Start 487: householder_6
487/801 Test #487: householder_6 ....................   Passed    1.49 sec
        Start 488: householder_7
488/801 Test #488: householder_7 ....................   Passed    0.09 sec
        Start 489: householder_8
489/801 Test #489: householder_8 ....................   Passed    0.00 sec
        Start 490: geo_orthomethods_1
490/801 Test #490: geo_orthomethods_1 ...............   Passed    0.00 sec
        Start 491: geo_orthomethods_2
491/801 Test #491: geo_orthomethods_2 ...............   Passed    0.00 sec
        Start 492: geo_orthomethods_4
492/801 Test #492: geo_orthomethods_4 ...............   Passed    0.00 sec
        Start 493: geo_orthomethods_3
493/801 Test #493: geo_orthomethods_3 ...............   Passed    0.00 sec
        Start 494: geo_orthomethods_5
494/801 Test #494: geo_orthomethods_5 ...............   Passed    0.00 sec
        Start 495: geo_orthomethods_6
495/801 Test #495: geo_orthomethods_6 ...............   Passed    0.00 sec
        Start 496: geo_quaternion_1
496/801 Test #496: geo_quaternion_1 .................   Passed    0.00 sec
        Start 497: geo_quaternion_2
497/801 Test #497: geo_quaternion_2 .................   Passed    0.00 sec
        Start 498: geo_quaternion_3
498/801 Test #498: geo_quaternion_3 .................   Passed    0.00 sec
        Start 499: geo_quaternion_4
499/801 Test #499: geo_quaternion_4 .................   Passed    0.00 sec
        Start 500: geo_quaternion_5
500/801 Test #500: geo_quaternion_5 .................   Passed    0.00 sec
        Start 501: geo_quaternion_6
501/801 Test #501: geo_quaternion_6 .................   Passed    0.00 sec
        Start 502: geo_eulerangles_1
502/801 Test #502: geo_eulerangles_1 ................   Passed    0.00 sec
        Start 503: geo_eulerangles_2
503/801 Test #503: geo_eulerangles_2 ................   Passed    0.00 sec
        Start 504: geo_parametrizedline_1
504/801 Test #504: geo_parametrizedline_1 ...........   Passed    0.00 sec
        Start 505: geo_parametrizedline_2
505/801 Test #505: geo_parametrizedline_2 ...........   Passed    0.00 sec
        Start 506: geo_parametrizedline_3
506/801 Test #506: geo_parametrizedline_3 ...........   Passed    0.00 sec
        Start 507: geo_parametrizedline_4
507/801 Test #507: geo_parametrizedline_4 ...........   Passed    0.00 sec
        Start 508: geo_alignedbox_1
508/801 Test #508: geo_alignedbox_1 .................   Passed    0.00 sec
        Start 509: geo_alignedbox_2
509/801 Test #509: geo_alignedbox_2 .................   Passed    0.00 sec
        Start 510: geo_alignedbox_3
510/801 Test #510: geo_alignedbox_3 .................   Passed    0.00 sec
        Start 511: geo_alignedbox_4
511/801 Test #511: geo_alignedbox_4 .................   Passed    0.00 sec
        Start 512: geo_alignedbox_5
512/801 Test #512: geo_alignedbox_5 .................   Passed    0.00 sec
        Start 513: geo_alignedbox_6
513/801 Test #513: geo_alignedbox_6 .................   Passed    0.00 sec
        Start 514: geo_alignedbox_7
514/801 Test #514: geo_alignedbox_7 .................   Passed    0.00 sec
        Start 515: geo_alignedbox_8
515/801 Test #515: geo_alignedbox_8 .................   Passed    0.00 sec
        Start 516: geo_alignedbox_9
516/801 Test #516: geo_alignedbox_9 .................   Passed    0.00 sec
        Start 517: geo_alignedbox_10
517/801 Test #517: geo_alignedbox_10 ................   Passed    0.00 sec
        Start 518: geo_alignedbox_11
518/801 Test #518: geo_alignedbox_11 ................   Passed    0.00 sec
        Start 519: geo_alignedbox_14
519/801 Test #519: geo_alignedbox_14 ................   Passed    0.00 sec
        Start 520: geo_alignedbox_12
520/801 Test #520: geo_alignedbox_12 ................   Passed    0.00 sec
        Start 521: geo_alignedbox_13
521/801 Test #521: geo_alignedbox_13 ................   Passed    0.00 sec
        Start 522: geo_hyperplane_1
522/801 Test #522: geo_hyperplane_1 .................   Passed    0.00 sec
        Start 523: geo_hyperplane_2
523/801 Test #523: geo_hyperplane_2 .................   Passed    0.00 sec
        Start 524: geo_hyperplane_3
524/801 Test #524: geo_hyperplane_3 .................   Passed    0.00 sec
        Start 525: geo_hyperplane_4
525/801 Test #525: geo_hyperplane_4 .................   Passed    0.00 sec
        Start 526: geo_hyperplane_5
526/801 Test #526: geo_hyperplane_5 .................   Passed    0.00 sec
        Start 527: geo_transformations_1
527/801 Test #527: geo_transformations_1 ............   Passed    0.00 sec
        Start 528: geo_transformations_2
528/801 Test #528: geo_transformations_2 ............   Passed    0.01 sec
        Start 529: geo_transformations_3
529/801 Test #529: geo_transformations_3 ............   Passed    0.01 sec
        Start 530: geo_transformations_4
530/801 Test #530: geo_transformations_4 ............   Passed    0.00 sec
        Start 531: geo_transformations_5
531/801 Test #531: geo_transformations_5 ............   Passed    0.01 sec
        Start 532: geo_transformations_6
532/801 Test #532: geo_transformations_6 ............   Passed    0.01 sec
        Start 533: geo_transformations_7
533/801 Test #533: geo_transformations_7 ............   Passed    0.00 sec
        Start 534: geo_transformations_8
534/801 Test #534: geo_transformations_8 ............   Passed    0.00 sec
        Start 535: geo_homogeneous_1
535/801 Test #535: geo_homogeneous_1 ................   Passed    0.00 sec
        Start 536: geo_homogeneous_2
536/801 Test #536: geo_homogeneous_2 ................   Passed    0.00 sec
        Start 537: geo_homogeneous_3
537/801 Test #537: geo_homogeneous_3 ................   Passed    0.00 sec
        Start 538: stdvector_1
538/801 Test #538: stdvector_1 ......................   Passed    0.00 sec
        Start 539: stdvector_2
539/801 Test #539: stdvector_2 ......................   Passed    0.00 sec
        Start 540: stdvector_3
540/801 Test #540: stdvector_3 ......................   Passed    0.00 sec
        Start 541: stdvector_4
541/801 Test #541: stdvector_4 ......................   Passed    0.00 sec
        Start 542: stdvector_5
542/801 Test #542: stdvector_5 ......................   Passed    0.00 sec
        Start 543: stdvector_overload_1
543/801 Test #543: stdvector_overload_1 .............   Passed    0.00 sec
        Start 544: stdvector_overload_2
544/801 Test #544: stdvector_overload_2 .............   Passed    0.00 sec
        Start 545: stdvector_overload_3
545/801 Test #545: stdvector_overload_3 .............   Passed    0.00 sec
        Start 546: stdvector_overload_4
546/801 Test #546: stdvector_overload_4 .............   Passed    0.00 sec
        Start 547: stdvector_overload_5
547/801 Test #547: stdvector_overload_5 .............   Passed    0.00 sec
        Start 548: stdlist_1
548/801 Test #548: stdlist_1 ........................   Passed    0.00 sec
        Start 549: stdlist_2
549/801 Test #549: stdlist_2 ........................   Passed    0.00 sec
        Start 550: stdlist_3
550/801 Test #550: stdlist_3 ........................   Passed    0.00 sec
        Start 551: stdlist_4
551/801 Test #551: stdlist_4 ........................   Passed    0.00 sec
        Start 552: stdlist_5
552/801 Test #552: stdlist_5 ........................   Passed    0.00 sec
        Start 553: stdlist_overload_1
553/801 Test #553: stdlist_overload_1 ...............   Passed    0.00 sec
        Start 554: stdlist_overload_2
554/801 Test #554: stdlist_overload_2 ...............   Passed    0.00 sec
        Start 555: stdlist_overload_3
555/801 Test #555: stdlist_overload_3 ...............   Passed    0.00 sec
        Start 556: stdlist_overload_4
556/801 Test #556: stdlist_overload_4 ...............   Passed    0.00 sec
        Start 557: stdlist_overload_5
557/801 Test #557: stdlist_overload_5 ...............   Passed    0.00 sec
        Start 558: stddeque_1
558/801 Test #558: stddeque_1 .......................   Passed    0.00 sec
        Start 559: stddeque_2
559/801 Test #559: stddeque_2 .......................   Passed    0.00 sec
        Start 560: stddeque_3
560/801 Test #560: stddeque_3 .......................   Passed    0.00 sec
        Start 561: stddeque_4
561/801 Test #561: stddeque_4 .......................   Passed    0.00 sec
        Start 562: stddeque_5
562/801 Test #562: stddeque_5 .......................   Passed    0.00 sec
        Start 563: stddeque_overload_1
563/801 Test #563: stddeque_overload_1 ..............   Passed    0.00 sec
        Start 564: stddeque_overload_2
564/801 Test #564: stddeque_overload_2 ..............   Passed    0.00 sec
        Start 565: stddeque_overload_3
565/801 Test #565: stddeque_overload_3 ..............   Passed    0.00 sec
        Start 566: stddeque_overload_4
566/801 Test #566: stddeque_overload_4 ..............   Passed    0.00 sec
        Start 567: stddeque_overload_5
567/801 Test #567: stddeque_overload_5 ..............   Passed    0.00 sec
        Start 568: sparse_basic_1
568/801 Test #568: sparse_basic_1 ...................   Passed    3.47 sec
        Start 569: sparse_basic_2
569/801 Test #569: sparse_basic_2 ...................   Passed   10.31 sec
        Start 570: sparse_basic_5
570/801 Test #570: sparse_basic_5 ...................   Passed   12.76 sec
        Start 571: sparse_basic_6
571/801 Test #571: sparse_basic_6 ...................***Exception: Other  0.57 sec
        Start 572: sparse_basic_3
572/801 Test #572: sparse_basic_3 ...................   Passed    1.58 sec
        Start 573: sparse_basic_4
573/801 Test #573: sparse_basic_4 ...................   Passed    1.91 sec
        Start 574: sparse_basic_7
574/801 Test #574: sparse_basic_7 ...................   Passed    0.01 sec
        Start 575: sparse_block_1
575/801 Test #575: sparse_block_1 ...................   Passed    0.08 sec
        Start 576: sparse_block_2
576/801 Test #576: sparse_block_2 ...................   Passed    0.23 sec
        Start 577: sparse_block_3
577/801 Test #577: sparse_block_3 ...................   Passed    0.12 sec
        Start 578: sparse_block_4
578/801 Test #578: sparse_block_4 ...................   Passed    0.03 sec
        Start 579: sparse_vector_1
579/801 Test #579: sparse_vector_1 ..................   Passed    0.04 sec
        Start 580: sparse_vector_2
580/801 Test #580: sparse_vector_2 ..................   Passed    0.02 sec
        Start 581: sparse_product_1
581/801 Test #581: sparse_product_1 .................   Passed    0.23 sec
        Start 582: sparse_product_2
582/801 Test #582: sparse_product_2 .................   Passed    0.76 sec
        Start 583: sparse_product_3
583/801 Test #583: sparse_product_3 .................   Passed    0.09 sec
        Start 584: sparse_product_4
584/801 Test #584: sparse_product_4 .................   Passed    0.01 sec
        Start 585: sparse_ref_1
585/801 Test #585: sparse_ref_1 .....................   Passed    0.00 sec
        Start 586: sparse_ref_2
586/801 Test #586: sparse_ref_2 .....................   Passed    0.00 sec
        Start 587: sparse_ref_3
587/801 Test #587: sparse_ref_3 .....................   Passed    0.00 sec
        Start 588: sparse_solvers_1
588/801 Test #588: sparse_solvers_1 .................   Passed    0.11 sec
        Start 589: sparse_solvers_2
589/801 Test #589: sparse_solvers_2 .................   Passed    0.25 sec
        Start 590: sparse_permutations_1
590/801 Test #590: sparse_permutations_1 ............   Passed    0.01 sec
        Start 591: sparse_permutations_2
591/801 Test #591: sparse_permutations_2 ............   Passed    0.02 sec
        Start 592: simplicial_cholesky_1
592/801 Test #592: simplicial_cholesky_1 ............   Passed    4.04 sec
        Start 593: simplicial_cholesky_2
593/801 Test #593: simplicial_cholesky_2 ............   Passed   15.38 sec
        Start 594: simplicial_cholesky_3
594/801 Test #594: simplicial_cholesky_3 ............   Passed    3.87 sec
        Start 595: conjugate_gradient_1
595/801 Test #595: conjugate_gradient_1 .............   Passed    3.65 sec
        Start 596: conjugate_gradient_2
596/801 Test #596: conjugate_gradient_2 .............   Passed   12.98 sec
        Start 597: conjugate_gradient_3
597/801 Test #597: conjugate_gradient_3 .............   Passed    4.66 sec
        Start 598: incomplete_cholesky_1
598/801 Test #598: incomplete_cholesky_1 ............   Passed    3.56 sec
        Start 599: incomplete_cholesky_2
599/801 Test #599: incomplete_cholesky_2 ............   Passed    7.77 sec
        Start 600: incomplete_cholesky_3
600/801 Test #600: incomplete_cholesky_3 ............   Passed    4.28 sec
        Start 601: bicgstab_1
601/801 Test #601: bicgstab_1 .......................   Passed    0.50 sec
        Start 602: bicgstab_2
602/801 Test #602: bicgstab_2 .......................   Passed    2.16 sec
        Start 603: bicgstab_3
603/801 Test #603: bicgstab_3 .......................   Passed    0.29 sec
        Start 604: lscg_1
604/801 Test #604: lscg_1 ...........................   Passed    1.82 sec
        Start 605: lscg_2
605/801 Test #605: lscg_2 ...........................   Passed    8.44 sec
        Start 606: sparselu_1
606/801 Test #606: sparselu_1 .......................   Passed    1.14 sec
        Start 607: sparselu_2
607/801 Test #607: sparselu_2 .......................   Passed    0.82 sec
        Start 608: sparselu_3
608/801 Test #608: sparselu_3 .......................   Passed    2.09 sec
        Start 609: sparselu_4
609/801 Test #609: sparselu_4 .......................   Passed    2.71 sec
        Start 610: sparseqr_1
610/801 Test #610: sparseqr_1 .......................   Passed    0.96 sec
        Start 611: sparseqr_2
611/801 Test #611: sparseqr_2 .......................   Passed    7.27 sec
        Start 612: umeyama_1
612/801 Test #612: umeyama_1 ........................   Passed    0.01 sec
        Start 613: umeyama_2
613/801 Test #613: umeyama_2 ........................   Passed    0.01 sec
        Start 614: umeyama_3
614/801 Test #614: umeyama_3 ........................   Passed    0.00 sec
        Start 615: umeyama_4
615/801 Test #615: umeyama_4 ........................   Passed    0.00 sec
        Start 616: umeyama_5
616/801 Test #616: umeyama_5 ........................   Passed    0.00 sec
        Start 617: umeyama_6
617/801 Test #617: umeyama_6 ........................   Passed    0.00 sec
        Start 618: umeyama_7
618/801 Test #618: umeyama_7 ........................   Passed    0.00 sec
        Start 619: umeyama_8
619/801 Test #619: umeyama_8 ........................   Passed    0.00 sec
        Start 620: nesting_ops_1
620/801 Test #620: nesting_ops_1 ....................   Passed    0.00 sec
        Start 621: nesting_ops_2
621/801 Test #621: nesting_ops_2 ....................   Passed    0.01 sec
        Start 622: nesting_ops_3
622/801 Test #622: nesting_ops_3 ....................   Passed    0.00 sec
        Start 623: nesting_ops_4
623/801 Test #623: nesting_ops_4 ....................   Passed    0.00 sec
        Start 624: zerosized
624/801 Test #624: zerosized ........................   Passed    0.00 sec
        Start 625: dontalign_1
625/801 Test #625: dontalign_1 ......................   Passed    0.00 sec
        Start 626: dontalign_2
626/801 Test #626: dontalign_2 ......................   Passed    0.00 sec
        Start 627: dontalign_3
627/801 Test #627: dontalign_3 ......................   Passed    0.00 sec
        Start 628: dontalign_4
628/801 Test #628: dontalign_4 ......................   Passed    0.00 sec
        Start 629: dontalign_5
629/801 Test #629: dontalign_5 ......................   Passed    0.00 sec
        Start 630: dontalign_6
630/801 Test #630: dontalign_6 ......................   Passed    0.00 sec
        Start 631: dontalign_7
631/801 Test #631: dontalign_7 ......................   Passed    0.00 sec
        Start 632: dontalign_8
632/801 Test #632: dontalign_8 ......................   Passed    0.00 sec
        Start 633: evaluators
633/801 Test #633: evaluators .......................   Passed    0.00 sec
        Start 634: sizeoverflow
634/801 Test #634: sizeoverflow .....................   Passed    0.00 sec
        Start 635: prec_inverse_4x4_1
635/801 Test #635: prec_inverse_4x4_1 ...............   Passed    1.20 sec
        Start 636: prec_inverse_4x4_2
636/801 Test #636: prec_inverse_4x4_2 ...............   Passed    1.23 sec
        Start 637: prec_inverse_4x4_3
637/801 Test #637: prec_inverse_4x4_3 ...............   Passed    1.60 sec
        Start 638: vectorwiseop_1
638/801 Test #638: vectorwiseop_1 ...................   Passed    0.00 sec
        Start 639: vectorwiseop_2
639/801 Test #639: vectorwiseop_2 ...................   Passed    0.00 sec
        Start 640: vectorwiseop_3
640/801 Test #640: vectorwiseop_3 ...................   Passed    0.00 sec
        Start 641: vectorwiseop_4
641/801 Test #641: vectorwiseop_4 ...................   Passed    0.00 sec
        Start 642: vectorwiseop_5
642/801 Test #642: vectorwiseop_5 ...................   Passed    0.00 sec
        Start 643: vectorwiseop_6
643/801 Test #643: vectorwiseop_6 ...................   Passed    0.00 sec
        Start 644: vectorwiseop_7
644/801 Test #644: vectorwiseop_7 ...................   Passed    0.00 sec
        Start 645: special_numbers_1
645/801 Test #645: special_numbers_1 ................   Passed    0.20 sec
        Start 646: rvalue_types_1
646/801 Test #646: rvalue_types_1 ...................   Passed    0.00 sec
        Start 647: rvalue_types_2
647/801 Test #647: rvalue_types_2 ...................   Passed    0.00 sec
        Start 648: dense_storage
648/801 Test #648: dense_storage ....................   Passed    0.00 sec
        Start 649: ctorleak
649/801 Test #649: ctorleak .........................   Passed    0.00 sec
        Start 650: mpl2only
650/801 Test #650: mpl2only .........................   Passed    0.00 sec
        Start 651: inplace_decomposition_1
651/801 Test #651: inplace_decomposition_1 ..........   Passed    0.01 sec
        Start 652: inplace_decomposition_2
652/801 Test #652: inplace_decomposition_2 ..........   Passed    0.01 sec
        Start 653: inplace_decomposition_3
653/801 Test #653: inplace_decomposition_3 ..........   Passed    0.01 sec
        Start 654: inplace_decomposition_4
654/801 Test #654: inplace_decomposition_4 ..........   Passed    0.01 sec
        Start 655: inplace_decomposition_5
655/801 Test #655: inplace_decomposition_5 ..........   Passed    0.02 sec
        Start 656: inplace_decomposition_6
656/801 Test #656: inplace_decomposition_6 ..........   Passed    0.01 sec
        Start 657: inplace_decomposition_7
657/801 Test #657: inplace_decomposition_7 ..........   Passed    0.02 sec
        Start 658: inplace_decomposition_8
658/801 Test #658: inplace_decomposition_8 ..........   Passed    0.02 sec
        Start 659: half_float
659/801 Test #659: half_float .......................   Passed    0.00 sec
        Start 660: array_of_string
660/801 Test #660: array_of_string ..................   Passed    0.00 sec
        Start 661: fastmath
661/801 Test #661: fastmath .........................   Passed    0.00 sec
        Start 662: qtvector
662/801 Test #662: qtvector .........................   Passed    0.01 sec
        Start 663: umfpack_support_1
663/801 Test #663: umfpack_support_1 ................   Passed    0.39 sec
        Start 664: umfpack_support_2
664/801 Test #664: umfpack_support_2 ................   Passed    1.06 sec
        Start 665: cholmod_support_1
665/801 Test #665: cholmod_support_1 ................   Passed    6.47 sec
        Start 666: cholmod_support_2
666/801 Test #666: cholmod_support_2 ................   Passed   20.49 sec
        Start 667: spqr_support_1
667/801 Test #667: spqr_support_1 ...................   Passed    0.01 sec
        Start 668: spqr_support_2
668/801 Test #668: spqr_support_2 ...................   Passed    0.01 sec
        Start 669: boostmultiprec_1
669/801 Test #669: boostmultiprec_1 .................   Passed   12.04 sec
        Start 670: boostmultiprec_2
670/801 Test #670: boostmultiprec_2 .................   Passed   17.41 sec
        Start 671: boostmultiprec_3
671/801 Test #671: boostmultiprec_3 .................   Passed    2.03 sec
        Start 672: boostmultiprec_4
672/801 Test #672: boostmultiprec_4 .................   Passed    3.18 sec
        Start 673: boostmultiprec_5
673/801 Test #673: boostmultiprec_5 .................   Passed    1.80 sec
        Start 674: boostmultiprec_6
674/801 Test #674: boostmultiprec_6 .................   Passed   12.29 sec
        Start 675: boostmultiprec_7
675/801 Test #675: boostmultiprec_7 .................   Passed   10.57 sec
        Start 676: boostmultiprec_8
676/801 Test #676: boostmultiprec_8 .................   Passed   12.33 sec
        Start 677: boostmultiprec_9
677/801 Test #677: boostmultiprec_9 .................   Passed    9.40 sec
        Start 678: boostmultiprec_10
678/801 Test #678: boostmultiprec_10 ................   Passed    0.96 sec
        Start 679: failtests
679/801 Test #679: failtests ........................   Passed  152.38 sec
        Start 680: sblat1
680/801 Test #680: sblat1 ...........................   Passed    0.01 sec
        Start 681: sblat2
681/801 Test #681: sblat2 ...........................   Passed    0.03 sec
        Start 682: sblat3
682/801 Test #682: sblat3 ...........................   Passed    0.04 sec
        Start 683: dblat1
683/801 Test #683: dblat1 ...........................   Passed    0.01 sec
        Start 684: dblat2
684/801 Test #684: dblat2 ...........................   Passed    0.03 sec
        Start 685: dblat3
685/801 Test #685: dblat3 ...........................   Passed    0.04 sec
        Start 686: cblat1
686/801 Test #686: cblat1 ...........................   Passed    0.01 sec
        Start 687: cblat2
687/801 Test #687: cblat2 ...........................   Passed    0.04 sec
        Start 688: cblat3
688/801 Test #688: cblat3 ...........................   Passed    0.06 sec
        Start 689: zblat1
689/801 Test #689: zblat1 ...........................   Passed    0.01 sec
        Start 690: zblat2
690/801 Test #690: zblat2 ...........................   Passed    0.04 sec
        Start 691: zblat3
691/801 Test #691: zblat3 ...........................   Passed    0.05 sec
        Start 692: NonLinearOptimization
692/801 Test #692: NonLinearOptimization ............   Passed    0.06 sec
        Start 693: NumericalDiff
693/801 Test #693: NumericalDiff ....................   Passed    0.00 sec
        Start 694: autodiff_scalar_1
694/801 Test #694: autodiff_scalar_1 ................   Passed    0.00 sec
        Start 695: autodiff_scalar_2
695/801 Test #695: autodiff_scalar_2 ................   Passed    0.00 sec
        Start 696: autodiff_scalar_3
696/801 Test #696: autodiff_scalar_3 ................   Passed    0.00 sec
        Start 697: autodiff_scalar_4
697/801 Test #697: autodiff_scalar_4 ................   Passed    0.00 sec
        Start 698: autodiff_scalar_5
698/801 Test #698: autodiff_scalar_5 ................   Passed    0.00 sec
        Start 699: autodiff_1
699/801 Test #699: autodiff_1 .......................   Passed    0.00 sec
        Start 700: autodiff_2
700/801 Test #700: autodiff_2 .......................   Passed    0.00 sec
        Start 701: autodiff_3
701/801 Test #701: autodiff_3 .......................   Passed    0.00 sec
        Start 702: autodiff_4
702/801 Test #702: autodiff_4 .......................   Passed    0.00 sec
        Start 703: BVH_1
703/801 Test #703: BVH_1 ............................   Passed    0.01 sec
        Start 704: BVH_2
704/801 Test #704: BVH_2 ............................   Passed    0.01 sec
        Start 705: BVH_3
705/801 Test #705: BVH_3 ............................   Passed    0.01 sec
        Start 706: matrix_exponential_2
706/801 Test #706: matrix_exponential_2 .............   Passed    0.00 sec
        Start 707: matrix_exponential_1
707/801 Test #707: matrix_exponential_1 .............   Passed    0.00 sec
        Start 708: matrix_exponential_8
708/801 Test #708: matrix_exponential_8 .............   Passed    0.00 sec
        Start 709: matrix_exponential_6
709/801 Test #709: matrix_exponential_6 .............   Passed    0.01 sec
        Start 710: matrix_exponential_5
710/801 Test #710: matrix_exponential_5 .............   Passed    0.01 sec
        Start 711: matrix_exponential_7
711/801 Test #711: matrix_exponential_7 .............   Passed    0.00 sec
        Start 712: matrix_exponential_3
712/801 Test #712: matrix_exponential_3 .............   Passed    0.00 sec
        Start 713: matrix_exponential_4
713/801 Test #713: matrix_exponential_4 .............   Passed    0.01 sec
        Start 714: matrix_exponential_9
714/801 Test #714: matrix_exponential_9 .............   Passed    0.01 sec
        Start 715: matrix_function_1
715/801 Test #715: matrix_function_1 ................   Passed    0.00 sec
        Start 716: matrix_function_2
716/801 Test #716: matrix_function_2 ................   Passed    0.01 sec
        Start 717: matrix_function_3
717/801 Test #717: matrix_function_3 ................   Passed    0.03 sec
        Start 718: matrix_function_4
718/801 Test #718: matrix_function_4 ................   Passed    0.00 sec
        Start 719: matrix_function_5
719/801 Test #719: matrix_function_5 ................   Passed    0.01 sec
        Start 720: matrix_function_6
720/801 Test #720: matrix_function_6 ................   Passed    0.01 sec
        Start 721: matrix_function_7
721/801 Test #721: matrix_function_7 ................   Passed    0.07 sec
        Start 722: matrix_power_2
722/801 Test #722: matrix_power_2 ...................   Passed    0.01 sec
        Start 723: matrix_power_1
723/801 Test #723: matrix_power_1 ...................   Passed    0.00 sec
        Start 724: matrix_power_9
724/801 Test #724: matrix_power_9 ...................   Passed    0.05 sec
        Start 725: matrix_power_10
725/801 Test #725: matrix_power_10 ..................   Passed    0.01 sec
        Start 726: matrix_power_11
726/801 Test #726: matrix_power_11 ..................   Passed    0.01 sec
        Start 727: matrix_power_12
727/801 Test #727: matrix_power_12 ..................   Passed    0.01 sec
        Start 728: matrix_power_7
728/801 Test #728: matrix_power_7 ...................   Passed    0.01 sec
        Start 729: matrix_power_3
729/801 Test #729: matrix_power_3 ...................   Passed    0.01 sec
        Start 730: matrix_power_4
730/801 Test #730: matrix_power_4 ...................   Passed    0.02 sec
        Start 731: matrix_power_5
731/801 Test #731: matrix_power_5 ...................   Passed    0.00 sec
        Start 732: matrix_power_8
732/801 Test #732: matrix_power_8 ...................   Passed    0.01 sec
        Start 733: matrix_power_6
733/801 Test #733: matrix_power_6 ...................   Passed    0.00 sec
        Start 734: matrix_square_root_1
734/801 Test #734: matrix_square_root_1 .............   Passed    0.00 sec
        Start 735: matrix_square_root_2
735/801 Test #735: matrix_square_root_2 .............   Passed    0.01 sec
        Start 736: matrix_square_root_3
736/801 Test #736: matrix_square_root_3 .............   Passed    0.00 sec
        Start 737: matrix_square_root_4
737/801 Test #737: matrix_square_root_4 .............   Passed    0.01 sec
        Start 738: matrix_square_root_5
738/801 Test #738: matrix_square_root_5 .............   Passed    0.00 sec
        Start 739: alignedvector3
739/801 Test #739: alignedvector3 ...................   Passed    0.00 sec
        Start 740: FFT
740/801 Test #740: FFT ..............................   Passed    1.52 sec
        Start 741: EulerAngles_1
741/801 Test #741: EulerAngles_1 ....................   Passed    0.01 sec
        Start 742: EulerAngles_2
742/801 Test #742: EulerAngles_2 ....................   Passed    0.02 sec
        Start 743: sparse_extra_1
743/801 Test #743: sparse_extra_1 ...................   Passed    0.01 sec
        Start 744: sparse_extra_2
744/801 Test #744: sparse_extra_2 ...................   Passed    0.00 sec
        Start 745: sparse_extra_3
745/801 Test #745: sparse_extra_3 ...................***Exception: Other  0.18 sec
        Start 746: openglsupport
746/801 Test #746: openglsupport ....................***Exception: Other  0.27 sec
        Start 747: polynomialsolver_1
747/801 Test #747: polynomialsolver_1 ...............   Passed    0.00 sec
        Start 748: polynomialsolver_2
748/801 Test #748: polynomialsolver_2 ...............   Passed    0.01 sec
        Start 749: polynomialsolver_3
749/801 Test #749: polynomialsolver_3 ...............   Passed    0.01 sec
        Start 750: polynomialsolver_4
750/801 Test #750: polynomialsolver_4 ...............   Passed    0.01 sec
        Start 751: polynomialsolver_5
751/801 Test #751: polynomialsolver_5 ...............   Passed    0.01 sec
        Start 752: polynomialsolver_6
752/801 Test #752: polynomialsolver_6 ...............   Passed    0.01 sec
        Start 753: polynomialsolver_7
753/801 Test #753: polynomialsolver_7 ...............   Passed    0.01 sec
        Start 754: polynomialsolver_8
754/801 Test #754: polynomialsolver_8 ...............   Passed    0.01 sec
        Start 755: polynomialsolver_9
755/801 Test #755: polynomialsolver_9 ...............   Passed    0.01 sec
        Start 756: polynomialsolver_10
756/801 Test #756: polynomialsolver_10 ..............   Passed    0.01 sec
        Start 757: polynomialsolver_11
757/801 Test #757: polynomialsolver_11 ..............   Passed    0.01 sec
        Start 758: polynomialutils_2
758/801 Test #758: polynomialutils_2 ................   Passed    0.00 sec
        Start 759: polynomialutils_3
759/801 Test #759: polynomialutils_3 ................   Passed    0.00 sec
        Start 760: polynomialutils_4
760/801 Test #760: polynomialutils_4 ................   Passed    0.00 sec
        Start 761: polynomialutils_5
761/801 Test #761: polynomialutils_5 ................   Passed    0.00 sec
        Start 762: polynomialutils_6
762/801 Test #762: polynomialutils_6 ................   Passed    0.01 sec
        Start 763: polynomialutils_7
763/801 Test #763: polynomialutils_7 ................   Passed    0.00 sec
        Start 764: polynomialutils_8
764/801 Test #764: polynomialutils_8 ................   Passed    0.00 sec
        Start 765: polynomialutils_9
765/801 Test #765: polynomialutils_9 ................   Passed    0.00 sec
        Start 766: splines
766/801 Test #766: splines ..........................   Passed    0.09 sec
        Start 767: gmres_1
767/801 Test #767: gmres_1 ..........................   Passed    0.63 sec
        Start 768: gmres_2
768/801 Test #768: gmres_2 ..........................   Passed    2.26 sec
        Start 769: minres_1
769/801 Test #769: minres_1 .........................   Passed    4.35 sec
        Start 770: minres_2
770/801 Test #770: minres_2 .........................   Passed    0.00 sec
        Start 771: levenberg_marquardt
771/801 Test #771: levenberg_marquardt ..............   Passed    0.06 sec
        Start 772: kronecker_product_1
772/801 Test #772: kronecker_product_1 ..............   Passed   31.28 sec
        Start 773: kronecker_product_2
773/801 Test #773: kronecker_product_2 ..............   Passed    0.00 sec
        Start 774: special_functions_1
774/801 Test #774: special_functions_1 ..............   Passed    0.00 sec
        Start 775: special_functions_2
775/801 Test #775: special_functions_2 ..............   Passed    0.00 sec
        Start 776: cxx11_tensor_dimension
776/801 Test #776: cxx11_tensor_dimension ...........   Passed    0.00 sec
        Start 777: cxx11_tensor_map
777/801 Test #777: cxx11_tensor_map .................   Passed    0.00 sec
        Start 778: cxx11_tensor_assign
778/801 Test #778: cxx11_tensor_assign ..............   Passed    0.00 sec
        Start 779: cxx11_tensor_comparisons
779/801 Test #779: cxx11_tensor_comparisons .........   Passed    0.00 sec
        Start 780: cxx11_tensor_forced_eval
780/801 Test #780: cxx11_tensor_forced_eval .........   Passed    0.00 sec
        Start 781: cxx11_tensor_math
781/801 Test #781: cxx11_tensor_math ................   Passed    0.00 sec
        Start 782: cxx11_tensor_const
782/801 Test #782: cxx11_tensor_const ...............   Passed    0.00 sec
        Start 783: cxx11_tensor_intdiv_1
783/801 Test #783: cxx11_tensor_intdiv_1 ............   Passed    4.21 sec
        Start 784: cxx11_tensor_intdiv_2
784/801 Test #784: cxx11_tensor_intdiv_2 ............   Passed    2.11 sec
        Start 785: cxx11_tensor_intdiv_3
785/801 Test #785: cxx11_tensor_intdiv_3 ............   Passed    5.88 sec
        Start 786: cxx11_tensor_intdiv_4
786/801 Test #786: cxx11_tensor_intdiv_4 ............   Passed    5.67 sec
        Start 787: cxx11_tensor_intdiv_5
787/801 Test #787: cxx11_tensor_intdiv_5 ............   Passed    0.00 sec
        Start 788: cxx11_tensor_intdiv_6
788/801 Test #788: cxx11_tensor_intdiv_6 ............   Passed    0.01 sec
        Start 789: cxx11_tensor_intdiv_7
789/801 Test #789: cxx11_tensor_intdiv_7 ............   Passed    0.00 sec
        Start 790: cxx11_tensor_casts
790/801 Test #790: cxx11_tensor_casts ...............   Passed    0.00 sec
        Start 791: cxx11_tensor_empty
791/801 Test #791: cxx11_tensor_empty ...............   Passed    0.00 sec
        Start 792: cxx11_tensor_sugar
792/801 Test #792: cxx11_tensor_sugar ...............   Passed    0.00 sec
        Start 793: cxx11_tensor_roundings
793/801 Test #793: cxx11_tensor_roundings ...........   Passed    0.00 sec
        Start 794: cxx11_tensor_layout_swap
794/801 Test #794: cxx11_tensor_layout_swap .........   Passed    0.00 sec
        Start 795: cxx11_tensor_io
795/801 Test #795: cxx11_tensor_io ..................***Exception: SegFault  0.15 sec
        Start 796: cxx11_tensor_uint128_1
796/801 Test #796: cxx11_tensor_uint128_1 ...........   Passed    0.17 sec
        Start 797: cxx11_tensor_uint128_2
797/801 Test #797: cxx11_tensor_uint128_2 ...........   Passed    0.18 sec
        Start 798: cxx11_tensor_uint128_3
798/801 Test #798: cxx11_tensor_uint128_3 ...........   Passed    0.73 sec
        Start 799: cxx11_tensor_uint128_4
799/801 Test #799: cxx11_tensor_uint128_4 ...........   Passed    2.53 sec
        Start 800: cxx11_tensor_uint128_5
800/801 Test #800: cxx11_tensor_uint128_5 ...........   Passed    0.00 sec
        Start 801: cxx11_tensor_uint128_6
801/801 Test #801: cxx11_tensor_uint128_6 ...........   Passed   40.21 sec

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


## Install g2o
[g2o github](https://github.com/RainerKuemmerle/g2o)
```bsh
$ sudo apt install libsuitesparse-dev - qtdeclarative5-dev - qt5-qmake - libqglviewer-dev
$ mkdir ~/g2o_src && cd ~/g2o_src
$ git clone https://github.com/RainerKuemmerle/g2o.git
$ cd g2o
$ mkdir build && cd build
$ cmake ..
$ make
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
