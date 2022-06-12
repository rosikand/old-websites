Date: 03/21/2021

## Introduction

Textblob. A Python library for natural language processing. A simple one—but one that spans many features. A while back, I was working on an extension project for my computer science class. The assignment itself consisted of working with strings—but we are allowed to create our own extensions. So I decided to build a political bias classifier that can classify sequences of text as either partisan or neutral. Without much NLP background behind me, I was fortunate enough to come across Textblob. Within minutes, I was able to setup a rough outline of what needed to be done. I would love to talk more about the details behind it, but that isn't the purpose of this post. Instead, we will focus on how to deploy your Textblob classifier using Flask—a web-routing microframework for Python. Fast forward a few months to the present time, I wanted to build a little demo for it. It was a simple program: **a sequence of text is inputted** and **a predicted label is outputted.** Since the program was written in Python, and I much prefer writing Python than Javascript, I decided to build the web application using Python. For the purposes of this project, Flask was indeed the perfect fit. 

## The procedure

1. After the Textblob classifier is trained, serialize the object using [pickle](https://docs.python.org/3/library/pickle.html). 
2. Create a new `.py` file consisting of a function that loads in and unserializes model, and another function that is used as a 'prediction' function. 
3. Create the Flask app which makes use of the 'prediction' function powered by the trained model. 

### Serialization

Since this post isn't about serialization, I won't go into the details, but know that it is a concept where we can store some sort of data—in this case a Python object variable. In Python, pickle is used for serialization. I recommend reading [this](https://www.datacamp.com/community/tutorials/pickle-python-tutorial) post for more information. 

In the file in which you trained your Textblob classifier (i.e. your current file may look something like: 

```python
from textblob import TextBlob
from textblob.classifiers import NaiveBayesClassifier
# training data set 
train_set = ...

# define and train the model on train_set
model = NaiveBayesClassifier(train_set) 
```

). 

After defining and training the model, we need to serialize. A note: sometimes trained models can get quite large (i.e. > ~100 GB). If that is the case for your model, you may want to use gzip in additional to Pickle. Surpisingly, there are only a couple more lines you need to add for that though. Read the end of [this](https://www.datacamp.com/community/tutorials/pickle-python-tutorial) post for detailed instructions. For the purposes of this post, we will use plain pickle. 

Serialize `model` like so: 

```python
import pickle 

model = NaiveBayesClassifier(train_set) 

outputted_file = open('name_of_outputted_file.pkl', 'wb')
pickle.dump(model, outputted_file)
outputted_file.close()
```

### Create a modular 'prediction' function

Now that we got our model all pickled up, let's create our prediction function. In this context, the prediction function is defined as follows: 

> The prediction function takes in a sequence of text (string) and outputs the classified result of that string using the trained model.

I decided to do this in a separate [file](https://github.com/rosikand/political-bias-classifier/blob/main/pred.py) with two functions: one for importing your model, and another for the actual prediction. 

Loading the model through pickle:

```python
import pickle

def load_model():
	# Load in the model using Pickle 
	input_file = open('name_of_outputted_file.pkl','rb')
	global loaded_model
	loaded_model = pickle.load(input_file)
	input_file.close()
```

The actual prediction function should call `load_model` which declares the global variable that is usable within the scope of the prediction function. Thus far: 

```python
def predict(txt):
	load_model()
```

Now, we have our model loaded in within the scope of this function as well (because we declared it as 'global'). 

All we have left to do is to make a prediction on `txt` and return that prediction: 

```python
def predict(txt):
	load_model()
	prediction = loaded_model.classify(txt)
	return prediction 
```

Now we have a nice little function that we can import and call in our Flask app. 

### Creating the Flask app

*To be continued.* 

Note: this blog post is not finished yet :)
