# Installing all the needed packages
> LET OP: WERKT (NOG) NIET
## Grasp library with RGB-D Camera
>Make sure you installed [OpenVINO](https://github.com/mattijsk14/BinPicking/blob/main/Installation/2%20-%20Install%20OpenVINO.md) & [ROS 2 dashing](https://github.com/mattijsk14/BinPicking/blob/main/Installation/1%20-%20Install%20ROS%202.md)

### 1. Install the non ROS packages needed for this application
```
sudo apt-get install libpcl-dev libeigen3-dev
```

### 2. Install Grasp Pose Detection package 
[Source] (https://github.com/intel/ros2_grasp_library/blob/master/grasp_tutorials/doc/grasp_ros2/install_gpd.md)


#### 2.1. Install GPG
Get the code:
```
cd ~/dev_ws
git clone https://github.com/atenpas/gpg.git
cd gpg
```
Build the library:
```
mkdir build && cd build
cmake ..
make
sudo make install
```

#### 2.2. Install GPD
Get the code, originally derived from GPD tag 1.5.0:
```
cd ~/dev_ws
git clone https://github.com/atenpas/gpd
cd gpd
```
Build the library:
```
mkdir build
cd build
cmake -DUSE_OPENVINO=ON ..
make
sudo make install
```
#### 2.3. Install the right PCL version
Download the 'tar.gz' file from the [PCL releases](https://github.com/PointCloudLibrary/pcl/releases) page or directly [here](https://github.com/PointCloudLibrary/pcl/archive/refs/tags/pcl-1.11.1.tar.gz). When the pop-up download screen is opened, click `save`.
```
cd ~/dev_ws
mkdir pcl
cd ~/Downloads
mv pcl-pcl-1.11.1.tar.gz ~/dev_ws/pcl
```
Unpack the tar.gz file:
```
cd ~/dev_ws/pcl
tar -xzvf pcl-pcl-1.11.1.tar.gz
```
Build the library:
```
cd pcl-pcl-1.11.1
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=None -DCMAKE_INSTALL_PREFIX=/usr \ -DBUILD_GPU=ON-DBUILD_apps=ON -DBUILD_examples=ON \ -DCMAKE_INSTALL_PREFIX=/usr .. -DUSE_OPENVINO=ON ..
make -j6
sudo make install
```
note: This will take some time.

- note: by default, "libgrasp_pose_detection.so" shall be installed to "/usr/local/lib" and header files installed to "/usr/local/include/gpd"

#### 3 Install packages for de Intel Realsense RGB-D Camera D435i
jooo werkt nog niet
