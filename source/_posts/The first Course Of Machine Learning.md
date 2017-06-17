---
title: 'The first Course Of Machine Learning'
date: 2016-08-05 08:06:16
categories: Machine Learning
comments: true
tags:
- Machine Learning
- Big Data
---
well, today we'll talk something about Machine Learning.
First, I have to say, I do not often use English to write article, if you can help me find some mistake in grammar, I'll be very happy.
So, let's get into today's business.
# 1.What’s the Machine Learning?
This phrase has became more and more hot in recent years, but what is it?
All right, these information about Machine Learning were come from **Andrew Ng**, I'm here to pay my homage to him.
In 1959, Arthur Samuel,he defined **machine learning as the field of study that gives computers the ability to learn without being explicitly programmed**, this man wrote a checkers playing program.
Arthur Samuel is not a very good checkers player, but he let the program to play 10's of 1000's of games against itself. And by watching what sorts of board positions tended to lead to wins and what sorts of board positions tended to lead to losses.
Eventually, this computer play checkers better than himself.
So,this is an old definition.

A more recent definition was defined by Tom Mitchell:
**A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T as measured by p improves with Exprience E.**
well, that a long sentence, in fact,it's just like a tongue twister.
In the Checkers Game ,E is having the program played 1000's Games against itself,T is the task of playing Checkers,and P, will be the probability that it wins the next game of checkers against new opponent.

# 2.Our Life With Machine Learning
So, we talk about so many things about what is Machine Learning, may be you still not have any interest in this field.
Don't Worry, I'll say some information more Close  to our life:
This technology is looks so useful, but where can we use it?

Please calm down, I'll be list in the following:
1. **intercept Spam message and E-mail.**That's so useful ,thanks for it.
2. **To classify the customers needs and preferences.**Which kind of music would you like?
3. **Search engine just like geogle and baidu.**You want a better Search engine?Well,Machine Learning is important.
4. **Robots made a decision.** Like AlphaGo? perhaps.

etc.

In fact, I'm very excecting when I write this article. why?
"It's must be the most important Century in humans history."  by SUNIL RAY.
There may be some exaggerated but most are correct.
The democratization of the tools and techniques will take the development to the technology.
In the future, everyone will be Contributing to the future of humanity.

# 3.Machine Learning
Broadly, there are 3 types of Machine Learning Algorithms:
- Supervised Learning
- Unsupervised Learning
- Reinforcement Learning
And I will introduce each module muinutely.

## (1) Supervised Learning
Supervised Learning,this must be the first type of Machine Learning Algorithms you met.
This algorithm consist of a target / outcome variable (or dependent variable) which is to be predicted from a given set of predictors (independent variables).
Using these set of variables, we generate a function that map inputs to desired outputs. The training process continues until the model achieves a desired level of accuracy on the training data.
Here are some famous algorithms are belongs to Supervised Learning:
- Regression ( OK.I will introduce this later )
- KNN algorithms ( the easiest one )
- Decision Tree ( if you only have a little data ,It's may be easy to Overfitting,but to be honest,it's a classic algorithm )
- Random Forest ( based on the decision tree )
- Logistic Regression ( different from Regression,this  is a classification not a regression algorithm)
- SVM( The support vector machines ) ( a important algorithm ,you must know it )
etc.
## (2) Unsupervised Learning
I'd like to introduce this kind of Machine algorithm after the Supervised Learning.
The Unsupervised Learning do not have any target or outcome variable to predict or estimate,it is used for clustering population in different groups.When you face to the large Scale data,you can consider to use the Unsupervised Learning.
Here are some famous algorithms are belongs to Unsupervised Learning:
- k-means ( want to do a classification about your customer? this one is the Basic algorithm )
- Mini Batch K-Means ( k-means can't deal with the big data,it will take you a lot of time to compute.In this situation you can use this algorithm )
- Neural network models ( A famous One ,right? You must know about this model---perpare for the course of Deep Learning )
- Gaussian Mixture Model ( GMM )( If you want to do a speaker recognition,the methods of MFCC + GMM  will be a good choice )
- Dimensionality Reduction Algorithms ( high-dimensional? No ,you can't design a algorithm base on this situation,So---you need this One )
etc.

## (3)Reinforcement Learning
Using this algorithm, the machine is trained to make a specific decisions. It works On this way: the machine is exposed to an environment where it trains itself continually using trial and error.
if you want to make a very smart Chinese chess program, the Supervised Learning and Unsupervised Learning will spend a lots of time on Traversal calculation. So, the better method is use Reinforcement Learning.
Here are some famous algorithms are belongs to Reinforcement Learning:
- Markov Decision Process,(MDP)
- Monte Carlo Methods(an important value compute algrorithm)
I didn't use so much about Reinforcement Learning, So I'll talk in the later published articles.
# 4.Summary
Well, today we have a general overview of the Machine Learning, after this article, I'll published more articles about the algorithms and new Technology of Machine Learning, maybe you can see something else. you may feel difficult to read this article because it's my first time to use English write a long article as this One.
Well, it's not a problem, for me this is a new beginning,and maybe it's same to you.