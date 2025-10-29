# Image Segmentation

### Installing Language Segment-Anything

By using a segmentation mask to pre-process the images, the manual process of editing background splats in the final rendered model is reduced.

Language Segment-Anything is a package used for object detection and image segmentation. To install the Language Segment-Anything model, create a new Conda environment. 

``conda create -n lang-sam``

``conda activate lang-sam``

Clone the repository and change directory into it.
```
git clone https://github.com/luca-medeiros/lang-segment-anything && cd lang-segment-anything
```
Install the package as such:
```
pip install -e .
```

## Data Preparation
The images are setup in the same format format as COLMAP. This is because the segmentation step must be ran AFTER creating a point cloud from COLMAP. Please refer to the "Data Preparation" section under [Setting up 3DGS](https://christine-deng.github.io/3dgs-vr-unity-plants/install.html#data-preparation) for more details on COLMAP.

The structure after running COLMAP is seen below:

```
📂.../ 
├──📂gaussian-splatting/ 
│   ├──📂input_data/
│   │	├──📂plant/
│   │	│	├──📂input/
│   │	│	│	├── 🖼️ <raw image 0>
│   │	│	│	├── 🖼️ <raw image 1>
│   │	│	│	│...
│   │	│	├──📂images/
│   │	│	│	├── 🖼️ <image 0>
│   │	│	│	├── 🖼️ <image 1>
│   │	│	│	│...
│   │   │...
│   │...
│...
```
Here, the images inside the ``input`` folder are the original JPEG photos. The images inside the ``image`` folder are geometrically corrected versions of the original photos.

## Masking
Change the directory into where the images are stored, and run the script to create the masks.

```
cd C:\Users\<username>\gaussian-splatting\input_data\plant

python ..\..\create_mask.py
```
The script will utilize Language Segment-Anything to detect the plant from the rest of the image. Then, an alpha channel is applied to extract the parts of the image corresponding to the mask.

Note that the new plant foreground image is saved as a JPEG in the ``masked_images`` folder, with a black background.

![plants](images/before_seg.jpeg)
![plants](images/after_seg.png)

The folder structure at this stage should appear as such:
```
📂.../ 
├──📂gaussian-splatting/ 
│   ├──📂input_data/
│   │	├──📂plant/
│   │	│	├──📂input/
│   │	│	│	├── 🖼️ <raw image 0>
│   │	│	│	├── 🖼️ <raw image 1>
│   │	│	│	│...
│   │	│	├──📂images/
│   │	│	│	├── 🖼️ <image 0>
│   │	│	│	├── 🖼️ <image 1>
│   │	│	│	│...
│   │	│	├──📂masked_images/
│   │	│	│	├── 🖼️ <masked image 0>
│   │	│	│	├── 🖼️ <masked image 1>
│   │	│	│	│...
│   │   │...
│   │...
│...
```
Now, DELETE the current ``images`` folder. Then, rename ``masked_images`` to ``images`` without altering the contents of the folder. The folders should look like this after:
```
📂.../ 
├──📂gaussian-splatting/ 
│   ├──📂input_data/
│   │	├──📂plant/
│   │	│	├──📂input/
│   │	│	│	├── 🖼️ <raw image 0>
│   │	│	│	├── 🖼️ <raw image 1>
│   │	│	│	│...
│   │	│	├──📂images/
│   │	│	│	├── 🖼️ <masked image 0>
│   │	│	│	├── 🖼️ <masked image 1>
│   │	│	│	│...
│   │   │...
│   │...
│...
```

