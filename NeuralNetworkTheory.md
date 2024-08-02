# **Neural Network Theory**
Welcome to the Neural Network Theory! The Self-Learning Plugin for Unreal Engine 5.3 utilizes a neural network to enable AI agents to learn and improve their task performance. This page explains the theory behind the neural network implementation used in this plugin.

<p align="center">
  <img src=https://github.com/user-attachments/assets/599ced15-ac23-46d9-9870-2fe195b9ae55>
</p>

## **Table of Contents**
1. [Introduction](#introduction)
2. [AI Agent](#ai-agent)
3. [Weight Initialization](#weight-initialization)
4. [Forward Propagation](#forward-propagation)
5. [Activation Functions](#activation-functions)
6. [Rewards and Selection of the Best Neural Network](#rewards-and-selection-of-the-best-neural-network)
7. [Backward Propagation](#backward-propagation)
8. [Weight Adjustment](#weight-adjustment)
9. [Optimization Strategy](#optimization-strategy)
   
## **Introduction**
Neural networks are a key component of modern machine learning, allowing systems to learn from data and make decisions based on that learning. In the Self-Learning Plugin, a neural network is employed to enable AI agents to perform and improve in various tasks within Unreal Engine 5.3 environments.

## **AI Agent**
An AI agent in the Self-Learning Plugin acts as the entity that interacts with the environment, making decisions based on the neural network's output. The agent's behavior and performance are critical for achieving desired tasks and improving over time through learning.

### **1. Interaction with Environment:**

+ The AI agent receives inputs from the environment, which could include game state information, sensor data, or other relevant variables.
+ These inputs are fed into the neural network, which processes them and generates corresponding outputs or actions.

### **2. Decision Making:**

+ The outputs of the neural network determine the actions taken by the AI agent.
+ These actions can range from simple movements and choices to complex strategies and behaviors depending on the task.

### **3. Learning and Adaptation:**

+ The agent's performance is evaluated based on a reward system, which provides feedback on the effectiveness of its actions.
+ Over time, through repeated interactions and weight adjustments, the AI agent learns to optimize its actions to achieve better performance and higher rewards.

### **4. Continuous Improvement:**

+ By selecting and adjusting the weights of the top-performing neural networks, the AI agent continually evolves.
+ This process ensures that the agent adapts to changing environments and improves its ability to complete tasks efficiently.

The AI agent, powered by the neural network, is the cornerstone of the Self-Learning Plugin, enabling dynamic and intelligent behavior within Unreal Engine 5.3 environments.

## **Weight Initialization**
Proper initialization of weights is crucial for the effective training of neural networks. In the Self-Learning Plugin, weights are initialized to small random values within a specified range.

### **Recommended Initialization Range**
+ Weights are typically initialized in the range of **-1** to **1**.

Initializing weights in this range ensures that the network starts with small values, which helps in preventing issues related to exploding or vanishing gradients.

## **Forward Propagation**
Forward propagation is the process by which input data is passed through the neural network to produce an output. This involves a series of steps where each neuron's output is calculated as a weighted sum of its inputs, passed through an activation function.

### **Steps in Forward Propagation**
1. **Input Layer:** The neural network receives input data (e.g., sensor data, game state). These input values often need to be scaled to ensure they are within a range suitable for the neural network (e.g., 0 to 1).
2. **Hidden Layers:** The input data is processed through one or more hidden layers. Each neuron in a hidden layer calculates a weighted sum of its inputs, applies an activation function, and passes the result to the next layer. Hidden layers are useful for capturing complex patterns and interactions in the data, although they are not strictly necessary for all tasks.
3. **Output Layer:** The final layer produces the output, which can be a decision or action taken by the AI agent.

### **Example**
For a simple neural network with one hidden layer:

1. **Inputs:** $x_1, x_2$

2. **Weights for the hidden layer:** $w_{1,1}, w_{1,2}, w_{2,1}, w_{2,2}$
 
3. **Hidden layers:**

$$h_1 = \text{ActivationFunction}(x_1 \cdot w_{1,1} + x_2 \cdot w_{1,2})$$

$$h_2 = \text{ActivationFunction}(x_1 \cdot w_{2,1} + x_2 \cdot w_{2,2})$$

4. **Weights for the output layer:** $w_{3,1}, w_{3,2}$

5. **Output:**

$$y = \text{ActivationFunction}(h_1 \cdot w_{3,1} + h_2 \cdot w_{3,2})$$
   
## **Activation Functions**
Activation functions are crucial in a neural network as they introduce non-linearity, enabling the network to model complex patterns. The Self-Learning Plugin supports several activation functions:

1. **ReLU (Rectified Linear Unit):**
   
$$ReLU(x)=max(0,x)$$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ReLU is widely used for its simplicity and effectiveness in deep networks and is particularly useful in hidden layers.

2. **Sigmoid:**
   
$$σ(x) = \frac{1}{1 + e^{-x}}$$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The sigmoid function maps input values to the range (0, 1), making it useful for probability-based outputs.

3. **Hyperbolic Tangent (Tanh):**
   
$$Tanh(x) = \frac{1}{1 + e^{-2x}} - 1$$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tanh maps input values to the range (-1, 1), offering a zero-centered output.

4. **Step Function (StepUnit):**

$$StepUnit(x) =\begin{cases} 1, \text{if } x ≥ 0 \cr 0, \text{if } x < 0 \cr \end{cases}$$

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The step function is a simple threshold-based activation function.

## **Rewards and Selection of the Best Neural Network**
In the context of training AI agents, rewards play a crucial role in evaluating and selecting the best-performing neural networks. The reward system is designed to quantify the success or performance of an AI agent in completing tasks or achieving specific goals within the environment.

### **1. Reward System:**

+ Each AI agent receives a reward based on its performance. This could be related to achieving objectives, minimizing errors, or optimizing certain metrics within the game environment.
+ The rewards are accumulated over time or specific episodes, providing a comprehensive measure of the agent's effectiveness.

### **2. Selection Criteria:**

+ After a training session, the neural networks are evaluated based on the total rewards they have accumulated.
+ The top $n$ neural networks with the highest rewards are considered the best-performing ones.
  
### **3. Purpose of Rewards:**

+ The reward system ensures that the neural networks are driven towards desired behaviors and outcomes.
+ It helps in identifying which network configurations are most successful, guiding the learning process towards more optimal solutions.

By utilizing a reward-based selection process, the training methodology focuses on continuously improving the AI agents' performance, leading to the selection of highly effective neural networks. This approach ensures that the adjustments and learning are aligned with the ultimate goals and objectives defined within the Unreal Engine environment.

## **Backward Propagation**
In typical neural networks, backward propagation (backpropagation) is used to adjust the weights based on the error of the output. However, in this plugin, we employ a simplified approach to weight adjustment.

### **Simplified Backward Propagation**
1. **Select One of the Best Networks:** After each training session, one network from the top $n$ best-performing networks is selected.
2. **Random Weight Changes:** Random changes are made to the weights of this selected network to explore new potential configurations.
   
This approach simplifies the traditional backpropagation process, making it easier to implement and potentially avoiding some local minima.

## **Weight Adjustment**
The weight adjustment process in our plugin is designed to be simple yet effective:

1. **Select One of the Best Networks:** Select randomly one network from the top $n$ best-performing networks during the training session.
2. **Random Modifications:** Apply random changes to the weights of this network. This involves slightly increasing or decreasing the weight values to explore new network behaviors.
3. **Learning Rate:** Adjust the magnitude of weight changes based on a learning rate parameter, which controls how drastically the weights are modified.
   
### **Example**

1. **Original weights:** $w_{1,1}, w_{1,2}, w_{2,1}, w_{2,2}, w_{3,1}, w_{3,2}$

2. **Learning Rate:** $\alpha$

3. **Random Value:** $\delta_{1,1}, \delta_{1,2}, \delta_{2,1}, \delta_{2,2}, \delta_{3,1}, \delta_{3,2}$

4. **Update Weights:**

$$w_{1,1} = w_{1,1} + \alpha \cdot (w_{1,1} - w_{1,1} \cdot \delta_{1,1})$$

$$w_{1,2} = w_{1,2} + \alpha \cdot (w_{1,2} - w_{1,2} \cdot \delta_{1,2})$$

$$w_{2,1} = w_{2,1} + \alpha \cdot (w_{2,1} - w_{2,1} \cdot \delta_{2,1})$$

$$w_{2,2} = w_{2,2} + \alpha \cdot (w_{2,2} - w_{2,2} \cdot \delta_{2,2})$$

$$w_{3,1} = w_{3,1} + \alpha \cdot (w_{3,1} - w_{3,1} \cdot \delta_{3,1})$$

$$w_{3,2} = w_{3,2} + \alpha \cdot (w_{3,2} - w_{3,2} \cdot \delta_{3,2})$$

## **Optimization Strategy**
The optimization strategy employed by the Self-Learning Plugin focuses on:

1. **Exploration:** Random weight changes encourage the exploration of different network configurations, potentially discovering more effective AI behaviors.
2. **Exploitation:** By selecting from the best-performing networks as the basis for modifications, the plugin ensures that learned knowledge is retained and built upon.
   
This combination of exploration and exploitation helps the AI agents gradually improve their performance over time without the complexity of traditional backpropagation.
