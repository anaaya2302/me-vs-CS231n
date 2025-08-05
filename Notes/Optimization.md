# The Problem  
For any model, there will be an ideal set of parameters, which will yield the lowest loss. Those are the parameters we want the model to have. Okay but how do you figure out which parameters those are, out of inifinitely many possbile weights and biases. 

Well... you could just guess randomly until it works... but you'd have better luck winning the lottery five times in a row.  

# Gradient Descent
Assume a model with only one variable subject to change. For a certain value of this variable, the loss is at its absoulte lowest possible value (global minimum). But, you don't know where this is... all you know is your current loss. 
<p align="center"> <img src="diagrams/2d loss lanscape.jpg" alt="Classifier diagram" width="70%"/> </p> 



