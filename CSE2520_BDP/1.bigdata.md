# Introduction to Big Data

---
> Big data are data too large to be efficiently processed on a single computer
> <br>or massive amounts of diverse, unstructured data produced by high-performance application.
> 

## 1. Many V's
- Volume: large amounts of data
- Variety: data comes in various forms from diverse sources
- Velocity: the content is changing quickly

## 2. Processing
Big data is processed by the ETL cycle:
- Extract: covert raw or semi-structured data into structured data
- Transform: covert units, join data sources, cleanup etc.
- Load: load the data into another system for further processing.

### Big data engineering vs analysis
- Big data engineering
  - concerned with building pipelines
- Big data analysis
  - concerned with discovering patterns

### Types of processing
- Batch processing
  - all data exists in some data store
  - a program processes the whole dataset at once
- Stream processing
  - processing of data as they arrive to the system

### Desired properties of a big data processing system
- Robustness and fault-tolerance
- Low latency (in reads and updates)
- Scalability
- Generalisation
- Extensibility
- Ad hoc queries
- Minimal maintenance
- Debuggability

### When to use big data
- Modelling: what factors influence particular outcomes/behaviours?
- Information retrieval: finding needles in haystacks(search engines)
- Collaborative filtering: recommending items based on items other users with similar tastes have chosen
- Outlier detection: discovering outstanding transactions