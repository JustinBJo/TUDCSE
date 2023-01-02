# Introduction to Data Mining

---

## What is Data Mining?
- Examining a large database to generate new information
- Development of models for data in order to extract information
- Process of analysing data from different perspectives and summarising it into useful information
- Done by humans


Data mining differs from ML; they have similar pipelines, but ML focuses more on fitting a classifier and applying algorithm,
where DM focuses more on the train and test data and the output.

Designing the learning algorithm is not part of data mining.

## Bonferroni's Principle
Events will be found in the data, even if the data is completely random.<br>
These events are to be avoided as they are false positives.

In statistics, we correct for this using a technique called *Bonferroni correction*.<br>
A simpler version of this idea is called Bonferroni's Principle.

1. Compute the expected number of occurrences of the event in random data
2. If this number is larger than the number of events you expect to see, you will likely only find bogus events
   - For instance, we can only detect terrorists by looking for "very rare" events
   - very rare means extremely unlikely to occur in random data