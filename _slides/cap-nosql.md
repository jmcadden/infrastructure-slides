---
title: Cap Conjecture & NoSQL databases 
---

# CAP Theorem 
### CAS CS451/651 Spring 2016

Speaker: Jim Cadden

---
### Today:

- Overview key concepts of CAP
- Differentiate 'conjecture' and the 'theorem' 
- Highlight where CAP does/does-not apply
- Discuss underlying consistency trade-offs 

---

# Context for "CAP" 

==

## Distributed applications

Modern distributed applications and services, deployed in-or-across large datacenters or in "cloud" infrastructures.

==

## Fault-tolerant distributed applications 

Microsoft datacenters 46 failures per-day

==

## Latency-critical, fault tolerant distributed applications

Low-latency: Yahoo! PNUTs latency budget >100ms (Theoretical Global RTT: 133.7ms)

==

## "Always on", latency-critical, fault tolerant distributed applications

Availability: 99.99% system availability results in 1 hour downtime per year 


==

## Large-scale, "always on", latency-critical, fault tolerant distributed applications

Facebook RockDB reports 9 billion request-per-second 

==

### Large-scale,
### "always on",
### latency-critical,
### fault tolerant
### distributed applications

---

# What is this "CAP" thing? 

==

## What is CAP?

- "CAP" describes an impossibility result 

- Applicable with data replication in a fault-tolerance system.

- Original insights from 70s and “re-discovered” in the late 90s

==

## What is CAP Conjecture?

- Informally, "CAP" is an conjecture (Brewer 1999)

- ***Conjecture***: An opinion or conclusion formed on the basis of incomplete information. **Synonyms**: speculation, presumption 

==

## What is CAP Theorem?

- Formally, "CAP" is a theorem (Gilbert,Fox 2002)

- ***Theorem***: A proposition that has been proven formally by means of accepted truths. 

---

# Why is CAP important?

==

## Why is CAP important?

- Often-cited when describing/comparing/critiquing distributed systems
- Tool for reasoning about trade-offs and limitations
- Influential on distributed database architectures 
- Embodies *core* concepts of distributed systems (consistency
  and failures).

---

# The CAP Conjecture 

==

## The partition question:

- A distributed application services client read/write requests from many independent components. 
- Each component acts as a replica of a shared dataset
- Client requests interact (read/write) directly with the data

==

### During a network partition, a client 'write' request arrives

- A. Wait until the partition is repaired to continue
- B. Immediately process client requests

==

### In general, CAP Conjecture states that these choices are mutually exclusive. 

---

# Pick 2 of 3

==

## CAP rule of pick "2 of 3"

- **C**onsistency
- **A**vailability
- **P**artition tolerance

==

## CAP rule of pick "2 of 3"

- **AP** system prioritizes availability over consistency
- **CP** system prioritizes consistency over availability
- **CA** system sacrifices partition tolerance (N/A)

###(Terms have taken a life of their own.)

---

## Consistency vs availability Trade-off

==

When buying a plane ticket online the site communicates with a replicated database of available seats, risk that planes get overbooked (seat for 1 gets sold twice!) 

### AP or CP? Solution?

==

Make a post to a social network, call your friend who says she cannot see the post on their page.

### AP or CP? Solution?

==

Concurrent withdrawals to empty a bank account. Same money is given out twice. 

### AP or CP? Solution?

---

# "C" in CAP

==

## "C" in CAP

- Consistency, as defined by CAP Conjecture
  - One-copy serializability.

- Consistency, as defined by CAP Theorem
  - Linearizability.

==

## Linearizability & Serializability

- Two types of "strong consistency"
- Avoids: stale reads, lost writes, monotonicity/causality violations 

==

## Value of "CP" 

- Preserves correctness and integrity 
- Prevents data loss

---

# "A" in CAP

==

## "A" in CAP

- As defined by CAP Conjecture:
  - Every requests results in a valid response with a high probability
- As defined by CAP Theorem:
  - Every request received by a non-failing node eventually results in a valid response.

==

## Value of "AP" 

- Downtime damages reliability, prevents client transactions 

---

# "P" in CAP

In both the CAP Theorem and CAP Conjecture, partition tolerance requires a system to assume partitions exists and continue to operate correctly in the presence of a partition.

---

# Accuracy of "CP" & "AP"?  

==

## Accuracy of "CP" & "AP"?  

- CAP applies **during** a network partition
- Makes no restriction on normal/majority behaviour

==

## Accuracy of "CP" & "AP"?  

- Counter-intuitive to many established system designs
  - "Best-effort consistency" - AP acts like CP
  - Master-minion replication - CP acts like AP

==

## Accuracy of "CP" & "AP"?  

- Are the invariants of CAP really invariant? 
- Spanner: Clock-skew variance
- FaRM: RDMA

---

## Observation

Many fault-tolerant highly-available systems do not guarantee 100% availability with failures (i.e., not "AP"), while also only providing a weak consistency model. 

### What would motivate a "CP" system to avoid providing strong consistency guarantees? 

---

# Costs of Coordination 

==

## Costs of Coordination 

- Strict consistency requires coordination between replicas (e.g., 2PC, Paxos)
- Overhead of messaging, time-outs, protocol processing

==

## Coordination increases latency

Request based on slowest RTT, Throughput capacity is lowered

==

## Coordination inhibits scalability

Node asymmetry, interdependency

==

## Coordination decreases flexibility 

Not all data need strong consistency yet everyone pays the same cost.

---

# Take-Aways 

==

## Take-Aways 

CAP Theorem highlights an important design point in distributed systems:  behaviour during a partition (aka. the partition question.) 

==

## Take-Aways 

"CP" and "AP" often inaccurate when describing a systems consistency vs. availability trade-offs.

==
 
## Take-Aways 

Many reasons beyond 100% availability that a system may want to sacrifice consistency guarantees: lower latency, increased scalability, decreased flexibility. 

---

![](https://dl.dropboxusercontent.com/u/11161963/captalk/DisorderOfOperations.004.jpeg)

---

# Programmable Consistency 

==

![](https://dl.dropboxusercontent.com/u/11161963/captalk/DisorderOfOperations.001.jpeg)

==

![](https://dl.dropboxusercontent.com/u/11161963/captalk/DisorderOfOperations.002.jpeg)

==

![](https://dl.dropboxusercontent.com/u/11161963/captalk/DisorderOfOperations.003.jpeg)
