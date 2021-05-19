# Installing all the needed packages
> LET OP: WERKT VOOR GEEN ENE KANKER
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

#### 2.1. Install GPD
Get the code, originally derived from GPD tag 1.5.0:
```
cd
git clone https://github.com/sharronliu/gpd.git
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
error bij cmake
- note: by default, "libgrasp_pose_detection.so" shall be installed to "/usr/local/lib" and header files installed to "/usr/local/include/gpd"


