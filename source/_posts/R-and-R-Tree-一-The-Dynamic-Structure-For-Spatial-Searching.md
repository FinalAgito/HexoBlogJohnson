---
title: 'R and R*Tree(一):The Dynamic Structure For Spatial Searching'
date: 2016-11-01 21:56:55
categories:
- algorithm
tags:
- Mining Data
---
This article is not completed, I will add the demo codes to this article.
## 1.Spatial Searching
Before I start to talking about it, you may have to know something of two words: "Dimensional" and "Searching".

You always can hear a word called "Dimensional", we used it in every aspect of life, and we always need to solve some problem about it. Straight line belongs to one dimensional space, and the plane is two dimensional and a cube is three-dimensional.

And "Searching", If you are engaged in industries related to IT then you will not be unfamiliar with it, because we have mentioned so many, many times in our work and life. Searching for the information, the food's information, the place's information, the people's information, We have been searching for this all the time.

So, what's "Spatial Searching"?

Now we must post a question first: If our data is not one-dimensional(As we just said, an area, and other multi-dimentional data), how can we make the searching more efficiently?

That's must be interesting, and you not need to be feel confuse for this because we have give you a method to resolve this problem : R-tree, and its change version,R* tree .

In this article, I will introduce this amazing invention to you(We will pay more focus on R*tree). To describe and explain its structure, and after that I will use the programming language to implement it(I'm  familiar with c++, so I will use this).

I assume that you already have considerable programming knowledge. And I will make it easy to understand as much as possible.

## 2. R-tree
I would like to create a new figure to express what's the R-tree, so I want to use a picture of R-tree's bounding box(It has a more serious name: minimum bounding rectangle, I guess.) and a tree structure's figure to express the R-tree's feature.
![figure 2-0 The example of the R-tree's minimum bounding box](\images\Algorithm\RTree\RTreeBound.png)
In this picture, you can see the different Space division.
So, we can express the tree's structure as this one:
![figure 2-1 The R-Tree's Structure(In this figure, the m equal to 2, M equal to 3)](\images\Algorithm\RTree\RtreeStructure.jpg)
We can learn more about the r-tree's structure. Anytime when we have a new node insert in our tree, we should consider about which path can keep the tree's bounding box's area in a minimum value, then we will choose that place.

Now, I will list its features:
1. R-tree have two important value, we use m and M as trait of R-tree, each node（Except the root node） has child nodes from m to M. And the two values are depend on the situation.
If a leaf node is not a root, it should have a amount of records from m to M.
2. Each record belongs to a leaf node have a unified form, *(ex:[I, tumple identifier])* the *I* is a minimum bounding box on the n-dimentional space.
3. If a node isn't a leaf node or a root node, it musts have a range of child nodes from m to M.
4. A Not-Leaf node's structure,[I, child-pointer], the *I* a minimum bounding box which can include all the bounding boxes of its child-pointer.
5. If root node is not a leaf node, it must contain at least two nodes.
6. All the leaf nodes are on the same layer.

*The max value of R-tree's height is (|Log2 m^n| - 1), because each node has m nodes at least, and the biggest value of nodes is equal to |N/M|+|N/M^2|+....+1 , so if all the nodes of a R-tree have m child-pointers except root node, it's achieve the worst situation that when we excute this program's searching operation.*
If the tree's structure meets all the requirements above, we can call this structure "R-tree".
This Structure is very important in Database's application, when we want to find some exact spots in your country, or a more a bigger range(The earth?), your searching program would use lots of time.........(Just imagine you wait for five minutes to find a restaurant you are hungry.)

Now, we should Implement this tree sturcture by using the programming language(Matlab? Well, we can use matlab right? It's a very convenient tool to do the experiment,but I want you to better understand this knowledge, I'd like to use C++.)
![figure 2-2 A diagram of the contact between the classes](\images\Algorithm\RTree\RTreeProFigure.png)

If you don't mind......, I will follow this structure to write the program. First, let's look at its structure:

```
#pragma once
 //R Tree's definition
#include <iostream>
#include <vector>
using namespace std;
 //interval
class RTInter{
public:
	float IMax;  // lower bound
	float IMin;  // upper bound

};
// Use RTRange to define the Range of a Node,
// you can use it to describe high-dimensional rectangle.
typedef vector <RTInter>  RTRange;


//Tree's Node
class RTNode{

public:
	int type; // Node's type
	RTNode * Parent;        // Parent node
	RTRange Nrange;         // Node's area
	int childNum;           // children's number
	RTNode ** childSet;     // child node pointer
};
typedef vector <RTNode *> RTNodeSet;  //a set for all the Node
typedef vector <double  > RTPoint;    //use to record multidimensional point

class Tree{
public:
	int height;     // The height of the tree
	int dim;        // The dimention of the tree
	RTNode * Root;  // Root of the tree
	int m;          // The minimum number of nodes
	int M;          // The maximum number of nodes

public:
	Tree(void);
	~Tree(void);

};


```
Until now, we have given the R-tree's defination, but we didn't give the R*tree's structure.
Don't worry, because that's my decision. I will write the Rtree's program, and when you understand the basic program, I will tell you the part of R*tree.
But to be honest, That's must be a long article.... When I start to write this, I haven't to realize this situation....Just Joking. :)

## 3.Algorithm

Of course, the first operation is initialization, but I will start with a step that we all in common sence--------
### 3.1 Searching Algorithm
First, we will implement the searching algorithm, we use this to find the node in our searching area.
purpose: Find the nodes we want
When I try to describe these algorithm, you can see some different function in our code, some easy function I don't perpare to display because I can't make this article so long. :)
But I will give some interpretion.
Now, we begin, and we assume that the *T* represents the Root node, and the input parameter is S(the rectangle， if your R-tree is a structure with n-dimentional data, that's must be a region that difficult to imagine.)
1. If node T is not a leaf node, do the Searching in its child trees, find a EI intersect with the region S, and change the T to proto node's child node, until find a leaf node.
2. If node T is a leaf node, get the *TI*(The T's area.) and check if the EI' region include the *S*.

```
RTNode * Searching(RTNode * S_node,RTRange rect){
	if(S_node->childSet == NULL){
		if (Check(S_node->Nrange, rect)){

			return S_node;
		}
	}
	else{
		for(int i = 0;i < S_node->childNum - 1; i++)
		{
			Searching(S_node ->childSet[i], rect);
		}
		return 0;
	};

}

```
### 3.2 Insert Algorithm
purpose: Insert a new index E in the R-Tree
1. Call this function *Choose Leaf* to find a place P to insert the new item E
2. If P have the room(L not have M nodes) we will insert the E to P, but if P is filled with nodes, then we would call the *splitNode* function and get p and pp which have the whole nodes include E and the original entry P.
3. Call the funcition *AdjustTree* on L, if we have already split the L, we adjusted the LL, too.
4. If the node split caused the division of root node, the program will create a new root node which have two exist nodes.


### 3.3 Choose Leaf Algorithm

Then, we should find a place to store our new node.
We call the "Choose Leaf".

We called it "the Choose Leaf Algorithm", it not only consider for the initialization, but also  for the insert opreration.
We use this algorithm to find a leaf node to insert a new node.
Should we describe this algorithm by the natural language? Well, just for help you get more understand about this algorithm, it also can helpful to myself.
purpose: Find a leaf node to place a new item E
1. We set the root node is N.
2. If N is a leaf node, the function will add the new node E to N.
3. If N is not a leaf node, and the N has several pointers of index. We use F as a index in N, and if we want to add the E to the F's child-pointer, we should expend the area of F to include the area of E(Of course we should keep the minimum area.), then we caculate the new area of F(We called it FI.), but we couldn't to choose this 'F' by chosing randomly.
We will do this operation for all the child-pointers of N. And we can get the minimum area, and find a benefit child node of N, we use the x to express it.
4. And we do the loop operation from the '2', until we find the 'x' is a leaf node.

```
int ChooseLeaf(RTNode N_node, RTNode * S_node){
	double Area_t = 0; //create for store the area
	if(S_node->childSet == NULL){
		*(S_node->childSet)[0] = N_node; //as a new child node of N_node
	}
	else{
		for(int i = 0; i < S_node->childNum - 1 ;i++)
		{
			//add the new node's region in a child node, and calculate the new value of range
            //Area_t = addArea();

             //addnode();
		}
	}
	return 0;
}

```
### 3.4 Adjust Tree Algorithm

purpose: Change the "L" node to become the root node, this function can adjust the R-tree's structure.
1. We use the N as a signal of L, and if L has already spilt, we will use the NN to represent the LL.
2. If N is a root node, then we will stop this algorithm.
3. We use P to represent N's parent's node, and EN is the N's index in P's child-pointer. Adjusting the ENI to include all the nodes of N.
4. If N have already spilt, there must be a NN node in our sequence, if this happen, we will create a new node ENN(NN is it's parent node, we can use "Let ENNP points to NN" to express), and of course, the ENN's rectangle(ENNI) is enclosing to the all the rectangle of NNI. If P still has the enough space, add the ENN to the P's child-set, or use the *splitNode* to create the P, PP, ENN, and all the nodes of P.
5. Set N = P, if a split program cause the NN = PP, loop the step from the *2.* step.
To Be Continue........
I will see you in next article. :)