# 1 - Install ROS 2  ![452](https://user-images.githubusercontent.com/79080234/118667055-f331df80-b7f3-11eb-9b9b-0debfd435b95.png)

Installation manual for installing ROS 2 (on Ubuntu 18.04).
[_From Docs.Ros.org_](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Binary.html)

### System Requirements:
We support Ubuntu Linux Bionic Beaver (18.04) and Ubuntu Xenial Xerus (16.04) on 64-bit x86 and 64-bit ARM.

Note: Ardent and beta versions supported Ubuntu Xenial Xerus 16.04.
#### 1. Add the ROS 2 apt repository
You will need to add the ROS 2 apt repositories to your system. To do so, first authorize our GPG key with apt like this:
```
sudo apt update && sudo apt install curl gnupg2 lsb-release
```
And
```
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg
```
#### 2. And then add the repository to your sources list:
And then add the repository to your sources list:
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
#### 3. Downloading ROS 2
- Go to [the releases page](https://github.com/ros2/ros2/releases) or download the dashing version [now](https://github.com/ros2/ros2/releases/download/release-dashing-20201202/ros2-dashing-20201202-linux-bionic-amd64.tar.bz2). Choose the option ` save ` in the pop-up window. _(downloading this release will take about 2 minutes.)_
- The version for this project is: `ros2-dashing-20201202-linux-bionic-amd64.tar.bz2` .
- Unpack it with the next commands:
```
mkdir -p ~/ros2_dashing
cd ~/ros2_dashing
tar xf ~/Downloads/ros2-dashing-20201202-linux-bionic-amd64.tar.bz2
```
- note:  this will take about 2-5 minutes
#### 4. Installing and initializing rosdep
```
sudo apt update
sudo apt install -y python-rosdep
sudo rosdep init
rosdep update
```

#### 5. Installing the missing dependencies
Set your rosdistro according to the release you downloaded.
```
rosdep install --from-paths ~/ros2_dashing/ros2-linux/share --ignore-src --rosdistro dashing -y --skip-keys "console_bridge fastcdr fastrtps libopensplice67 libopensplice69 osrf_testing_tools_cpp poco_vendor rmw_connext_cpp rosidl_typesupport_connext_c rosidl_typesupport_connext_cpp rti-connext-dds-5.3.1 tinyxml_vendor tinyxml2_vendor urdfdom urdfdom_headers"
```
 - Optional:  if you want to use the ROS 1<->2 bridge, then you must also install ROS 1. Follow the normal install instructions: https://wiki.ros.org/melodic/Installation/Ubuntu

#### 6. Installing python3 libraries
```
sudo apt install -y libpython3-dev python3-pip
pip3 install -U argcomplete
```

#### 7. Environment setup
```
. ~/ros2_dashing/ros2-linux/setup.bash
source /opt/ros/dashing/setup.bash
```
#### 8. Testing your ROS2 Dashing

Open 2 terminals, in the first terminal set up the ROS 2 environment as described and run a C++ talker:
```
ros2 run demo_nodes_cpp talker
```
In the second terminal, run the py listener:
```
ros2 run demo_nodes_py listener
```
You should see the talker saying that it’s Publishing messages and the listener saying I heard those messages. This verifies both the C++ and Python APIs are working properly.

#### 9. Using the ROS 1 bridge
The ROS 1 bridge can connect topics from ROS 1 to ROS 2 and vice-versa. See the dedicated [documentation](https://github.com/ros2/ros1_bridge/blob/master/README.md) on how to build and use the ROS 1 bridge.

#### 10. Uninstall ROS 2
If you installed your workspace with colcon as instructed above, “uninstalling” could be just a matter of opening a new terminal and not sourcing the workspace’s setup file. This way, your environment will behave as though there is no Dashing install on your system.

If you’re also trying to free up space, you can delete the entire workspace directory with:
```
rm -rf ~/ros2_dashing
```

[Next step of the installation](https://github.com/mattijsk14/BinPicking/blob/main/Installation/2%20-%20Install%20OpenVino.md)
