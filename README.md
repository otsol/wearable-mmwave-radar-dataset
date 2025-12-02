# wearable-mmwave-radar-dataset
This GitHub repository is dedicated for a wearable mmWave radar dataset presented in an upcoming article (paper name and link will be added here). The dataset collected from 11 participants provides a collection of 3300 equal length samples that each contain one gesture movement tracked by the radar. The charateristics of the participants, the radar system parameters and the experimental setup are explained in detail in the aforementioned article.

The dataset is currently (2025-12-02) hosted on Hugging Face website. See "How to Download". This GitHub page is dedicated to displaying information and used as an anchor if the location of the files would change in the future. Please note that the dataset is large, approximately 22 GB in total size.

Link to the dataset files:
https://huggingface.co/datasets/otsol/wearable-mmwave-radar-dataset. 

In the following, a summary of the dataset, a more detailed description of the files and a guide for downloading the dataset is presented.

## Summary

### Dataset
The dataset is collected from 11 participants between August and September 2025 using DEMO BGT60TR13C 60 GHz radar evaluation kit manufactured by Infineon Technologies AG, Germany. 300 samples were collected from each participant, 30 samples from 10 classes of gestures, totaling 3300. Lenght of one sample is 71 radar frames which is just under 3 seconds.

### Ten Gestures
| Gesture           | Description                                             |
| ----------------- | ------------------------------------------------------- |
| **pinch-index**   | Pinching the index finger against the thumb.            |
| **release-index** | Releasing the pinched index finger and thumb.           |
| **palm-to-fist**  | Closing an open hand into a fist.                       |
| **fist-to-palm**  | Opening a fist into an open palm.                       |
| **palm-only**     | Holding the hand open without movement.                 |
| **horn**          | Opening the fist into the “horns” hand sign.            |
| **finger-slider** | Sliding the thumb toward the fingertip and back twice.  |
| **v-sign**        | Straightening the index and middle fingers from a fist. |
| **pinch-pinky**   | Pinching the little finger against the thumb.           |
| **phone**         | Straightening the little finger and thumb from a fist.  |


### Radar System parameters
The radar has a 5 GHz bandwidth between 58-63 GHz. Data is collected 24 (radar) frames per second. The device is an interrupted frequency-modulated continuous wave (FMCW) radar which means that is has pause between each chirp and a longer pause between each collected frame. The radar has one transmitting (TX) channel and three simultaneous receiving (RX) channels.

### Data Collection
The novel idea presented in the article is to place a mmWave radar pointing toward the skin just a few millimiters away. It is placed on top of the carpal tunnel on the inside of the wrist. The prototype is quite similar to the form of a smart watch, held in place by a plastic enclosure and a wrist strap.

## Description of the Dataset

### File Structure
The file structure of the *Hugging Face dataset* repository is as follows:
The folder "wearable-mmwave-radar-dataset" includes a subdirectory for each participants from "person_12" to "person_22". Under each participant, there are 10 folders labeled after the gesture name. The folder names are the same as in the table "Ten Gestures". In addition, each directory representing a participant has a "metadata.txt" file which includes physiological measurements of the participant, including age, height etc.
```
wearable-mmwave-radar-dataset/
└── person_12/
    └── ...
    └── pinch-pinky/
        └── sample_0.npy
        └── ...
        └── sample_29.npy
    └── metadata.txt
└── ...
└── person_22/
└── sequence.json
```
Each directory labeled after gestures has 30 sample files from "sample_0.npy" to "sample_29.npy". These are the individual gesture samples. In addition, the radar parameters are have been saved to "wearable-mmwave-radar-dataset/sequence.json" file. Radar parameters do not change between classes or users.

### Format of .npy Files
The recorded data is in numpy float32 format. In the .npy files, the data is saved as a 4D tensor with (F, C, N, M) dimensions, where F is the number of radar frames in time domain, C is the number of receiver antennas, N is the number of up-chirps in one frame and M is the number of data points. The collected tensors have shape (71,3,64,64).

### Minimal Example
```
import numpy as np
data = np.load("wearable-mmwave-radar-dataset/person_11/pinch-index/sample_1.npy")
print("One sample")
print(data.dtype)
print(data.shape)
```
Output:
```
One sample
float32
(71, 3, 64, 64)
```

## How to Download
Currently (2025-12-02), the dataset is available from 
https://huggingface.co/datasets/otsol/wearable-mmwave-radar-dataset.

The dataset can be downloaded using "datasets" or "croissant" Python packages, or by using Git Large File Storage (LFS) or Xet backend.

Reference the Hugging Face documentation for details:
https://huggingface.co/docs/hub/datasets-downloading
