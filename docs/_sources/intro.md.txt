# Introduction to the Project 

This project was part of my 2025 DOE SULI internship project, overseen by my mentor, [Wei Xu](https://www.bnl.gov/staff/xuw) at Brookhaven National Laboratory. In this project, I utilize Unity as a medium to render and interact with 3D Gaussian Splatting (3DGS) plant models. I use aras-p's [Gaussian Splatting playground Unity](https://github.com/aras-p/UnityGaussianSplatting) project to render the models. I incorporate virtual reality (VR) as a means to interact and visualize the plants. My forked repository can be found on my [GitHub](https://github.com/lajazz23/unity-gs-with-plants).

## What is 3D Gaussian Splatting?

[3D Gaussian Splatting](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/) (3D GS) is a point-based rendering method that uses 2D images to reconstruct realistic 3D scenes. Compared to other notable rendering methods such as [NeRF](https://www.matthewtancik.com/nerf), 3D GS can produce equal or even higher quality models at fast training speeds using real-time rendering and efficient rasterization, increasing the realm of complex scene generation. Through the use of anisotropic splats to represent surface geometry and texture, 3D GS eliminates the use of manual mesh generation, greatly increasing efficiency.

### 3DGS Pipeline

The 3DGS pipeline reconstructs a 3D scene from a collection of 2D images with known camera poses. The process typically begins with input images and corresponding camera parameters, which are often obtained through Structure-from-Motion (SfM) tools such as COLMAP. The camera poses are extracted into a JSON file. Importantly, each Gaussian in the 3DGS model stores spherical harmonic (SH) coefficients, which encode how that point reflects light from various viewing angles. This view-dependent shading enables realistic lighting without needing physical light sources or detailed surface geometry. As a result, the model can reproduce subtle changes in appearance based on camera position.

These inputs are used to generate a scene composed of 3D Gaussian primitives—each representing position, scale, color, and orientation. Instead of relying on traditional mesh geometry, 3DGS renders the scene directly from these point-based representations using efficient rasterization techniques. The output is a high-fidelity, real-time-renderable 3D scene that can be visualized in applications such as Unity, with full support for camera movement and scene interaction.

![plants](images/plant_pictures.png)

## Why Use Virtual Reality?

Virtual Reality (VR) provides a modern and immersive interface for interacting directly with the 3DGS models. By integrating the scene into a VR environment using Unity, users can intuitively explore complex biological structures from multiple perspectives in real time. Being hands-on, interaction using VR enables us to analyze data directly within the 3D environment. Unlike static images or flat screens, VR allows for natural navigation around the model, making it easier to observe fine details and perform spatial analysis.


## Integration in Unity

Unity serves as the foundation of the project, bringing together 3DGS rendering and VR interaction in one environment. It functions both as the rendering engine for 3D Gaussian Splatting (3DGS) models and as the user interface for immersive exploration in Virtual Reality. The 3DGS rendering repository is integrated directly into the Unity project, enabling real-time visualization of complex point-based scenes. With Unity’s built-in support for VR and interactive controls, users can navigate, inspect, and eventually analyze the 3D models within a cohesive, interactive space.

When rendering 3DGS models in Unity, the SH coefficients are used to determine the color and shading of each point based on the current view direction. This means that different perspectives of the same model produce slightly different lighting effects, enhancing realism and visual depth within the VR environment. This allows for a realistic representation of the plant within VR.

### OpenXR Integration

To enable VR interaction within Unity, this project uses OpenXR—-an open standard for accessing virtual and augmented reality devices. OpenXR provides a unified interface for connecting various hardware (such as VR headsets and controllers) without relying on platform-specific SDKs. In this setup, OpenXR allows Unity to detect and respond to controller input, enabling users to interact naturally with the 3DGS model in VR.
