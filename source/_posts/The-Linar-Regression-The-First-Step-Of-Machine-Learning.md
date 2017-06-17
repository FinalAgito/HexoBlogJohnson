---
title: 'The Linar Regression: The First Step Of Machine Learning'
date: 2016-08-17 15:36:00
categories: Machine Learning
comments: true
tags:
- Machine Learning
---
## 1. Why did I introduce regression algorithm in the first place?
I glad to start write this article, and just as the title's words, I want to use 'Regression' as the first step of the Machine Learning's world. Some senior learner may have some suggest about this article, and I'm glad to see you feedback some information.

Regrassion, This is a base course when you get into the field of Supervised Learning. Now I'll introduce this knowledgepoint for you. And may be, I'll do more introduce about Supervised Learning  latter.

## 2. Linar Regression
I perpare to talk about Regression from the most simple one: The Linar Regression.

You may be famillar with this name, that's great. Because you have alreadly learned some basic knowledge of the Regression. This part of lecture is called least squares technique(Maybe? I  can't be too sure). You can see this topic in your primary school's textbooks.

Now, Let's Start.
### (1) Single Variable Linear Regression
You may have some questions: What's the Regression problem? Well, the regression problem is that we had got the data in the past time and we use it  to predict a continuous output like price.

And now, I would give you an example to help you understand the algorithm.

If you wants to predict the championship results of Meter race project in the next Olympic Game. So, What would you do?

Ok, Now, I  provide you the figure of the sports scores of recent years:
![figure 0-0 The sports scores of Meter race project in recent years](\images\MachineLearning\Regression\OneValuableRegresstion.jpg)
Then, you can do the predict to the scores of meter race project in the next Olympic game.

So, how I can do that?
![figure 0-1 The correlation between input and output](\images\MachineLearning\Regression\ForHousePrice.png)

When you check  the data in this figure, you can find some regulation, every 4 years there are a score to fit them. And you can use a algorithm to fit, then you can get the rules between in these data time.
Perhaps, you can make a quation to describe this line:
```
f(x) = kX + b;
```
but, it can't be so simple like this, our data is confusion and disorder, we should to consider for the error, so, the true equation is:
```
Y[i] = f(x[i]) + E(x[i]);
```
The i is the serial number of the Training data we got, and the Y is the output.
we gave the definition of the f(x), and the E(x[i]) is the error of the x[i].
Now, I have a equation.

In this function,we have simple input and  output, we put into the value of the year and get a output, just one feature(year), that's why we called it 'Single'.
Now, we can assume that the model is a quadratic function:


Then, let us see a more complicated one.

You would follow with me, right?
### (2)Multivariate Linear Regression
I could use a example to tell you what's call the multivariate linear regression, in fact, it's a very common example.
If I want to buy a house, I would do a predict to the house's price, then, I can get the price that I may have to pay.
Of course, you can still use the house's area as an input and the house's price to be an output, but if we do this, the question we will meet is that we can't make a high accuracy of prediction.
It's not difficult to think, because there isn't only a simple feature to influence the house's price, so, we should take the other features into this model, then we will have several inputs and one output, this is a form of Multiple Linar Regression.
If you don't understand, don't worry, I'll use a diagram to explain this concept.
So, this time I want to use another example to descripe the multivariate linear regression, may be you are similar with this event:

If you want to  by a house, you will find some factors to predict the house's price, but only one feature can't get a good accuracy, so you may need to use two, three or more features  as the inputs value, so, that's what I want to say.

Now, I will give two figures, one is for Single  value's situation and another is for the Multiple's.

![figure 2-0 The Simple Linar Regression for House Price](\images\MachineLearning\Regression\SimplePicForHouse.png)
This picture comes from the Machine Learning course of Washington.

![figure 2-1 Two inputs for House Predict model](\images\MachineLearning\Regression\MultiplePicForHouse.png)
If we compare this picture and the above one, we can see the diffience of the two situations.(Suppose we function has two inputs: the house's age and the square feet)
The Results no longer only decided by an element, but controlled by house's age and square feet.
As you know, We cannot be too severely limit your thinking, So you can expand your thinking:

How the situation will be If we get a (n + 1) dimensional input?
So we also can use a fuction to describle the relationship between the (n + 1) dimensional input and house price( In the above example, we only used a two-dimensional input, Here I will it to expand to if we have the 'n + 1' d):
![figure 2-2 The equation For multivariate linear regression](\images\MachineLearning\Regression\EuqationForMul.png)

We assumed the X[0] = 1;
If you have the knowledge of linear algebra, you can find that this quation equal to* θ'X*.

### (3)Gradient Descent Algorithm

![figure 3-0 The Module process of Regression(from Washington college's courses) ](\images\MachineLearning\Regression\MLModelForRegress.png)
Now, if we  use the idea in upon part of this article, we have to set a part called "quality metric"(That's right, look at the orange block in the picture). This module makes the program working.
Our Predict of house price could be have error(In fact, there is error is certain), we need to have a method to let computer to make more accurate predictions by calculation accuracy.
The method to resolve this question is that we called the Gradient Descent Algorithm.

Aha, this gradicent algorithm is very important in the Machine Learning's history.
Ok, let us look about it.

May be you have already find the key of the above equation, yes, the Gradient Descent Algorithm is a method to find the most suitable value for the θ[1.....n].(The value of n is definited by your features number)
Now we have a question: How can we make a assess of the predict result?
To diffierent situation have diffierent methods, but we just talk about one function for the Regression(Is this because of our title).

Now, I used this equation to describe the deviation between the predicted and actual values:
  *h(θ)(x[i])-y[i]*
And we will the n results together, this is the first assessment of the eqation(just for one feature).
![figure 3-1 Equation For assessment in gradient descent](\images\MachineLearning\Regression\EuqationForGrad.png)
*Remeber the 1/n has did a balance for the value.*
We got the function about the assessment, now how we define the value of the θ?
Can I use this picture at this location and  take a relaxed?

![figure 3-2 To define the θ(This pic come from ML course of Standford)](\images\MachineLearning\Regression\EuqationForTheta.png)

*We called this "Cost Function".*
And the Alpha(*α*) in the equation is called the * "learning rate"*, I'll introduce this on the below.

So, this is the one feature's situation, and you can imagine that there is multidimensional for θ[1.......n].

#### <1>feature normalization - for Multivariate Linear Regression
feature normalization is important，So we have to do some feature scaling,  Let all the value of the change in the interval [- 1, 1].
You should make sure feature's value are on a similar scale, use different methods according to different situations, don't asking me about this, maybe you could try *xi=(xi-μi)/σi*.
#### <2>Learning Rate and How Can It Stop?
Will, that's the most importance, and this is a problem that you want to know.

How can it Stop and, when?

Look this picture(Also from the Andred Ng's class):
![figure 3-3 Find the  most suitable value for θ1 and θ2(two-dimensional)](\images\MachineLearning\Regression\ThetaAndCost.png)
We can see that, through the iteration step by step procedure, we  arrived at the  centre of the circle in the picture.

That's what I wanted.(To find the minmum of J(θ))
But if the *α* is so big, then we can't find the minmum of J(θ).

![figure 3-4 The figure about the unsuitable and suitable value for α](\images\MachineLearning\Regression\LearningRate.png)

Now, you have a intuitive impression of Learning Rate, and in some situation, you have to design a method to find it.
Well, the worst and common method is  try to verify every possible values. :)
## 3.Summary
Now, today we have done a macro for the " Linar Regression", but there are a special kind of species called "the Logistic Regression".
*This belongs to the category of "classification".*
I will continue this in a future article. :)