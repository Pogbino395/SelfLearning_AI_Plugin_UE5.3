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

5. **Add Checkpoints:**
    Create a new blueprint **Checkpoint** that contains only a collision box. Place this checkpoint blueprint at various positions along the track to serve as reference points for the AI.

<p align="center">
  <img src=https://github.com/user-attachments/assets/2f643cab-af44-4566-99a5-6a6cf6550373>
</p>

## **Configuring the AI Agent**

### **Create a Copy of VehicleAdvPawn**

1. **Duplicate VehicleAdvPawn:**
    Create a copy of the **VehicleAdvPawn** blueprint. Use the original for player control, allowing you to play against the AI.
   
### **Modify Components**

1. **Remove Unnecessary Components:**
    In the duplicated VehicleAdvPawn blueprint, remove the SpringArm components and Camera components.

2. **Add P_ANN_BP_Component Component:**
    Add the **P_ANN_BP_Component** component to the blueprint.

3. **Set Skeletal Mesh:**
    Set the **Skeletal Mesh** to the desired vehicle model.

4. **Add Collision Box:**
    Add a **Collision Box** that encloses the entire car mesh.

5. **Add Arrows for Directions:**
    Add five **Arrow** components in front of the vehicle, each pointing in different directions.

<p float="left">
  <img src=https://github.com/user-attachments/assets/635e9301-cdc9-4a21-8c60-f8aa8b10fb41 width="300" />
  <img src=https://github.com/user-attachments/assets/d9d9d062-cd07-470b-9589-31eb3968a838 width="700" /> 
</p>

### **Configure Collisions**

1. **Car Mesh Collision:**
   
    + Set the car mesh Collision Preset to **Custom**, the Object Type to **Vehicle**.
      
    + Block everything except **Vehicle**, which should be set to **Ignore**.

<p align="center">
  <img src=https://github.com/user-attachments/assets/497c7736-f86a-481f-97b9-dda4c515da76>
</p>
   
2. **Collision Box:**
   
    + Set the collision box Collision Preset to **Custom** and the Object Type to **Vehicle**, matching the car mesh settings.
      
    + Overlap everything except **Vehicle**.

<p align="center">
  <img src=https://github.com/user-attachments/assets/24cc05af-6abb-4264-a9a6-15a3ee25f4f8>
</p>

### **Create Functions**

1. **Make Arrows Array:**
    Create a function to add all the arrows to an array.

<p align="center">
  <img src=https://github.com/user-attachments/assets/3ed280f3-6925-473c-86cd-4548c23b67e4>
</p>

2. **Line Trace:**
    Create a function that performs a line trace from the car in the direction of the arrow. Output the distance from the hit of the track border, scaled using the P_ANN_BP_Component's provided function **Scale Value** (min: 0, max: 2000).

<p align="center">
  <img src=https://github.com/user-attachments/assets/db0ce6e5-8ee0-4372-8968-734e54bcca66>
</p>

3. **Calculate Inputs:**
    Create a pure function to calculate the inputs. Use a **For Each Loop** to iterate through the arrows, using the line trace function.

<p align="center">
  <img src=https://github.com/user-attachments/assets/2bc61e9f-77fd-48f6-9735-83bf9aace505>
</p>

### **Event Graph Adjustments**

1. **Remove Unnecessary Functions:**
    Delete all functions except **Event Begin Play** and **Event Tick**.

2. **Event Begin Play Setup:**
    At the end, add the **Make Arrows Array** function.

<p align="center">
  <img src=https://github.com/user-attachments/assets/75abe989-9ba4-40e4-ab3a-0329821bc05b>
</p>

3. **Event Tick Setup:**
    Remove Interps to Original Rotation from Event Tick. Add a **Sequence** node to **Event Tick**:
   
    + **First pin:** Set Angular Damping.
      
    + **Second pin:** Call a new custom event called **Neural Network**.
 
<p align="center">
  <img src=https://github.com/user-attachments/assets/a0f79b26-1860-4adf-b4d5-0f5f98987de4>
</p> 

### **Custom Event: Neural Network**

1. **Select Action:**
    Add the **Select Action** function from the P_ANN_BP_Component. Input the output of the **Calculate Inputs** function.

2. **Switch on Integer:**
    Use a **Switch on Int** node with options 0, 1, and 2 (no default). Create a variable called **Steering:**
    + **Int 0:** Steering 0
    + **Int 1:** Steering 1
    + **Int 2:** Steering -1

<p align="center">
  <img src=https://github.com/user-attachments/assets/5810dc35-83ab-4780-a5ab-d1d45d123131>
</p> 

3. **Set Steering Input:**
    Connect the pins to the **Set Steering Input** function from the **Vehicle Movement Component**. Insert the **Steering** variable as the input.

4. **Set Throttle Input:**
    Add the **Set Throttle Input** function from the **Vehicle Movement Component**. Insert a new variable called **Acceleration** with the desired acceleration (e.g., 0.3 for completing the track without hitting walls).

<p align="center">
  <img src=https://github.com/user-attachments/assets/2fbbdf9b-c364-4bd7-8940-e1d876d0c626>
</p> 

### **Rewards Handling**

1. **Cast to Checkpoint:**
    Check if the overlapping actor is a checkpoint.

2. **Reward System:**
    + If the overlapping actor is a checkpoint:
        - Use the **Add Rewards** function provided by the P_ANN_BP_Component.
        - Set **Reward** to 100.
        - Set **Override Value** to false.
     
    + If the overlapping actor is not a checkpoint:
        - Use the **Add Rewards** function provided by the P_ANN_BP_Component.
        - Set **Reward** to -5.
        - Set **Override Value** to false.

<p align="center">
  <img src=https://github.com/user-attachments/assets/d85b7a02-9e02-41fa-8f56-963b20907225>
</p> 

## **Configuring the AI Data Assets**
To set up your AI data assets:

1. **Create Save Data Assets:**
    + **Best Data Asset:** Create a data asset to store the best-performing neural network.
    + **Training Data Assets:** Create at least three data assets specifically for training the neural networks. These assets will store different states of the neural network during the training process.
    + **Generation Testing Assets:** Optionally, create additional data assets to save different generations of neural networks. These are used for testing against the best-performing network.

<p float="left">
  <img src=https://github.com/user-attachments/assets/22df42b2-b54b-4e26-aa38-4ec4c8dc8c15 width="500" />
  <img src=https://github.com/user-attachments/assets/4aa962a0-e862-4178-80a4-99f0173186ca width="500" /> 
</p>

2. **Create a Training Values Data Asset:**
This data asset contains five key sections:

    + **InitializationTiming:**
        - **Start Timing:** Set the variable to "start at the beginning" to ensure the neural network initializes as soon as training begins.
         
<p align="center">
  <img src=https://github.com/user-attachments/assets/9f6c2171-5973-47f1-aac3-4051c933e066>
</p> 
    + **Save:**
        - **Save Generations:** Define the data assets to save different generations for testing.
        - **Data Assets:** Include at least three data assets for training.
        
<p align="center">
  <img src=https://github.com/user-attachments/assets/b80ed6b2-b7e6-4935-815d-468ddff3a015>
</p> 
    + **Training:**
        - **Generation Size:** Adjust this based on your PC's processing capability. Larger generation sizes require more computational resources.
        
<p align="center">
  <img src=https://github.com/user-attachments/assets/e002ff57-ea51-4947-b216-4d12b7f29187>
</p> 
    + **NeuralNetworksValues:**
        Follow these values for optimal performance.

<p align="center">
  <img src=https://github.com/user-attachments/assets/0441421e-2f22-4761-bc93-54d25cb9e337>
</p> 
    + **PrintDebugs:**
        Decide if you want to print debug information.
        
<p align="center">
  <img src=https://github.com/user-attachments/assets/4e3422c1-a326-4b72-a731-9b21ce969b0d>
</p> 

By correctly setting up these data assets, you ensure that your AI has the necessary configuration for both training and deployment.

## **Running the Training**

<p align="center">
  <img src=https://github.com/user-attachments/assets/6724860b-4eda-41ff-b6f1-cbc348befb10>
</p> 

<p align="center">
  <img src=https://github.com/user-attachments/assets/c98ddc1d-3084-49e6-958a-e2f2753cda28>
</p> 

## **Deploying the AI**

<p align="center">
  <img src=https://github.com/user-attachments/assets/edd5f7ef-e573-4653-9ab4-79084917c868>
</p> 

<p align="center">
  <img src=https://github.com/user-attachments/assets/acb91350-de6c-489d-8c77-e3a7d10633a7>
</p> 

<p align="center">
  <img src=https://github.com/user-attachments/assets/dbf34ef9-90a2-4401-adf9-f81969835b33>
</p> 

<p align="center">
  <img src=https://github.com/user-attachments/assets/e1de868f-e082-4eb1-a920-815270c06051>
</p> 

<p align="center">
  <img src=https://github.com/user-attachments/assets/03321b80-5d26-4a18-9cfd-d428baad3d59>
</p> 

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
