# VideoTo3D 🎥 ➡️ 🧊

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![PyQt6](https://img.shields.io/badge/GUI-PyQt6-green.svg)](https://riverbankcomputing.com/software/pyqt/)
[![CUDA Accelerated](https://img.shields.io/badge/CUDA-12.x%20Ready-76B900.svg)](https://developer.nvidia.com/cuda-zone)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**VideoTo3D** is an all-in-one desktop application designed for **Photogrammetry, 3D Drone Scene Reconstruction, and AI-Powered 2D-to-VR 3D Conversion**.

Turn normal 2D videos, drone footage (1080p/4K), and images into **interactive 3D models (OBJ, PLY, GLB, LAS, GeoTIFF)** and **immersive stereoscopic 3D video (Side-by-Side, Anaglyph, VR180)**.

---

## 🌟 Key Capabilities

### 🚁 1. Drone Photogrammetry & 3D Reconstruction (SIH Compliant)
* **Drone Video Processing**: Ingest 1080p and 4K aerial footage with customizable sampling rates.
* **GPS & Flight Metadata Geotagging**: Native parsing of DJI subtitle files (`.srt`), CSV telemetry, JSON, and GeoJSON flight logs.
* **Full SfM & MVS Pipeline**:
  1. Automated frame extraction
  2. Feature extraction & sequential matching (CUDA-accelerated)
  3. Sparse mapper (reconstructing camera trajectory and sparse points)
  4. Multi-View Stereo (MVS) depth estimation via PatchMatch
  5. Stereo fusion & Poisson surface reconstruction
* **High Performance**: Optimized for RTX 4050/4060 GPUs to reconstruct a 10-minute video in under 15 minutes.
* **Multi-Format 3D Export**:
  * **Meshes & 3D Models**: `.glb`, `.gltf`, `.obj`, `.ply`, `.fbx`
  * **GIS & Point Clouds**: `.las` (LiDAR standard), `.ply`
  * **Orthophoto / Elevation**: GeoTIFF (`.tif`)
  * **One-Click Bundle**: Export all formats simultaneously into a compressed `.zip`.

### 🎮 2. Interactive 3D Model Viewers
* **Native Desktop Viewer**: Embedded 3D canvas with full mouse interaction (Left-click drag to rotate in 3D, scroll wheel to zoom, right-click drag to pan).
* **1-Click WebGL Browser Viewer**: Automatically generates an offline-ready HTML5 Three.js viewer with smooth OrbitControls, grid helpers, and dynamic lighting.

### 👓 3. AI 2D-to-3D Stereo Video Generator (VR & 3D Displays)
* **Depth Estimation**: Powered by state-of-the-art vision models:
  * *Depth Anything V2* (Small / Base / Large)
  * *Distill-Any-Depth*
  * *Video Depth Anything* (temporal stabilization)
  * *Marigold Depth* (diffusion-based)
* **Stereo Output Formats**:
  * **Half-SBS (Side-by-Side)**: Standard for Meta Quest, Apple Vision Pro, and VR video players.
  * **Full-SBS**: Full 1:1 resolution per eye.
  * **Anaglyph**: Red/Cyan glasses compatibility.
  * **VR180**: Hemispherical equirectangular projection.
  * **Passive Interlaced**: Row-interleaved for 3D TVs.
* **Comfort & Disparity Analytics**: Real-time parallax and comfort scoring to eliminate visual strain.

---

## 🚀 Quick Start

### Prerequisites
* Windows 10 / 11 (64-bit)
* NVIDIA GPU (RTX 30xx/40xx series recommended with CUDA 12.x; CPU fallback supported)
* Python 3.10+ (or Anaconda / Miniconda)

### Installation
1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/VideoTo3D.git
   cd VideoTo3D
