+++
title = "Deep Margins"
date = 2018-09-17T10:46:56-05:00
draft = false

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["machine-learning", "research", "deep-learning"]

# Project summary to display on homepage.
summary = "Attempting to increase decision margins in neural networks through techniques similar to margin maximization in SVMs. Mentored by Prof. Nicholas Ruozzi, UTD."

# Optional image to display on homepage.
image_preview = "margins.png"

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Does the project detail page use source code highlighting?
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = ""
caption = ""

+++

_This was orginally a submission to an on-campus undergraduate research journal. I have modified the submission a bit, and posted it here since I have not heard back regarding my application._
### Introduction/Background
Recent developments in computer hardware have enabled a specific part of the computer, the Graphics Processing Unit (GPU), to accelerate developments within a subfield of artificial intelligence: machine learning. Specifically, GPU’s have enabled computers to quickly create accurate prediction systems known as “Neural networks” — previously a computationally infeasible task.

We begin our analysis of neural networks by examining them in the context of a classical machine learning classification task: differentiating between pictures of cats and dogs. We have a dataset of 10,000 images of cats and dogs. Every image in the dataset belongs to the set of classes `{cat, dog}`, and the neural network’s job is to accurately predict which class a given image belongs to.

The neural network’s life cycle is separated into two distinct phases: training and inference. Training is a process wherein the network is given large a quantity of labeled data, and self-modifies to improve its predictions. Inference is where we take such “trained” networks and perform classification on images they have never before seen.

A neural network comprises of thousands of nodes and weighted connections between these nodes that attempt to accurately predict an output given a certain input. At the beginning of the training process, the values of the nodes and connections are initialised randomly. The network is essentially guessing the output for a given input.

The network begins training by passing each of the 10,000 images of cats and dogs through itself. Since the network was pre-populated with random values, it starts off by guessing the class of each image at random. While doing this, it remembers what its guess was for each image. 
Once it has processed all 10,000 images, it compares its answers to the correct answers provided by a creator of the dataset. If the network marked down “cat” for an image that a human has determined was obviously a dog, it notes this for correction, adding it to its “computed error”.

Next, the network modifies the internal values of its nodes and connections in an attempt to minimize the computed error.  The network’s goal is to be able to classify all 10,000 images correctly as either “cat” or “dog”. The process is repeated thousands of times, thus “training” the network. Once the network can correctly predict every image that we have trained it on, the training phase ends.

In the inference stage, we present to the network images not previously seen in the training phase. Remarkably, it is able to classify them with a very high degree of accuracy - up to 95% or better. Why, after training, does the network give the correct answer when it is shown an image of a cat or dog it has never seen before? This is the so-called “generalization mystery” of neural networks.

### Simple Vector Machines
Simple Vector Machines (SVMs) are another tool in Machine Learning (ML) that attempt to learn a set of linear separators through a given dataset. While the inner workings of SVMs are not relevant to this research, they are unique in that they have a maximum margin guarantee, as seen in [Figure 1]. The “maximum margin” separator through a dataset, in general, is a good choice since it allows the most examples to fall within this “margin” and be correctly classified. 

To help build some intuition behind choosing a maximum margin, imagine that a new blue data point is to be inserted into [Figure 1]. Since it loosely belongs to the “blue” dataset, it is reasonable to assume that the new blue point will lie in close proximity to the existing blue points. Now, if a sub-optimal hyperplane was selected on the original dataset, closer to the blue points and not maximum margin, it would misclassify this plausible blue point [Figure 2].

![Figure 1](fig1.png)

### Methods
Now that the intuition behind margin maximization has been described, we may focus on designing a method to deliberately increase the decision margin for a neural network in a binary classification task. Currently, when training a network, there are no “margin guarantees”: the decision boundary may be close to or far from all data points, and we have no way of knowing. We cannot simply “check” what the margin of a neural network is because it is a large system of nodes and connections and not simply a function in a 2-dimensional space, as simplified in that diagram. 

One way to guarantee that the margin will increase in a neural network is to add new data points which the network will use to learn and then to classify correctly, as in the training phase of a network, the goal is to classify every image correctly.

As an aside, a point lies in 2-d space and an image resides in n-dimensional space. A point has a (x,y) coordinate, and since our images have dimensions 32 x 32 x 3, we can consider them as points in their n-dimensional space.

We can exploit this by giving the network some artificial that we have constructed to learn from. Specifically, we would like to generate fake data points in an n-sphere around every data point that we have, so that our network decision boundary will be pushed out by the radius of that sphere. As shown in [Figure 3], by creating a set of fake data points around the real data, the decision boundary has no choice but to move outward so that it may classify all points correctly during its training phase.

We can generate these fake data points uniformly and systematically by sampling randomly from everywhere within an n-sphere of radius r around a given data point. Programmatically, we do this as follows:

Generate a matrix of the same dimensions as our image. I.E. if our image is a 32 x 32 x 3 image of a cat (32 by 32 pixels, and 3 color planes: red, green and blue), we generate a random image of the same size.
Populate that matrix with random values.
Normalize the image. In linear algebra, when we wish to obtain a vector pointing in the same direction as another vector but with length 1, we divide each element in the vector by its total magnitude. We can do the same for each image, taking an element-wise magnitude division, so that the “length” of the random matrix is 1.
Now that we have a random point in the same data space as our original image (for example, an image of a cat), we multiply this random point by a random value m, where 0 <= m <= r, where r is the radius of the sphere within which we would like to generate points. It is important to make sure m is uniformly distributed within the sphere, and not only on the boundary, by drawing m from within a range of values less than r.
Finally, we take our new image g = m*[random matrix] and add it to our original image using matrix addition. This “localizes” g to the dataspace of our image, not unlike how we move a vector around a 2d-space by adding it to another vector [Figure 4 CREATE THIS].

We now have a method of generating data points within an n-sphere of radius r of a single image.  For each image in our dataset, we then generate 20 random points within some radius r.
	How do we choose a suitable radius for our n-sphere? Consider the two closest points from opposing classes within data space. That is, the pair of (dog,cat) images that have the least distance between them by a n-dimensional euclidean distance metric.
Similar to how we can use the distance formula in two dimensions to compute the planar distance between two points, we can generalize the distance formula to n-dimensions, and use it to calculate the distance between any pair of images. We can write a programming script to calculate this n-dimensional distance and find the closest pair of images. 
	The maximum value that our final network margin can be is then half of the distance between the closest pair of opposing class points [Figure 5]. As an example, if  the distance between them was calculated as 369,  we begin by setting our radius r to 184.

Previous Work
Previous papers regarding a maximum margin guarantee rely on the construction of an “objective function” which rewards maximized margins. Instead, our work relies on providing a true guarantee of this margin by forcing the network to fit it with fake data.


Results
	As a control set, we teach a separate network using only native, ungenerated data, with a dataset of 10,000 cat and dog images. Using a model described in [1], we are able to achieve ~73% accuracy on a set of data we withhold from the network during training, called the “validation set”. Results on the validation set truly reflect how well a network is performing, because the network has not seen any images from it before.
	We then generate our 20 random images per image in our original dataset, at a radius value of r=184. The more images we generate per original image, the greater probability guarantee of learning an expanded margin.
	Initially, our data looks promising. However, it is important to note that to begin training a neural network we need to initialize all parameters randomly. This means that two instances of training a network will yield different results since we start at different points along a non-guaranteed optimization process. This process has no guarantee of converging to a “good” result. To combat this, we take the average highest validation score of 10 runs to compare against each other, the results of which are listed in [Figure 6].
	Our top validation accuracy average for training on an augmented dataset does not show a significant improvement over training on the original dataset. We look for a new direction to move towards for image generation.
By inspecting our list of pairs of euclidean distances, we discover that 99% of our distances between points belonging to opposing classes are, in fact, near the value of 568. Hence, we do more training runs, but this time with the radius value of r=284 [Figure 6].
	The results indicate that this method of attempting to improve generalization is not effective. Although there is no way to compute the true “uncertainty” of our results and to measure whether our result is truly improving or degrading final accuracy, we can estimate this uncertainty to be around 2-3%. That is, if we were to increase our accuracy by 4% or more over a 10 run average, this would hold as a “significant result”.

Conclusion
	The “margin maximization” method of attempting to improve neural network accuracy has proven, in this case, to be unsuccessful. Currently, we are working on numerous other methods in an attempt to provide a “generalization guarantee” during the training of a network. The development of a generalization guarantee would be important because no such guarantee currently exists for neural networks, and it is still a mystery as to why they perform well on unseen data.
	
