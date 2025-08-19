# Documentation

## 1. Day - Wendsday 13.8

- Learning about Spiking Neural Networks
- Looking at different Backpropagation techniques for SNNs (surrogate gradient, BPTT, STDP, ...)
- Taking a look at how Leak-and-Fire Neurons work
- 
## 2. Day Thursday 14.8

- Set up Laptop with pycharm
- Code a LIF Neuron from Scratch using https://snntorch.readthedocs.io/en/latest/tutorials/tutorial_2.html
- Test its functionality with different currents

## 3. Day - Friday 15.8

- Take a look at the Heidelberg Spiking Datatset 
- Examine different properties of the Dataset
- Plot Dataset

- Come up with a potential SNN architecture for the Datatset
- Think about how to reduce the Input Neuron Number down from originally 700

- Cut parts of the Data after looking at the Datatset with more plots
- Input neuron num: 700 --> 550
- 
- Reduce the Dataset further by converting it to a Matrix and using a 3x3 Kernel on it
- Input neuron num: 550 --> 183

## 4. Day - Monday 18.8

- Learn about the SNNtorch libary through videos and previous experience 
- Code up the before imagined SNN architecture using the libary
- Train the model on the heidelberg Dataset
- Investigate the inner workings of the SNNlibary/architecture 
  - Backpropagation used by SNNTorch
  - plot weight Matrix
  - investigate hidden layer

![loss_accuracy-plot SNN model.png](../../Downloads/loss_accuracy-plot%20SNN%20model.png)