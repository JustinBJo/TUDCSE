# Formalising Negotiations

Contents
- Domain Model
- Preferences
- Utility functions
- Negotiation analysis

Recap
- Why negotiate?
    - Joint decision needed
    - Hidden information
    - Cannot be decided otherwise
- Principles for human negotiators
- Phases of negotiation
- Definisions
- Styles: negotiation & conflict handling


## 1. Domain Modelling
### Domain
Validity and Added value
- The added value of using artificial intelligence techniques highly depends on the quality/validity of the model:
    - Weak model -> weak support by the technique
    - Faulty model -> faulty advice

Transparency
- Model should be transparent for the user of technique
    - Trust
    - Understanding the advice

### Domain Model
For the negotiations we do, we need:
- A set of issues (attributes) X
- A set of values for each of those issue V(x) where x ε X
- A Preference profile for each stakeholder

If repeated negotiations in a domain:
- apply ML to build and extend the domain and cluster preferences to a set of preferences that occur most

Learn from other negotiating agents by sharing anonymised negotiation logs


## 2. Preferences
Given:
- a finite set of issues X
- i and j ε X
- sets of value for each of those issues: V(i), V(j)

Stakeholders have preferences over the values per issue and over combinations (bids) of values for a range of issues
- This is expressed by a preference relation <_p
- Suppose a, b, c, d ε V(i), for some issue i
    - a <_p b expresses that the stakeholder prefers b over a
    - (a, c) <_p (b, d) expresses that the combination (b, d) is preferred over (a, c)

### Preference Independence
A set of attributes Y ⊂ X is preferentially independent of its complement X-Y when the preference order over outcomes with varying values of attributes in Y does not change when the attributes of X-Y are fixed to any value

Independence allows for linear additive utility functions

