> [Wiki](Home) ▸ **Configuring OpenStudio Build Environments**

## Contents
**Recommended**: [Using the Superbuild](#using-the-superbuild)
- [Windows](#windows)
- [Linux](#linux)
- [Mac](#mac)

**Advanced**: [Manual Build Instructions](#manual-build-instructions)
- [Windows Configuration](#windows-configuration)
    * [Prerequisites](#prerequisites)
    * [Windows 7/8.1, Visual Studio 2013](#windows-781-visual-studio-2013)
        - [Professional](#professional-1)
- [Linux Configuration](#linux-configuration)
    * [Ubuntu 14.04 (x86 and x64)](#ubuntu-1404-x86-and-x64)
- [Mac Configuration](#mac-configuration)
    * [Prerequisites](#prerequisites-1)
    * [OS X 10.9](#os-x-109)

# Using the Superbuild
This is the fastest, most reliable method of getting a working OpenStudio build.  These instructions assume that you have successfully [cloned the OpenStudio repository](Using-OpenStudio-with-Git-and-GitHub#cloning-the-repository-to-your-local-computer) already, and installed [Qt](http://qt-project.org/downloads) (Note that creating a universal mac build will require that you build Qt yourself - follow the instructions below).

### Windows
Install Visual Studio 2013, [CMake](http://www.cmake.org/files/v3.0/cmake-3.0.0-win32-x86.exe), and [EnergyPlus 8.1](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus).

Clone the repository, create a build directory, and launch CMake:

[[/images/Configuring-OpenStudio-Build-Environments/cmake.windows.png]]

### Linux
Install the command line tools and [EnergyPlus 8.1](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus).

    sudo apt-get install dpkg-dev git cmake-curses-gui libqt4-dev libboost-all-dev libxt-dev

Clone the repository, create a build directory, and launch CMake:

[[/images/Configuring-OpenStudio-Build-Environments/cmake.linux.png]]

### Mac
Install Xcode, [CMake](http://www.cmake.org/files/v3.0/cmake-3.0.0-Darwin64-universal.dmg), and [EnergyPlus 8.1](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus).

Clone the repository, create a build directory, and launch CMake:

[[/images/Configuring-OpenStudio-Build-Environments/cmake.mac.png]]

---

# Manual Build Instructions

## Windows Configuration

### Prerequisites
Install [msysGit](http://msysgit.github.io/)

Extract [SWIG](http://developer.nrel.gov/downloads/buildings/openstudio/src/swigwin-3.0.2.zip) to `C:\swig`
Append `C:\swig\swigwin-3.0.2;` to the System `Path` variable
> _Latest v3.0.2 tested and working_

Install [CMake](http://www.cmake.org/files/v3.0/cmake-3.0.0-win32-x86.exe)
> _Latest v3.0.0 tested and working_

Install [EnergyPlus 8.1](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus)

#### For Building Documentation
Install [Doxygen](http://ftp.stack.nl/pub/users/dimitri/doxygen-1.8.7-setup.exe)
> _Latest v1.8.7 tested and working_

Install [Graphviz](http://www.graphviz.org/pub/graphviz/stable/windows/graphviz-2.38.msi)
> _Latest v2.38 tested and working_

#### For Building C# Bindings
Install [Sandcastle](http://sandcastle.codeplex.com/releases/view/47665?DownloadId=128770)
> _Latest v2.6.1062.1 tested and working_

#### For Using Radiance
Install [Radiance](https://openstudio.nrel.gov/accept/file/1043) using the installer
> _Latest v4.2a tested and working_

#### For Building Installer Packages
Install [NSIS](http://prdownloads.sourceforge.net/nsis/nsis-2.46-setup.exe?download)
> _v2.46 tested and working_

### Windows 7/8.1, Visual Studio 2013
Install [Boost](http://sourceforge.net/projects/boost/files/boost-binaries/1.55.0-build2/boost_1_55_0-msvc-12.0-32.exe/download) to the default directory of `C:\local`
> _v1.55.0 tested and working_

Install [Qt](http://download.qt-project.org/official_releases/qt/5.3/5.3.1/qt-opensource-windows-x86-msvc2013_opengl-5.3.1.exe)
> _v5.3.1 VS2013 OpenGL tested and working_

#### Professional
Install [Visual Studio 2013 Update 2](http://www.microsoft.com/en-us/download/details.aspx?id=42666)

#### Professional x64
Follow the previous instructions above to configure the environment for VS2013 Professional.  Within CMake, choose _Visual Studio 12 2013 Win64_ as the generator for the project.

Ensure that you have installed 64-bit Qt.

`BUILD_BOOST`, and `BUILD_SWIG` CMake options are _required_ for 64-bit builds, so they should be enabled.  Other options can be chosen like usual.

#### Express
Install [Visual C++ 2013 Express](http://www.microsoft.com/en-us/download/details.aspx?id=40787) (all of the optional installs are unnecessary and may be unchecked)

The `MSVC_IS_EXPRESS` CMake option is required and should be enabled.

#### Express x64
Follow the previous instructions to configure the environment for VS2013 Express.  

Install Windows SDK 8, and then add `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin;C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\bin\amd64` to the System `Path` variable.

Within CMake, choose _Visual Studio 12 2013 Win64_ as the generator for the project.

Ensure that you have installed 64-bit Qt.

The `BUILD_BOOST`, and `BUILD_SWIG` CMake options are _required_ for 64-bit builds, so they should be enabled.  Other options can be chosen like usual.

The `MSVC_IS_EXPRESS` CMake option is required and should be enabled.

## Linux Configuration

### Ubuntu 14.04 (x86 and x64)
Build Dependencies:
```bash
sudo apt-get install dpkg-dev git cmake-curses-gui qt5-default libqt5webkit5-dev libboost1.55-all-dev swig libssl-dev libxt-dev doxygen graphviz

wget ftp://ftp.ruby-lang.org/pub/ruby/2.0/ruby-2.0.0-p451.tar.gz
tar -xzf ruby-2.0.0-p451.tar.gz
rm ruby-2.0.0-p451.tar.gz
cd ruby-2.0.0-p451
./configure --enable-shared --prefix=/usr/local
make -j2
sudo make install
cd ..
rm -rf ruby-2.0.0-p451

sudo ln -fs /usr/local/bin/ruby /usr/bin/ruby
```

EnergyPlus 8.1
```bash
# Download from http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus with the correct architecture
sudo sh SetEPlusV810009-lin-64.sh
rm SetEPlusV810009-lin-64.sh
```

## Mac Configuration

### Prerequisites
Install [EnergyPlus 8.1](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus)

Install [CMake](http://www.cmake.org/files/v3.0/cmake-3.0.0-Darwin64-universal.dmg) with the option of creating symbolic links in /usr/bin

Install Xcode from the App Store

Install [SWIG](http://developer.nrel.gov/downloads/buildings/openstudio/src/swig-3.0.2.tar.gz)
```bash
curl -LO ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.35.tar.gz
tar -xzf pcre-8.35.tar.gz
rm pcre-8.35.tar.gz
cd pcre-8.35
./configure
make
sudo make install
cd ..
rm -rf pcre-8.35
curl -LO http://developer.nrel.gov/downloads/buildings/openstudio/src/swig-3.0.2.tar.gz
tar -xzf swig-3.0.2.tar.gz
rm swig-3.0.2.tar.gz
cd swig-3.0.2
./configure
make
sudo make install
cd ..
rm -rf swig-3.0.2
```

Modify `~/.bash_profile` to help give CMake defaults for the build options

```bash
export CMAKE_OSX_ARCHITECTURES='i386;x86_64'
export MACOSX_DEPLOYMENT_TARGET=10.9
```

#### For Building Installer Packages
> Download the Auxiliary Tools for Xcode - Late July 2012 from https://developer.apple.com/downloads/ then drag PackageMaker.app to `/Applications/`

#### For Building Documentation
Download [Doxygen](http://ftp.stack.nl/pub/users/dimitri/Doxygen-1.8.6.dmg) and drag it to Applications

Install [Graphviz](http://www.graphviz.org/pub/graphviz/stable/macos/mountainlion/graphviz-2.36.0.pkg)

### OS X 10.9
Install [Boost](http://downloads.sourceforge.net/project/boost/boost/1.55.0/boost_1_55_0.tar.gz)
```bash
curl -LO http://downloads.sourceforge.net/project/boost/boost/1.55.0/boost_1_55_0.tar.gz
tar -xzf boost_1_55_0.tar.gz
rm boost_1_55_0.tar.gz
cd boost_1_55_0
sh ./bootstrap.sh
# *Deprecated*
sudo ./b2 cxxflags="-stdlib=libstdc++" linkflags="-stdlib=libstdc++" variant=release variant=debug address-model=32_64 architecture=x86 --layout=tagged macosx-version-min=10.9 macosx-version=10.9 --without-python --without-math install --prefix=/usr/local -j2
cd ..
rm -rf boost_1_55_0
```

Install [Qt](http://qt.mirror.constant.com/archive/qt/5.3/5.3.1/single/qt-everywhere-opensource-src-5.3.1.tar.gz)
```bash
curl -LO http://qt.mirror.constant.com/archive/qt/5.3/5.3.1/single/qt-everywhere-opensource-src-5.3.1.tar.gz
tar -xzf qt-everywhere-opensource-src-5.3.1.tar.gz
rm qt-everywhere-opensource-src-5.3.1.tar.gz
cd qt-everywhere-opensource-src-5.3.1
# *Deprecated*
./configure -sdk /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.8.sdk -debug-and-release -opensource -openssl -arch x86 -arch x86_64 -qt-sql-sqlite -plugin-sql-sqlite -nomake examples -nomake demos -nomake docs -no-phonon -no-phonon-backend -no-qt3support -confirm-license
make -j2
sudo make install
cd ..
rm -rf qt-everywhere-opensource-src-5.3.1
# *Deprecated*
echo 'export PATH=$PATH:/usr/local/Trolltech/Qt-5.3.1/bin' >> ~/.bash_profile
```