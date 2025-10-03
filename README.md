This repository demonstrates a membership inference attack on a Convolutional Neural Network (CNN) trained on the MNIST dataset.
The project shows how an attacker can distinguish between training samples (members) and unseen samples (non-members) based on the model’s output confidence, and explores whether adding Gaussian noise during training can mitigate this privacy risk.

First, I loaded the MNIST dataset using TensorFlow and displayed a few training samples with Matplotlib.
Then, I built a simple CNN model with PyTorch, which included a convolutional layer (Conv2D + ReLU + MaxPooling) and a fully connected layer for 10 classes.

To simulate noise, I defined a function called add_noise(images, epsilon) that modifies the training images with Gaussian noise (the lower the epsilon, the more noise is added). This part was designed for defense against privacy attacks.

Next, I wrote the get_confidence(model, image) function, which returns the maximum softmax value, representing the model's confidence in its input prediction.

I converted the data into PyTorch tensors and normalized them. The training set was split into two parts:
Member dataset → Data used to train the model.
Non-member dataset → Data from the test set that the model hasn't seen.

I trained two models:
A base model on clean data (without noise).
A noisy model on data modified with Gaussian noise.

Both models were trained for 5 epochs using Adam and Cross-Entropy.
During the Membership Inference evaluation phase, I calculated the model's confidence for a member sample and a non-member sample. If the model's confidence for member data is significantly higher, it indicates that the model leaks membership information.
Finally, I compared the confidence of the base model and the noisy model to see whether the noise reduces this leakage or not.
