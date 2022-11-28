# Introduction to Software Engineering

## What is Software Engineering?
Three critical differences between programming and software engineering:
1. Time and Change
   - "What is the life span of your code?"
   - We aim to write sustainable code that can be easily changed and adapted over time
2. Scale and Growth
   - "How many people are involved software?"
   - Programming is an act of individual creation
   - Software engineering is a team effort
3. Trade-offs and Costs
   - There is no single solution that works in all contexts
   - We need to consider the different trade-offs

## Software Development Life Cycle (SDLC)
> Process followed in SE for planning, designing, developing, testing, and deploying software projects

Usually follows steps along the lines of:
- Analysis
- Design
- Implementation
- Maintenance
- Planning

There are different SDLC models
- Waterfall
- Spiral
- V-model
- Agile
- Scrum

The analysis step is understanding the problem domain and what the system should do.<BR>
This process is called requirement engineering.

## Requirement engineering
> A requirement is a statement about one feature (or constraint) of the system we are going to develop

A requirement can be expressed in three main ways:
1. Natural language requirements
2. Model-based requirements
   - Graphs (e.g. UML diagrams)
   - Formulas
   - Pseudo-code
3. Artifacts-based requirements

### Requirement Elicitation
A stakeholder is a person or organisation who influences a system's requirements or who is impacted by that system

Elicitation Techniques:
- Survey
  - Interviews
  - Questionnaires
- Creativity
  - Brainstorming
  - Change of perspective
- Document-centric
  - System archaeology
  - Perspective-based reading
- Observation
  - Field observation
  - Apprenticing
- Support
  - Mind mapping
  - Workshops
  - Audio and video recordings
  - Prototypes

### Functional vs Non-Functional requirements
Functional requirements
- Describe what services the system should provide and how the system should react to particular inputs
- May also include what the system should not do

Non-functional requirements
- Constraints on the services or functions offered by the system
- Include timing constraints, constraints on the development process, and constraints imposed by standards

We have three types of non-functional requirements:
1. Product requirements
   - Specify that the product must behave in a particular way.
   - Example: performance requirements on how fast the system must execute
2. Organisational requirements
   - Broad system requirements derived from policies and procedures in the customer's and developer's organisation
   - Examples: process standards used, programming language, operating system
3. External requirements
   - Arise from factors which are external to the system and its development process

### Requirement analysis process
1. Identify the stakeholders and use elicitation techniques to find requirements
2. Classify the requirements in function and non-functional requirements
3. Make an agreement on the priorities for the requirements (MoSCoW method)
4. Output: the requirement specification document
