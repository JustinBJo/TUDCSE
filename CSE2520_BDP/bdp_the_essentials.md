BDP - The Ultimate Cheat Sheet
===

# 0. Introduction to Big Data
> Big data are data too large to be efficiently processed on a single computer,<br>
> or massive amounts of diverse, unstructured data produced by high-performance applications

## Many V's
- Volume: large amount of data
- Variety: data comes in various forms and sources
- Velocity: the content is changing quickly

## Processing
The ETL cycle:
- Extract: convert raw or semi-structured data into structured data
- Transform: covert units, join data sources, cleanup etc
- Load: load the data into another system for further processing

Big data engineering: concerned with building pipelines
Big data analysis: concerned with discovering patterns

Types of processing:
- Batch processing
- Stream processing


# 1. Programming for Big Data

## 1. Data types
- Unstructured: data formats not known (txt, html)
- Semi-structured: known format (json, csv, xml)
- Structured: known format, linked together in graphs or tables (SQL or Graph DBs)


1. Sequences/Lists
2. Sets
3. Maps or Dictionaries
4. Nested data type: Graph
   - Nodes and Edges
   - Represented as Map[Node, List[Edge]]
5. nested data type: Tree
6. Tuples
7. Relations
8. K/V pairs

## 2. Functional programming
1. No side effects
2. Immutable data structures
3. Higher order functions
4. Laziness

[Function signatures](2.programming_for_bd.md#Functions and signatures)


# 3. Unix
> A true multiuser operating system<br>
> Users have their own private space on the machine's hard disk and are identified by an id number

## 1. Filesystem
Permissions: Owner - Group - Other
- r: read(4)
- w: write(2)
- x: execute(1)

## 2. Pipe
> Pipes combine commands<br>
> Pipes forward a program's STDOUT line-by-line to the input of another program<br>

## 3. Commands
[link](3.unix.md#3-commands)


