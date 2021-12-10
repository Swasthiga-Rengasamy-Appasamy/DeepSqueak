# Overview
DeepSqueak is a USV detection and analysis software suite that can perform human quality USV detection and classification automatically, rapidly, and reliably using cutting-edge regional convolutional neural network architecture (Faster-RCNN). DeepSqueak was engineered to allow non-experts easy entry into USV detection and analysis yet is flexible and adaptable with a graphical user interface and offers access to numerous input and analysis features. 

# Installation

DeepSqueak v3 relies on recently introduced neural network architecture and will only run on MATLAB 2020a or later.
To install MATLAB follow the instruction at https://in.mathworks.com/help/install/install-products.html

### Required Matlab toolboxes:
```
Computer Vision System Toolbox™
Curve Fitting Toolbox™
Image Processing Toolbox™
Deep Learning Toolbox™ (formerly Neural Network Toolbox™)
Parallel Computing Toolbox™
Statistics and Machine Learning Toolbox™
Signal Processing Toolbox™
```

Clone the repository
```
git clone https://github.com/DrCoffey/DeepSqueak.git
```

To run DeepSqueak, navigate to the main DeepSqueak folder in MATLAB, and type "DeepSqeak" into the command line. DeepSqueak will add itself to the MATLAB path after running.

### Troubleshooting
```
Q : DeepSqueak V3 requires MATLAB 20201 or later. It looks like you are use MATLAB
A : Update MATLAB to the latest version
```
```
Q : Toolbox not found
A : 1. Launch the MATLAB Installer
    2. Choose the necessary toolboxes.
    3. Install the toolboxes.
```

# Main Window
![Main Window](https://i.imgur.com/6KMLQiD.png)

**1\. Main Menus**

  - File: Working Folder Selection, Session Save, & Import/Export 

**2\. Call Statistics**

  - See [Export to Excel](export-to-excel)

**3\. Waveform and Extracted Contour**

  - Call [<span class="underline">contour</span>](contour-detection),
    slope line.
  - Contour extraction is now handled automatically
  - Contour extraction thresholds are still editable in Tools menu 

**4\. Working Folder Dropdowns**

  - Selected items will used when detect and load buttons are called

**5\. Detect, Load, and Record Buttons**

  - [Detect Calls] Load selected neural network and audio file
  - [Load Calls] Load selected detected call file
  - [Load Audio] Load selected audio file without any detections

**6\. Detection Review Buttons**

  - Keyboard shortcuts in parentheses
  - Drag box corners to adjust 
  - Right click to delete box
  - Double click for custom labels
  - Custom label keyboard shortcuts can be defined in "Tools "

**7\. Navigation Buttons**

  - [>] Move one call
  - [>>] Move one focus window
  - [>>>] Move one page window
 
**8\. Quick Access Settings**

  - [Focus] Change focus window (Labelled 11 in the figure) scale
  - [Page] Change page window (Labelled 10 in the figure) scale
  - [Scale] Change spectrogram display settings
  - [Colormap] Change colormap, invert colormap, adjust brightness/contrast

**9\. Complete Audio File Timeline**

  - Green curve represents detected call density
  - Click anywhere to jump locations in the file

**10\. Page Window**

  - View a large chuck of the audio file for better context
  - Click anywhere to move focus window (Labelled 11 in the figure)

**11\. Focus Window**

  - Adjust call boxes
  - Delete call boxes
  - Reject call boxes
  - Add new call boxes


# Recording Audio Files
```
1. Click "Record Audio" (Refer Main Window(5))
```
![Recording Menu](https://i.imgur.com/Ma0ImG7.png)
```
Paramters:
    Recording length: 
    Sample rate:
    Display time:
    Filename:
 - The recorded audio file is saved in the ****
```

# Loading Audio Files

- To load audio, select the folder where the audio is stored by selecting "File > Select Audio Folder".

- If the folder is successfully loaded, the audio files will appear in the "Audio Files" drop down menu.

- DeepSqueak is capable of reading WAV (\*.wav), .FLAC (\*.flac), and Ultravox (\*.UVD) audio files.

- DeepSqueak was tested with a sampling frequency of 250 kHz; however, the spectrograms are created using fft windows of constant duration, rather than constant sample numbers, so other sample rates are accepted.

# Training a detection network:

In order to detect the USVs from the sonogram we would need a trained detection network. 

Training a detection network can be done by feeding images with principles of image processing and spatial analysis.

## Creating images to train detection network:

- Click  the tools icon in the task bar 
- Choose "Network Training" in the drop down menu
- Choose "create detection network training images"
- Choose a pre-detected file for your network to use for training. 
- Output window is displayed
- Generated images are saved under the images folder

![Imgur](https://i.imgur.com/hXQGoEL.png)

Window description:

Window length

Overlap****************************

Nfft

Image length

Number of augmented duplicates

## Using images to train:

- Tools>network training>training detection network>choose images>save detection network in a folder.

## Detection of audio file:

Click the drop down menu for files in the task bar >select the network folder containing the required detection network>select audio folder containing the audio to be detected

In the left bottom :
##### image
Choose the respective network and audio files by clicking on the icons.

##### multiload
Window description:
********

ok>window showing number of  cell fragments and speed of detection
The detected file is saved in the folder that was earlier selected in step **** under “detection folder”.

## Loading and viewing the detected call:
Click the detected call file icon in the bottom left and select the preferred call to load. 
Click load call
You can see the sonogram with the detected syllables .
This version of deepsqueek is inbuilt with a denoising network and thus automatically rejects noise.This can be done manually too

## Manual selection:

Calls can be heard using the play call option.Calls can be accepted or rejected  . Unrecognised USVs can be recognised by using the draw option .
#image
The bar can be used to navigate around the entire call with respect to time.


# Classification:
DeepSqueak classifies the detected USV syllables to around 20-25 clusters . 

Unsupervised clustering is done without the input of labelled calls. The calls are  clustered as the software segregates USV types by analysing a detection file containing unsegregated detected USVs. 
Supervised classification requires a classifier network trained with *********. For  the training process , labelled USVs are required to train an efficient network.
This is done by using either supervised classifier or unsupervised clustering.

## Unsupervised Clustering:

Tools (task bar)>Call Classification>Unsupervised Clustering>clustering method

Window description:

K-Means:

Variational Auto-encoder:

ARTwarp:

Choose the clustering method. ARTwarp & Variational Auto Encoders are still experimental, so k-means is currently recommended


### Selecting K-Means:
Tools (task bar)>Call Classification>Unsupervised Clustering>clustering method>K-Means :
Here , one can choose to use previously existing models  to classify . (“Default is no”)

### By Choosing  pre existing clustering network:
Tools (task bar)>Call Classification>Unsupervised Clustering>clustering method>K-Means>clustering from existing model>yes>choose ******** file> choose the detection file that needs to be classified> The extracted contours can be saved .

  
### By building a customised  clustering network
Tools (task bar)>Call Classification>Unsupervised Clustering>clustering method>K-Means>clustering from existing model>no> choose detection or extracted file>save extracted contours if needed>window for choosing cluster parameters>

Window description:
Shape weight:
Frequency weight:
Duration weight:
 
Enter the weights (relative importance) of each of the three dimensions. 

Tools (task bar)>Call Classification>Unsupervised Clustering>clustering method>K-Means>clustering from existing model>no> choose detection or extracted file>save extracted contours if needed>window for choosing cluster parameters> window for cluster optimisation method( elbow optimised or user-defined)



### Elbow optimised:
Elbow optimization will cluster the data sequentially from 1 to max cluster and calculate the within cluster error. At the end of this procedure it will look for the elbow of the error curve and decide on an optimal number of clusters for the users data set.
On  selecting “elbow optimised”,the following window for cluster optimisation appears


Enter the maximum number of cluster to test (Default = 100)
Once clustering finishes, you will be prompted to save the model. This is optional.
You will be able to see a graph showing “normalised error” vs “number of clusters” and the cut-off or elbow location will thus be determined. 
example:

A new interface will appear, showing the clusters. This interface can also be found under "Tools > Call Classification > View Clusters"

### User Defined:
Tools (task bar)>Call Classification>Unsupervised Clustering>clustering method>K-Means>clustering from existing model>no> choose detection or extracted file>save extracted contours if needed>window for choosing cluster parameters> window for cluster optimisation method( elbow optimised or user-defined)>user defined>window for choosing number for k means(default:15)>


K-means number:*******************
A new interface will appear, showing the clusters. This interface can also be found under "Tools > Call Classification > View Clusters"

### Viewing clusters:
Name the clusters by entering a name in the text box. Clusters with the same name will be merged upon saving.

View different clusters with the "Next" and "Back" buttons.

View more calls within a cluster with the "Next Page" and "Previous Page" buttons.

Reject calls by clicking on them. Calls highlighted in red will be rejected upon saving.

Update the call files by clicking "Save", or redo the clustering with "Redo"


VAE
ARTwarp:




Supervised classification:
Uses a trained network to classify and name the detected USV calls
This network operates on the spectrogram, rather than the contour.
 

Training a supervised classifier:
The supervised classifier requires a detection file with labels.
Tools>network training> train supervised classifier>select detection file>
A window showing the training process is now displayed. There are two main graphs shown :accuracy vc iteration and loss vs iteration. This process  can be terminated at any point by clicking the stop button on the top right corner.

Once the training process is complete , the trained network can be saved and a confusion matrix is displayed.******************


## Classification using a network:
tools>call classification>supervised classification>select the preferred network> choose the detection file that needs classification
You can save the output label either by updating the detection file or in another file. The detection file can be viewed in MATLAB or exported to Excel (See Export to Excel).

# Syntax analysis:

Click "Tools > Call Classification > Syntax Analysis"

In the dialog box, select the files you wish to use. You may choose either detection files(*.mat), or the exported call statistics files (.xlsx)

A dialog box will appear. Enter the maximum call separation, in seconds, to define a bout, and a threshold for excluding uncommon call categories.

After the files are loaded, a transition matrix, and syntax graph will appear.


A dialog box will appear, giving the option to save the transition matrix and syllable counts as an Excel table.
