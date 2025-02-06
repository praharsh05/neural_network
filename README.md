# Neural Network from Scratch

A simple explanation of how neural networks work and how to implement one from scratch. The term "neural network" gets used as a buzzword a lot, but in reality they are often nuch simpler than people imagine. 

This project is was carried out as part of learning on how does neural network work and how to create the most basic component of a neural network i.e. a Neuron.

Following the creation of Neuron, we will move forward with understanding how to use a Neuron in a network and end the project with a simple prediction network.


## 1. Neurons

A Neuron is the fundamental unit of a neural network. It takes inputs, does some maths with them, and produces one output.

The following things happen in a neuron:

1. Each input is multiplied by a weight:
`x[1] -> x[1] * w[1]`
`x[2] -> x[2] * w[2]`

2. All weighted inputs are added together with a bias b:
`(x[1] * w[1]) + (x[2] * w[2]) + b`

3. The sum is passed through an activation function:
`y = f(x[1] * w[1] + x[2] * w[2] + b)`

The activation function is used to turn an unbounded input into an output that has a nice, predictable form. A commonly used activation function is the sigmoid function.