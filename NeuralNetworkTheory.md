# **Neural Network Theory**
The Self-Learning Plugin for Unreal Engine 5.3 utilizes a neural network to enable AI agents to learn and improve their task performance. This page explains the theory behind the neural network implementation used in this plugin.

## **Table of Contents**
1. [Introduction](#introduction)
2. [Weight Initialization](#weightinitialization)
3. [Forward Propagation](#forwardpropagation)
4. [Activation Functions](#activationfunctions)
5. [Backward Propagation](#backwardpropagation)
6. [Weight Adjustment](#weightadjustment)
7. [Optimization Strategy](#optimizationstrategy)
   
## **Introduction**
Neural networks are a key component of modern machine learning, allowing systems to learn from data and make decisions based on that learning. In the Self-Learning Plugin, a neural network is employed to enable AI agents to perform and improve in various tasks within Unreal Engine 5.3 environments.

Weight Initialization
Proper initialization of weights is crucial for the effective training of neural networks. In the Self-Learning Plugin, weights are initialized to small random values within a specified range.

Recommended Initialization Range
Weights are typically initialized in the range of 
−
1
−1 to 
1
1.
Initializing weights in this range ensures that the network starts with small values, which helps in preventing issues related to exploding or vanishing gradients.

Forward Propagation
Forward propagation is the process by which input data is passed through the neural network to produce an output. This involves a series of steps where each neuron's output is calculated as a weighted sum of its inputs, passed through an activation function.

Steps in Forward Propagation
Input Layer: The neural network receives input data (e.g., sensor data, game state). These input values often need to be scaled to ensure they are within a range suitable for the neural network (e.g., 0 to 1).
Hidden Layers: The input data is processed through one or more hidden layers. Each neuron in a hidden layer calculates a weighted sum of its inputs, applies an activation function, and passes the result to the next layer. Hidden layers are useful for capturing complex patterns and interactions in the data, although they are not strictly necessary for all tasks.
Output Layer: The final layer produces the output, which can be a decision or action taken by the AI agent.
Example
For a simple neural network with one hidden layer:

Inputs: 
𝑥
1
,
𝑥
2
x 
1
​
 ,x 
2
​
 
Weights for the hidden layer: 
𝑤
1
,
1
,
𝑤
1
,
2
,
𝑤
2
,
1
,
𝑤
2
,
2
w 
1,1
​
 ,w 
1,2
​
 ,w 
2,1
​
 ,w 
2,2
​
 
Hidden layer outputs:
ℎ
1
=
activation
(
𝑥
1
⋅
𝑤
1
,
1
+
𝑥
2
⋅
𝑤
1
,
2
)
h 
1
​
 =activation(x 
1
​
 ⋅w 
1,1
​
 +x 
2
​
 ⋅w 
1,2
​
 )

ℎ
2
=
activation
(
𝑥
1
⋅
𝑤
2
,
1
+
𝑥
2
⋅
𝑤
2
,
2
)
h 
2
​
 =activation(x 
1
​
 ⋅w 
2,1
​
 +x 
2
​
 ⋅w 
2,2
​
 )
Weights for the output layer: 
𝑤
3
,
1
,
𝑤
3
,
2
w 
3,1
​
 ,w 
3,2
​
 
Output:
𝑦
=
activation
(
ℎ
1
⋅
𝑤
3
,
1
+
ℎ
2
⋅
𝑤
3
,
2
)
y=activation(h 
1
​
 ⋅w 
3,1
​
 +h 
2
​
 ⋅w 
3,2
​
 )
Activation Functions
Activation functions are crucial in a neural network as they introduce non-linearity, enabling the network to model complex patterns. The Self-Learning Plugin supports several activation functions:

ReLU (Rectified Linear Unit):

ReLU
(
𝑥
)
=
max
⁡
(
0
,
𝑥
)
ReLU(x)=max(0,x)
ReLU is widely used for its simplicity and effectiveness in deep networks and is particularly useful in hidden layers.

Sigmoid:

𝜎
(
𝑥
)
=
1
1
+
𝑒
−
𝑥
σ(x)= 
1+e 
−x
 
1
​
 
The sigmoid function maps input values to the range (0, 1), making it useful for probability-based outputs.

Hyperbolic Tangent (Tanh):

tanh
⁡
(
𝑥
)
=
2
1
+
𝑒
−
2
𝑥
−
1
tanh(x)= 
1+e 
−2x
 
2
​
 −1
Tanh maps input values to the range (-1, 1), offering a zero-centered output.

Step Function (StepUnit):

StepUnit
(
𝑥
)
=
{
1
if 
𝑥
≥
0
0
if 
𝑥
<
0
StepUnit(x)={ 
1
0
​
  
if x≥0
if x<0
​
 
The step function is a simple threshold-based activation function.

Backward Propagation
In typical neural networks, backward propagation (backpropagation) is used to adjust the weights based on the error of the output. However, in this plugin, we employ a simplified and unique approach to weight adjustment.

Simplified Backward Propagation
Select One of the Best Networks: After each training session, one network from the top 
𝑛
n best-performing networks is selected.
Random Weight Changes: Random changes are made to the weights of this selected network to explore new potential configurations.
This approach simplifies the traditional backpropagation process, making it easier to implement and potentially avoiding some local minima.

Weight Adjustment
The weight adjustment process in our plugin is designed to be simple yet effective:

Select One of the Best Networks: Identify one network from the top 
𝑛
n best-performing networks during the training session.
Random Modifications: Apply random changes to the weights of this network. This involves slightly increasing or decreasing the weight values to explore new network behaviors.
Learning Rate: Adjust the magnitude of weight changes based on a learning rate parameter, which controls how drastically the weights are modified.
Example
Original weights: 
𝑤
1
,
1
,
𝑤
1
,
2
,
𝑤
2
,
1
,
𝑤
2
,
2
,
𝑤
3
,
1
,
𝑤
3
,
2
w 
1,1
​
 ,w 
1,2
​
 ,w 
2,1
​
 ,w 
2,2
​
 ,w 
3,1
​
 ,w 
3,2
​
 
Random changes:
𝑤
1
,
1
→
𝑤
1
,
1
+
Δ
𝑤
1
,
1
w 
1,1
​
 →w 
1,1
​
 +Δw 
1,1
​
 

𝑤
2
,
2
→
𝑤
2
,
2
+
Δ
𝑤
2
,
2
w 
2,2
​
 →w 
2,2
​
 +Δw 
2,2
​
 

(where 
Δ
𝑤
Δw are small random values scaled by the learning rate)
Optimization Strategy
The optimization strategy employed by the Self-Learning Plugin focuses on:

Exploration: Random weight changes encourage the exploration of different network configurations, potentially discovering more effective AI behaviors.
Exploitation: By selecting from the best-performing networks as the basis for modifications, the plugin ensures that learned knowledge is retained and built upon.
This combination of exploration and exploitation helps the AI agents gradually improve their performance over time without the complexity of traditional backpropagation.
