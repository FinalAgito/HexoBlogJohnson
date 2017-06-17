---
title: 'R and R*Tree(二):The Dynamic Structure For Spatial Searching'
date: 2017-01-17 10:17:27
categories:
- algorithm
tags:
- Mining Data
---
This article is not completed, I will add the demo codes to this article.
Ok, after so many time, now we can finally start our second trip.
Today I will introduce the rest of the algorithms, and make a comparison between the R-tree and the R\* tree.
Most of them are the same, but the R\* tree has some important change in the algorithms.
But first, let's finish the last part of R-tree.
## 1.Algorithm(Undertake section in the previous article)

### 1.1 Delete Algorithm
First, let's start with a easy one, the delete algorithm.
We use this function to deal with the situation that you want to delete a index (or we called it Value) E from the tree. We denoted as E.
Now I will show you the steps:
1. Use the *Find Leaf* Function to find the Leaf L which include the record E, end this program when the record can't be find.
2. Delete L from E.
3. Use the Function *Condense Tree* , and pass the  L as the parameter.
4. If the Root node have only one leaf node after the condense, use the leaf node as the new root node.

### 1.2 Condense Tree Algorithm
Using a node which has deleted one record as the parameter.
Translating the records of the node and delete itself if the records'number has became so small.
We also can delete the transport node if we have the demand. Ajusting the area of all the rectangles from root node to which node you choose. Keeping their area smallest.
Steps:
1. We transite the L to N, assume Q as the delete nodes, which equals to NULL.
2. If N is the root node, go to the step 6, or denote P as N's parent node, 'EN' as the record in N.
3. If N's record nodes smaller than the limit number m, delete the EN from P, and add N to Q's room.
4. If N hasn't be deleted, we should adjust ENI to help it include all the records in N.
5. Let N equals to P, loop the step from 2.
6. Reinsert the node from Q into the tree, and you should put the nodes which at the upper layer on the tree's upper layer. (In order to make the original child nodes become the root's child nodes.)

### 1.3 Node Split Algorithm
In order to make a best split method for control the rectangle's area smallest.
#### 1.4 Quadratic Cost  Algorithm
In order to find a split method to get the smallest area.
Step:
1. Find two nodes in the line(We have amount m+1 nodes) which have waste the biggest area if we put them together. (Use the area of the rectangle include with the two nodes minus each area of the two nodes)
2. Others use the same method to divide into two groups.
