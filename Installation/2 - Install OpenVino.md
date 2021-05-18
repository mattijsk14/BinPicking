# 2 Install OpenVino

## Install the Intel® Distribution of OpenVINO™ Toolkit Core Components
#### 1. Download the Intel® Distribution of OpenVINO™ toolkit package file from [Intel® Distribution of OpenVINO™ toolkit for Linux](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit/download.html?operatingsystem=linux&distributions=github). 
```
git clone https://github.com/openvinotoolkit/openvino.git
```
#### 2. Change directories to where you downloaded the Intel Distribution of OpenVINO toolkit for Linux* package file.
If you downloaded the package file to the current user's Downloads directory:
```
cd ~/Downloads/
```
- Note: By default, the file is saved as l_openvino_toolkit_p_<version>.tgz.

#### 3. Unpack the .tgz file:
```
tar -xvzf l_openvino_toolkit_p_<version>.tgz
```
- Note: The files are unpacked to the l_openvino_toolkit_p_<version> directory.

#### 4. Go to the directory:

```
cd l_openvino_toolkit_p_<version>
```
- Note: If you have a previous version of the Intel Distribution of OpenVINO toolkit installed, rename or delete these two directories: 
```
~/inference_engine_samples_build
~/openvino_models
```
#### 5. Install with GUI installation wizard:
```
sudo ./install_GUI.sh
```
- Note: Follow the instructions on your screen.
- When installed as root the default installation directory for the Intel Distribution of OpenVINO is ```/opt/intel/openvino_<version>/.```
- Note: For simplicity, a symbolic link to the latest installation is also created: ```/opt/intel/openvino/```.
- A completement screen indicates that the core components have been installed.

## Install External Software Dependencies
These dependencies are required for:
- Intel-optimized build of OpenCV library
- Deep Learning Inference Engine
- Deep Learning Model Optimizer tools

#### 1. Change to the ``` install_dependencies``` directory:
```
cd /opt/intel/openvino/install_dependencies
```

#### 2. Run a script to download and install the external software dependencies:
```
sudo -E ./install_openvino_dependencies.sh
```
The dependencies are installed. Continue to the next section to set your environment variables.

## Set the Envionment Variables
You must update several environment variables before you can compile and run OpenVINO™ applications. Run the following script to temporarily set your environment variables:
```
source /opt/intel/openvino/bin/setupvars.sh
```


#### 1. Open the .bashrc file in <user_directory>:
```
vi <user_directory>/.bashrc
```
#### 2. Add this line to the end of the file:
```
source /opt/intel/openvino/bin/setupvars.sh
```
#### 3. Save and close the file: press the _Esc_ key and type ```:wq```.
#### 4. To test your change, open a new terminal. You will see ```[setupvars.sh] OpenVINO environment initialized.```
The environment variables are set. Continue to the next section to configure the Model Optimizer.


