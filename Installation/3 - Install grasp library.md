# Installing all the needed packages
> LET OP: WERKT (NOG) NIET
## Grasp library with RGB-D Camera
>Make sure you installed [OpenVINO](https://github.com/mattijsk14/BinPicking/blob/main/Installation/2%20-%20Install%20OpenVINO.md) & [ROS 2 dashing](https://github.com/mattijsk14/BinPicking/blob/main/Installation/1%20-%20Install%20ROS%202.md)

### Install the non ROS packages needed for this application
```
sudo apt-get install libpcl-dev libeigen3-dev
```
#### 1.1. Install latest version of Cmake.
Check your current version with `cmake --version`. (minimum version required: 3.13).
Visit https://cmake.org/download/ and download the latest binaries (for linux: `x86_64.sh` file.
Click `save` when the download pop-up is being opened
unpack:
```
cd ~/Downloads
sudo mv cmake-3.$version.sh /opt/
cd
chmod +x /opt/cmake$version.sh
sudo bash /opt/cmake$version.sh
```
Click `enter` until terminal is asking for a `Y`.
Overwrite the old version:
```
sudo ln -s /home/$user/cmake$version/bin/* /usr/local/bin
cmake --version
```

#### 1.1. Install DLDT
##### 1.1.1. Download:
```
git clone https://github.com/opencv/dldt.git
cd dldt
git checkout 2019_R3
```
##### 1.1.2. Follow the instructions:
```
cd dldt/inference-engine
git submodule init
git submodule update --recursive
```
##### 1.1.3. Install the dependencies
```
sudo ./install_dependencies.sh
```
##### 1.1.4. Build:
```
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make --jobs=$(nproc --all)
```
Note: this will take some time (10-30 mins approx.)

##### 1.1.5. Build and install inference engine:
For CMake projects, set an environment variable InferenceEngine_DIR:
```
export InferenceEngine_DIR=/path/to/dldt/inference-engine/build/
```
onderstaande werkt niet.
```
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local -DGEMM=MKL -DMKLROOT=/usr/local/lib/mklml -DENABLE_MKL_DNN=ON -DENABLE_CLDNN=ON ..
make -j8
sudo make install
```


##### 1.1.6. Share the Cmake configures for the Inference Engine to be found by other packages
```
sudo mkdir /usr/share/InferenceEngine
sudo cp InferenceEngineConfig*.cmake /usr/share/InferenceEngine
sudo cp targets.cmake /usr/share/InferenceEngine
```
> Then Inference Engine will be found when adding "find_package(InferenceEngine)" into the CMakeLists.txt

##### 1.1.7. Configure library path
```
echo `pwd`/../bin/intel64/Release/lib | sudo tee -a /etc/ld.so.conf.d/openvino.conf
sudo ldconfig

```
#### 1.2 Install colcon

```
sudo apt install python3-colcon-common-extensions
```
_______



### 2. Install Grasp Pose Detection package 
[Source] (https://github.com/intel/ros2_grasp_library/blob/master/grasp_tutorials/doc/grasp_ros2/install_gpd.md)

#### 2.1. Install the latest PCL version
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

#### 2.2. Install GPG
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

#### 2.3. Install GPD
Get the code, originally derived from GPD tag 1.5.0:

```
cd ~/dev_ws/
git clone https://github.com/sharronliu/gpd
cd gpd
git checkout libgpd
```
Build:
```
cd src/gpd
mkdir build
cd build
cmake -DUSE_OPENVINO=ON ..
make
sudo make install
```

- note: by default, "libgrasp_pose_detection.so" shall be installed to "/usr/local/lib" and header files installed to "/usr/local/include/gpd"
______________
### 3. Build grasp library
[Source](https://github.com/intel/ros2_grasp_library/blob/master/grasp_tutorials/doc/grasp_ros2/tutorials_1_grasp_ros2_with_camera.md)
> Install pcl 1.8.1

Get the source code:
```
cd
mkdir ~/dev_ws/src -p
cd ~/dev_ws/src
git clone https://github.com/intel/ros2_grasp_library.git
```
Copy the models:
```
cp -a ~/dev_ws/gpd/models ros2_grasp_library/gpd 
```
Build:
```
cd ..
source /opt/ros/dashing/setup.bash
sudo colcon build --symlink-install --packages-select grasp_msgs moveit_msgs grasp_ros2
source ./install/local_setup.bash
```

> Error after colcon build: CMake Error at CMakeLists.txt:36 (find_package):
  By not providing "Findament_cmake.cmake" in CMAKE_MODULE_PATH this project
  has asked CMake to find a package configuration file provided by
  "ament_cmake", but CMake did not find one.

#### Launch Grasp Library
Terminal 1, Optionally, launch Rviz2 to illustrate detection results.
```
ros2 run rviz2 rviz2 -d src/ros2_grasp_library/grasp_ros2/rviz2/grasp.rviz
```
>Note You may customize the ".rviz" file for your own camera, for example:
>To change to fixed frame: "Global Options -> Fixed Frame"
>To change the point cloud topic: "Point Cloud 2 -> Topic"

Terminal 2, launch RGBD camera
>e.g. launch [ROS2 Realsenes](https://github.com/intel/ros2_intel_realsense/tree/refactor)
>or, with a ros-bridge, launch any ROS OpenNI RGBD cameras, like [ROS Realsense](https://github.com/intel-ros/realsense)
```
ros2 run realsense_node realsense_node
```
#Terminal 3, launch Grasp Library
```
ros2 run grasp_ros2 grasp_ros2 __params:=src/ros2_grasp_library/grasp_ros2/cfg/grasp_ros2_params.yaml
```

### 4 Install packages for de Intel Realsense RGB-D Camera D435i
Ja weetje, werkt niet joe

[Previous](https://github.com/mattijsk14/BinPicking/blob/main/Installation/2%20-%20Install%20OpenVINO.md) / [Next]()
