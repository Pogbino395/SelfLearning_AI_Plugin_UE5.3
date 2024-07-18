# **Plugin Configuration**
After downloading and installing the Self-Learning Plugin, follow these steps to configure it for your Unreal Engine 5.3 project:

## **Table of Contents**
1. [Initial Setup](#initialsetup)
2. [Creating a Training Environment](#creatingatrainingenvironment)
3. [Configuring the AI Agent](#configuringtheaiagent)
4. [Configuring the AI Data Assets](#configuringtheaidataassets)
5. [Running the Training](#runningthetraining)
6. [Deploying the AI](#deployingtheai)
    
## **1. Initial Setup**

### **Verify Installation**

   1. Open your Unreal Engine 5.3 project.
   2. Navigate to the **Plugin Folder**.
   3. Ensure there is a folder named **SelfLearning_AI**. If the folder is present, the plugin is successfully installed and enabled.

## **2. Creating a Training Environment**

### **Setup Training Environment**

   1. Create a new level or open an existing one in the Content Folder.
   2. Design the environment where the AI agent will be trained, including necessary elements like obstacles, targets, and pathways.
   3. Save the level.

## **3. Configuring the AI Agent**

   ### **Add AI Component to Actor**

   1. Open the actor blueprint that will be used for training.
   2. In the **Components** tab, add the **P_ANN_BP_Component** from the **SelfLearning_AI** to your actor.

   ### **Create Function to Calculate Inputs**

   ### **Create Function to Analize Output**
      
   ### **Calculate and Add Rewards**

## **4. Configuring the AI Data Assets**

1. Create a new data asset based on the **P_ANN_BP_DT_TrainingValue** class from the **SelfLearning_AI** plugin.
2. Set the values for the training variables:
   + ### **Save:**

     1. **Load or Save:**
        
        - **Load And Save:** Allows loading existing data and saving any modifications.
          
        - **Delete And Save:** Deletes current data and saves new changes.
          
        - **Do Not Save:** No actions are taken to load, delete, or save data.
          
     2. **Best Data Asset:** Specifies the preferred neural network data asset for saving values of the best neural network. If the actor is not
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actively training, it will utilize the data stored in this data asset for its operations.
        
     3. **Save Generations:** Structs to save a generation best neural network.
        
        - **Data Asset:** Data asset used to save neural network details.
          
        - **Generation Number:** Indicates which generation's best neural network to save.
          
     4. **Data Assets:** An array of data assets used for training, requiring at least three data assets.
        
   + ### **Training:**

     1. **Training:** Indicates whether the network is currently undergoing training.

     2. **Generation Size:** Specifies the number of actors to be trained within each generation.

     3. **Generation Number:** Duration (in time) allocated to each generation of training.

     4. **Class Neural Network:** Specifies the actor class to be spawned for neural network training.

     5. **Spawn Offset:** Defines the distance between each sequentially spawned actor's position relative to the previous one, starting from
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the P_ANN_BP_DT_TrainingValue's location by default.

     6. **Min Reward Best Data:** Minimum reward threshold required to retain actor data.

   + ### **Neural Networks Values:**

     1. **Input Nodes:** Number of input nodes in the neural network.

     2. **Hidden Nodes:** Represents an array of hidden layers within the neural network, where each index corresponds to a distinct node
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;layer.

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

   + ### **Print Debugs:**

     1. **Print Debug Manager:** Enables debug printing for the training manager.

     2. **Print Debug ANNs:** Enables debug printing for the neural networks.

3. Set the values for the save asset:

   + ### **Save Slot:**

     1. **Save Name:** Name assigned to the save game.

     2. **Save Index:** Index indicating the position of the save game.

   + ### **Save Value:**
     Refrain from altering these values as they are intended solely for reading and saving purposes.

     1. **Hiddens Nodes:** Hidden nodes configuration within the neural network.

     2. **Output Nodes:** Output nodes configuration within the neural network.

     3. **Total Rewards:** Total rewards accumulated by the neural network.

     4. **Current Generation:** Indicates the current generation from which values are saved.

## **5. Running the Training**

### **Add Training Manager**

### **Start Training Session**

### **Adjust Parameters**

## **6. Deploying the AI**

### **Integrate into Gameplay**

### **Test and Finalize**
   
