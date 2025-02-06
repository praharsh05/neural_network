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

### Sigmoid Function

The sigmoid function only outputs in the range (0,1). Think of it as compressing (-∞, +∞) to (0,1) i.e. large negative numbers become approximately 0 and large positive numbers become approximately 1.

### Feed_Forward Function

The process of passing inputs forward to get an ouput is known as feed forward.


## 2. Combining Neurons into a Network

A neural network is nothing more than a bunch of neurons connected together.

We will create a simple neural network which will have 2 inputs, a hiddedn layer, which is any layer between the input layer and output layer, with 2 neurons (h[1] and h[2]), and an output layer with 1 neuron(o[1]). the inouts for o[1] are the outputs from h[1] and h[2], which makes it a network.

## 3. Training a Neural Network

For this project we are going to take a simple case of predicting someone's gender based on their weight and height.

We have the following data in the format:

`Name   Weight(lb)  Height(in)  Gender`
`Alice  133 65  F`
`Bob    160 72  M`
`Charlie    152 70  M`
`Diana  120 60  F`

We will represent Male with a 0 and Female with a 1.
We will also shift the data to make it easier to use, we have shifted it arbitrarily by amounts 135 and 66 to make the numbers look nice, though we should shift it by the mean.

### Loss

Before we train our network, we first need a way to quantify how "good" it's doing so that it can try to do "better", this is what loss is.

In this project we will use Mean Squared Error (MSE) Loss, which is:

`1/n 1->n ∑(y[true] - y[pred])**2`

where,

n is the number of samples, which is 4 (Alice, Bob, Charlie, Diana).

y represents the variable being predicted, which is Gender.

y[true] is the true value of the variable (the “correct answer”). For example, y[true] for Alice would be 1 (Female).

y[pred] is the predicted value of the variable. It’s whatever our network outputs.


(y[true] - y[pred])**2 is known as the squared error. Our loss function is simply taking the average over all squared errors (hence the name mean squared error). The better our predictions are, the lower our loss will be!

Better predictions = Lower loss. Training a network = trying to minimize its loss.


We now have a clear goal: minimize the loss of the neural network. We know we can change the network’s weights and biases to influence its predictions, but how do we do so in a way that decreases loss?

We’ll use an optimization algorithm called stochastic gradient descent (SGD) that tells us how to change our weights and biases to minimize loss.

Our training process will look like this:

1. Choose one sample from our dataset. This is what makes it stochastic gradient descent - we only operate on one sample at a time.
2. Calculate all the partial derivatives of loss with respect to weights or biases.
3. Use the update equation to update each weight and bias.
4. Go back to step 1.

Based on this approach we see our loss steadily decreases as the network learns.

We now use the network to predict genders:

`emily = np.array([-7, -3]) # 128 pounds, 63 inches`


`frank = np.array([20, 2])  # 155 pounds, 68 inches`


`print("Emily: %.3f" % network.feed_forward(emily)) # 0.948 - F`


`print("Frank: %.3f" % network.feed_forward(frank)) # 0.039 - M`

`Emily: 0.948`


`Frank: 0.039`

If we increase the number of epochs for the training the accuracy of the network also increases. for example: training for 1,000 epochs gave us the above prediction and training for 10,000 epochs gave us the preiction:

`Emily: 0.990`
`Frank: 0.016`