
___
# 1 - Install ROS2
Installation manual for installing ROS2 (on Ubuntu 18.04).
[_From Docs.Ros.org_](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Binary.html)

### System Requirements:
We support Ubuntu Linux Bionic Beaver (18.04) and Ubuntu Xenial Xerus (16.04) on 64-bit x86 and 64-bit ARM.

Note: Ardent and beta versions supported Ubuntu Xenial Xerus 16.04.
### Add the ROS 2 apt repository
You will need to add the ROS 2 apt repositories to your system. To do so, first authorize our GPG key with apt like this:
```
sudo apt update && sudo apt install curl gnupg2 lsb-release
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg
```
### And then add the repository to your sources list:
And then add the repository to your sources list:
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
### Downloading ROS 2
- Go to [the releases page](https://github.com/ros2/ros2/releases)
- Download the latest package for Ubuntu; let’s assume that it ends up at ~/Downloads/ros2-dashing-linux-x86_64.tar.bz2.
  - Note: there may be more than one binary download option which might cause the file name to differ.
- Unpack it:
```
mkdir -p ~/ros2_dashing
cd ~/ros2_dashing
tar xf ~/Downloads/ros2-dashing-linux-x86_64.tar.bz2
```

### Installing and initializing rosdep
```
sudo apt update
sudo apt install -y python-rosdep
sudo rosdep init
rosdep update
```

### Installing the missing dependencies
Set your rosdistro according to the release you downloaded.
```
rosdep install --from-paths ~/ros2_dashing/ros2-linux/share --ignore-src --rosdistro dashing -y --skip-keys "console_bridge fastcdr fastrtps libopensplice67 libopensplice69 osrf_testing_tools_cpp poco_vendor rmw_connext_cpp rosidl_typesupport_connext_c rosidl_typesupport_connext_cpp rti-connext-dds-5.3.1 tinyxml_vendor tinyxml2_vendor urdfdom urdfdom_headers"
```
 - Optional:  if you want to use the ROS 1<->2 bridge, then you must also install ROS 1. Follow the normal install instructions: https://wiki.ros.org/melodic/Installation/Ubuntu

### Installing python3 libraries
```
sudo apt install -y libpython3-dev python3-pip
pip3 install -U argcomplete
```

### Environment setup
```
. ~/ros2_dashing/ros2-linux/setup.bash
```

### Using the ROS 1 bridge
The ROS 1 bridge can connect topics from ROS 1 to ROS 2 and vice-versa. See the dedicated [documentation](https://github.com/ros2/ros1_bridge/blob/master/README.md) on how to build and use the ROS 1 bridge.

### Uninstall ROS 2
If you installed your workspace with colcon as instructed above, “uninstalling” could be just a matter of opening a new terminal and not sourcing the workspace’s setup file. This way, your environment will behave as though there is no Dashing install on your system.

If you’re also trying to free up space, you can delete the entire workspace directory with:
```
rm -rf ~/ros2_dashing
```



___
