

# 🧠 Comparative Analysis of 3D Deep Learning Models on ModelNet10
This repository benchmarks 3D object classification on the ModelNet10 dataset, with a focus on our
PointNet implementation. We convert the ModelNet10 .mesh (.off) files into point clouds (sampling 1024
surface points per object) and normalize them to a unit sphere . The core of the code is a PyTorch
PointNet trained for 10-way classification. For comparison, we also include subdirectories documenting
several voxel- and graph-based models: a voxel CNN (ModelNet-CNN), VoxNet (shallow 3D CNN) ,
Voxception-ResNet (deep 3D ResNet-Inception network) , and a Graph Convolutional Network (e.g.
DGCNN on point clouds) . Each of these has its own README summarizing architecture, training
setup, and performance.

---

## 🗂️ System Overview

<p align="center">
  <img src="results/system_overview.png" width="700">
</p>

The process involves:
1. **EDA** (Exploratory Data Analysis) — Data distribution and t-SNE visualization  
2. **Point Cloud Dataset Creation** → Augmentation (`jitter`, `shuffle`)  
3. **Voxel Grid Dataset Creation** → Augmentation (`rotation`, `flip`)  
4. **Model Training and Evaluation**

---

## 🚀 Models Implemented

| Model | Representation Type | Framework | Accuracy |
|--------|---------------------|------------|-----------|
| PointNet | Point Cloud | PyTorch | **90%** |
| ModelNet-CNN | Voxel Grid | PyTorch | 87% |
| Graph Convolution Network (GCN) | Graph/Mesh | PyTorch Geometric | 82% |
| VoxNet | Voxel Grid | PyTorch | 79% |
| Voxception-ResNet | Voxel Grid | PyTorch | 76% |

---

## 🧩 Dataset

- **Dataset:** [ModelNet10](https://modelnet.cs.princeton.edu/)
- **Format:** `.off`
- **Classes:** 10 object categories (e.g., chair, table, sofa, bathtub)
- **Preprocessing:** Conversion to point clouds and voxel grids

---
## 📊 Results & Analysis

| Model | Accuracy | Precision | Recall | F1-Score | Time Efficiency |
|--------|-----------|------------|---------|-----------|----------------|
| **PointNet** | **90%** | **0.91** | **0.90** | **0.90** | 21s |
| **ModelNet-CNN** | 87% | 0.86 | 0.86 | 0.86 | 42s |
| **Graph Convolution Network (GCN)** | 82% | 0.81 | 0.82 | 0.81 | 3m 10s |
| **VoxNet** | 79% | 0.79 | 0.78 | 0.78 | **0.93s** |
| **Voxception-ResNet** | 76% | 0.74 | 0.75 | 0.75 | 3.31 hours |

## Model Performance Comparison 

The table above summarizes our classification accuracies. PointNet (point-based MLP network) achieves
the highest accuracy (90%), while volumetric CNNs lag behind (ModelNet-CNN 87%, VoxNet 79%,
Voxception-ResNet 76%). A graph-based point cloud network (GCN/DGCNN) achieves about 82%. These
results align with recent studies showing point-based networks outperform voxel-CNNs on ModelNet10
. In particular, Shamil et al. report PointNet at 90%, vs. 87% for a voxel-CNN, 79% for VoxNet, and
76% for a deep ResNet-Inception model

### Key Observations
- 🟢 **PointNet** achieved the **best overall performance** across all metrics (accuracy, precision, recall, and F1-score) with a balanced computation time of **21 seconds**.  
- ⚡ **VoxNet** was the **most time-efficient model** (0.93 seconds per epoch) while maintaining moderate performance — ideal for **real-time or low-compute applications**.  
- 🔵 **ModelNet-CNN** showed strong voxel-based learning stability.  
- 🔴 **Voxception-ResNet**, although deep, was **computationally intensive (3.31 hours)** and achieved **lowest F1 score**, making it less practical for lightweight 3D classification tasks.

---

<p align="center">
  <img src="results/system_overview.png" width="700">
</p>


## ⚙️ Installation

```bash
git clone https://github.com/yourusername/3D-Model-Classification-on-ModelNet10.git
cd 3D-Model-Classification-on-ModelNet10
pip install -r requirements.txt
