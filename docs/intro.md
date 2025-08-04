# Introduction to the Project 

This project was part of my 2025 DOE SULI internship project, overseen by my mentor, [Wei Xu](https://www.bnl.gov/staff/xuw)at Brookhaven National Laboratory. In this project, I utilize Unity as a medium to render and interact with 3D Gaussian Splatting (3DGS) plant models. I use aras-p's [Gaussian Splatting playground Unity](https://github.com/aras-p/UnityGaussianSplatting) project to render the models. I incorporate virtual reality (VR) as a means to interact and visualize the plants.

## What is 3D Gaussian Splatting?

3D Gaussian Splatting (3D GS)--a point-based rendering method that uses 2D images to reconstruct realistic 3D scenes. Compared to other notable rendering methods such as NeRF and InstantNGP, 3D GS can produce equal or even higher quality models at fast training speeds using real-time rendering and efficient rasterization, increasing the realm of complex scene generation. Through the use of anisotropic splats to represent surface geometry and texture, 3D GS eliminates the use of manual mesh generation, greatly increasing efficiency.


## Why Use Virtual Reality?

Virtual Reality (VR) provides a modern and immersive interface for interacting directly with the 3DGS models. By integrating the scene into a VR environment using Unity, users can intuitively explore complex biological structures from multiple perspectives in real time. Being hands-on, interaction using VR enables us to analyze data directly within the 3D environment. Unlike static images or flat screens, VR allows for natural navigation around the model, making it easier to observe fine details and perform spatial analysis.

## Integration in Unity

Unity serves as the foundation of the project, bringing together 3DGS rendering and VR interaction in one environment. It functions both as the rendering engine for 3D Gaussian Splatting (3DGS) models and as the user interface for immersive exploration in Virtual Reality. The 3DGS rendering repository is integrated directly into the Unity project, enabling real-time visualization of complex point-based scenes. With Unity’s built-in support for VR and interactive controls, users can navigate, inspect, and eventually analyze the 3D models within a cohesive, interactive space.
