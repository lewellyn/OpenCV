# Blackberry Port of OpenCV 2.4.1

Officially sanctioned port of OpenCV to the Blackberry/QNX platform. To avoid fragmentation, please do not use any other version of OpenCV.

OpenCV has a CMake-based build system. This port was based on the sources for the Unix variant downloaded from http://sourceforge.net/projects/opencvlibrary/files/opencv-unix/2.4.1/.

### What's working, what's not?

This is an untested compilation of the OpenCV libraries for PlayBook and BlackBerry 10.  Areas that are highly dependent on the support of the operating system, such as the window system and (video) camera input facilities, have not been modified and will not work as-is.
Basic data types (points, matrices, rectangles, etc..), colour space transformations and the like appear to work, as does the 
source code that provides mean shift based tracking (meanshift and CAMShift), optical flow (good features to track, 
LK pyramids), histograms and back projection.  The machine learning components needed for ADABoost and Haar Training also seem to work, as do
Kalman filters.  Other parts of OpenCV have not been looked at in any way.

### Prerequisites

- Blackberry Native SDK (NDK) for Tablet OS

### Instructions for cross-compiling

1.  If not already installed, obtain a native development kit for the BlackBerry PlayBook or BlackBerry 10 and
    install it. We'll use $NDK as the name of the directory where the native development kit is installed, such
    as /opt/bbndk or C:\bbndk.

2.  If not already installed, install CMake from your package manager on Linux or obtain a binary distribution
    from http://cmake.org/cmake/resources/software.html for your operating system. If presented the option, you
    may wish to add CMake to your PATH.

3.  Initialize the NDK environment.

    a. (Linux/Mac OS X)  Open a new command line terminal or shell and invoke the script that initializes
       critical environment variables. 

       i.  source $NDK/bbndk-env.sh

    b. (Windows)  Open a new Command Prompt to invoke the script that initializes critical environment variables.

       i.  $NDK\bbndk-env.bat

4.  Create a sub-directory called "build".

    a.  mkdir build

5.  Change to the "build" directory, then invoke the configuration script to run CMake for the ARM architecture:

    a.   cd build
    b.1. (Linux/Mac OS X) ../configure-qsk arm a9
    b.2. (Windows) ..\configure-qsk arm a9

    The output will report that, for example certain GUI features have been enabled.  Other 3rd party libraries
    are already disabled by default.  Also, this will use the GNU STL implementation rather than the default
    "Dinkum" implementation.

6.  Compile the libraries using "make".  If it makes sense, use "make -j" to accelerate the compile. You do not
    want to set the number to more CPU cores than you have available.

    a.  make -j4

    Both static and dynamic libraries will be built.  They can be found in build/lib.
