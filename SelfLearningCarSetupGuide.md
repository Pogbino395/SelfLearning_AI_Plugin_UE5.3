# **Self-Learning Car Setup Guide**
Welcome to the Self-Learning Car Setup Guide! This guide will help you configure the Self-Learning Plugin for creating a self-steering car AI in Unreal Engine 5.3.

## **Table of Contents**
1. [Setup Project](#setup-project)
2. [Create the Track](#create-the-track)
3. [Configuring the AI Agent](#configuring-the-ai-agent)
4. [Configuring the AI Data Assets](#configuring-the-ai-data-assets)
5. [Running the Training](#running-the-training)
6. [Deploying the AI](#deploying-the-ai)
7. [Self-Learning Car Example](#self-learning-car-example)

## **Setup Project**

### **Create a New Project**

1. **Select Vehicle Template:**
    Create a new project in Unreal Engine 5.3, select the **Vehicle** template. This template provides a ready-made vehicle setup that will serve as the basis for your self-learning car.

### **Download the Plugin**

1. **Clone the Repository or Download the ZIP File:**
    Obtain the plugin from the repository.
   
2. **Add to Project:**
    Copy the plugin folder into the Plugins directory of your Unreal Engine 5.3 project.
   
3. **Enable the Plugin:**
    Open your project in Unreal Engine 5.3, go to Edit -> Plugins, and enable the Self-Learning Plugin.
   
4. **Restart:**
    Restart Unreal Engine to finalize the installation.

## **Create the Track**

### **Create a Mesh for the Track**

1. **Design the Track:**
    Create a mesh with a floor and two borders to define the track layout.

<p align="center">
  <img src=https://github.com/user-attachments/assets/510492a6-9527-4e35-8cc0-b18ba5ba9346>
</p>

### **Use the Landscape Tool**

1. **Create a New Layer:**
   Open the Landscape Tool and create a new layer.
      
<p align="center">
  <img src=https://github.com/user-attachments/assets/9529bae8-2e2c-4446-8141-498f71cfbe57>
</p>
    
2. **Convert the layer to a spline layer:**
    Right-click on the new layer and convert it to a spline layer.
      
<p align="center">
  <img src=https://github.com/user-attachments/assets/20f32f76-0f7e-4c10-b11b-4351c6ae9f6f>
</p>
   
3. **Set the mesh to the track:**
   In the Landscape Tool, select **Splines**. Open the **Segments** section, and in the **Details** panel, add the mesh to the **Spline Meshes** field.

<p align="center">
  <img src=https://github.com/user-attachments/assets/0c99da15-79d1-41de-b361-a47eb9166116>
</p>

4. **Shape the Track:**
   Press **Ctrl + Left Click** to place a new segment. Adjust the track to form a circular shape.

<p align="center">
  <img src=https://github.com/user-attachments/assets/40c71100-4911-47d9-8d9c-c0d0dab4ac90>
</p>

## **Configuring the AI Agent**

## **Configuring the AI Data Assets**

## **Running the Training**

## **Deploying the AI**

## **Self-Learning Car Example**
Watch this example to see the progression of a self-learning car in Unreal Engine 5.3. This demonstration includes two short videos showcasing the car's development through different generations of training.

### **1st Generation**
In this video, observe the initial attempts of the AI-driven car as it begins learning how to navigate the environment. The car's movements are basic and somewhat erratic as it starts to understand the dynamics of the virtual world.

<p align="center">
  <img src=https://github.com/user-attachments/assets/844ee1e8-c159-4fa1-81ef-349080e92106 alt="animated" />
</p>

### **4th Generation**
This video highlights the significant improvements in the car's navigation skills by the fourth generation of training. Notice how the car moves more smoothly and efficiently, having learned from its previous iterations.

<p align="center">
  <img src=https://github.com/user-attachments/assets/335fb249-d75b-4f0b-a0f5-35f13436d6af alt="animated" />
</p>
