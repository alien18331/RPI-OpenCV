## OpenCV: Open Source Computer Vision Library

### Resources

* Homepage: <https://opencv.org>
* Docs: <https://docs.opencv.org/master/>
* Q&A forum: <http://answers.opencv.org>
* Issue tracking: <https://github.com/opencv/opencv/issues>

### Contributing

Please read the [contribution guidelines](https://github.com/opencv/opencv/wiki/How_to_contribute) before starting work on a pull request.

#### Summary of the guidelines:

* One pull request per issue;
* Choose the right base branch;
* Include tests and documentation;
* Clean up "oops" commits before submitting;
* Follow the [coding style guide](https://github.com/opencv/opencv/wiki/Coding_Style_Guide).
  
## RPI-OpenCV  
  
# Step 0: Select OpenCV version to install  
> sudo apt-get -y purge wolfram-engine  
> sudo apt-get -y purge libreoffice*  
> sudo apt-get -y clean  
> sudo apt-get -y autoremove  
> echo "OpenCV installation by learnOpenCV.com"   
> cvVersion="master"  
  
#Clean build directories (optional)  
> rm -rf opencv/build  
> rm -rf opencv_contrib/build  
  
#Create directory for installation  
> mkdir installation  
> mkdir installation/OpenCV-"$cvVersion"  
  
#Save current working directory (OpenCV_Home_Dir)  
> cwd=$(pwd)  
  
# Step 1: Update Packages  
> sudo apt -y update  
> sudo apt -y upgrade  
  
# Step 2: Install OS Libraries  
sudo apt-get -y remove x264 libx264-dev  
   
#Install dependencies  
> sudo apt-get -y install build-essential checkinstall cmake pkg-config yasm  
> sudo apt-get -y install git gfortran  
> sudo apt-get -y install libjpeg8-dev libjasper-dev libpng12-dev  
> sudo apt-get -y install libtiff5-dev  
> sudo apt-get -y install libtiff-dev  
> sudo apt-get -y install libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev  
> sudo apt-get -y install libxine2-dev libv4l-dev  
> cd /usr/include/linux  
> sudo ln -s -f ../libv4l1-videodev.h videodev.h  
> $cwd  
    
> sudo apt-get -y install libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev  
> sudo apt-get -y install libgtk2.0-dev libtbb-dev qt5-default  
> sudo apt-get -y install libatlas-base-dev  
> sudo apt-get -y install libmp3lame-dev libtheora-dev  
> sudo apt-get -y install libvorbis-dev libxvidcore-dev libx264-dev  
> sudo apt-get -y install libopencore-amrnb-dev libopencore-amrwb-dev  
> sudo apt-get -y install libavresample-dev  
> sudo apt-get -y install x264 v4l-utils  
   
#Optional dependencies  
> sudo apt-get -y install libprotobuf-dev protobuf-compiler  
> sudo apt-get -y install libgoogle-glog-dev libgflags-dev  
> sudo apt-get -y install libgphoto2-dev libeigen3-dev libhdf5-dev doxygen  
  
# Step 3: Install Python Libraries  
> sudo apt-get -y install python3-dev python3-pip  
> sudo -H pip3 install -U pip numpy  
> sudo apt-get -y install python3-testresources  
  
# Step 4: Download opencv and opencv_contrib  
> git clone https://github.com/opencv/opencv.git
> cd opencv  
> git checkout $cvVersion  
> cd ..  
   
> git clone https://github.com/opencv/opencv_contrib.git  
> cd opencv_contrib  
> git checkout $cvVersion  
> cd ..  
  
# Step 5: Compile and install OpenCV with contrib modules  
> cd opencv  
> mkdir build  
> cd build  
  
> cmake -D CMAKE_BUILD_TYPE=RELEASE
            -D CMAKE_INSTALL_PREFIX=/usr/local 
            -D INSTALL_C_EXAMPLES=ON 
            -D INSTALL_PYTHON_EXAMPLES=ON 
            -D WITH_TBB=ON 
            -D WITH_V4L=ON 
            -D OPENCV_PYTHON3_INSTALL_PATH=$cwd/OpenCV-$cvVersion-py3/lib/python3.5/site-packages 
            -D WITH_QT=ON 
            -D WITH_OPENGL=ON 
            -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules 
            -D BUILD_EXAMPLES=ON .. 
  
> make -j$(nproc)  
> make install  
  
# Step 6: Reset swap file  
> sudo sed -i 's/CONF_SWAPSIZE=1024/CONF_SWAPSIZE=100/g' /etc/dphys-swapfile  
> sudo /etc/init.d/dphys-swapfile stop  
> sudo /etc/init.d/dphys-swapfile start  
