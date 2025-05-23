<H3>Name: Mohamed Faizal M</H3> 
<H3>Register no: 212223243002</H3> 
<H3>Date:</H3>
<H3>Ex No.2 </H3>
## Implementation of Perceptron for Binary Classification
# AIM:
To implement a perceptron for classification using Python<BR>

# EQUIPMENTS REQUIRED:
Hardware – PCs
Anaconda – Python 3.7 Installation / Google Colab /Jupiter Notebook

# RELATED THEORETICAL CONCEPT:
A Perceptron is a basic learning algorithm invented in 1959 by Frank Rosenblatt. It is meant to mimic the working logic of a biological neuron. The human brain is basically a collection of many interconnected neurons. Each one receives a set of inputs, applies some sort of computation on them and propagates the result to other neurons.<BR>
A Perceptron is an algorithm used for supervised learning of binary classifiers.Given a sample, the neuron classifies it by assigning a weight to its features. To accomplish this a Perceptron undergoes two phases: training and testing. During training phase weights are initialized to an arbitrary value. Perceptron is then asked to evaluate a sample and compare its decision with the actual class of the sample.If the algorithm chose the wrong class weights are adjusted to better match that particular sample. This process is repeated over and over to finely optimize the biases. After that, the algorithm is ready to be tested against a new set of completely unknown samples to evaluate if the trained model is general enough to cope with real-world samples.<BR>
The important Key points to be focused to implement a perceptron:
Models have to be trained with a high number of already classified samples. It is difficult to know a priori this number: a few dozen may be enough in very simple cases while in others thousands or more are needed.
Data is almost never perfect: a preprocessing phase has to take care of missing features, uncorrelated data and, as we are going to see soon, scaling.<BR>
Perceptron requires linearly separable samples to achieve convergence.
The math of Perceptron. <BR>
If we represent samples as vectors of size n, where ‘n’ is the number of its features, a Perceptron can be modeled through the composition of two functions. The first one f(x) maps the input features  ‘x’  vector to a scalar value, shifted by a bias ‘b’
f(x)=w.x+b
 <BR>
A threshold function, usually Heaviside or sign functions, maps the scalar value to a binary output:

 


<img width="283" alt="image" src="https://github.com/Lavanyajoyce/Ex-2--NN/assets/112920679/c6d2bd42-3ec1-42c1-8662-899fa450f483">


Indeed if the neuron output is exactly zero it cannot be assumed that the sample belongs to the first sample since it lies on the boundary between the two classes. Nonetheless for the sake of simplicity,ignore this situation.<BR>


# ALGORITHM:
STEP 1: Importing the libraries<BR>
STEP 2:Importing the dataset<BR>
STEP 3:Plot the data to verify the linear separable dataset and consider only two classes<BR>
STEP 4:Convert the data set to scale the data to uniform range by using Feature scaling<BR>
STEP 4:Split the dataset for training and testing<BR>
STEP 5:Define the input vector ‘X’ from the training dataset<BR>
STEP 6:Define the desired output vector ‘Y’ scaled to +1 or -1 for two classes C1 and C2<BR>
STEP 7:Assign Initial Weight vector ‘W’ as 0 as the dimension of ‘X’
STEP 8:Assign the learning rate<BR>
STEP 9:For ‘N ‘ iterations ,do the following:<BR>
        v(i) = w(i)*x(i)<BR>
         
        W (i+i)= W(i) + learning_rate*(y(i)-t(i))*x(i)<BR>
STEP 10:Plot the error for each iteration <BR>
STEP 11:Print the accuracy<BR>
# PROGRAM:
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

class Perceptron:
    def __init__(self, learning_rate=0.1):
        self.learning_rate = learning_rate
        self.weights = None
        self.bias = 0

    def fit(self, X, y, epochs=10):
        self.weights = np.zeros(X.shape[1])
        self.errors = []

        for _ in range(epochs):
            error_count = 0
            for xi, yi in zip(X, y):
                update = self.learning_rate * (yi - self.predict(xi))
                self.weights += update * xi
                self.bias += update
                error_count += int(update != 0.0)
            self.errors.append(error_count)
            print(f"Epoch {_+1}, Errors: {error_count}")

    def predict(self, X):
        return np.where(np.dot(X, self.weights) + self.bias >= 0, 1, -1)

# Load and preprocess the dataset
data = pd.read_csv("/content/Iris_NN2.csv")
X = data.iloc[:, :2].values  # Use first two features
y = np.where(data.iloc[:, 4] == 'Iris-Setosa', 1, -1)  # Binary labels

# Standardize features
X = (X - X.mean(axis=0)) / X.std(axis=0)

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=0)

# Train and test Perceptron
model = Perceptron(learning_rate=0.01)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
print(f"Accuracy: {accuracy_score(y_test, y_pred) * 100:.2f}%")

# Plot errors
plt.plot(range(1, len(model.errors) + 1), model.errors, marker='o')
plt.xlabel('Epoch')
plt.ylabel('Errors')
plt.title('Training Errors')
plt.show()

```

# OUTPUT:

![image](https://github.com/user-attachments/assets/459922a7-9fac-4da4-b2fd-d112f7814472)

![image](https://github.com/user-attachments/assets/351c4a05-819d-4246-93cc-71afeb5a7665)


# RESULT:
 Thus, a single layer perceptron model is implemented using python to classify Iris data set.

 
