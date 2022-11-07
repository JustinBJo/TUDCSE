# The Ultimate Cheat Sheet

---

## 0. Probability and Bayes Rule

### Bayes' Rule
$ p(y|x) = \frac{p(x)}{p(x|y)p(y)} $
- p(y) = class prior
- p(x|y) = class conditional pdf
  - usually modelled by Gaussian distribution
- p(x) = unconditional probability

### Classification error
$p(error) = \sum_{i=1}^{C} p(error|w_i)p(w_i)$

### Bayes' error
- Minimum attainable error
- Typically larger than 0
- Cannot obtain them because we do not know the true distribution
- Bayes' error depends on distribution, not classifcation rule


## 1. Generative models
Generative model calculates p(y|x) y approximating p(x|y) and p(x)

### A. Parametric models
Parametric models depend on Gaussian distribution.<br>
![2510img/img_4.png](2510img/img_4.png)<br>
![2510img/img_5.png](2510img/img_5.png)<br>
μ = mean, σ^2 = variance, Σ = covariance matrix.

Mean can be approximated as:<br>
![2510img/img_6.png](2510img/img_6.png)

Covariance matrix can be approximated as:<br>
![2510img/img_7.png](2510img/img_7.png)

#### QDA
- Given by ln(p(x|yi)p(yi)) - ln(p(x|yj)p(yj))
- f(x) = wTWx + wTx + w0
  - W = 1/2 (Σ_2^-1 - Σ_1^-1)
- Separate covariance matrix
- High variance - Low bias

#### LDA
- Assuming that all covariance matrices are equal.
- f(x) = wTx + w0
- Low variance - High bias

#### Nearest mean classifier
- Assuming that all covariance matrices are identity matrix and all features are uncorrelated
- Uses distance to the mean of each class => Sensitive to feature scaling
- Normalisation needed: one method is zero-mean unit-variance (~x = (x-μ)/σ)
- Low variance - High bias

### B. Non-parametric models

#### Parzen/Kernel density function
1. Place cells around data points
2. Define the cell shape (box, tri, triweight, Gaussian)
3. Fix the size of the cell (h)
4. Add contributions of cells

![2510img/img_17.png](2510img/img_17.png)<br>

Depending on the size of h, the model can be underfitting(too large h) or overfitting(too small h)

#### K-nearest neighbours
1. Locate the cell on the new point x
2. Increase the cell volume until it covers k objects
3. Predict class y

p(x|yi) = ki / niVk (Vk)<br>
p(yi) = ni/n

- We could use different distances
- Choose k wisely
- Resolving tie algorithm
- Good because no explicit training is needed
- Sensitive to feature scaling

#### Naive Bayes
p(x|yi) = p(x1|yi) p(x2|yi) ... p(xd|yi)<br>
class conditional pdf is calculated by multiplying all the feature values.

- We assume that all the data are independent
- It can handle high dimensional feature space
- Training time is fast
- Missing values can be ignored
- Easily fooled
- Zero frequency problem: never allow zero probabilities


## 2. Discriminative models
Discriminative models directly approximates p(y|x).

Empirical risk minimisation
- for joint probability, we can construct the classifier using empirical risk minimisation
- min 1/N * Σ(i=1, N) L(h(xi),yi)
  - h: hypothesis function
  - L: loss/cost function

Different measures of loss function:
- Regression: linear regression
- Classification: logistic regression, support vector machine

### A. Linear classifiers

#### Linear regression
Comparing the outcome of our hypothesis function and the actual label
- Absolute difference
- Squared difference (can penalise large differences)

min 1/N Σ(i=1, N) (xiTw + w0 - yi)^2 = min _w,w0 J(w,w0)

We can find the best w and w0 using gradient descent.

##### Gradient descent
Follow the derivative until we hit a local minimum.
1. Take the derivative of the loss function in terms of both w and w0
2. Pick random values for parameters
3. Plug the parameter values into derivatives
4. Calculate the step sizes: StepSize = Slope * Learning Rate
5. Calculate the new parameters:
   - New parameter = old parameter - step size
6. Repeat from step 3 and repeat until
   - Step size is smaller than the minimum step size
   - or you reach the maximum number of steps

Learning rate is the speed of descent: too high can lead to overshooting; too small can lead to slow performance

Initial parameter important because it decides if we reach local or global minimum

Stochastic gradient descent updates parameters on each iteration

Linear regression has low variance and high bias

#### Logistic regression
Use logistic function σ(x) = 1/(1+e^-x)

Maximum likelihood function:<br>
![img.png](2510img/imag.png)<br>

Equivalent to negative log likelihood, which is the cost function:<br>
![img_1.png](2510img/imag_1.png)<br>

Do gradient descent to find optimal parameters

Low variance and high bias

#### Support Vector Machine
Maximise the margin
- margin: the distance between the classification boundary and the closest objects
- support vectors: objects on the margin

The decision boundary is defined by wx - b = 0<br>
The offset from the boundary to the support vectors is given by b/||w||<br>
We maximise b/||w||, or minimise ||w||

Hinge loss used for violations (max(1-y h(x), 0))

Low variance and high bias

#### Multiclass Classification
1. Directly construct a multi-class classifier
2. Combine multiple binary classifiers
   - One vs rest: k-1 binary classifiers that discriminates each class from all others
   - One vs one: k(k-1)/2 binary classifiers that discriminates between all pairs of classes 


### B. Non-linear classifiers

#### Decision Trees
1. Make partitions in the feature space
2. Assign values to each part
   - If all objects in a node belong to one class: we are done
   - If not, find a node-variable combination that increases the quality of the tree the most after splitting
     - Measure of improvement
       - Information gain
         - ![2510img/img_24.png](2510img/img_24.png)
         - I: impurity
           - Misclassification (1 - max_c(p_c))
           - Entropy: -Σ p_c * log(p_c)
           - Gini index: Σ p_c * (1 - p_c)
         - S: set of objects in the node
         - F: feature that we consider
         - S_V: Number of objects in the node with value V
       - Gain ratio
         - Because information gain is biased towards features with many discrete values, we use gain ratio to avoid overfitting
         - ![2510img/img_29.png](2510img/img_29.png)
3. When to stop training
   - minimum node size
   - minimum gain
   - max depth
   - Pruning (subtree replacement pruning)
     - For each node we pretend to remove the node and all its children and measure performance on the validation set
     - Remove node that result in the greatest improvement
     - Repeat until further pruning is harmful

Insensitive to feature scaling

#### Classifier combining
Combining different classifiers can lead to improvement in overall performance by exploiting classifiers' strengths.

Combining strategies
- Fixed rules
  - Hard rules e.g. majority voting
  - Soft rules e.g. mean, product
- Learned rules
  - Learn a classifier to output a decision based on the outputs of a set of base classifiers

What to combine
- Randomly selecting samples: bagging
- Randomly selecting features: random subspaces

Random forest: construct a large number of trees using randomly selected objects and features and combine their decisions

It is flexible and has low bias. It also works for many different types of data

#### Multilayer Perceptron
A perceptron has:
- input unit xi
- bias x0
- connection weight wi
- output unit y

Then the final output is calculated by putting y into the activation function.

Layers in multilayer perceptron:
1. input layer
2. hidden layer
3. output layer

Perceptron training
1. Forward-pass
   - Process of perceptron training by passing on the result of the activation function of the previous layer to the next layer's activation function
   - We initialise the weights with a random value, but this is not sufficient. We therefore apply gradient descent on the output value to find the optimal weights.
   - This means we need to move backward: backpropagation
2. Backpropagation
   1. Output value of forward pass is compared to the label
   2. Calculate error using a loss function
   3. Error is propagated back through the network, layer by layer:
      - Update weights depending on how much they contributed to the error, thus trying to find the weights that minimise the loss function:
        - Calculate the gradients of the error function with respect to each weight
        - The gradient vector indicates the direction of the highest increase in a function, while we want the highest decrease
   
    The iterative updating of the weights can be done as follows:
   1. Recalculate the gradients at the beginning of each training iteration step
   2. Stop when error < θ or if we are at the max number of iterations
   3. The general to update weights is as follows :w_t <- w_(t-1) - α(δΕ/δw), where
      - α is the learning rate
      - δΕ/δw are partial derivatives of the error function E with respect to each weight of the array w