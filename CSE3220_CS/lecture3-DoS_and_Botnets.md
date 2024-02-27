# Denial of Service and Botnets

Contents
- Denial of Service attacks
    - Volumetric attacks
    - Protocol attacks
- Botnets

L.O.
- Understand different types of (D)DoS attacks
- Explain the imbalance in costs for the attacker and defender
- Describe how a botnet works
- Evaluate why botnets are hard to take down

## 1. Denial of Service
> Attacks on Availability

Availability can be attacked on every layer of the OSI model

### What is a DoS attack?
- DoS attack overwhelms a target system with a flood of traffic, rendering it unavailable to users

### Types of DoS attacks
- Volumetric attacks
- Protocol attacks
- Application layer attacks

#### Volumetric attacks
> Overwhelm victims with a high volume of traffic

Amplification attack
- Requirements:
    - A server that provides large responses on small queries
    - IP spoofing
- Can be done with many protocols, commonly over UDP
- A popular protocol is DNS using IP spoofing

#### Protocol attacks
> Exploit vulnerabilities in network protocols

- Draining resources of a system until it does not function
- Targets the network and transport layer

TCP SYN Flood
- Attacker sends spoofed SYN packet to the target
- The target sends SYN-ACK to the spoofed IP, which did not send SYN
- The target waits for ACK but does not receives it. This is repeated many times until the target runs out of memory

#### Application layer attacks
> Target specific applications to exhaust resources

- Focuses on the application and services provided to end-users
- Hard to be identified as malicious traffic because it looks like a normal user traffic

HTTP Flood
- The attacker requests many pages, images, and/or other (large) files from a website at once
- As the attacker must complete the TCP handshake to do this, the attack cannot be spoofed


### DDoS Mitigation
- Redundant network infrastructures
    - ensures that a single point of failure cannot bring down the entire system
- Traffic filtering
    - aims to identify malicious packets and block them
- Content Delivery Networks
    - distribute and cache content over a large network, which can absorb and mitigate the DDoS traffic by serving content from distributed servers
- Web Application Firewalls
    - can protect against application layer attacks by identifying malicious traffic



## 2. Botnets
> A network of compromised computers (bots) that are under the control of a single entity, usually a malicious actor

Purpose: for various malicious activities, including DDoS attacks, spreading malware, and stealing information

### Architecture of a botnet
- Infected devices (bots)
    - can be any device: IoT, PC, Phones, ...
- Command and control (C2 or C&C) infrastructure
    - the bots receive commands through the C2 infrastructure
- Communication channels
    - many protocols/methods are used: IRC, HTTP, P2P, Blockchain
    
### Mitigating botnets
- Securing many devices to make harder to compromise a large number of devices
- Taking down C2 infrastructure
- Blocklisting devices that are infected by a botnet so that owners clean them

### Strategies of attackers to go around these
#### Domain Generation Algorithm (DGA)
- A static domain name or IP address can be blocked
- Malware authors generate many domain names and only have to register one

#### Peer to peer architecture
- Using the bots as C2 channel can solve the issue of C2 server being taken down

#### Sending the C2 location through the blockchain
- Ensures complete control over the C2 channel, and is changeable at any moment
- Decentralised by design
- Blockchain will not be taken down