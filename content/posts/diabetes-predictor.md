---
title: "Building a Simple Neural Network for Diabetes Prediction"
date: 2022-12-27
draft: false
tags: ["Python"]
---
Happy Holidays! I've recently taken some time to read about medicine (a longstanding interest!) and have found ML applications in medical diagnosis/prediction really interesting. I'm very much a beginner to ML so much of this post is limited by a very rudimentary understanding of the subject. I've been watching a series of videos by [APEER](https://www.youtube.com/@apeer_micro5558), an image analysis company, from which I've been able to learn how to create simple deep learning models in Python. ML-ready data is easily accessible on sites such as [University of California Irvine's ML Repository](https://archive.ics.uci.edu/ml/datasets.php) and [Kaggle](https://www.kaggle.com/datasets)! 

## About the model

The model in this post is a binary classification model (learnt from [this]("https://www.youtube.com/watch?v=kbkLLPcyU-Q&t=2291s) video) which takes in 16 parameters (risk factors) such as age, obesity, polyuria, etc., to predict whether whether someone has diabetes. (I guess Type 1 & 2 diabetes exhibit similar enough symptoms such that the researchers didn't figure to specify the diabetes type when publishing the [data](https://www.kaggle.com/datasets/andrewmvd/early-diabetes-classification).) In context of medicine, the researchers note that "around 50% of all people suffering from diabetes are undiagnosed because of its long-term asymptomatic phase": accurate ML models that help with early detection of diabetes are thus highly desirable. 

Here's [my code](https://colab.research.google.com/drive/1UwWWSas1DOdTpgz8O7UV8QV98bdi2DDi?usp=sharing) and the [code template](https://colab.research.google.com/drive/1WEZxybgoxQz8Lmp_r6Zq6OHYdvwaz2Df?usp=sharing) I used.

**The Model**

    model = Sequential()
    model.add(Dense(8, input_dim=16, activation='relu')) 
    model.add(Dropout(0.2))
    model.add(Dense(1)) 
    model.add(Activation('sigmoid'))
     
    model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])

A neural network is constructed from three layer types: an input layer, hidden layers, and an output layer. In our model, we have an input layer with 16 nodes ("input_dim") for each of the 16 features we want to feed into the model (e.g., obesity, age, etc.), a hidden layer with 8 nodes, and an output layer with 1 node (since this is a binary classification problem - we classify into diabetes or no diabetes). My choice for having 8 hidden layer nodes was fairly arbitrary: I followed a particular [rule of thumb](https://towardsdatascience.com/17-rules-of-thumb-for-building-a-neural-network-93356f9930af) that it should be around half of the input layer, but note there exists other guidelines/rules of thumb. 

Between the input layer and hidden layer, we choose to drop off 20% of connections randomly to help better generalise the model. Ultimately, the purpose of our model is to help predict diabetes in general, and not just for our training data: in the process of learning the different features of our data, neural networks might learn the statistical noise in our data, leading to the problem of "overfitting". By dropping off connections, we help reduce this noise.

The activation functions "relu" and "sigmoid" were chosen according to [rules of thumb](https://towardsdatascience.com/17-rules-of-thumb-for-building-a-neural-network-93356f9930af): "relu" is recommended for intermediate layers while sigmoid is used for binary classification. The loss function, "binary_crossentropy" and optimizer, "adam", were also chosen in accordance with rules of thumb specified in the same article. (These are features I hope to learn more about to better understand neural networks!)

## Results
As seen from the chart, it appears this model works well on the diabetes dataset used: on the training data (which I selected to be 25% of the total data => 130 datapoints), the model achieves an accuracy of ~91% (118/130). Only 6 results are false positives and only 6 are false negatives.

![Diabetes Model Results](/diabetes-model-results.png)

For fun, I also created a correlation matrix for each of the features of the model to possibly help identify which risk factors/symptoms are most closely associated with diabetes. Below, the two highest coefficients are from label (diabetes status) with polyuria and polydipsia, respectively. A quick [search](https://www.mayoclinic.org/diseases-conditions/diabetes/in-depth/diabetes-symptoms/art-20044248#:~:text=Excessive%20thirst%20and%20increased%20urination%20are%20common%20diabetes%20signs%20and,and%20absorb%20the%20excess%20glucose.) showed that increased urination (polyuria) and excessive thirst (polydipsia) are common signs/symptoms of diabetes: this reaffirms our matrix!

![Diabetes Correl Matrix](/diabetes-correl-matrix.png)

This process has served as a fun, instructive introduction to the significant ramifications ML can have wherever data is present!

