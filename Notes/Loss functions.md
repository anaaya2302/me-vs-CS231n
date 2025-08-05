# Cost Function
A cost function is a measure of how bad your model is. It is the metaphorical distance of the actual prediction from the desired prediction. A higher cost corresponds to a worse model.  

The general form of a cost function given a dataset {(xᵢ, yᵢ)} i=1, N:  

$$ C = \frac{1}{N} \sum_{i=1}^{N} L_i(f(x_i, W), y_i) $$  

where f(x_i, W), is the model's prediciton (logit), yᵢ is the true prediction (label), and Lᵢ is the loss function.  

The cost is the average loss. For each training example, we'll calculate the loss using a loss function, and the average of all those losses is the cost.

<- The terms logit and label are relevant only to classification problems. And I'll talk about all the loss functions with respect to classification problems. ->
## Hinge loss
This is a loss function. It's really simple but works pretty well.  
So if your model is really good, it will output a really high score for the correct class and really low ones for the incorrect classes. A hinge loss iterates over each incorrect class and sums up the output. For each iteration, it compares the score of the incorrect class with the incorrect class. If the score of the correct class is greater than that of the incorrect class by atleast one, it outputs zero. If not, it outputs the score of the incorrect class - the correct class + 1. 1 is basically your safety margin. It'll work even without the 1. 

$$
L_i = \sum_{j \neq y_i} 
\begin{cases}
0 & \text{if }  s_{y_i} >  s_j + 1\\
s_j - s_{y_i} + 1 & \text{otherwise}
\end{cases}
$$

where sⱼ is the incorrrect class and sᵧᵢ is the correct class.  

This can also be thought of as a max function:  

$$
L_i = \sum_{j \neq y_i} \max(0, s_j - s_{y_i} + 1)
$$

This works the same because if the score of the correct class is lesser than the incorrect class, you get a negative number. But, since the minimum possible value of the max is 0, it turns out to be the exact same thing.

<- Even if you sum up over the correct class, it just shifts the loss up by 1, causing no real change. ->   

<- This is also known as SVM (Support Vector Machine) loss because this is the particular loss function an SVM tries to minimize. A Linear SVM is basically a linear classifier, though the same cannot be said for a non-linear SVM. ->   

<- You should stare at it for a while. You should also test a few random examples to really get a feel for it. ->  

## Negative Log Likelihood Loss
**Softmax function**: A function which converts raw logits to probabilites. It does this by first exponentiating and then normalising.   
A softmax function for one particular logit is as follows:  

$$
p(y = i \mid x) = \frac{e^{z_i}}{\sum_{j=1}^{K} e^{z_j}}
$$  

The numerator represents the current logit, and the denominator is the total sum. Therefore, this returns probabilites.  
We exponentiate to make the difference between logits more pronounced.  
<- why e then? why not just 2? That's because it'll be useful when later, we calculate the derivatives. (the derivative of eˣ is eˣ) -> 


**Negative Log Likelihood Loss**  
The goal of a loss function is to evaluate the likelihood that our model distributes the data the same as the true model. With a high likelihood returning a low loss and vice versa.  

<- Note that we do not know the true underlying dataset of all the images of the classes that we have. Also note that likelihood and probability are not the same thing. Likelihood is the chance of an underlying model given a set of observations, and probability is the chance of getting a certain observation after an experiment, given a model. ->

The likelihood of the parameters θ given data (𝑥,𝑦) is equal to the probability assigned to the true label by the model under θ.  
                                                            <p align='center'> OR </p>
The chance of our model being correct is equal to the probability of the true label which the model predicts.  

$$
\mathcal{L}(\theta) = p_\theta(y \mid x)
$$  

(this is the core concept behind maximum likelihood estimation)  
<- If the probability of the correct class is really high, Then the likelihood that our model is on point is also really high. Also, we use probabilites because if the probability of the correct class is really high, then the probability of the other classes has to be really low. The same cannot be said for raw logits-> 

Okay, so a better model gives a higher likelihood. But, the loss should be less for a better model. Umm, you could just slap on a negative sign to make big values small. But loss by definiton has to be positive. (0 loss means that the model has no error, so negative loss would mean better less error than none... it doesn't make any sense)  
So, we use the natural logarithm. Hypothetically, if softmax output one as the probability of the correct class as 1, the loss would then be 0. (This would need the raw logit for the correct class to be positive infinity and the logits of the wrong classes to be negative infinity but let's continue for the sake of discussion). If the probability of the correct class was 0.9, the loss would be -0.105, and if it were 0.01, it would be -4.605.   

But wait, that's still negative... So now finally, we add a negative sign to make it make sense. The higher the likelihood, the lower the loss. Et Voila, Negative log likelihood loss.  

$$
\mathcal{L}(\theta) = -\ln p_\theta(y \mid x)
$$


<- One thing I thought was why not just do 1 - probability? That would mean the loss at 0.9 would be 0.1 (low) and the loss at 0.01 would be 0.99 (high). But even this ends up being worse. Firstly, wrong predictions aren't really penalised, and the gradient is not "clean". I'll experiment with this loss in a file and show why it sucks. ->





