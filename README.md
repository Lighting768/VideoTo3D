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
   ```

2. **Run the automated setup**:
   Double-click `run.bat` or run:
   ```bash
   python setup.py
   ```
   *This automatically verifies CUDA, installs Python dependencies, and ensures bundled FFmpeg and COLMAP binaries are present.*

3. **Launch the Application**:
   ```bash
   run.bat
   ```
   *or:*
   ```bash
   python VideoTo3D.py
   ```

4. **Verify System Setup**:
   ```bash
   python VideoTo3D.py --check
   ```

---

## 🖥️ User Guide

### 🛰️ Drone 3D Reconstruction Workflow
1. Navigate to the **COLMAP / NeRF** tab.
2. Click **Browse** and select your drone video (`.mp4` / `.mov`).
3. *(Optional)* Select your flight metadata or DJI `.srt` file. The GPS parser will display coordinates, bounding box, and altitude stats.
4. Set **Sample FPS** (typically `2.0` to `3.0` fps).
5. Ensure **Use GPU (CUDA)** and **Dense Reconstruction** are checked.
6. Click **▶ Run Full Pipeline**.
7. Once finished:
   * View the camera path in **Camera Positions**.
   * Inspect the 3D model in the **3D Model (Interactive)** tab.
   * Click **Open in 3D Browser Viewer** to view with full OrbitControls.
   * Click **Save / Download 3D** and choose your desired format (`GLB`, `OBJ`, `PLY`, `LAS`, `GeoTIFF`, or `ZIP`).

### 🎬 2D to VR 3D Video Conversion Workflow
1. Go to the **3D Generator** tab.
2. Select your input video or photo.
3. Choose your depth model (e.g., *Depth Anything V2 Small* for high speed or *Large* for maximum detail).
4. Select your **Stereo Format** (e.g., `half_sbs` for VR headsets).
5. Adjust **Strength** and **FG Pop** sliders.
6. Click **⚡ Preview** to inspect the 2D stereo result and rotate the generated **Interactive 3D model**.
7. Click **▶ Render** to generate the final stereoscopic video.

---

## 📁 Repository Structure

```text
VideoTo3D/
├── VideoTo3D.py              # Main GUI application entry point
├── run.bat                   # 1-click Windows launcher
├── setup.py                  # Automated dependency installer & hardware detector
├── requirements.txt          # Python dependencies
├── config.json               # Application configuration
├── bin/                      # Bundled portable binaries
│   ├── ffmpeg.exe            # Video encoding/decoding engine
│   ├── ffprobe.exe           # Stream analysis
│   └── colmap/               # Portable CUDA-enabled COLMAP binary
├── core/                     # Processing & algorithm backend
│   ├── colmap_pipeline.py    # SfM & MVS pipeline manager
│   ├── gps_parser.py         # DJI SRT, CSV, GeoJSON GPS parser
│   ├── mesh_exporter.py      # OBJ, PLY, GLB, LAS, GeoTIFF, FBX exporters
│   ├── depth_engine.py       # AI depth estimation model manager
│   ├── stereo_renderer.py    # Stereoscopic disparity warping engine
│   ├── frame_processor.py    # Video I/O & frame manipulation
│   ├── rife_interpolator.py  # AI motion interpolation
│   └── upscaler.py           # Super-resolution upscaling
└── ui/                       # Modern dark-mode Qt interface
    ├── main_window.py        # Top-level window and tab management
    ├── model_3d_viewer.py    # Interactive 3D point cloud & mesh viewer
    ├── camera_preview.py     # 3D trajectory visualizer
    ├── preview_widget.py     # 2D image preview component
    ├── tab_3d_generator.py   # Stereo VR conversion tab
    ├── tab_colmap.py         # Photogrammetry & reconstruction tab
    ├── tab_depth.py          # Standalone depth estimation tab
    ├── tab_fps_upscale.py    # Frame rate interpolation & upscaling tab
    └── style.py              # CSS/QSS dark design system
```

---


### Installation
1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/VideoTo3D.git
   cd VideoTo3D
