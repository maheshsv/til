# Nginx Microservices Series

Nginx blog has a seriers of microservices articles starts from [Introduction to Microservice](https://www.nginx.com/blog/introduction-to-microservices/).

### Problems with monolithic:

- overwhelmingly complex
- hard to do continues deployment
- hard to scale because of resource conflicts of different modules
- reliability chanllenge because of module coupling
- hard to adopt new frameworks and languages

### Microservice to the rescue

- **Pros**
  - each service can be developed independently (as long as the interface doesn't change)
  - deploy independently
  - scale independently
- **Cons**
  - complex system because of distributed nature
  - partitioned database: make it hard to for transaction
  - testing is complex
  - deploying is more complex

### API Gateway

API Gateway is the single entry point into the system.

- **Pros**
  - encapsulate internal structure of the application
- **Cons**
  - yet another HA component that must be developed, deployed and managed(should be as lightweight as possible)

### Inter-Process Communication

Services much interact using an inter-process communication mechanism.

- Interactive Style
  - One-to-one
  - One-to-many
- synchronous or asynchronous
- message-based: pub/sub
- format: 
  - text-based: JSON/XML
  - binary format: Avro/Protocol Buffers
- Handle partial failure strategies ([Netflix Hystrix](https://github.com/Netflix/Hystrix))
  - network timeouts
  - limiting outstading requests number
  - [circuit breaker pattern](http://martinfowler.com/bliki/CircuitBreaker.html)
  - Provide fallbacks

### Service Discovery

- Client-Side Discovery Pattern
- Service-Side Discovery Pattern(e.g: AWS ELB)

service registry:

 - etcd
 - consul
 - zookeeper
 - Eureka

### Event-Driven Data Management

Distributed transaction usually solved by 2PC(two-phase commit).

> For many applications, the solution is to use an event‑driven 
> architecture. One challenge with implementing an event‑driven 
> architecture is how to atomically update state and how to publish 
> events. There are a few ways to accomplish this, including using the 
> database as a message queue, transaction log mining, and event sourcing.

### Deployment Strategy

- multiple service instances per host(bad for production)
- service instance per host(VM/container)
- serverless

### Refactor Monolith into microservices

**Incrementally refactor monolithic application!!!**

Strategies:

1. stop digging: stop making the monolith bigger
2. split service to layers, such as frontend and backend service seperation
3. extract services

---

My experience refactoring monolith into microservices matches the strategies here very well! :-)

