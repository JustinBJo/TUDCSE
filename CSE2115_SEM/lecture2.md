# Software Architecture

---

## Recap - Software Development Life Cycle
SDLC: process followed in SE for planning, designing, developing, testing, and deploying software projects
- Planning
- Analysis
  - Requirement Engineering
- Design
  - Software design + architecture
  - Design patterns
- Implementation
  - Design patterns
- Maintenance

## 1. Design
From requirements, to design, to the final product

> Software design is to process of defining the architecture components, interfaces, and other characteristics of a system or component <br>
> Software architecture is the product of the software design

### D,D,D
- Decompose the system into components
- Determine the relationship between components
- Determine each component functionality

Design is about decomposition: how we take a complex system and chop it up into pieces that we can build relatively independently.

### Approaches to Software Design
1. Top-down design
2. Bottom-up design
3. View-based design
4. Iterative and incremental design
5. Domain Driven Design (DDD)
6. Model-driven design


## 2. Architecture
> Software Architecture is how the components of a software system are organised and assembled, <BR>
> how they communicate with each other, <BR>
> and the constraints that rule the software

Changing the architecture can take a long time.

### Component diagram
Describes how components are connected with each other, along with the interfaces and dependencies.
- Boxes represent components
- The lollipop notation denotes the main interface of each component
  - the sockets (-c) denote the interfaces the component requires (input)
  - the lollipops (-o) denote the interfaces a given component provides (output)
- Ports 
  - In UML we can cluster balls and sockets into ports, which can be named. 
  - Ports can support uni-directional communication (only inputs or only output) or bi-directional communication (with both input and output)

Component Diagrams for Microservices
- <<*>>: Stereotype to indicate the type of component
- o-: API of the microservices
- -c: Interfaces required by the microservice


## 3. Architectural Patterns
> An architectural pattern is a general, reusable solution to a commonly occurring problem in software architecture within a given context. <BR>
> Architectural patterns describe the overall structure of the system.

Examples:
- Client/server
- Layered architectural patterns
- microservices

Classifications of architectural patterns
- Monolithic
  - Layered
- Service-based
  - microservices
  - service-oriented
- Distributed
  - event-driven

Quality attributes
- Performance
- Usability
- Maintainability
- Scalability
- ...

### 1. Client and Server
- The server hosts, delivers, and manages most of the resources and services to be consumed by the client
- Has one or more client computers connected to a central server over a network or internet connection


- The server does not know the number or identities of clients
- Clients know the server's identity
- Connectors are RPC-based network interaction protocols
  - RPC = remote procedure calls

- Disadvantages
  - Scalability

### 2. Layered Architectures
- Used for systems that can be decomposed into groups of layers, each of which is at a particular level of abstraction
- Each layer provides services to the next higher layer and consumers services from the lower layer

Example: Computer network, Operating system

Disadvantages:
- Higher complexity: additional abstraction increases overall complexity
- Lower performance

### 3. Model-View-Controller
- An architectural patterns that divides the application into three main layers: Model, View, Controller
- Often used in web development

### 4. Multi-Tier pattern
- Runtime structures are organised into logical groups (tier)
- These logical groups are allocated to specific physical components, such as a server of cloud computing

Difference with multi-layer: (logical division vs physical division)

### 5. Pipe-and Filter
- Provides a structure for systems that produce a stream of data
- Each processing step is encapsulated in a filter component while data is passed through pipes.


- Pipe: a connector, which transports data from one filter to next, preserving the order
- Filter: a component that reads data, transforms it, and return the transformed data

Example: ML pipelines, Unix shell commands with pipes(|)

### 6. Microservices
from last lecture