# Explanation of Scripts

Within Unity, we designed a pipeline that ued C# scripts within Unity to pass coordinate information to Python scripts outside of Unity, which then retrieved pixel coordinates of pictures.

## C# Scripts

### CoordinateDisplayUI.cs

This script diplays the XYZ world coordinate of where the VR controller's ray hits the 3D mesh of the 3DGS model. When the trigger button is pressed, the 

### CameraLoader.cs

This script is used to load in each individual camera, using the camera metadata file, `cameras.json`. The metadata contains:
- image name: `"image00.png"`
- image dimensions: `"width": 2200 , "height":4000`
- image position (1x3 matrix)
- image rotation (3x3 matrix)
- focal length (x, and y)
The script loads in each camera into their respective locations using calculatinos to tranform the camera poition $ rotation into a Unity poition. It then converts the rotation matrix to quaternion, which Unity uses to apply 3D rotations. 

## Python Scripts
