# Explanation of Scripts

Within Unity, we designed a pipeline that ued C# scripts within Unity to pass coordinate information to Python scripts outside of Unity, which then retrieved pixel coordinates of pictures.

## C# Scripts


### FolderPathSaver.cs.cs

Yes, the script is named `FolderPathSaver.cs.cs`. This script is central to giving all the other scripts access to the files. Users can input file paths into the Unity Inspector where the script is attatched. This method allows for a more efficient way to control file paths in each script.

### CoordinateDisplayUI.cs

This script diplays the XYZ world coordinate of where the VR controller's ray hits the 3D mesh of the 3DGS model. When the trigger button is pressed, the script display the coordinate at the interection of the ray and the mesh, and then saves the coordinate to `found_images.json`, which is passed to other scripts. This script calls onto the [Python](#python-scripts) scripts.

### CameraLoader.cs

This script is used to load in each individual camera, using the camera metadata file, `cameras.json`. The metadata contains:
- image name: `"image00.png"`
- image dimensions: `"width": 2200 , "height":4000`
- image position (1x3 matrix)
- image rotation (3x3 matrix)
- focal length (x, and y)

The script loads in each camera into their respective locations using calculatinos to tranform the camera position & rotation into a Unity position. It then converts the rotation matrix to quaternion, which Unity uses to apply 3D rotations. 

### ImageDisplay.cs

This script imports the image inside `found_images.json` and displays it inside the world space inside Unity. 

## Python Scripts

### camera_unloader.py

Thi script finds the best camera that is associated with the chosen coordinate. It transforms the 3D world point into the camera coordinate system to determine the closest and best oriented camera relative to the point. 

### image_retriever.py

This script call on `camera_unloader.py` to obtain the camera coordinates. It projects the point to 2D image pixels using the camera pinhole model. The image retrieved is saved alongside it pixel information to `found_images.json`.