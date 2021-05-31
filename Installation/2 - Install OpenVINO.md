# 2 - Install OpenVINO
_Source: [docs.openvinotoolkit.org](https://docs.openvinotoolkit.org/2020.2/_docs_install_guides_installing_openvino_linux.html)_

> When following this installation guide, make sure [ROS 2](https://github.com/mattijsk14/BinPicking/blob/main/Installation/1%20-%20Install%20ROS%202.md) is installed on your Ubuntu 18.04. Otherwise follow the previous installation guide.

#### Introduction
The Intel® Distribution of OpenVINO™ toolkit quickly deploys applications and solutions that emulate human vision. Based on Convolutional Neural Networks (CNN), the toolkit extends computer vision (CV) workloads across Intel® hardware, maximizing performance. The Intel® Distribution of OpenVINO™ toolkit includes the Intel® Deep Learning Deployment Toolkit (Intel® DLDT).

**The Intel® Distribution of OpenVINO™ toolkit for Linux:**

Enables CNN-based deep learning inference on the edge
Supports heterogeneous execution across Intel® CPU, Intel® Integrated Graphics, Intel® Movidius™ Neural Compute Stick, Intel® Neural Compute Stick 2, and Intel® Vision Accelerator Design with Intel® Movidius™ VPUs
Speeds time-to-market via an easy-to-use library of computer vision functions and pre-optimized kernels
Includes optimized calls for computer vision standards including OpenCV* and OpenCL™

**Included with the Installation and installed by default:**

| Component | Description |
| --- | --- |
| [Model Optimizer](https://docs.openvinotoolkit.org/2020.2/_docs_MO_DG_Deep_Learning_Model_Optimizer_DevGuide.html) | This tool imports, converts, and optimizes models that were trained in popular frameworks to a format usable by Intel tools, especially the Inference Engine. Popular frameworks include Caffe*, TensorFlow*, MXNet*, and ONNX*. | 
| [Inference Engine](https://docs.openvinotoolkit.org/2020.2/_docs_IE_DG_inference_engine_intro.html) | This is the engine that runs the deep learning model. It includes a set of libraries for an easy inference integration into your applications. |
| Drivers for OpenCL™ | Enables OpenCL on the GPU/CPU for Intel® processors | 
| Intel® Media SDK | Offers access to hardware accelerated video codecs and frame processing | 
| [OpenCV](https://docs.opencv.org/master/) | OpenCV* community version compiled for Intel® hardware | 
| [Sample Applications](https://docs.openvinotoolkit.org/2020.2/_docs_IE_DG_Samples_Overview.html) | A set of simple console applications demonstrating how to use the Inference Engine in your applications | 
| [Demos](https://docs.openvinotoolkit.org/2020.2/_demos_README.html) | 	A set of console applications that demonstrate how you can use the Inference Engine in your applications to solve specific use-cases | 
| [Additional Tools](https://docs.openvinotoolkit.org/2020.2/_docs_IE_DG_Tools_Overview.html) | 	A set of tools to work with your models | 
| [Documentation for pre-trained models](https://docs.openvinotoolkit.org/2020.2/_models_intel_index.html) | Documentation for the pre-trained models available in the [Open Model Zoo repo](https://github.com/openvinotoolkit/open_model_zoo) | 


## 2.2 Install the Intel® Distribution of OpenVINO™ Toolkit Core Components
#### 2.2.1. Download the Intel® Distribution of OpenVINO™ toolkit package file 
1. Download the package from [here](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit/download.html?operatingsystem=linux&distributions=webdownload&version=2021.3%20(latest)&options=offline). 
2. Make sure you are signed in to Intel Developers Zone
3. Click `download`
4. Click `save file`
5. Click `OK`
7. Enter the following commands in the terminal:

```
sudo apt update
sudo apt upgrade
```

#### 2.2.2. Change directories to where you downloaded the Intel Distribution of OpenVINO toolkit for Linux* package file.
Make sure your package is downloaded, check the download icon in the top-right of the Firefox Browser.
If you downloaded the package file to the current user's Downloads directory:
```
cd ~/Downloads/
```
- Note: By default, the file is saved as l_openvino_toolkit_p_[version].tgz.

#### 2.2.3. Unpack the ```.tgz``` file:
```
tar -xvzf l_openvino_toolkit_p_[version].tgz
```
- Note: The files are unpacked to the l_openvino_toolkit_p_[version] directory.

#### 2.2.4. Go to the directory:

```
cd l_openvino_toolkit_p_[version]
```
- Note: If you have a previous version of the Intel Distribution of OpenVINO toolkit installed, rename or delete these two directories: 
```
~/inference_engine_samples_build
~/openvino_models
```
#### 2.2.5. Install with GUI installation wizard:
```
sudo ./install_GUI.sh
```
- Follow the instructions on your screen as follows:
1. Click `next`
2. Accept the terms of the license agreement
3. Click `next`
4. Agree or disagree to the collection of your information, recommended: `I do NOT consent`
5. Click `next`
6. Click `next`
7. Click `install`
8. Click `finish` when installation is completed
9. Now, linux will open a browserpage, ignore this and continue this tutorial at step 2.2.6!

- When installed as root the default installation directory for the Intel Distribution of OpenVINO is ```/opt/intel/openvino_2021.3.394/.```
- Note: For simplicity, a symbolic link to the latest installation is also created: ```/opt/intel/openvino_2021/```.

#### 2.2.6. A completement screen indicates that the core components have been installed.

## 2.3 Install External Software Dependencies
These dependencies are required for:
- Intel-optimized build of OpenCV library
- Deep Learning Inference Engine
- Deep Learning Model Optimizer tools

#### 2.3.1. Change to the ``` install_dependencies``` directory:
```
cd /opt/intel/openvino_2021/install_dependencies
```

#### 2.3.2. Run a script to download and install the external software dependencies:
```
sudo -E ./install_openvino_dependencies.sh
```
The dependencies are installed. Continue to the next section to set your environment variables.

## 2.4 Set the Envionment Variables
You must update several environment variables before you can compile and run OpenVINO™ applications. Run the following script to temporarily set your environment variables:
```
source /opt/intel/openvino_2021/bin/setupvars.sh
```


#### 2.4.1. Open the ```.bashrc``` file in ```<user_directory>```:
```
vi /.bashrc
```
#### 2.4.2. Add this line to the end of the file:
```
source /opt/intel/openvino_2021/bin/setupvars.sh
```
#### 2.4.3. Save and close the file: press the ```Esc``` key and type ```:wq```.
#### 2.4.4. To test your change, open a new terminal. You will see ```[setupvars.sh] OpenVINO environment initialized.```
The environment variables are set. Continue to the next section to configure the Model Optimizer.

## 2.5 Configure the Model Optimizer
The Model Optimizer is a Python*-based command line tool for importing trained models from popular deep learning frameworks such as Caffe*, TensorFlow*, Apache MXNet*, ONNX* and Kaldi*.

The Model Optimizer is a key component of the Intel Distribution of OpenVINO toolkit. You cannot perform inference on your trained model without running the model through the Model Optimizer. When you run a pre-trained model through the Model Optimizer, your output is an Intermediate Representation (IR) of the network. The Intermediate Representation is a pair of files that describe the whole model:

.xml: Describes the network topology
.bin: Contains the weights and biases binary data
For more information about the Model Optimizer, refer to the [Model Optimizer Developer Guide](https://docs.openvinotoolkit.org/2020.2/_docs_MO_DG_Deep_Learning_Model_Optimizer_DevGuide.html). 

#### 2.6 Configure all supported frameworks at the same time

#### 2.6.1. Go to the Model Optimizer prerequisites directory:
```
cd /opt/intel/openvino_2021/deployment_tools/model_optimizer/install_prerequisites
```
#### 2.6.2. Run the script to configure the Model Optimizer for Caffe, TensorFlow, MXNet, Kaldi*, and ONNX:
```
sudo ./install_prerequisites.sh
```

## 2.7 Run the Verification Scripts to Verify Installation
#### 2.7.1. Go to the Inference Engine demo directory:
```
cd /opt/intel/openvino_2021/deployment_tools/demo
```
#### 2.7.2. Run the Image Classification verification script:
```
./demo_squeezenet_download_convert_run.sh
```
This verification script downloads a SqueezeNet model, uses the Model Optimizer to convert the model to the .bin and .xml Intermediate Representation (IR) files. The Inference Engine requires this model conversion so it can use the IR as input and achieve optimum performance on Intel hardware.

#### 2.7.3. Run the Inference Pipeline verification script:
```
./demo_security_barrier_camera.sh
```
This script downloads three pre-trained model IRs, builds the Security Barrier Camera Demo application, and runs it with the downloaded models and the car_1.bmp image from the demo directory to show an inference pipeline. The verification script uses vehicle recognition in which vehicle attributes build on each other to narrow in on a specific attribute.

First, an object is identified as a vehicle. This identification is used as input to the next model, which identifies specific vehicle attributes, including the license plate. Finally, the attributes identified as the license plate are used as input to the third model, which recognizes specific characters in the license plate.

When the verification script completes, you will see an image that displays the resulting frame with detections rendered as bounding boxes, and text.

#### 2.7.4. Close the image viewer window to complete the verification script.
You have completed all required installation, configuration and build steps in this guide to use your CPU to work with your trained models.

#### Installation of OpenVINO completed!

## 2.8. Uninstall OpenVino
If you are done with OpenVino, follow these steps.

#### 2.8.1 Enter the installation path, find openvino_toolkit_uninstaller
```
cd /opt/intel/openvino_2021/openvino_toolkit_uninstaller
```
#### 2.8.2 If there is ubuntu use the GNOME desktop, try to uninstall using the GUI interface, more convenient. Please uninstall instructions step by step according to the operation.
```
sudo ./uninstall_GUI.sh
```
After the uninstall is complete cd to / opt / intel directory, see the installation package has been removed.

#### 2.8.3 open ```~/.bashrc```, delete environment variables
```
source /opt/intel/openvino_2021/bin/setupvars.sh
```


[Previous](https://github.com/mattijsk14/BinPicking/blob/main/Installation/1%20-%20Install%20ROS%202.md) /  [Next](https://github.com/mattijsk14/BinPicking/blob/main/Installation/3%20-%20Install%20packages.md)
