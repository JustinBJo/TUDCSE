# Bias and Fairness

---
## 1. What is Bias?

### Bias
> Preference or inclination for or against something. <br>
> Often accompanied by a tendency to ignore the merits of relevant alternatives or others points of view.

#### Implicit Bias
> Expectations based on learned coincidences, which unknowingly affect everyday perceptions, judgement, memory, and behaviour. <br>
> An implicit bias may lead to discrimination.
#### Explicit Bias
> The explicit bias is informed by our implicit bias but is also at least in part a conscious choice.<br>
> For example, walking on the other side of the street when you see a scary-looking person(implicit bias).

### Prejudice
> An assumption made without adequate knowledge.<br>
> It is most commonly used to refer to a preconceived judgement toward a person or a group of people because of a personal or specific characteristic.

Prejudice is usually resistant to rational influence.

### Discrimination
> Actions taken based on a prejudice. <br>
> For example treating a person or group of persons based solely on their membership of a certain group or category.

### Proxy Bias
> Proxy variable: a variable that is related to a variable of interest to the degree that it can operate as a substitute.<br>
> A proxy bias is a bias by way of a proxy variable

For example, in the US, zipcodes are proxies for crime, income, ethnicity etc.

## 2. Bias in ML
AI systems or ML techniques are not inherently "bad" nor turn "bad" by themselves; an important source for bias is the training set.<br>
This can happen because some features might seem correlated, even though they aren't, thus leading to incorrect (biased) conclusions.<br>

Other sources could be:
- Lack of diversity in ML developers
- Implicit human biases in our culture
- Evil programmers

### Fairness
> The absence of bias or discrimination on specific realms.

There are three ways of quantifying fairness in ML:
1. Data vs Model
   - Fairness can be measured at different stages in a machine learning pipeline. Specifically, fairness can be quantified in the training dataset or in the learned model of a machine learning solution.
2. Individual vs Group
   - Individual fairness: in its broadest sense, seeks for similar individuals to be treated similarly.
   - Group fairness: in its broadest sense, partitions a population into groups defined by protected attributes and seeks for some statistical measure to be equal across groups.
3. WAE vs WYSIWIG
   - WAE (we are all equal): defines fairness as an equal distribution of skills and opportunities among the participants in a machine learning task
   - WYSIWIG (what you see is what you get): observations reflect ability with respect to the task
   - Example: using SAT scores as future success
     - WAE: SAT score could contain structural bias and distribution in scores is not the same is distribution in ability
     - WYSIWIG: it correlates well with the future success and can be used correctly for prediction

### Debiasing
To debias the three previously mentioned measurements, we can do the following:
- Data vs Model
  - Check the distribution of class labels in training set. If there are more examples in group A than in B, equalize the distribution in the training set
- Individual vs Group
  - Individual fairness: 2 individuals on either side of the line are very similar but different outcome
  - Group fairness: be aware of correlations of variables with other variables that the algorithm uses, e.g. surnames with geographical census data
- WAE vs WYSIWIG
  - Can be debiased by a smart implementation of the algorithm