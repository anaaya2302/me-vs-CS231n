# Image Classification Pipeline
## The Semantic gap
To understand the semantic gap, one must ponder the seemingly stupid question- How would you write an algorithm to identify a cat. Well one might sketch out a shape, but they deform, move, stretch and hide under furniture. No matter
what you try to do, you will not be able to explicitly write a hardcoded algorithm for identifying a cat. Or any object for that matter.<br>
There are so many aspects subject
to change. i.e illumination, deformity, occlusion, background clutter, inter-class variations( tabby or siamese ), etc. ( wtf even is a cat )  
This is just in the real world... images are just matrices of RGB values — the cat isn’t in the pixels, it’s in our interpretation. <- On a side note, people TRIED to write explicit algorithms... I'm not joking ->  
Therefore, we must ditch this approach entirely. Here, We'll go through two elementary methods of classifying images.
