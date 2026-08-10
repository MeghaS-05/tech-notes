System Design is the process of deciding how different architecture, components of a software system work together to satisfy user’s requirement.

For example, imagine designing Youtube. You need to think about:

- How user’s upload video
- Where videos are stored
- How videos are delivered to millions users
- How user authenticate
- How comments and likes are stored
- How the system handles millions of concurrent users
- What happens when a server or database fails

A system design discussion usually moves thorugh:

—> Requirement → architecture → Components → Data Flow → Scaling → Reliability → Trade-offs

## **Functional vs Non-Functional Requirements**

The first thing to clarify when designing a software system.

Functional requirement which describes what the system should do whereas Non-Functional requirement describe how well the system should perform.

For example:

for an e-commerce system:

- Users can browse products
- Users can add products to a cart.
- Users can place order.
- Users can make payments.

This was all about functional requirement, whereas the non-functional requirement will be:

- Should support 10 million users.
- API response should usually be below 200ms.
- System should be available 99.99% of the time.
- Data should not be lost.
- System should be easy to maintain.

In conclusion, Functional requirement is about Features/behavior whereas Non-Functional requirement is about Quality attributes / constraints.

## Scalability

It is the ability of a system to handle increasing workload by adding resources.

For example, suppose your application currently handles 1000 request/second and eventually needs to handle 1,00,000 request/second.

Your architecture needs a way to grow with that workload. There are two fundamental approaches:

### i) Vertical Scaling (Scaling up)

You make your existing machine more powerful. 

for example suppose your current system has 8 CPU & 16 GB RAM and you upgraded your system to 32 CPU & 128 GB RAM.

Advantages :

- Simple
- Often requires little architectural change
- Easier to manage initially

Disadvantages :

- Hardware has a limit
- Expensive at higher levels
- Creates a potential single point of failure
- Eventually you cannot keep making one machine bigger

### ii) Horizontal Scaling (Scaling out)

Instead of making one server more powerful, you can add more servers.

```
             Load Balancer
              /    |    \
             /     |     \
        Server   Server   Server
           1        2        3
```

If traffic increases, you can add more servers:

```
             Load Balancer
          /    /    |    \    \
       S1    S2    S3    S4    S5
```

Advantages :

- Can scale to very large workloads
- Better fault tolerance
- Hardware limits are less restrictive
- Servers can be added/removed based on demand

Disadvantages :

- More architectural complexity
- Requires load balancing
- Distributed systems introduce problems such as:
    - Data consistency
    - Network failures
    - Distributed transactions
    - Coordination

## Availability

It means, how often is the system operational and accessible when users need it?. Commonly expressed in percentage (eg. 99% availability, means roughly 1% of the time the service can be unavailable).

### How do we improve availability?

Instead of:

```
User → Server
```

we can have:

```
              Load Balancer
             /             \
        Server A          Server B
```

If Server A fails, traffic can go to Server B.

This is an important system-design principle: **Avoid single points of failure.**

## Reliability

It is the ability of a system to perform correctly and consitently over the time, including when things go wrong. 

Availability and reliability are related but different.

Imagine a payment service that is always reachable:

```
99.99% available
```

but occasionally charges customers twice.

It's highly available, but **not reliable**.

A reliable system should:

- Produce correct results
- Avoid data corruption
- Handle failures gracefully
- Recover from failures
- Preserve important data

## Maintainability

Maintainability is how easily we can : understand the whole system, Fix bugs, Add features, Deploy changes, Monitor the system etc.

Maintainability becomes increasingly important as systems and engineering teams grow.

In summary, 

Suppose you're asked:

> **Design a messaging system like WhatsApp.**
> 

You might start with requirements.

### Functional

- Send messages
- Receive messages
- Create groups
- See message history
- Send images

### Non-functional

- Support 100M users
- Low message latency
- High availability
- Messages should not be lost
- System should scale horizontally

Then you'd start thinking about architecture:

```
                Clients
              /    |    \
             /     |     \
            ↓      ↓      ↓
        Load Balancer
              |
      ┌───────┴────────┐
      ↓       ↓        ↓
   Server   Server   Server
      |       |        |
      └───────┬────────┘
              ↓
          Database
              |
           Cache
```

Then you ask:

- How do we scale the servers?
- How do we scale the database?
- What happens if a server dies?
- What happens if the database goes down?
- How do we guarantee message delivery?
- How do we reduce latency?
- How do we monitor failures?

**That is system design.**
