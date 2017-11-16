# LUNA SDK Examples
This repository contains examples code for VisionLabs LUNA SDK and is compatible
with SDK version 3.0.0 and newer.

**Please note, that while these examples are released under MIT license, the SDK itself is not.
Contact us via email (info@visionlabs.ru) for evaluation and/or licensing terms and conditions.**

Aside from examples itself, there are some supplementary materials you may find useful.
Look into *cmake/* folder for a CMake find script for the SDK. You are not forced to use
CMake but we advise for it.

Currently we support 64 bit Windows and Linux. On Windows everything should work with
Visual Studio 2015. On Linux we tested this code with GCC 4.8.5.
Other versions may work as well. Note, that the SDK is officially supported on RedHat
Linux families (RHEL, CentOS, Fedora).

## Build examples
*To build the example 4 WITH_FREEIMAGE_EXAMPLE option must be installed.
Example 4 shows how to work with images of different formats, for example, jpeg.
Default  WITH_FREEIMAGE_EXAMPLE option is enabled.*

From Luna SDK root.
```
$ mkdir build && cd build
$ cmake -DCMAKE_BUILD_TYPE=Release -DFSDK_ROOT=.. ../examples
$ make
```

## Run examples
Note: data folder must be at <LUNA_SDK_root>/data on Windows and on Linux.
```
# Detecting, Extracting, Matching
$ build/example1/Example1 examples/images/Cameron_Diaz.ppm examples/images/Cameron_Diaz_2.ppm 0.7
$ build/example1/Example1 examples/images/Cameron_Diaz.ppm examples/images/Jennifer_Aniston.ppm 0.7

# Detecting, Landmarks, Estimating( Attributes, Quality, Eyes, Head pose)
$ build/example2/Example2 examples/images/portrait.ppm
 
# Indexing
$ build/example5/Example5 examples/images/Cameron_Diaz.ppm examples/images/ examples/images_lists/list.txt 0.7

# Descriptor and batch saving
$ build/example6/Example6 examples/images/portrait.ppm

# Descriptor and batch loading
$ build/example7/Example7 examples/descriptors/Cameron_Diaz.xpk examples/descriptors/Cameron_Diaz_2.xpk 0.7
```

## Liveness example 

**Simple liveness**

*To build the example 8 WITH_LIVENESS_EXAMPLE option must be installed.
Example 8 shows how to work with Liveness Engine and simple liveness tests.
Default  WITH_LIVENESS_EXAMPLE option is enabled.
Also example8 requires OpenCV library with imgproc, highgui and videoio modules.*

**Build example8 with OpenCV (from FSDK_ROOT/build):**
```
$ cmake ../examples -DCMAKE_BUILD_TYPE=Release -DWITH_LIVENESS_EXAMPLE=ON -DOpenCV_DIR=<path_to_opencv> -DFSDK_ROOT=.. -DLSDK_ROOT=..
```
**Run example8:**
```
$ build/example8/Example8 <web_cam_id> <test_number>
```

**Complex liveness**

**Depth Liveness**

###### Disclaimer
This liveness type works with 8bit rgb images and 16bit depth maps.
Example9 initially was designed to work with kinect *v1* depth camera on Windows.
Rest OS are not supported and require additional/substitutional software.

Interaction with device functionality is based on OpenCV interfaces with OPENNI2 support, according to this scheme:
```
|Example9|-->|OpenCV|-->|OpenNI2|-->|Device Driver|-->|KinectV1|
```
Required 3rdparty software: 
* OpenNI2.2;
* Required middleware: 
  * KinectSDK-v1.8 or above;
  * KinectRuntime-v1.8 or above;
  * KinectDeveloperToolkit-v1.8 or above;
* OpenCV with OpenNI2 support (imgproc, highgui, videoio).

*To build the example 9 WITH_DEPTH_LIVENESS option must be installed.
Example 9 shows how to work with Liveness Engine and complex liveness test.
Default  WITH_DEPTH_LIVENESS option is disabled.*

**Build example9 with OpenCV (from FSDK_ROOT/build):**
```
$ cmake ../examples -DCMAKE_BUILD_TYPE=Release -DWITH_LIVENESS_EXAMPLE=ON -DWITH_DEPTH_LIVENESS=ON -DOpenCV_DIR=<path_to_opencv> -DFSDK_ROOT=.. -DLSDK_ROOT=..
```
**Run example9:**
```
$ build/example9/Example9
```

## FreeImage example
Note: the installation command FreeImage for Centos:
```
$ sudo yum install freeimage-devel
```
Ubuntu:
```
$ sudo apt-get install libfreeimage3 libfreeimage-dev
```
Windows: automatic installation from CMakeLists file.

**Build with FreeImage example (from FSDK_ROOT/build):**
```
$ cmake -DFSDK_ROOT=.. -DWITH_FREEIMAGE_EXAMPLE=ON ../examples
```
Note for windows: when you build and install FreeImage example, freeimage dynamic library (freeimage.dll) is installed.

**Run FreeImage example:**
```
$ build/example3/Example3 examples/images/Cameron_Diaz.jpg
```

## Qt example
**Build with Qt example (from FSDK_ROOT/build):**
```
$ cmake -DFSDK_ROOT=.. -DWITH_QT_EXAMPLE=ON ../examples
```

If Qt is installed in non-system directory and can't be found by cmake automatically, you also need to specify path to Qt.
**Example:**
```
$ cmake -DFSDK_ROOT=.. -DWITH_QT_EXAMPLE=ON -DQt5Core_DIR=/usr/lib64/cmake/Qt5Core -DQt5Gui_DIR=/usr/lib64/cmake/Qt5Gui -DQt5_DIR=/usr/lib64/cmake/Qt5 ../examples
```
Note for windows: when you build and install Qt example, qt dynamic libraries (QtCore.dll, QtGui.dll) is installed.

**Run Qt example:**
```
$ build/example4/Example4 examples/images/Jennifer_Aniston.jpg
```

