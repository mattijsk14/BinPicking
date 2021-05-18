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

## Configure the Model Optimizer
The Model Optimizer is a Python*-based command line tool for importing trained models from popular deep learning frameworks such as Caffe*, TensorFlow*, Apache MXNet*, ONNX* and Kaldi*.

The Model Optimizer is a key component of the Intel Distribution of OpenVINO toolkit. You cannot perform inference on your trained model without running the model through the Model Optimizer. When you run a pre-trained model through the Model Optimizer, your output is an Intermediate Representation (IR) of the network. The Intermediate Representation is a pair of files that describe the whole model:

.xml: Describes the network topology
.bin: Contains the weights and biases binary data
For more information about the Model Optimizer, refer to the [Model Optimizer Developer Guide](https://docs.openvinotoolkit.org/2020.2/_docs_MO_DG_Deep_Learning_Model_Optimizer_DevGuide.html). 

#### Configure all supported frameworks at the same time

#### 1. Go to the Model Optimizer prerequisites directory:
```
cd /opt/intel/openvino/deployment_tools/model_optimizer/install_prerequisites
```
#### 2. Run the script to configure the Model Optimizer for Caffe, TensorFlow, MXNet, Kaldi*, and ONNX:
```
sudo ./install_prerequisites.sh
```

## Run the Verification Scripts to Verify Installation
#### 1. Go to the Inference Engine demo directory:
```
cd /opt/intel/openvino/deployment_tools/demo
```
#### 2. Run the Image Classification verification script:
```
./demo_squeezenet_download_convert_run.sh
```
This verification script downloads a SqueezeNet model, uses the Model Optimizer to convert the model to the .bin and .xml Intermediate Representation (IR) files. The Inference Engine requires this model conversion so it can use the IR as input and achieve optimum performance on Intel hardware.

#### 3. Run the Inference Pipeline verification script:
```
./demo_security_barrier_camera.sh
```
This script downloads three pre-trained model IRs, builds the Security Barrier Camera Demo application, and runs it with the downloaded models and the car_1.bmp image from the demo directory to show an inference pipeline. The verification script uses vehicle recognition in which vehicle attributes build on each other to narrow in on a specific attribute.

First, an object is identified as a vehicle. This identification is used as input to the next model, which identifies specific vehicle attributes, including the license plate. Finally, the attributes identified as the license plate are used as input to the third model, which recognizes specific characters in the license plate.

When the verification script completes, you will see an image that displays the resulting frame with detections rendered as bounding boxes, and text.

#### 4. Close the image viewer window to complete the verification script.



[Next]()
