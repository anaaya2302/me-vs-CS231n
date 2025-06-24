# Image Classification Pipeline
## The Semantic gap
To understand the semantic gap, one must ponder the seemingly stupid question- How would you write an algorithm to identify a cat. One might sketch out a shape, but they deform, move, stretch and hide under furniture. No matter what you try to do, you will not be able to explicitly write a hardcoded algorithm for identifying a cat. Or any object for that matter.  

There are so many aspects subject to change. i.e illumination, deformity, occlusion, background clutter, inter-class variations( tabby or siamese ), etc. ( wtf even is a cat )  This is just in the real world... images are just matrices of RGB values — the cat isn’t in the pixels, it’s in our interpretation. <- On a side note, people TRIED to write explicit algorithms... I'm not joking ->  

Therefore, we must ditch this approach entirely. Here, we'll go through two elementary methods of classifying images.
## Nearest Neighbour Classifier
This is probably the simplest algorithm one might imagine. Memorise all the data, and for whatever image you must classify, compare it to ALL the images in your training data, then output the class of the closest match.  

Theoretically, if we had all the image data in the world as our training set, and infinite compute, this would be the perfect classifier. But we don't... so it ends up being slow and inefficient in practice.  

One might think about the possible classes as probability distributions and the image to be classified as the observation. Then, since we do not possess infinite data, we must guess which probability distribution the observation belongs to despite incomplete knowledge of the full underlying distribution.  

<- The Nearest Neighbour program is often wrongly attributed to a 1951 paper by Fix and Hodges. They came up with a method for guessing which probability distribution the observation belongs to given an observation. But, the term nearest neighbour and its application in a classification problem was first done by Cover and Hart in 1967 [^1]. They do mention Fix and Hodges approach in their introductory paragraphs, but do not build upon it. And that’s important — because knowing who did what helps us understand how the field actually progressed, not how it’s been summarized over time. ->

### Distance Metrics
Now, we must address what comparing two images even entails. How does one compare a matrix of RGB values with some way of capturing the intrinsic meaning. Turns out, one doesn't. We use rather silly algorithms for comparing two images. Or rather, calculating their distance. The higher the distance, the more different the images. 
- **L1 Distance**: The L1 distance or rather the Manhattan distance, involves subtracting pixel values. Pixel wise absolute difference.  
  	                                                <p align="center">d(I₁, I₂) = ∑|I₁ - I₂|</p>
  As one would realise, any similar looking image will be classified the same. If there are two images with a blue background having a white blob in the middle, both will be classified as one class, even if one blob is a dog and the other a toaster. 

- **L2 Distance**: The L2 or the Euclidean distance does the same thing... also measures pixel-wise differences, but squaring the differences gives more weight to large deviations, making it more sensitive to outliers and smoother.  
                                                  <p align="center"> d(I₁, I₂) = √( ∑(I₁ - I₂)² ) </p>
  If unfamiliar to vector geometry, Intuition can be built as follows- the Manhattan distance metric ensures you stick to the x and y axis... like a difference of the magnitude of the vectors. The Euclidean Distance would then be the hypotenuse between two perpendicular vectors ( Instead of in 2d, in some confounded dimensional space ). <br><br>


In this manner, a nearest neighbour classifier will compare the test image ( the image to be classified ), with all the images in the training data, and output the class of the image with which the distance is least.  

**K-Nearest Neighbour**: Takes a majority vote among K nearest neighbours. If all k nearest neighbours ( images with least distance ) have different classes, we either pick at random or choose the one with the lowest distance.
[^1]: Cover, T. M., & Hart, P. E. (1967). *Nearest Neighbor Pattern Classification*. [IEEE link](https://isl.stanford.edu/~cover/papers/transIT/0021cove.pdf)

