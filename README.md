# Cephalometric Landmark Detection using YOLOv11 and Graph Neural Networks (GNNs)

## 🧠 Abstract

Accurate detection of cephalometric landmarks is crucial for orthodontic diagnosis and treatment planning. Manual annotation is time-consuming and error-prone. To address this, we propose a hybrid deep learning framework that combines:

- **YOLOv11** for fast, coarse landmark detection
- **Graph Neural Networks (GNNs)** for refinement using spatial relationships

Our method was trained on the **ISBI 2015** dataset and evaluated on the **PKU** dataset. Results:

- **ISBI**: 77.37% detection rate within 2mm, Mean Radial Error (MRE): **1.58 ± 0.92mm**
- **PKU**: 78.12% detection rate within 2mm, MRE: **1.47 ± 1.07mm**

---

## 🔑 Keywords

`Cephalometric Analysis`, `Deep Learning`, `YOLO`, `Medical Imaging`, `Web-based Platform`, `Orthodontics`

---

## 📚 Introduction

Cephalometric analysis is essential for orthodontics and surgical planning. Traditional landmark annotation is manual, slow, and inconsistent. Our approach automates this with:

1. **YOLOv11**: Detects coarse locations of 19 cephalometric landmarks
2. **GNNs**: Refines detection using anatomical graphs

We also developed a full-featured **web-based DICOM viewer** with:
- AI overlays
- Measurement tools
- Structured reporting
- Docker-based deployment

---

## 🧾 Literature Review

Traditional methods like ASM, AAM, and template matching lacked generalizability. CNNs improved detection but ignored landmark relationships. GNNs provide a promising path by modeling both **local features** and **global dependencies** among landmarks.

---

## 📊 Dataset

### 📁 ISBI 2015 Cephalometric Dataset
- 400 lateral cephalograms
- 19 manually annotated landmarks (by 2 specialists)
- Resolution: 1935 × 2400 px (0.1 mm²/pixel)

### 🔧 Data Preparation
- Resized to **1000 × 1000 px**
- Train/Val/Test Split: 280 / 80 / 40
- Data Augmentations:
  - CLAHE, Histogram Equalization
  - Brightness, Contrast
  - Rotation, Shifting, Scaling
  - Gaussian Blur

Final training set: **1,400 images**

---

## 🏗️ Proposed Framework

### 🎯 Stage 1: YOLOv11 Object Detection
- 19 classes (each landmark is a class)
- Bounding box: 128×128 centered on the landmark
- Anchor-free, high-speed detection using attention mechanisms

### 🔗 Stage 2: GNN-Based Landmark Refinement

#### 📐 Graph Construction
- Nodes = landmarks
- Edges = spatial relationships between them

#### 🔍 Node Features
- Coordinates from YOLOv11
- Appearance features from **InceptionV3**-based ROI (512×512)

#### 🔁 Message Passing in GNN
- Leverages both **local** and **global** anatomical relationships

#### 🧩 GNN Modules

- **Graph Isomorphism Network (GIN)**:
  \[
  x'_i = \text{MLP} \left( (1 + \epsilon) \cdot x_i + \sum_{j \in \mathcal{N}(i)} x_j \right)
  \]

- **Dynamic Edge Convolution**:
  \[
  e_{ij} = h_0(x_i, x_j - x_i)
  \]
  - Graph is reconstructed dynamically at each forward pass

---

## 🖥️ Web-Based Platform

Built for real-world clinical integration with:

- **Cornerstone3D** DICOM viewer
- Annotation tools
- AI overlay support
- Structured reporting
- **Dockerized** deployment for portability

---

## 📈 Performance Summary

| Dataset | Success Rate (≤2mm) | Mean Radial Error (mm) |
|---------|----------------------|-------------------------|
| ISBI    | 77.37%               | 1.58 ± 0.92             |
| PKU     | 78.12%               | 1.47 ± 1.07             |

---

## 📌 Technologies Used

- YOLOv11 (Object Detection)
- GNN (Graph Isomorphism Network, Dynamic EdgeConv)
- InceptionV3 (Feature Extraction)
- Cornerstone3D (DICOM Viewer)
- Docker (Deployment)

  ## Contributors

<table>
  <tr>
    <td align="center">
   <td align="">
    <a href="https://github.com/merna-abdelmoez" target="_black">
    <img src="https://avatars.githubusercontent.com/u/115110339?v=4" width="150px;" alt="Merna Abdelmoez"/>
    <br />
    <sub><b>Merna Abdelmoez</b></sub></a>
    <td align="center">
    <a href="https://github.com/Habiba-Mohsen" target="_black">
    <img src="https://avatars.githubusercontent.com/u/101303283?v=4" width="150px;" alt="Habiba Mohsen"/>
    <br />
    <sub><b>Habiba Mohsen</b></sub></a>
    </td>
    </td>
    <td align="center">
    <a href="https://github.com/Hazem-Raafat" target="_black">
    <img src="https://avatars.githubusercontent.com/u/100636693?v=4" width="150px;" alt="Hazem Raafat"/>
    <br />
    <sub><b>Hazem Raafat</b></sub></a>
    </td>
    </td>
    </tr>
 </table>

---


---


