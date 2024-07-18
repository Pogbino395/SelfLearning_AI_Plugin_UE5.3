# **Plugin Configuration**
After downloading and installing the Self-Learning Plugin, follow these steps to configure it for your Unreal Engine 5.3 project:

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

1. Create a new data asset based on the **P_ANN_BP_DT_TrainingValue** class from the **SelfLearning_AI** plugin.
2. Set the values for the training variables:
   + **Save:**
     1. **Load or Save:**
     2. **Best Data Asset:**
     3. **Save Generations:**
     4. **Data Assets:**
   + **Training:**
     1. **Training:**
     2. **Generation Size:**
     3. **Generation Number:**
     4. **Class Neural Network:**
     5. **Spawn Offset:**
     6. **Min Reward Best Data:**
   + **NeuralNetworksValues:**
     1. **Input Nodes:**
     2. **Hidden Nodes:**
     3. **Output Nodes:**
     4. **Min Weight Start Value:**
     5. **Max Weight Start Value:**
     6. **Learning Rate:**
     7. **Min Update Weight Value:**
     8. **Max Update Weight Value:**
   + **PrintDebugs:**
     1. **Print Debug Manager:**
     2. **Print Debug ANNs:**
