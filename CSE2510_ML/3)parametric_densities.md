# Parametric densities

---
## 0. Models
We do not have the true distributions but only the sampled dataset from them. In order to classify the objects and train the model,
we have to approximate p(y|x) or p(x|y),p(y). <br>
We will consider:
- Discriminative vs generative models
- Parametric vs non-parametric models

## 1. Discriminative models vs Generative models
1. Discriminative model
    - Discriminative model approximates p(y|x).
    - Discriminative model is good for modelling the differences of classes as it models the boundaries between classes.
    - When we know the posterior probability densities, we can directly classify objects.
    - Problem is: given measurements, e.g. person's height, how can we estimate p(woman|height)?
    - Strong approximations are needed.

2. Generative model
    - Generative model calculates p(y|x) by approximating p(x|y) and p(x).
    - Generative model modles the distribution of each class and learns the joint probability distribution (how likely it is to encounter the features in each class)
    - Given examples from different classes, 'standard' density estimation is sufficient.

## 2. Parametric vs Non-Parametric models
1. Parametric model
    - Parametric models use parameters (such as mean, covariance) to create the model
    - They assume simple global model and estimate its parameters
2. Non-Parametric model
   - They assume simple local model
   - They do not use parameters but use other methods such as distance.

First, we are going to focus on the parametric approaches

## 3. Curse of dimensionality
- Intuitively, using more features should give us more information about the outcome to predict
- But more features mean more parameter estimation
- Therefore, we need to find the optimal number of features we are going to work with.