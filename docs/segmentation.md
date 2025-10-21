# Image Segmentation

## Setup
Before touching the code, ensure that:
- ``C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.29.30133\bin\HostX64\x64`` is added to the PATH. This should be the 2019 toolkit. 
- CUDA toolkit has been installed.
- Visual Studio 2022 is version 17.4.6. I didn't find success using the latest version of Visual Studio 2022.

I used Windows Command Prompt for the initial setup and optimizing for the code. Be sure to close and reopen a new cmd window everytime you make manual file changes.

### Cloning the Repository
I first cloned the repository, which could be found in the ``C:User/<username>`` folder.
```
git clone https://github.com/graphdeco-inria/gaussian-splatting --recursive
```
### Installing Language Segment-Anything
To install the optimizer, I created a Conda environment. 

``conda create -n lang-sam``

``conda activate gaussian_splatting``

NOTE: Always activate the gaussian_splatting environment before executing code.

``conda install -c conda-forge vs2022_win-64
pip install torch==1.13.1+cu117 torchvision==0.14.1+cu117 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu117``

NOTE: Certain versions of PyTorch and CUDA are not compatible. The versions above worked well for me.

### Installing Submodules
In the initial setup of the environment, the submodules did not install properly. It will  be done here. 

``cd C:\Users\<username>\gaussian-splatting``

``pip install submodules/diff-gaussian-rasterization``

``pip install submodules/simple-knn``

``pip install plyfile``

``pip install tqdm``

NOTE: I had failed installing the submodules many times. Using the Visual Studio 2019 C++ toolkit seemed to fix the issue. 

## Data Preparation
Both videos and images can be used. 
First, I renamed the video for clarity and moved it into ``../gaussian-splatting/input_data``. For example, with a video called ``room.mp4``:

```
📂.../ 
├──📂gaussian-splatting/ 
│   ├──📂input_data/
│   │	├──room.mp4		
│   │   │...
│   │...
│...
```

Now, opening Command Prompt again, input:
```
conda activate gaussian_splatting
cd gaussian-splatting
```
With the video in the correct location, input:
```
ffmpeg -i input_data/room.mp4 -r 1/1 input_data/room/image%03d.png
```
This will output a series of images inside ``../gaussian-splatting/input_data/room``. 

Images need to be setup in a specific way so that COLMAP can recognize it. I created another folder and manually moved the images into it. The structure is seen below:

```
📂.../ 
├──📂gaussian-splatting/ 
│   ├──📂input_data/
│   │	├──📂room/
│   │	│	├──📂input/
│   │	│	│	├── 🖼️ <image 0>
│   │	│	│	├── 🖼️ <image 1>
│   │	│	│	│...
│   │   │...
│   │...
│...
```
For optimization to work, COLMAP needs to format the images properly.
```
python convert.py -s input_data/room --colmap_executable "C:\Users\<username>\colmap-x64-windows-cuda\COLMAP.bat"
```
NOTE: COLMAP may be installed in a different location on your computer. Just change the path of COLMAP accordingly.

## Optimizing the data
With the Conda environment active and the correct directory on Command Prompt, input:

```
python train.py -s input_data/room
```

This step takes the longest. The code will generate a new folder in ````../gaussian-splatting/output`` that will contain the data. The name of the folder is usually randomized. I changed the name of this folder for clarity. The structure can be seen below:

```
📂.../ 
├──📂gaussian-splatting/ 
│   ├──📂output/
│   │	├──📂room/ # original name was "ade9c340-8"
│   │	│	├──📂point_cloud/
│   │	│	│	├──📂iteration_7000/
│   │	│	│	├──📂iteration_30000/ 
│   │	│	│...		
│   │   │...
│   │...
│...
```

## Viewing the 3D Gaussian Splats in SIBR
The original repository uses SIBR to view the generated model, called``SIBR_gaussianViewer_app.exe``. You can find it [here](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/binaries/viewers.zip).

Extract the zip file and move it to the ``../gaussian-splatting`` folder. 

To set it up:

```
cd C:\Users\<username>\gaussian-splatting\viewers\bin

SIBR_gaussianViewer_app.exe -m C:\Users\<username>\gaussian-splatting\output\room
```
This should open the viewer, of which you can explore the model in.