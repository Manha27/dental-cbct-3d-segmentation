---

# Deep Learning-Based Segmentation of Edentulous Regions in CBCT Scans

This repository contains a deep learning pipeline designed to automatically identify **edentulous (missing tooth) regions** in dental **Cone Beam Computed Tomography (CBCT)** scans.
The system performs **3D multi-class segmentation** of dental anatomy using a **3D U-Net architecture implemented with MONAI and PyTorch**, enabling clinicians to visualize missing tooth spaces directly from volumetric scans.

The work was developed as part of a research internship at **NIT Calicut**. 

---

# Overview

Dental implant planning requires accurate identification of anatomical structures and the **exact space where a tooth is missing**. Traditionally this is done manually by clinicians, which is time-consuming and may vary between experts.

This project explores how **deep learning-based volumetric segmentation** can automate this task. The proposed system processes CBCT scans, performs preprocessing and label merging, and trains a neural network to generate voxel-wise predictions for dental structures and edentulous regions.

The final output is a **segmented 3D volume** that can be visualized in clinical tools such as **3D Slicer** for implant planning.

---

# Key Features

* Automated **3D segmentation of dental CBCT volumes**
* Detection of **edentulous regions for implant planning**
* Multi-class segmentation including:

  * Maxilla and upper skull
  * Mandible
  * Upper teeth
  * Lower teeth
  * Mandibular nerve
  * Edentulous regions
* Preprocessing pipeline for **medical imaging formats**
* Training pipeline using **MONAI + PyTorch**
* Exportable segmentation outputs compatible with **clinical visualization software**

---

# Dataset

The dataset consists of **167 CBCT scans** collected from clinical imaging sources. 

Each scan represents a full dental arch and includes manually annotated segmentation masks.

### Data Characteristics

* Format: **DICOM volumes**
* Converted to: **NIfTI**
* Manual annotations created in **3D Slicer**
* Edentulous regions labeled manually and merged with existing anatomical segmentations

---

# Pipeline

The workflow of the system follows these main stages:

```
CBCT Scan
   ↓
Preprocessing
   ↓
Label Generation & Merging
   ↓
3D U-Net Training
   ↓
Segmentation Prediction
   ↓
Evaluation & Visualization
```

---

# Preprocessing

To standardize input volumes, the following preprocessing steps are applied:

* DICOM → NIfTI conversion
* Orientation normalization
* Voxel spacing resampling
* Intensity normalization
* Foreground cropping
* Data augmentation (rotation, flips, intensity variations)

These steps improve model stability and help the network generalize to different scan conditions.

---

# Model Architecture

The core segmentation model is a **3D U-Net**, which is widely used for volumetric medical image segmentation.

### Architecture Highlights

* Encoder–decoder structure
* Skip connections for multi-scale feature fusion
* Multi-class voxel-wise prediction
* Implemented using **MONAI’s UNet module**

Loss function:

```
Combined Dice Loss + Cross Entropy Loss
```

Optimizer:

```
Adam optimizer
Learning rate = 1e-4
```

---

# Training Setup

* Framework: **MONAI + PyTorch**
* Environment: Python + Jupyter
* GPU-based training
* Training epochs: **500**
* Dataset loader: **MONAI CacheDataset**

Training progress was monitored using:

* Training loss
* Validation loss
* Dice coefficient per class

---

# Results

The trained model successfully segments multiple anatomical structures from CBCT volumes.

### Mean Dice Scores

| Structure             | Dice Score |
| --------------------- | ---------- |
| Maxilla & Upper Skull | 0.62       |
| Mandible              | 0.65       |
| Mandibular Nerve      | 0.55       |
| Upper Teeth           | 0.61       |
| Lower Teeth           | 0.63       |
| Edentulous Region     | 0.58       |
| Other Structures      | 0.59       |

**Overall Mean Dice Score:** ~0.60 

Despite anatomical variability and imaging artifacts, the system demonstrates reliable segmentation performance.

---

# Technologies Used

* Python
* PyTorch
* MONAI
* SimpleITK
* nibabel
* pynrrd
* tqdm
* 3D Slicer

---

# Future Improvements

Possible directions to extend this work include:

* Increasing dataset size and diversity
* Incorporating **attention-based or transformer architectures**
* Improving boundary refinement with **CRF or morphological post-processing**
* Estimating **bone density and bone quality** for implant suitability
* Integrating the pipeline directly with **clinical implant planning systems**

---

# References

Key references that influenced this work include research on U-Net segmentation and deep learning in dental imaging.

* Ronneberger et al., *U-Net: Convolutional Networks for Biomedical Image Segmentation*
* MONAI Consortium – Medical Open Network for AI
* Park et al., Deep learning-based missing tooth detection
* 3D Slicer medical imaging platform 

---
