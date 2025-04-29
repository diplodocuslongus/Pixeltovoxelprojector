# Pixeltovoxelprojector
Projects motion of pixels to a voxel
A system for projecting 2D pixel motion into 3D voxel space, mainly used for astronomical image processing and motion analysis.

g++ -std=c++17 -O2 ray_voxel.cpp -o ray_voxel

needs json.hpp

pip install pybind11
pip install -e .


## Project structure

```
.
├── ray_voxel.cpp # Core ray casting algorithm
├── process_image.cpp # Image processing module
├── spacevoxelviewer.py # Astronomical visualization tool
├── voxelmotionviewer.py # 3D voxel viewer
├── setup.py # Build script
└── examplebuildvoxelgridfrommotion.bat # Example run script
```

## Core component details

### C++ core module

#### ray_voxel.cpp
- Load camera parameters and image sequence metadata from JSON file
- Implement the Digital Differential Analyzer (DDA) algorithm for efficient ray casting
- Detect pixel motion changes between consecutive frames
- Build 3D voxel grid and save in binary format
- Key functions:
- Euler angle to rotation matrix conversion
- Intersection detection between rays and voxel grid
- Motion vector calculation and aggregation

#### process_image.cpp
- Use pybind11 to provide Python interface
- Process astronomical images in FITS format
- Implement background subtraction and noise filtering
- Support OpenMP parallel computing
- Update voxel grid and celestial sphere texture data

### Python visualization tool

#### spacevoxelviewer.py
- Read FITS astronomical image files
- Calculate the position of the earth and the direction of the telescope
- Call C++ module to process image sequence
- Visualize analysis results:
- 3D voxel grid
- Celestial sphere texture mapping
- Motion trajectory analysis

#### voxelmotionviewer.py
- Interactive 3D visualization interface
- Support the following functions:
- Voxel grid rotation and scaling
- High brightness voxel screening
- Animation recording of perspective
- Automatic screenshot saving
- Efficient 3D rendering using PyVista

## Technical details

### Ray casting algorithm
- Using the Digital Differential Analyzer (DDA) algorithm
- Support voxel grids of arbitrary resolution
- Configurable ray step size and sampling rate

### Parallel processing
- Multithreading using OpenMP
- Parallelization of image processing
- Ray casting task distribution

### Astronomical calculations
- Accurate coordinate system transformations
- Telescope pointing calculations
- Time series analysis

## Installation and usage

### Dependencies
- C++17 compiler
- Python 3.8+
- pybind11
- OpenMP
- PyVista
- Astropy

### Build steps
1. Install dependencies: `pip install -r requirements.txt`
2. Compile C++ module: `python setup.py build_ext --inplace`
3. Run the example: `examplebuildvoxelgridfrommotion.bat`

### Usage 

1. Prepare input data:
- Image sequence (FITS format)
- Camera parameter JSON file
2. Run the process:
```bash
./ray_voxel input.json output.bin
```
3. Visualize the results:
```python
python voxelmotionviewer.py output.bin
```

## Applications (see youtube video)

- Astronomical Satellite Trajectory Analysis
- Space Debris Motion Tracking
- Anomaly Detection in Telescope Images
- 3D Visualization of Scientific Data

