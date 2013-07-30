> [Wiki](Home) ▸ **Configuring OpenStudio Build Environments**

## Contents
- [Windows Configuration](Configuring-OpenStudio-Build-Environments#windows-configuration)
    * [Prerequisites](Configuring-OpenStudio-Build-Environments#prerequisites)
    * [Windows 7/XP, Visual Studio 2008](Configuring-OpenStudio-Build-Environments#windows-7xp-visual-studio-2008)
        - [Professional](Configuring-OpenStudio-Build-Environments#professional)
        - [Express](Configuring-OpenStudio-Build-Environments#express)
    * [Windows 7, Visual Studio 2010](Configuring-OpenStudio-Build-Environments#windows-7-visual-studio-2010)
        - [Professional](Configuring-OpenStudio-Build-Environments#professional-1)
- [Linux Configuration](Configuring-OpenStudio-Build-Environments#linux-configuration)
    * [Ubuntu 12.04 (x86 and x64)](Configuring-OpenStudio-Build-Environments#ubuntu-1204-x86-and-x64)
    * [Ubuntu 13.04 (x86 and x64)](Configuring-OpenStudio-Build-Environments#ubuntu-1304-x86-and-x64)
    * [Fedora 19 (x86 and x64)](Configuring-OpenStudio-Build-Environments#fedora-19-x86-and-x64)
    * [RHEL 5 (x86 and x64)](Configuring-OpenStudio-Build-Environments#rhel-5-x86-and-x64)
- [Mac Configuration](Configuring-OpenStudio-Build-Environments#mac-configuration)
    * [Prerequisites](Configuring-OpenStudio-Build-Environments#prerequisites-1)
    * [OS X 10.7](Configuring-OpenStudio-Build-Environments#os-x-107)
    * [OS X 10.8](Configuring-OpenStudio-Build-Environments#os-x-108)

## Windows Configuration

### Prerequisites
Extract [Ruby](http://developer.nrel.gov/downloads/buildings/openstudio/src/ruby-1.8.6-msvc.zip) to `C:\Ruby`
> _v1.8.6 MSVC tested and working_

Extract [SWIG](http://sourceforge.net/projects/swig/files/swigwin/swigwin-2.0.10/swigwin-2.0.10.zip/download) to `C:\swig\swigwin-2.0.10`
> _Latest v2.0.10 tested and working_

Install [CMake](http://www.cmake.org/files/v2.8/cmake-2.8.11.2-win32-x86.exe) with the option of adding CMake to the system PATH for all users
> _Latest v2.8.11.2 tested and working_

Install [OpenSSL](http://slproweb.com/download/Win32OpenSSL-1_0_1e.exe), ignoring the warning regarding Visual C++ 2008 Redistributables, with the option of copying OpenSSL DLLs to the OpenSSL binaries `/bin` directory
> _Latest Win32 1.0.1e tested and working_

Extract [DAKOTA](http://dakota.sandia.gov/download.html) to C:\dakota-5.3.1-public-CYGWIN.i686
> _Latest v5.3.1 tested and working_

Install [EnergyPlus 8.0](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus)

Append `C:\Ruby\bin;C:\Qt\4.8.5\bin;C:\swig\swigwin-2.0.10;C:\Program Files (x86)\boost\boost_1_47` to the System `Path` variable

#### For Building Documentation
Install [Doxygen](http://ftp.stack.nl/pub/users/dimitri/doxygen-1.8.4-setup.exe)
> _Latest v1.8.4 tested and working_

Install [Graphviz](http://www.graphviz.org/pub/graphviz/stable/windows/graphviz-2.30.1.msi)
> _Latest v2.30.1 tested and working_

#### For Building C# Bindings
Install [Sandcastle](http://sandcastle.codeplex.com/releases/view/47665?DownloadId=128770)
> _Latest v2.6.1062.1 tested and working - XP Users: Requires .NET Framework 2.0 or higher, so if you get a warning, come back to this step after installing .NET Framework 4.0 as part of the Visual Studio installation steps_

#### For Using Radiance
Install [Radiance](https://openstudio.nrel.gov/accept/file/1043) using the installer

#### For Building Installer Packages
Install [NSIS](http://prdownloads.sourceforge.net/nsis/nsis-2.46-setup.exe?download)
> _v2.46 tested and working_

### Windows 7/XP, Visual Studio 2008
Install [Boost](http://boostpro.com/download/boost_1_47_setup.exe) for the Visual C++ 9.0 compiler with the _Multithreaded_ and _Multithreaded Debug_ variants
> _v1.47.0 MSVC installer tested and working_

Install [Qt Libraries](http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-win-opensource-4.8.5-vs2008.exe)
> _Latest v4.8.5 tested and working_

#### Professional
Install Visual Studio 2008 Professional with the Complete option is recommended, or at least with Visual C++ and Visual C#

Install [Windows SDK 6.1](http://www.microsoft.com/download/en/confirmation.aspx?id=11310)

Install [.NET Framework 4](http://www.microsoft.com/download/en/confirmation.aspx?id=17851)

Install [Windows SDK 7.1](http://www.microsoft.com/download/en/confirmation.aspx?id=8279), and launch the Windows SDK Configuration Tool to make 7.1 the current SDK `Start Menu->Microsoft Windows SDK v7.1->Visual Studio Registration->Windows SDK Configuration Tool`

Add `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin` to the System `Path` variable

##### Special Notes
Windows SDK 6.0A that comes with Visual Studio 2008 Professional is sufficient, but it is recommended that the Windows SDK 6.1, .NET Framework 4, Windows SDK 7.1, and all relevant Windows Updates be installed, with 7.1 set as the current SDK and added to the System Path.

#### Express
_Order of installation is important_

Install [Visual C++ 2008 Express SP1](http://go.microsoft.com/?linkid=7729279) (the Silverlight Runtime and SQL Server 2008 Express options are unnecessary and may be unchecked)

Install [Windows SDK 6.1](http://www.microsoft.com/download/en/confirmation.aspx?id=11310)

Install [.NET Framework 4](http://www.microsoft.com/download/en/confirmation.aspx?id=17851)

Install [Windows SDK 7.1](http://www.microsoft.com/download/en/confirmation.aspx?id=8279), and launch the Windows SDK Configuration Tool to make 7.1 the current SDK `Start Menu->Microsoft Windows SDK v7.1->Visual Studio Registration->Windows SDK Configuration Tool`

> VERY IMPORTANT: If your SDK 7.1 installation fails, uninstall all 2010 Redistributables from `Control Panel->Programs and Features`

Add `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin` to the System `Path` variable

##### To Build C# Bindings
Install [Visual C# 2008 Express SP1](http://go.microsoft.com/?linkid=7729278) (the Silverlight Runtime and SQL Server 2008 Express options are unnecessary and may be unchecked)

##### Special Notes
It is recommended that all important Windows Updates be installed.

### Windows 7, Visual Studio 2010 Professional
Install [Boost](http://boostpro.com/download/boost_1_47_setup.exe) for the Visual C++ 10.0 compiler with the _Multithreaded_ and _Multithreaded Debug_ variants
> _v1.47.0 MSVC installer tested and working_

Install [Qt Libraries](http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-win-opensource-4.8.5-vs2010.exe)
> _Latest v4.8.5 tested and working_

Add `C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\Bin` to the System `Path` variable

## Linux Configuration

### Ubuntu 12.04 (x86 and x64)
Build Dependencies:
```bash
sudo apt-get install dpkg-dev subversion cmake-curses-gui libqt4-dev libboost-all-dev ruby-dev ruby swig libxt-dev doxygen graphviz
```

EnergyPlus 8.0
```bash
# Download from http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus with the correct architecture
sudo sh SetEPlusV800008-lin-64.sh
rm SetEPlusV800008-lin-64.sh
```

CMake
```bash
sudo apt-get install libncurses-dev
wget http://www.cmake.org/files/v2.8/cmake-2.8.11.2.tar.gz
tar -xzf cmake-2.8.11.2.tar.gz
rm cmake-2.8.11.2.tar.gz
cd cmake-2.8.11.2
./configure
make
sudo make install
cd ..
rm -rf cmake-2.8.11.2
```

Dakota
```bash
sudo apt-get install gfortran libatlas-base-dev liblapack-dev

# Download DAKOTA 5.3.1 first
tar -xzf dakota-5.3.1-public-src.tar.gz
rm dakota-5.3.1-public-src.tar.gz
cd dakota-5.3.1.src
mkdir build
cd build
ccmake ..
#Set CMAKE_BUILD_TYPE to ‘Release’
#Set CMAKE_INSTALL_PREFIX to `/usr/local/dakota-5.3.1`
#Ensure HAVE_X_GRAPHICS is set to OFF
export F77=gfortran
make
sudo make install
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/dakota-5.3.1/lib' >> ~/.bashrc
cd ../..
rm -rf dakota-5.3.1.src
```

### Ubuntu 13.04 (x86 and x64)
Build Dependencies:
```bash
sudo apt-get install dpkg-dev subversion cmake-curses-gui libqt4-dev libboost1.49-all-dev ruby1.8-dev ruby1.8 swig libssl-dev libxt-dev doxygen graphviz
sudo ln -fs /usr/bin/ruby1.8 /usr/bin/ruby
```

EnergyPlus 8.0
```bash
# Download from http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus with the correct architecture
sudo sh SetEPlusV800008-lin-64.sh
rm SetEPlusV800008-lin-64.sh
```

Dakota

_Dakota 5.3.1 is untested with Ubuntu 13_

### Fedora 19 (x86 and x64)
Build Dependencies:
```bash
sudo yum groupinstall development-libs development-tools
sudo yum install gcc-c++ cmake swig patch qt-devel qtwebkit-devel ruby ruby-devel graphviz
sudo yum remove boost-devel
curl -O http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz
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
# SWIG 2.0.10 #
###############
wget http://prdownloads.sourceforge.net/swig/swig-2.0.10.tar.gz
tar -xzf swig-2.0.10.tar.gz
rm swig-2.0.10.tar.gz
cd swig-2.0.10
sudo yum install pcre-devel
./configure 
make
sudo make install
cd ..
rm -rf swig-2.0.10

################
# Boost 1.47.0 #
################
wget http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz
tar -xzf boost_1_47_0.tar.gz
rm boost_1_47_0.tar.gz
cd boost_1_47_0
./bootstrap.sh
./bjam
sudo ./bjam install
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
# CMake 2.8.11.2 #
##################
wget http://www.cmake.org/files/v2.8/cmake-2.8.11.2.tar.gz
tar -xzf cmake-2.8.11.2.tar.gz
rm cmake-2.8.11.2.tar.gz
cd cmake-2.8.11.2
./configure
gmake
sudo gmake install
cd ..
rm -rf cmake-2.8.11.2

################
# Dakota 5.3.1 #
################
sudo yum -y install gcc-gfortran blas-devel lapack-devel

# Download DAKOTA 5.3.1 first
tar -xzf dakota-5.3.1-public-src.tar.gz
rm dakota-5.3.1-public-src.tar.gz
cd dakota-5.3.1.src
mkdir build
cd build
ccmake ..
#Set CMAKE_BUILD_TYPE to ‘Release’
#Set CMAKE_INSTALL_PREFIX to `/usr/local/dakota-5.3.1`
#Ensure HAVE_X_GRAPHICS is set to OFF
export F77=gfortran
make
sudo make install
cd ../..
rm -rf dakota-5.3.1.src
```

EnergyPlus 8.0

RHEL will require a special EnergyPlus build for 8.0 due to glibc incompatibility

```bash
curl -O http://apps1.eere.energy.gov/buildings/energyplus/download/SetEPlusV800008-lin-64-RHEL5.sh
sudo sh ./SetEPlusV800008-lin-64-RHEL5.sh
rm SetEPlusV800008-lin-64-RHEL5.sh
```

## Mac Configuration

### Prerequisites
Install [EnergyPlus 8.0](http://apps1.eere.energy.gov/buildings/energyplus/register.cfm?goto=eplus)

Install [CMake](http://www.cmake.org/files/v2.8/cmake-2.8.11.2-Darwin64-universal.dmg) with the option of creating symbolic links in /usr/bin

Install Xcode from the App Store:
> Install the command line tools from `Xcode->Preferences->Downloads->Components->Command Line Tools`
> Install the latest Auxiliary Tools for Xcode from `Xcode->Open Developer Tool->More Developer Tools...` then drag PackageMaker.app to `/Applications/`

Boost
```bash
curl -O http://downloads.sourceforge.net/project/boost/boost/1.47.0/boost_1_47_0.tar.gz
tar -xzf boost_1_47_0.tar.gz
rm boost_1_47_0.tar.gz
cd boost_1_47_0
# Apply patch: https://svn.boost.org/trac/boost/attachment/ticket/6686/xcode_43.diff
sh ./bootstrap.sh
./b2 variant=release variant=debug address-model=32_64 architecture=x86 --layout=tagged macosx-version=10.7 --without-python --without-math install --prefix=build -j2
cd build
sudo cp -r * /usr/local/
cd ../../
rm -rf boost_1_47_0
```

SWIG
```bash
curl -O ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.33.tar.gz
tar -xzf pcre-8.33.tar.gz
rm pcre-8.33.tar.gz
cd pcre-8.33
./configure
make
sudo make install
cd ..
rm -rf pcre-8.33
curl -O http://prdownloads.sourceforge.net/swig/swig-2.0.10.tar.gz
tar -xzf swig-2.0.10.tar.gz
rm swig-2.0.10.tar.gz
cd swig-2.0.10
./configure
make
sudo make install
cd ..
rm -rf swig-2.0.10
```

### OS X 10.7
Qt
```bash
curl -O http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-everywhere-opensource-src-4.8.5.tar.gz
tar -xzf qt-everywhere-opensource-src-4.8.5.tar.gz
rm qt-everywhere-opensource-src-4.8.5.tar.gz
cd qt-everywhere-opensource-src-4.8.5
./configure -sdk /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.7.sdk -debug-and-release -opensource -arch x86 -arch x86_64 -qt-sql-sqlite -plugin-sql-sqlite -nomake examples -nomake demos -nomake docs -no-qt3support -confirm-license
make
sudo make install
cd ..
rm -rf qt-everywhere-opensource-src-4.8.5

#sudo nano /etc/paths
##Add "/usr/local/Trolltech/Qt-4.8.5/bin"
```

For Building Documentation

> Download [Doxygen](http://ftp.stack.nl/pub/users/dimitri/Doxygen-1.8.4.dmg) and drag it to Applications
> Install [Graphviz](http://www.graphviz.org/pub/graphviz/stable/macos/lion/graphviz-2.30.1.pkg)

### OS X 10.8
Qt
```bash
curl -O http://download.qt-project.org/official_releases/qt/4.8/4.8.5/qt-everywhere-opensource-src-4.8.5.tar.gz
tar -xzf qt-everywhere-opensource-src-4.8.5.tar.gz
rm qt-everywhere-opensource-src-4.8.5.tar.gz
cd qt-everywhere-opensource-src-4.8.5
cd src/3rdparty/webkit/WebKitLibraries
mv libWebKitSystemInterfaceMountainLion.a libWebKitSystemInterfaceMountainLion.a.bak
cp libWebKitSystemInterfaceLion.a libWebKitSystemInterfaceMountainLion.a
cd ../../../..
./configure -sdk /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.7.sdk -debug-and-release -opensource -arch x86 -arch x86_64 -qt-sql-sqlite -plugin-sql-sqlite -nomake examples -nomake demos -nomake docs -no-qt3support -confirm-license
make
sudo make install
cd ..
rm -rf qt-everywhere-opensource-src-4.8.5

#sudo nano /etc/paths
##Add "/usr/local/Trolltech/Qt-4.8.5/bin"
```

For Building Documentation

> Download [Doxygen](http://ftp.stack.nl/pub/users/dimitri/Doxygen-1.8.4.dmg) and drag it to Applications
> Install [Graphviz](http://www.graphviz.org/pub/graphviz/stable/macos/mountainlion/graphviz-2.30.1.pkg)