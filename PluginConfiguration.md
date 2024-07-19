# **Plugin Configuration**
After downloading and installing the Self-Learning Plugin, follow these steps to configure it for your Unreal Engine 5.3 project:

## **Table of Contents**
1. [Initial Setup](#initial-setup)
2. [Creating a Training Environment](#creating-a-training-environment)
3. [Configuring the AI Agent](#configuring-the-ai-agent)
4. [Configuring the AI Data Assets](#configuring-the-ai-data-assets)
5. [Running the Training](#running-the-training)
6. [Deploying the AI](#deploying-the-ai)
    
## **Initial Setup**

### **Verify Installation**

   1. Open your Unreal Engine 5.3 project.
   2. Navigate to the **Plugin Folder**.
   3. Ensure there is a folder named **SelfLearning_AI**. If the folder is present, the plugin is successfully installed and enabled.

## **Creating a Training Environment**

### **Setup Training Environment**

   1. **Open Level:**
      Create a new level or open an existing one in the Content Folder.
      
   2. **Design Environment:**
      Design the environment where the AI agent will be trained, including necessary elements like obstacles, targets, and pathways.
      
   3. **Save level:**
      Save the level.

## **Configuring the AI Agent**

   ### **Add AI Component to Actor**

   1. **Select the agent:**
      Open the actor blueprint that will be used for training.

   1. **Add Component:**
      In the **Components** tab, add the **P_ANN_BP_Component** from the **SelfLearning_AI** to your actor. This component will enable the actor to interact with the AI system, allowing it to receive inputs, process data, and produce outputs based on the neural network.

<p align="center">
  <img src=https://github.com/user-attachments/assets/aa968e41-f126-437c-813e-2ce88918d3b5/>
</p>

   ### **Create Function to Calculate Inputs**

   1. **Create a New Function:**
      Create a new function called **CalculateInputs** with a float array as the output.
      
   2. **Define Inputs:**
      Add logic to collect all necessary inputs for the neural network. These inputs might include sensor data, environmental variables, or other relevant information that the AI needs to make decisions.

   3. **Scale Inputs:**
      Use the **ScaleValue** function provided by the **P_ANN_BP_Component** to normalize each input value. The function typically requires three parameters: the input value, the minimum expected value, and the maximum expected value.
      
   4. **Add Inputs to Array:**
      Add each scaled input to an array that will be passed to the neural network.
      
   5. **Return the Inputs:**
      Ensure the function returns the array of scaled inputs that will be fed into the neural network.

<p align="center">
  <img src=https://github.com/user-attachments/assets/d2379f76-cdaa-4f5a-b960-25a62fd805ad/>
</p>
      
   ### **Analyze Output**

   1. **Use the SelectAction Function:**
      Use the **SelectAction** function from the **P_ANN_BP_Component**. This function takes the previously calculated inputs and outputs an integer that corresponds to a specific action. Call this function in the **Event Tick** or at the point when an action should be performed.
      
   2. **Switch the Output:**
      Implement a switch statement or similar logic to handle the output of the SelectAction function. Each output value corresponds to a different action that the actor should take.
      
   3. **Implement Actions:**
      Define the specific actions corresponding to each case in the switch statement. Ensure each case implements a distinct action for the actor.

<p align="center">
  <img src=https://github.com/user-attachments/assets/0b6cc668-a118-4295-afa7-e229aaa7ce3a>
</p>

   ### **Calculate and Add Rewards**

   1. **Define Reward Logic:**
      Add logic to calculate rewards based on the actor's performance. Rewards should be designed to encourage desired behaviors and discourage undesired ones. For example, if the task is to navigate a maze, you might add a reward for moving closer to the goal and a penalty for hitting walls.
      
   2. **Update Rewards:**
      Use the **AddRewards** function from the **P_ANN_BP_Component** to update the actor's total reward value. This function allows you to add a reward and optionally override the current reward value.

      + **Reward:** The amount of reward to be added.
      + **Override Value:** A boolean indicating whether to set the reward to the specified value (true) or to add to the existing reward (false).

   4. **Integration:**
      Call this function at appropriate points in the actor's lifecycle, such as after each action or at regular intervals, to continuously update the reward based on performance.

<p align="center">
  <img src=https://github.com/user-attachments/assets/76c3acc8-329e-4a6d-bc1f-2207f3f94a2c>
</p>
      
## **Configuring the AI Data Assets**

1. Create a new data asset based on the **P_ANN_BP_DT_TrainingValue** class from the **SelfLearning_AI** plugin.
2. Set the values for the training variables:
   + **Initialization:**
     
     1. **InitializationTiming:** Decide when to start training or deploying the neural networks.
        
        - **StartBeginning:** Initialize the networks at Event BeginPlay.
       
        - **CallFunction:** Initialize the networks when calling the function InitializeNetworks from the **P_ANN_BP_Training_Manager**.

        <p align="center">
          <img src=https://github.com/user-attachments/assets/dbb4e86e-e472-4b86-9498-758913aebebf>
        </p>

   + **Save:**

     1. **Load or Save:**
        
        - **Load And Save:** Allows loading existing data and saving any modifications.
          
        - **Delete And Save:** Deletes current data and saves new changes.
          
        - **Do Not Save:** No actions are taken to load, delete, or save data.
          
     2. **Best Data Asset:** Specifies the preferred neural network data asset for saving values of the best neural network. If the actor is not actively training, it will utilize the data stored in this data asset for its operations.
        
     3. **Save Generations:** Structs to save a generation best neural network.
        
        - **Data Asset:** Data asset used to save neural network details.
          
        - **Generation Number:** Indicates which generation's best neural network to save.
          
     4. **Data Assets:** An array of data assets used for training, requiring at least three data assets.

        <p align="center">
          <img src=https://github.com/user-attachments/assets/33ac8421-483b-420a-8047-36646815d3b9>
        </p>
        
   + **Training:**

     1. **Training:** Indicates whether the network is currently undergoing training.

     2. **Generation Size:** Specifies the number of actors to be trained within each generation.

     3. **Generation Number:** Duration (in time) allocated to each generation of training.

     4. **Class Neural Network:** Specifies the actor class to be spawned for neural network training.

     5. **Spawn Offset:** Defines the distance between each sequentially spawned actor's position relative to the previous one, starting from the P_ANN_BP_DT_TrainingValue's location by default.

     6. **Min Reward Best Data:** Minimum reward threshold required to retain actor data.
    
        <p align="center">
          <img src=https://github.com/user-attachments/assets/693b84f8-742b-4ac9-bef1-3ab69f876ba7>
        </p>

   + **Neural Networks Values:**

     1. **Input Nodes:** Number of input nodes in the neural network.

     2. **Hidden Nodes:** Represents an array of hidden layers within the neural network, where each index corresponds to a distinct node layer.

        - **Nodes Lenght:** Number of nodes per hidden layer.

        - **Activation Function:** Function determining node layer activation:
       
             + **Sigmoid:** Values range from 0 to 1.
         
             + **StepUnit:** Returns 1 if value > 0, else 0.
         
             + **HyperbolicTangent:** Values range from -1 to 1.
         
             + **ReLU:** Returns value if > 0, else 0.

     3. **Output Nodes:** Represents all output nodes within the neural network.

     4. **Min Weight Start Value:** Minimum initial weight value for the neural network.

     5. **Max Weight Start Value:** Maximum initial weight value for the neural network.

     6. **Learning Rate:** Determines the frequency of weight updates in the neural network; typically between 0 and 1.

     7. **Min Update Weight Value:** Minimum random range for multiplying weight values during updates.

     8. **Max Update Weight Value:** Maximum random range for multiplying weight values during updates.
    
        <p align="center">
          <img src=https://github.com/user-attachments/assets/943feed2-3775-4710-b9bf-f8d61f2e0ce8>
        </p>

   + **Print Debugs:**

     1. **Print Debug Manager:** Enables debug printing for the training manager.

     2. **Print Debug ANNs:** Enables debug printing for the neural networks.
        
        <p align="center">
          <img src=https://github.com/user-attachments/assets/7162f39a-ca45-462b-bf5a-a2ba453ceb82>
        </p>

3. Set the values for the data asset **P_ANN_BP_DT_SaveValue** for saving the neural networks:

   + **Save Slot:**

     1. **Save Name:** Name assigned to the save game.

     2. **Save Index:** Index indicating the position of the save game.

        <p align="center">
          <img src=https://github.com/user-attachments/assets/9522e008-b33a-4e05-9a84-0f85e55b3510>
        </p>

   + **Save Value:**
     *Refrain from altering these values as they are intended solely for reading and saving purposes.*

     1. **Hiddens Nodes:** Hidden nodes configuration within the neural network.

     2. **Output Nodes:** Output nodes configuration within the neural network.

     3. **Total Rewards:** Total rewards accumulated by the neural network.

     4. **Current Generation:** Indicates the current generation from which values are saved.
        
        <p align="center">
          <img src=https://github.com/user-attachments/assets/ffdb2e3d-f99e-49e0-bf4f-4c12eb4ff5f4>
        </p>

## **Running the Training**

### **Add Training Manager**

1. **Place Training Manager in Level:**
      Drag and drop the **P_ANN_BP_Training_Manager** blueprint into your level. Position it where you want the training to take place.

2. **Set Training Values:**
      Assign the **P_ANN_BP_DT_TrainingValue** to the Training Manager. This data asset should contain all the necessary training variables.

<p align="center">
  <img src=https://github.com/user-attachments/assets/2f0f9cb0-c9c5-4723-895e-1c0dd066a611>
</p>

### **Start Training Session**

1. **Initialize Training:**
      To start the training, play the level in **Simulate** mode. If the enum is set to **At the Beginning**, the network will initialize automatically. If set to **When a Function is Called**, ensure you manually call the appropriate function in the **P_ANN_BP_Training_Manager** to start the network initialization.

<p align="center">
  <img src=https://github.com/user-attachments/assets/24122643-2488-493d-9880-a5bad826f88e>
</p>

2. **Check Training Status:**
      If the AI agents are not training, verify that the Training parameter in the **P_ANN_BP_DT_TrainingValue** is set to false. This setting indicates that the agents are using the best neural network data asset for their operations rather than actively training.

3. **Monitor Progress:**
      Use the in-editor tools to monitor the progress of your training session. Check the **P_ANN_BP_DT_SaveValue** to obtain detailed information:

    - **Node Values:** Inspect the values of each node, including weights and node value, to understand how the network's internal states are evolving.
    - **Total Rewards:** View the total rewards accumulated by the network, which helps gauge overall performance.
    - **Current Generation:** See the generation from which the values are saved.
      
<p align="center">
  <img src=https://github.com/user-attachments/assets/df62d81b-db72-44d4-b80d-223f4859e3fd>
</p>

5. **Evaluate Performance:**
      Check the performance metrics of your AI agents. This includes their accumulated rewards, success rates, and other relevant statistics.
   
### **Adjust Parameters**

1. **Modify Training Parameters:**
      If needed, adjust the parameters in your **P_ANN_BP_DT_TrainingValue**. This can include changing the number of actors per generation, the duration of each generation, learning rates, and other neural network settings.

2. **Save Adjustments:**
      After making changes, ensure you save your data assets and reinitialize the training session to apply the new parameters.

3. **Fine-Tune for Optimization:**
      Continue tweaking the parameters based on observed performance. Fine-tuning these values can help optimize the learning process and improve the effectiveness of your AI agents.

## **Deploying the AI**

### **Integrate into Gameplay**

1. **Adjust Training Values:** Adjust the parameter in your **P_ANN_BP_DT_TrainingValue**:
      + Set the **Training** parameter to false. This ensures the AI uses the pre-trained data instead of training further.
      + Then, set the **BestDataAsset** to the saved neural network data asset you want the AI to use.
      + Adjust the **InitializationTiming** parameter if you want to change when the initialization occurs.

2. **Gameplay Execution:**
      By pressing play, the agent will no longer train and will perform according to the pre-trained neural network data.
   
### **Test and Finalize**

1. **In-Game Testing:**
      Conduct thorough in-game testing to observe the AI behavior in various scenarios. Monitor the AI performance and ensure it meets the desired gameplay requirements.

2. **Bug Fixing:**
      Identify and fix any bugs or issues that arise during testing. Ensure that the AI components and neural networks are functioning correctly without causing any gameplay disruptions.

3. **Final Validation:**
      Perform a final validation to confirm that the AI behaves as expected across different levels and game modes. Validate that the AI maintains consistent performance and reliability.

By following these steps, you can successfully integrate and deploy your trained AI into your Unreal Engine 5.3 project, ensuring it performs effectively within the gameplay environment.
