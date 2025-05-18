---
layout: post
title: Understanding neural networks- Part I
date: 2025-05-18 15:04:00
description: Defining the network architecture and intializing the NN parameters
tags: ML
categories: ML-concepts
featured: false
# pretty_table: true
---

## Step 1: Defining the Neural Network Structure: Understanding Layers

Before diving into code, it's essential to understand how a neural network is structured. At its core, a neural network is a system inspired by the human brain, consisting of layers of interconnected "neurons" that process data.
### 1. **Input Layer**
The input layer is the first layer of the network and serves as the gateway through which raw data enters the model. Each neuron in this layer represents one feature or attribute of the input data.

For example, if you're working with a dataset of handwritten digits (like the popular MNIST dataset), each image is typically 28×28 pixels, resulting in 784 input features (since 28 × 28 = 784). So, your input layer will have 784 neurons, each one receiving the pixel value of the corresponding location in the image.
### 2. **Hidden Layers**
Hidden layers are the intermediate layers between the input and output layers. These layers are where most of the computation happens. Each neuron in a hidden layer takes inputs from all the neurons in the previous layer, applies a weighted sum, adds a bias, and then passes the result through an activation function (like ReLU or sigmoid) to introduce non-linearity.

The number of hidden layers and the number of neurons in each is up to you. A single hidden layer can work for many simple tasks, but more complex problems often benefit from deeper networks with multiple hidden layers.
### 3. **Output Layer**
The output layer is the final layer of the network, and its structure depends on the task you're solving:
- For **classification**, the number of neurons equals the number of classes. For example, classifying digits 0–9 means having 10 output neurons, each one representing the probability of a particular digit.
- For **regression**, typically there's just one output neuron, giving a continuous numerical value.    
### Example We’ll Use: A Simple Binary Classifier
Let’s say we want to build a neural network that predicts whether a customer will make a purchase based on four input features:
1. **Age** (normalized between 0 and 1)
2. **Annual Income** (normalized)
3. **Browsing Time on Website** (in minutes, normalized)
4. **Number of Items Viewed** (normalized)

The output will be a binary value:
- `1` if the customer is likely to make a purchase
- `0` if not
### Network Architecture
- **Input Layer**: 4 neurons (each corresponding to one input feature)
- **Hidden Layer**: 3 neurons (fully connected to all input neurons)
- **Output Layer**: 1 neuron (outputs a value between 0 and 1 — interpreted as purchase probability)
## Example Training Data
Let’s define a few training examples to show what the network will learn from. Each training example consists of 4 input values and 1 target output.

| Age | Income | Browsing Time | Items Viewed | Purchase? |
| --- | ------ | ------------- | ------------ | --------- |
| 0.2 | 0.8    | 0.5           | 0.6          | 1         |
| 0.6 | 0.3    | 0.2           | 0.4          | 0         |
| 0.3 | 0.5    | 0.7           | 0.8          | 1         |
| 0.9 | 0.2    | 0.1           | 0.2          | 0         |

In practice, these inputs would be normalized to keep the values between 0 and 1 for better learning performance.

Great! Now that we’ve defined the structure of the neural network, the next step is to **initialize the parameters** — specifically, the **weights** and **biases**. These parameters are what the network will learn during training.
## Step 2: Initializing Parameters – Weights and Biases
Every connection between neurons in adjacent layers has a **weight**, and every neuron (except those in the input layer) has an associated **bias**. These are the values that the network updates during training to reduce the prediction error.
### What Are Weights?
Weights determine **how strongly an input influences** the output. Each weight connects a neuron in one layer to a neuron in the next layer.
- If a weight is large and positive, it strongly activates the next neuron.
- If it’s negative, it inhibits the next neuron.
- If it’s close to zero, the input has little effect.
### What Are Biases?
The **bias** is an extra parameter added to the weighted sum before applying the activation function. It allows the neuron to **shift the activation function**, enabling it to learn patterns that don’t pass through the origin.
Without biases, the neural network’s flexibility would be significantly limited.
### Parameter Dimensions for Our Example
Let’s define the parameter shapes for our specific example:
- **Input Layer → Hidden Layer**
    - Weights: `W1` will be a matrix of shape **(3, 4)**  
        (3 hidden neurons, each receiving 4 inputs)
    - Biases: `b1` will be a vector of shape **(3, 1)**  
        (1 bias for each hidden neuron)
- **Hidden Layer → Output Layer**
    - Weights: `W2` will be a matrix of shape **(1, 3)**  
        (1 output neuron, connected to 3 hidden neurons)
    - Bias: `b2` will be a scalar or a vector of shape **(1, 1)**  
        (bias for the output neuron)
This setup assumes that we're using **column vectors** for input examples (shape: 4 × 1).
### How to Initialize
When initializing weights and biases, the goal is to start with small random values to break symmetry:
- **Weights (`W1`, `W2`)**: Initialized with small random numbers (e.g., drawn from a uniform or normal distribution). This randomness helps the neurons learn different features during training.
    Example:
    ```text
    W1 = random values of shape (3, 4)
    W2 = random values of shape (1, 3)
    ```
- **Biases (`b1`, `b2`)**: Usually initialized to **zeros**. Starting biases at zero is safe, and they’ll quickly move during training.
### 🧠 Why Random Initialization Is Important
If all weights were initialized to the same value (like zero), all neurons in a layer would learn the same thing — this is known as the **symmetry problem**. Random initialization ensures that each neuron starts with a different perspective on the data.

To recap, our network has the following parameters:
- `W1`: shape (3, 4), randomly initialized
- `b1`: shape (3, 1), initialized to zeros
- `W2`: shape (1, 3), randomly initialized
- `b2`: shape (1, 1), initialized to zero
These parameters will be updated during training using **backpropagation** and **gradient descent**.
