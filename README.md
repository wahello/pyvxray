# pyvXRAY

**An ABAQUS plug-in for the creation of virtual x-rays from 3D finite element bone/implant models**

Copyright 2013, Michael Hogg (michael.christopher.hogg@gmail.com)

MIT license - See pyvxray/LICENSE.txt for details on usage and distribution

## Requirements

### Software requirements

* ABAQUS >= 6.11
* Python Image Library (PIL) >= 1.1.6

**NOTES:**

1.  ABAQUS is a commerical software package and requires a license from [Simulia](http://www.3ds.com/products-services/simulia/overview/)
2.  The authors of pyvXRAY are not associated with ABAQUS/Simulia 
3.  Python and numpy are heavily used by pyvXRAY. These are built in to ABAQUS. All of the last few releases (v6.11-v6.13) use Python 2.6 and numpy 1.4

For building cython modules from source (e.g. if not using versions with pre-built modules):
* A c compiler. The msvc compiler works best on Windows.
* Cython >= 0.17. This is optional, as c files generated by Cython are provided

### Model setup requirements

* The model must contain only linear or quadrilateral tetrahedral elements (ABAQUS element types C3D4 and C3D10, respectively)
* The model must have a scalar fieldoutput variable representing bone density. This is typically a state variable such as SDV1
* This scalar variable must be available in the last frame of each step to be analysed, as only the last frame is used.

**LIMITATIONS:**

* Virtual x-rays can only be created for element sets within part instances. Assembly element sets (which may contain elements from more than a single part) are currently not supported

## Installation

pyvXRAY is an ABAQUS plug-in. ABAQUS plug-ins may be installed in several ways. Only one of the ways is discussed here. For other options the user is referred to the ABAQUS user manuals.

The ABAQUS GUI is built on Python, and has its own Python installation. This Python installation is not the typically Python setup, so some guidance is provided here on how to install pyvXRAY's dependencies.

####1. Installation of pyvXRAY plug-in

####2. Installation of pyvXRAY dependencies

Currently pyvXRAY has only one dependency that is not part of the ABAQUS Python, which is PIL. On Windows it is easist to download and run the binary installers. However, ABAQUS python typically does not appear in the list of Python installations, so binary installers often do not work. There are two solutions to this:

* Separate Python installation and use a binary installer

  The SIMULIA support site suggests that a separate Python installation be setup. The dependencies can then be installed easily into this Python installation, which can then be used by ABAQUS Python. This Python version must match the ABAQUS version, which has been 2.6.x for the following few ABAQUS versions. 

  + Install [Python 2.6](http://python.org)
  + Download the PIL binary installer and install
  + Create an environment variable `PYTHONPATH=C:\Python26\Lib\site-packages`

* Edit the Windows registry and use a binary installer (Windows only)

  By editing the Windows registry the binary installers will be able to detect the ABAQUS Python version and install as usual. To edit the Windows registry, follow these steps:

  + Create an empty file called `filename.reg`, where `filename` can be anything
  + Copy and paste the following text into this file:

            Windows Registry Editor Version 5.00

            [HKEY_CURRENT_USER\Software\Python]
 
            [HKEY_CURRENT_USER\Software\Python\Pythoncore]
 
            [HKEY_CURRENT_USER\Software\Python\Pythoncore\2.6]
 
            [HKEY_CURRENT_USER\Software\Python\Pythoncore\2.6\InstallPath]
            @="path_to_ABAQUS_Python"

  + Replace the text `path_to_ABAQUS_Python` above with the actual path to the ABAQUS Python installation. This location depends on the ABAQUS version. For the default ABAQUS installation location, possible locations are:

    * v6.11-1: `C:\\SIMULIA\\Abaqus\\6.11-1\\External\\Python`
    * v6.12-1: `C:\\SIMULIA\\Abaqus\\6.12-1\\tools\\SMApy`
    * v6.13-1: `C:\\SIMULIA\\Abaqus\\6.13-1\\tools\\SMApy\\python2.6`

  + Save the file
  + In Windows Explorer, right click the file and select `Run with regedit`
  + Download the PIL binary installer and install

* Install PIL from source (requires Microsoft C++ to be installed)

  + Download the PIL source, typically called `Imaging-x.x.x.tar.gz` where x.x.x is the version number
  + Unpack this to a convenient location, giving directory `Imaging-x.x.x`
  + Open a command prompt and browse to this folder (containing the setup.py file)
  + At the command prompt enter:

            abaqus python setup.py install

##Documentation

The documentation can be found on the project [website](https://code.google.com/p/pyvxray/).

## Help
 
For help post a question on the [project support page](https://groups.google.com/forum/#!forum/pyvxray).
