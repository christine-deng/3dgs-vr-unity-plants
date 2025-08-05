
# Unity Gaussian Splatting
To view the 3D Gaussian Splatting model in Unity, I utilized the [Gaussian Splatting playground in Unity](https://github.com/aras-p/UnityGaussianSplatting) repository.

## Requirements

### Hardware
- Meta Quest Pro
- Meta Quest Link cable

### Software
- **[Unity 2022.3.7](https://unity.com/releases/editor/whats-new/2022.3.7) :** Newer versions of Unity may work as well.

## Setup
Clone the repository to have access to the toolkit.

```
git clone https://github.com/aras-p/UnityGaussianSplatting
```

In Unity Hub, open the file ``../<username>\UnityGaussianSplatting\projects\GaussianExample`` and open **GSTestScene** in Unity.

### Unity Setup
Inside Unity, navigate to ``Window > Package Manager``. Inside the Package Manager, install:
- OpenXR Plugin
- XR Plugin Management
- XR Interaction Toolkit
- Post-Processing

After installing the packages, navigate to ``Edit > Project Settings``. 
- In **XR Plugin Management**, ensure that ``OpenXR`` is selected under the Plug-in Providers tab.
- Under **XR Plugin Management**, navigate to **OpenXR** and change the Render Mode to ``Multi-pass``.
- Under **XR Plugin Management**, navigate to **Project Validation** and fix all of the errors by clicking the ``Fix All`` button.

## Importing the Generated 3D Gaussian Splatting Model
In the previous section, we generated a 3D Gaussian Splatting Model of a scene. It can be found in the folder ``C:\Users\<username>\gaussian-splatting\output\room``
Back in Unity, go to ``Tools > GaussianSplats > Create GaussianSplatAsset``. This should open a window that will allow for importing the .ply file. Select the .ply file, found in the folders in  ``C:\Users\jlin3\gaussian-splatting\output\room\point_cloud\...``.

Select ``Create Asset``, and it should show up within GaussianAssets.

## Viewing the Model
In the Hierarchy tab of Unity, create a new Game Object and name it accordingly. Go to its properties:
- add **Gaussian Splat Renderer** and select the asset that was just imported.
- add **Post-Process Layer**, and set the Layer to ``Everything``.

Next, add a Camera under the Game Object. In its Properties, add a **Tracked Pose Driver**. This will allow the scene to be static when viewed in VR. 

Connect the Meta Quest Pro to the computer via Quest Link. Inside, you should be able to view the desktop and control it remotely. Select Unity from the Desktop inside the Quest Pro, and press the **Play** button on the top.