> [Wiki](Home) ▸ **Configuring OpenStudio Build Environments**

## Contents
**Recommended**: [Using the Superbuild](Configuring-OpenStudio-Build-Environments#wiki-using-the-superbuild)
- [Windows](Configuring-OpenStudio-Build-Environments#wiki-windows)
- [Linux](Configuring-OpenStudio-Build-Environments#wiki-linux)
- [Mac](Configuring-OpenStudio-Build-Environments#wiki-mac)

**Advanced**: [Manual Build Instructions](Configuring-OpenStudio-Build-Environments#wiki-manual-build-instructions)
- [Windows Configuration](Configuring-OpenStudio-Build-Environments#wiki-windows-configuration)
    * [Prerequisites](Configuring-OpenStudio-Build-Environments#wiki-prerequisites)
    * [Windows 7/8.1, Visual Studio 2010](Configuring-OpenStudio-Build-Environments#wiki-windows-781-visual-studio-2010)
        - [Professional](Configuring-OpenStudio-Build-Environments#wiki-professional)
        - [Professional x64](Configuring-OpenStudio-Build-Environments#wiki-professional-x64)
        - [Express](Configuring-OpenStudio-Build-Environments#wiki-express)
        - [Express x64](Configuring-OpenStudio-Build-Environments#wiki-express-x64)
- [Linux Configuration](Configuring-OpenStudio-Build-Environments#wiki-linux-configuration)
    * [Ubuntu 12.04 (x86 and x64)](Configuring-OpenStudio-Build-Environments#wiki-ubuntu-1204-x86-and-x64)
    * [Ubuntu 14.04 (x86 and x64)](Configuring-OpenStudio-Build-Environments#wiki-ubuntu-1404-x86-and-x64)
    * [Fedora 19 (x86 and x64)](Configuring-OpenStudio-Build-Environments#wiki-fedora-19-x86-and-x64)
    * [RHEL 5 (x86 and x64)](Configuring-OpenStudio-Build-Environments#wiki-rhel-5-x86-and-x64)
- [Mac Configuration](Configuring-OpenStudio-Build-Environments#wiki-mac-configuration)
    * [Prerequisites](Configuring-OpenStudio-Build-Environments#wiki-prerequisites-1)
    * [OS X 10.8](Configuring-OpenStudio-Build-Environments#wiki-os-x-108)
    * [OS X 10.9](Configuring-OpenStudio-Build-Environments#wiki-os-x-109)

# Using the Superbuild
This is the fastest, most reliable method of getting a working OpenStudio build.  These instructions assume that you have successfully [cloned the OpenStudio repository](Using-OpenStudio-with-Git-and-GitHub#cloning-the-repository-to-your-local-computer) already.

### Windows
Install Visual Studio 2010, [CMake](http://www.cmake.org/files/v2.8/cmake-2.8.12.2-win32-x86.exe), and [EnergyPlus 8.0](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus).

Clone the repository, create a build directory, and launch CMake:

[[/images/Configuring-OpenStudio-Build-Environments/cmake.windows.png]]

### Linux
Install the command line tools and [EnergyPlus 8.0](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus).

    sudo apt-get install dpkg-dev git cmake-curses-gui libqt4-dev libboost-all-dev libxt-dev

Clone the repository, create a build directory, and launch CMake:

[[/images/Configuring-OpenStudio-Build-Environments/cmake.linux.png]]

### Mac
Install Xcode, Xcode's command line tools, [CMake](http://www.cmake.org/files/v2.8/cmake-2.8.12.2-Darwin64-universal.dmg), and [EnergyPlus 8.0](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus).

Clone the repository, create a build directory, and launch CMake:

[[/images/Configuring-OpenStudio-Build-Environments/cmake.mac.png]]

---

# Manual Build Instructions

## Windows Configuration

### Prerequisites
Extract [SWIG](http://developer.nrel.gov/downloads/buildings/openstudio/src/swigwin-3.0.0.zip) to `C:\swig\swigwin-3.0.0`
Append `C:\swig\swigwin-3.0.0;` to the System `Path` variable
> _Latest v3.0.0 tested and working_

Install [CMake](http://www.cmake.org/files/v2.8/cmake-2.8.12.2-win32-x86.exe) with the option of adding CMake to the system PATH for all users
> _Latest v2.8.12.2 tested and working_

Install [EnergyPlus 8.0](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus)

Optionally extract [Ruby](http://developer.nrel.gov/downloads/buildings/openstudio/src/ruby-1.8.6-msvc-ssl.zip) to `C:\Ruby` if you want a convenient location to access the OpenStudio Ruby bindings
> _v1.8.6 MSVC tested and working_

#### For Building Documentation
Install [Doxygen](http://ftp.stack.nl/pub/users/dimitri/doxygen-1.8.6-setup.exe)
> _Latest v1.8.6 tested and working_

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

### Windows 7/8.1, Visual Studio 2010
Install [Boost](http://developer.nrel.gov/downloads/buildings/openstudio/src/boost_1_47_setup.exe) for the Visual C++ 10.0 compiler with the _Multithreaded_ and _Multithreaded Debug_ variants
> _v1.47.0 MSVC installer tested and working_

Install [Qt](http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-win-opensource-4.8.5-vs2010.exe)
> _v4.8.5 VS2010 tested and working_

#### Professional
Install [Visual Studio 2010 SP1](http://www.microsoft.com/en-us/download/details.aspx?id=23691)

Add `C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\Bin` to the System `Path` variable

#### Professional x64
Follow the previous instructions above to configure the environment for VS2010 Professional.  Within CMake, choose _Visual Studio 10 Win64_ as the generator for the project.  CMake will give you some general warnings about 64-bit builds.

The BUILD_QT, BUILD_BOOST, and BUILD_SWIG CMake options are _required_ for 64-bit builds, so they should be enabled.  Other options can be chosen like usual.

#### Express
Install [Visual C++ 2010 Express](http://go.microsoft.com/?linkid=9709939) (the Silverlight Runtime and SQL 
Server 2008 Express options are unnecessary and may be unchecked)

Install [Visual Studio 2010 SP1](http://www.microsoft.com/en-us/download/details.aspx?id=23691)

The MSVC_IS_EXPRESS CMake option is required and should be enabled.

##### For Building C# Bindings
Install [Visual C# 2010 Express](http://go.microsoft.com/?linkid=9709949) (the Silverlight Runtime and SQL Server 2008 Express options are unnecessary and may be unchecked)

#### Express x64
Follow the previous instructions to configure the environment for VS2010 Express with optional C# support.  

Install [Windows SDK 7.1](http://www.microsoft.com/download/en/confirmation.aspx?id=8279), and then add `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin;C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\bin\amd64` to the System `Path` variable.

Within CMake, choose _Visual Studio 10 Win64_ as the generator for the project.  CMake will give you some general warnings about 64-bit builds.

The BUILD_QT, BUILD_BOOST, and BUILD_SWIG CMake options are _required_ for 64-bit builds, so they should be enabled.  Other options can be chosen like usual.

The MSVC_IS_EXPRESS CMake option is required and should be enabled.

## Linux Configuration

### Ubuntu 12.04 (x86 and x64)
Build Dependencies:
```bash
sudo apt-get install dpkg-dev git cmake-curses-gui libqt4-dev libboost-all-dev ruby-dev ruby swig libxt-dev doxygen graphviz
```

Install EnergyPlus 8.0
```bash
# Download from http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus with the correct architecture
sudo sh SetEPlusV800008-lin-64.sh
rm SetEPlusV800008-lin-64.sh
```

Install [CMake](http://www.cmake.org/files/v2.8/cmake-2.8.12.2.tar.gz)
```bash
sudo apt-get install libncurses-dev
wget http://www.cmake.org/files/v2.8/cmake-2.8.12.2.tar.gz
tar -xzf cmake-2.8.12.2.tar.gz
rm cmake-2.8.12.2.tar.gz
cd cmake-2.8.12.2
./configure
make
sudo make install
cd ..
rm -rf cmake-2.8.12.2
```

### Ubuntu 14.04 (x86 and x64)
Ubuntu 14 is not yet fully supported - the dependencies (particularly Qt) will be updated soon.

Build Dependencies:
```bash
sudo apt-get install dpkg-dev git cmake-curses-gui libboost1.55-all-dev ruby2.0-dev ruby2.0 swig libssl-dev libxt-dev doxygen graphviz
sudo ln -fs /usr/bin/ruby2.0 /usr/bin/ruby
```

EnergyPlus 8.0
```bash
# Download from http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus with the correct architecture
sudo sh SetEPlusV800008-lin-64.sh
rm SetEPlusV800008-lin-64.sh
```

### Fedora 19 (x86 and x64)
Prerequisites:
```bash
sudo yum groupinstall development-libs development-tools
sudo yum install gcc-c++ cmake swig patch qt-devel qtwebkit-devel ruby ruby-devel graphviz
sudo yum remove boost-devel
curl -LO http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz
tar -xzf boost_1_47_0.tar.gz
rm boost_1_47_0.tar.gz
cd boost_1_47_0
# Apply patch https://svn.boost.org/trac/boost/ticket/6165
# Replace all instances of "TIME_UTC" with "TIME_UTC_" in boost/thread/xtime.hpp and libs/thread/src/pthread/timeconv.inl
sh ./bootstrap.sh
./b2
sudo ./b2 install --prefix=/usr/local
cd ..
rm -rf boost_1_47_0
```

EnergyPlus 8.0
```bash
# Download from http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus with the correct architecture
sudo sh SetEPlusV800008-lin-64.sh
rm SetEPlusV800008-lin-64.sh
```

### RHEL 5 (x86 and x64)
```bash
sudo yum groupinstall development-libs development-tools  
sudo yum remove boost-devel

##############
# Ruby 1.8.7 #
##############
sudo yum remove ruby ruby-devel
wget http://ftp.ruby-lang.org/pub/ruby/1.8/ruby-1.8.7-p374.tar.gz
tar -xzf ruby-1.8.7-p374.tar.gz
rm ruby-1.8.7-p374.tar.gz
cd ruby-1.8.7-p374
./configure
make
sudo make install
cd ..
rm -rf ruby-1.8.7-p374

wget http://production.cf.rubygems.org/rubygems/rubygems-2.0.4.tgz 
tar -xzf rubygems-2.0.4.tgz
rm rubygems-2.0.4.tgz
cd rubygems-2.0.4
sudo ruby setup.rb
cd ..
rm -rf rubygems-2.0.4

gem install rake

###############
# SWIG 3.0.0 #
###############
wget http://developer.nrel.gov/downloads/buildings/openstudio/src/swig-3.0.0.tar.gz
tar -xzf swig-3.0.0.tar.gz
rm swig-3.0.0.tar.gz
cd swig-3.0.0
sudo yum install pcre-devel
./configure 
make
sudo make install
cd ..
rm -rf swig-3.0.0

################
# Boost 1.47.0 #
################
wget http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz
tar -xzf boost_1_47_0.tar.gz
rm boost_1_47_0.tar.gz
cd boost_1_47_0
./bootstrap.sh
./b2
sudo ./b2 install --prefix=/usr/local
cd ..
rm -rf boost_1_47_0
			
############
# Qt 4.8.5 #
############
wget http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-everywhere-opensource-src-4.8.5.tar.gz
tar -xzf qt-everywhere-opensource-src-4.8.5.tar.gz
rm qt-everywhere-opensource-src-4.8.5.tar.gz
cd qt-everywhere-opensource-src-4.8.5
./configure -debug-and-release -opensource -qt-sql-sqlite -plugin-sql-sqlite -no-qt3support -nomake examples -nomake demos -nomake docs -confirm-license
gmake
#Go through the Makefiles in the 3rd party directory and remove the -Werror compiler flags if build failed (This step may need to be repeated)
#find src/3rdparty/webkit/ -type f -name Makefile -exec sed -i 's/-Werror //g' {} \;
#find src/3rdparty/webkit/ -type f -name Makefile.* -exec sed -i 's/-Werror //g' {} \;
#gmake
sudo gmake install
cd ..
rm -rf qt-everywhere-opensource-src-4.8.5

##################
# CMake 2.8.12.2 #
##################
wget http://www.cmake.org/files/v2.8/cmake-2.8.12.2.tar.gz
tar -xzf cmake-2.8.12.2.tar.gz
rm cmake-2.8.12.2.tar.gz
cd cmake-2.8.12.2
./configure
gmake
sudo gmake install
cd ..
rm -rf cmake-2.8.12.2

EnergyPlus 8.0

_RHEL will require a special EnergyPlus build for 8.0 due to glibc incompatibility_

```bash
curl -LO http://apps1.eere.energy.gov/buildings/energyplus/download/SetEPlusV800008-lin-64-RHEL5.sh
sudo sh ./SetEPlusV800008-lin-64-RHEL5.sh
rm SetEPlusV800008-lin-64-RHEL5.sh
```

## Mac Configuration

### Prerequisites
Install [EnergyPlus 8.0](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus)

Install [CMake](http://www.cmake.org/files/v2.8/cmake-2.8.12.2-Darwin64-universal.dmg) with the option of creating symbolic links in /usr/bin

Install Xcode from the App Store:
> Download the Auxiliary Tools for Xcode - Late July 2012 from https://developer.apple.com/downloads/ then drag PackageMaker.app to `/Applications/`

Install [SWIG](http://developer.nrel.gov/downloads/buildings/openstudio/src/swig-3.0.0.tar.gz)
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
curl -LO http://developer.nrel.gov/downloads/buildings/openstudio/src/swig-3.0.0.tar.gz
tar -xzf swig-3.0.0.tar.gz
rm swig-3.0.0.tar.gz
cd swig-3.0.0
./configure
make
sudo make install
cd ..
rm -rf swig-3.0.0
```

Modify `~/.bash_profile` to help give CMake defaults for the build options

```bash
export CMAKE_OSX_ARCHITECTURES='i386;x86_64'
export MACOSX_DEPLOYMENT_TARGET=10.8
```

### OS X 10.8
Install [Boost](http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz)
```bash
curl -LO http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz
tar -xzf boost_1_47_0.tar.gz
rm boost_1_47_0.tar.gz
cd boost_1_47_0
curl -LO https://svn.boost.org/trac/boost/raw-attachment/ticket/6686/xcode_43.diff
patch tools/build/v2/tools/darwin.jam xcode_43.diff
sh ./bootstrap.sh
sudo ./b2 variant=release variant=debug address-model=32_64 architecture=x86 --layout=tagged macosx-version=10.8 --without-python --without-math install --prefix=/usr/local -j2
cd ..
rm -rf boost_1_47_0
```

Install [Qt](http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-everywhere-opensource-src-4.8.5.tar.gz)
```bash
curl -LO http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-everywhere-opensource-src-4.8.5.tar.gz
tar -xzf qt-everywhere-opensource-src-4.8.5.tar.gz
rm qt-everywhere-opensource-src-4.8.5.tar.gz
cd qt-everywhere-opensource-src-4.8.5
./configure -sdk /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.8.sdk -debug-and-release -opensource -arch x86 -arch x86_64 -qt-sql-sqlite -plugin-sql-sqlite -nomake examples -nomake demos -nomake docs -no-qt3support -confirm-license
make -j2
sudo make install
cd ..
rm -rf qt-everywhere-opensource-src-4.8.5
echo 'export PATH=$PATH:/usr/local/Trolltech/Qt-4.8.5/bin' >> ~/.bash_profile
```

#### For Building Documentation
Download [Doxygen](http://ftp.stack.nl/pub/users/dimitri/Doxygen-1.8.6.dmg) and drag it to Applications

Install [Graphviz](http://www.graphviz.org/pub/graphviz/stable/macos/mountainlion/graphviz-2.36.0.pkg)

### OS X 10.9
Install [Boost](http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz)
```bash
curl -LO http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz
tar -xzf boost_1_47_0.tar.gz
rm boost_1_47_0.tar.gz
cd boost_1_47_0
curl -LO https://svn.boost.org/trac/boost/raw-attachment/ticket/6686/xcode_43.diff
patch tools/build/v2/tools/darwin.jam xcode_43.diff
sh ./bootstrap.sh
sudo ./b2 cxxflags="-stdlib=libstdc++" linkflags="-stdlib=libstdc++" variant=release variant=debug address-model=32_64 architecture=x86 --layout=tagged macosx-version-min=10.8 macosx-version=10.8 --without-python --without-math install --prefix=/usr/local -j2
cd ..
rm -rf boost_1_47_0
```

Install [Qt](http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-everywhere-opensource-src-4.8.5.tar.gz)
```bash
curl -LO http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-everywhere-opensource-src-4.8.5.tar.gz
tar -xzf qt-everywhere-opensource-src-4.8.5.tar.gz
rm qt-everywhere-opensource-src-4.8.5.tar.gz
cd qt-everywhere-opensource-src-4.8.5
./configure -sdk /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.8.sdk -debug-and-release -opensource -openssl -arch x86 -arch x86_64 -qt-sql-sqlite -plugin-sql-sqlite -nomake examples -nomake demos -nomake docs -no-phonon -no-phonon-backend -no-qt3support -confirm-license
make -j2
sudo make install
cd ..
rm -rf qt-everywhere-opensource-src-4.8.5
echo 'export PATH=$PATH:/usr/local/Trolltech/Qt-4.8.5/bin' >> ~/.bash_profile
```

For convenience, consider making Ruby 1.8 the system default:
```bash
cd /usr/bin
sudo mv erb erb2.0
sudo mv gem gem2.0
sudo mv irb irb2.0
sudo mv rake rake2.0
sudo mv rdoc rdoc2.0
sudo mv ri ri2.0
sudo mv ruby ruby2.0
sudo mv testrb testrb2.0

sudo ln -s ../../System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/erb erb
sudo ln -s ../../System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/gem gem
sudo ln -s ../../System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/irb irb
sudo ln -s ../../System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/rake rake
sudo ln -s ../../System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/rdoc rdoc
sudo ln -s ../../System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/ri ri
sudo ln -s ../../System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/ruby ruby
sudo ln -s ../../System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/testrb testrb
```