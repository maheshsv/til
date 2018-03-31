# Code BEAM SF 2018

[Code BEAM SF 2018](https://www.codesync.global/conferences/code-beam-sf-2018/) was hosted by Erlang Solutions. I got a free ticket from Tyr. :)

### Notes

~ not well organized (last one is the best one, by Joe Armstrong)



#### **Aeternity: Scalable Smart Contracts Interfacing With Real World**

First class objects:

- Oracle: bring in information from the (real) world. e.g: anything from a simple boolean to the complete work of Shakespeare.

- Names: a human readable name

- Tokens

- Governance: done by voting on the chain on governance proposals.

- State channels

- Contracts: executable code, execution can be verified by miner

- - Safe
  - Efficient and scale: state channels and a new consensus algorithm
  - Cheap
  - …



### **Taking Elixir to the Metal**

Elixir:

- Concurrency
- Fault tolerance
- Distributed

Elixir and the Outside World

- Port
- Inet_dev
- NIFs
- …

Why NIF?

- CPU throughput
- Deal with hardware directly
- Interior with graphics

Usually in C

ErlEnv: first arg

Elixir & Rust

Erlang_nif-sys

Rustler: lib for writing Erlang NIFs with safe Rust.

Simple approaches:

- Use existing Rust lib
- 

Use existing Rust lib problem: if takes too long, can cause strange behavior

(Github)ThreadProgress: how scheduler thread works

Counting reductions

**Optimization: Chunking**

NIF resource objects

**Optimization: Rescheduling**

**Optimization: Threaded NIFs**



### **Event Sourcing and CQRS**

Event: not the final state

Sn = reduce(E, S0, apply)

E.g: git

State: files

Events: commits

Relational database?

CQRS

GitHub: commanded

Build a crypto currency:

\# commands

Mine_coin(account_id, nonce)

Transfer(from, to, amount)

\# query

Richest()

How to transfer?

Process manager: receive events and send commands



### **The HitchHiker’s Guide to the Unexpected**

By: Fred Hebert

System Architecture (draw and ask engineers to implement it)

Area of knowledge

How to shift bugs to the easy zone?

- Increase knowledge

- - Share knowledge, learnings, etc

- Decrease the unknown

- - Not write code, formal prove(TLA+), etc

- Make the unknown things less relevant

Super supervisors:

One for one, rest for one, one for all

Boots and shutdown

Let the unknown crash deal with the expected



### **Getting to know your rabbit (RabbitMQ)**

By: Brett Cameron

Briefly overview of RabbitMQ and AMQP

Evolution

HA: master-slave (not exactly master-slave, but have same view of the world)

Vhost:independent message brokers within the single RabbitMQ process, with their own queues, exchanges, permissions and so on.

Extensible:

- Plugin system
- ..

Multi-protocol messaging

- MQTT
- STOMP

“One size fit all” is flawed: because different protocol have diff properties.

Mix and match publish and consumer protocols

Getting help:

…

Integrate with other system: datadog, new relic, Prometheus…



### **IoT Blockchain with Erlang**

Blockchain: forge consensus

Anatomy:

- Consensus algorithm
- P2P network
- Transactions
- Blocks

Types of Consensus:

- PBFT derivatives - ripple, stellar, etc
- Nakamoto consensus
- Proof of stake
- Many others

PBFT based:

Practical Byzantine fault tolerance

Nakamoto Consensus:

Open membersh

Computing some hash over the block such that the numerical value of the ash falls under some threshold.

Proof of Stake:

…

Why Erlang?

Why not!

GitHub.com/helium

**What’s up with the IoT?**

Still hasn’t arrived. Why?...

Helium for the rescue!

Much ado about coverage???

How does it work?

What does that get us?

- Self-verifying, decentralized network of gateways fixed in space and time.
- Redundant wireless coverage
- Location services
- Cryptographic proof
- Profit from its usage

How is this better than Cellular/LoRa, etc?

- Open
- Cost efficient
- …



### The Erlang Ecosystem

By: Mariano Guerra, Robert Virding

Background (the problem)

- Handle large concurrent activities
- Distributed over servers
- …

Background(some reflections)

**Not** out to implement a functional language

**Not** out to implement the actor model

**TRYING TO SOLVE PROBLEMS!**

Solution: **first principles**

- Lightweight concurrency
- …


- High level lang to get real benefits
- Simple!

Concurrency: core ideas

- Light-waight isolated processes
- Async message passing

Error handling: basic premise

Error always happen

Error handling: basic goals

System must never go down!

OTP

What is the BEAM?

A virtual machine runs Erlang.

Properties:

…

Extending the system: native languages

Elixir, LFE(Lisp Flavored Erlang), Efene(Python/JS inspired Erlang dialect with minimal syntax), Clojerl(Clojure on Erlang VM), Alpaca(statically typed), Erlog(prolog), Luerl(Lua)

Extending the system: non-native language

Lua, Prolog

Extending the system: external systems

- External ports

- - Linked-in drivers

- NIFs(Natively implemented functions)

- C-nodes

- Rust

- WebAssembly



### **Why Elixir Matters**

By: Osa Gaius

geneology

History of FP:

Lambda calculus -> LISP -> Scheme -> ML -> Erlang -> Miranda -> Haskell -> F#/Scala -> Clojure -> Akka -> Rust -> Elixir -> Elm

Why Erlang/Elixir matters?

- Internet/scalability
- Non-interrupted Available

Moving forward

- Breadth vs depth

- - Libraries (aka Gems)
  - Domains: messaging, web development

- Evangelism

- - Marketing
  - Consultation
  - Fan Out



### **Keynote:  Two Testing Tools for the Erlang Ecosystem**

By: Kostis  Sagonas

**PropEr: property-based testing tool**

+generator

e.g: a sort function

Prop_ordered:

sorting a random generated integer list make it ordered.

Prop_sample_length:

The length is the same after sorting

Prop_same_set_of_elements?

User-defined simple type as a generator

-type bf() :: binary() | ‘apple’ | ‘banana’ | ‘orange’.

-type tree(T) :: ‘leaf’ | {‘node’, T, tree(T), tree(T)}.

PBT testing of sensor networks

Generate random graph(not working sometimes)

Possible Solutions:

- Write move involved(custom) generators
- Guide the input generation

Targeted Property-Based Testing

Testing X-MAC protocol

- Random PBT
- Targeted PBT

**Concuerror**

Aka Systematic Concurrency Testing

Systematic Exploration Example

Initially: x = y = 0

Thread 1: x := 1, y := 1

Thread 2: x := 2, y := 2

Correctness property(at the end) assert(x == y);

Explore all possible behaviors of a program annotated with some assertions.

Systematic != Stupid

Initially: x = y = … = z = 0 => n! combination

Bounding Techniques



### **Elixir in TubiTV**

By: Tyr Chen

Core problem: access policy

Compile business rules (in db) into fn

Latency from 200ms to 50us

More and more services built with Elixir

How to deploy at anytime?



### **Lazy Evaluation**

Function as data

What is a strategy?

- Random
- Echo
- No repeats
- Statistical
- …

Function evaluation in Erlang:

Evaluate the arguments before the body

But if an argument is a **function** then it’s passed unevaluated.

DELAY!

A lazy switch

Approaches:

1. Change argument to function
2. macro

(GitHub)STREAMS

GitHub.com/simonjohnthompson/streams



### **Erlang in** **WhatsApp** 

...



### **Next Generation SCADA**

Supervisory Control And Data Acquisition

Architecture

Essentially a 5-level architecture…

Challenges and Concerns

Security

ControlMachines

MQTT



### **Forgotten Ideas in Computer Science**

By: Joe Armstrong

Problems(1980)?

- How to find things
- How to store things
- How to program things

What problems should we solve now?

- Too much stuff
- We have invented all this stuff what the heck are we going to do with it all.

Methodology

How to make a list

- Collect lots of items **easy**
- Assign to lists **difficult**
- Shorten the lists to N items (N is small) **very difficult, throwing things away is much more difficult than collecting things - but what’s left is better.**

**Things to learn**

**…**

**4 old tools to learn**

- emacs
- bash
- make
- shell

**4 really bad things**

- Lack of privacy
- Attempt to manipulate us through social media
- Vendor lock in
- Terms and conditions

**3 great books to read**

- Algorithms + DS = programs
- The mythical man-month
- How to win friends and influence people

3 perf improvements

- Better algorithms
- Better programming language
- Better hardware

**5+ YouTube videos to watch**

- Computer resolution has not happened yet(Alan Kay)
- Computers for cynics
- Free is a lie
- How a handful of tech companies
- ..

C

Prolog

…

4 great forgotten ideas

- Linux pipes

6 areas to research

2 fantastic programs to try

- Tiddlywinks
- sonicPI

**Learn to write**

**Laws of physics and math**

**BIG ideas**

Things can be SMALL

Web broken:

Lack of symmetry

Wiki

Xnandu

- Like the web but better
- No broken links
- No difference between readers and writers
- Never loose any data
- All copyright and attribution correct
- Complete knowledge of parents and children

**What can we do**

