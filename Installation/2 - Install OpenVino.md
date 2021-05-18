# 2 Install OpenVino

### Install the Intel® Distribution of OpenVINO™ Toolkit Core Components
1. Download the Intel® Distribution of OpenVINO™ toolkit package file from [Intel® Distribution of OpenVINO™ toolkit for Linux](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit/download.html?operatingsystem=linux&distributions=github). 
```
git clone https://github.com/openvinotoolkit/openvino.git
```
2. Change directories to where you downloaded the Intel Distribution of OpenVINO toolkit for Linux* package file.
If you downloaded the package file to the current user's Downloads directory:
```
cd ~/Downloads/
```
- Note: By default, the file is saved as l_openvino_toolkit_p_<version>.tgz.

3. Unpack the .tgz file:
```
tar -xvzf l_openvino_toolkit_p_<version>.tgz
```
- Note: The files are unpacked to the l_openvino_toolkit_p_<version> directory.

4. Go to the directory:

```
cd l_openvino_toolkit_p_<version>
```
- Note: If you have a previous version of the Intel Distribution of OpenVINO toolkit installed, rename or delete these two directories: 
```
~/inference_engine_samples_build
~/openvino_models
```
5. Install with GUI installation wizard:
```
sudo ./install_GUI.sh
```
- Note: Follow the instructions on your screen.

6. When installed as root the default installation directory for the Intel Distribution of OpenVINO is ```/opt/intel/openvino_<version>/.```
- Note: For simplicity, a symbolic link to the latest installation is also created: ```/opt/intel/openvino/```.


