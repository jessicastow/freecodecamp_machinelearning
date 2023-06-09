# Introduction to Machine Learning and TensorFlow

###### tags: `FreeCodeCamp-MLwithPython`

* [Machine Learning Fundamentals](#machine-learning-fundamentals)
    * [AI vs Neural Networks vs Machine Learning](#ai-vs-neural-networks-vs-machine-learning)
    * [Data](#data)
* [Introduction to TensorFlow](#introduction-to-tensorflow)
    * [Setup](#setup)
    * [Tensors](#tensors)   
* [Sources](#sources)
---
## Machine Learning Fundamentals
https://www.freecodecamp.org/learn/machine-learning-with-python/tensorflow/introduction-to-tensorflow

### AI vs Neural Networks vs Machine Learning

![](./images/module1/IA-split.png)


* **AI**: The effort to automate intellectual tasks normally performed by humans.
    1950 -> Can computers think? AI were just a set of rules. AI can be simple or complex.
* **ML**: Takes data, takes what the output should be, and figures out the rules for us. So when we look at new data, we can hace the best possible output for that. That's why a lot of the times ML models do not have 100% accuracy. 
![](./images/module1/classic-ml.png)
* **NN** or **Deep Learning**: form of ML that uses a layered representation of data. They are not modeled after the brain.


### Data

Data is the most important part of ML and AI.

* **Features**: The <u>input info</u> that we will always have, and we need to give to the model to get some output.
* **Label**: The <u>output</u>, what we are trying to look for, or predict.

---


## Introduction to TensorFlow
https://www.freecodecamp.org/learn/machine-learning-with-python/tensorflow/introduction-to-tensorflow

### Setup

```python
pip install tensorflow-gpu
%tensorflow_version 2.x  # only if you are in a notebook
import tensorflow as tf  # now import the tensorflow module
print(tf.version)  # make sure the version is 2.x
```

### Tensors

"A tensor is a generalization of vectors and matrices to potentially higher dimensions. Internally, TensorFlow represents tensors as n-dimensional arrays of base datatypes."    (https://www.tensorflow.org/guide/tensor)


They are the main objects that are passed around and manipulated throughout the program. Each tensor represents a partially defined computation that will eventually produce a value.

Each tensor has a data type and a shape.

Data Types Include: float32, int32, string and others.

Shape: Represents the dimension of data.

#### Create Tensors

```python
#args: value and datatype
string = tf.Variable("this is a string", tf.string) 
number = tf.Variable(324, tf.int16)
floating = tf.Variable(3.567, tf.float64) # this is an example of a scalar
```

#### Rank/Degree of Tensors

Rank/Degree: Number of dimensions involved in the tensor.

```python
rank1_tensor = tf.Variable(["Test"], tf.string) @ rank 1 because it is 1 list/1 array which means 1 dimension
rank2_tensor = tf.Variable([["test", "ok"], ["test", "yes"]], tf.string) # rank2 because it is a list inside of a list
rank = tf.rank(rank2_tensor) # we use this to determine the rank of a tensor. Output = numpy2 which means rank 2 
```

#### Shape of Tensors

Shape: Number of elements that exist in each dimension.
`shape = rank2_tensor.shape` # output will tell us 1) how many lists and 2) how many elements 

#### Changing Shape

*Example:*
```python
# tf.ones() creates a shape [1,2,3] tensor full of ones
tensor1 = tf.ones([1,2,3])  
# reshape existing data to shape [2,3,1]
tensor2 = tf.reshape(tensor1, [2,3,1])
# 3 tells us there needs to be 3 lists
# -1 tells the tensor to calculate 
# the size of the dimension in that place
# this will reshape the tensor to [3,3]
tensor3 = tf.reshape(tensor2, [3, -1])  
                                        
#The numer of elements in the reshaped 
#tensor MUST match the number in the original  .                     
```

#### Slicing Tensors

The slice operator can be used on tensors to select specific axes or elements.

*Examples:*

```python
# Creating a 2D tensor
matrix = [[1,2,3,4,5],
          [6,7,8,9,10],
          [11,12,13,14,15],
          [16,17,18,19,20]]

tensor = tf.Variable(matrix, dtype=tf.int32) 
print(tf.rank(tensor))
print(tensor.shape)

# Now lets select some different rows and columns from our tensor

three = tensor[0,2]  # selects the 3rd element from the 1st row
print(three)  # -> 3

row1 = tensor[0]  # selects the first row
print(row1)

column1 = tensor[:, 0]  # selects the first column
print(column1)

row_2_and_4 = tensor[1::2]  # selects second and fourth row
print(row2and4)

column_1_in_row_2_and_3 = tensor[1:3, 0]
print(column_1_in_row_2_and_3)
```


#### Types of Tensors

* Variable
* Constant
* Placeholder
* SparseTensor
* few others as well

Note: With the exception of 'Variable' all of these tensors are immuttable (their value may not change during execution)


#### Evaluating Tensors

There will be some times throughout this guide that we need to evaluate a tensor. In other words, get its value. Since tensors represent a partially complete computation we will sometimes need to run what is called a 'session' to evaulate the tensor.

There are many different ways to achive this but I will note the simplest way below. 

```python
with tf.Sesion() as sess: # creates a session using the default graph
   tensor.eval() # tensor will of course be the name of your tensor
```

#### Examples of reshaping

```python
%tensorflow_version 2.x
import tensorflow as tf
print(tf.version)

t = tf.ones() # this means all the values will be set to be ones

# Let's set them to all be zeros

t = tf.zeros([5,5,5,5]) 
# To figure out how many elements we have we can multiply all these numbers
# So 5 x 5 x 5 x 5 = 625
print(t) # will print the tensor

# Now, let's reshape this tensor and take all these elements and flatten them out

t = tf.reshape(t, [625]) # makes a list of 625 zeros
print(t)

# We can also reshape it to 125 
t = tf.reshape(t, [125, -1]) # the -1 means that tensorflow needs to infer what the shape needs to be
print(t) # will print 125 sets of 5 
```


## Sources

* https://www.tensorflow.org/guide/tensor



---
