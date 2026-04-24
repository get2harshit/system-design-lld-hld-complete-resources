# 1. What happens when a request hits your backend system?

**Answer:**

“When a client sends a request, it first reaches the Load Balancer, which distributes traffic across multiple servers.
The request then goes to an API server, where routing and validation happen.
From there, it moves to the service layer containing business logic, which may interact with the database or cache.
Finally, the response is sent back through the same path to the client.”

---

# 2. Why do we need a Load Balancer? What problem does it solve?

**Answer:**

“A Load Balancer distributes incoming requests across multiple servers to prevent any single server from getting overloaded.
It improves system availability, enables horizontal scaling, and ensures high reliability by routing traffic only to healthy servers.”

---

# 3. What is a Stateless API and why is it important?

**Answer:**

“A stateless API means the server does not store any client session data between requests.
Each request contains all the information needed to process it.
This makes the system easier to scale, as any request can be handled by any server, and it also improves fault tolerance.”

---

# 4. When and why do we use caching?

**Answer:**

“We use caching to store frequently accessed data in a faster storage layer like memory.
This reduces database load and significantly improves response time.
Caching is especially useful for read-heavy systems where the same data is requested repeatedly.”

---

# 5. What is a Queue and where would you use it?

**Answer:**

“A queue is used to handle asynchronous processing by decoupling systems.
Instead of processing everything immediately, tasks are pushed to a queue and processed by workers later.
This helps in handling traffic spikes and improves system reliability.
Common use cases include sending emails, processing payments, and background jobs.”

---

# 6. SQL vs NoSQL — how do you decide?

**Answer:**

“I choose SQL when I need structured data, strong consistency, and transactions—like in banking systems.
I choose NoSQL when I need high scalability, flexible schema, and can tolerate eventual consistency—like in social media or analytics systems.”

---

# 7. What is the difference between scaling vertically and horizontally?

**Answer:**

“Vertical scaling means increasing the capacity of a single server, like adding more CPU or RAM.
Horizontal scaling means adding more servers and distributing the load across them.
Horizontal scaling is preferred in modern systems because it provides better scalability and fault tolerance.”

---

# 8. What is latency? How do you reduce it?

**Answer:**

“Latency is the time taken for a system to respond to a request.
It can be reduced by using caching, CDNs, efficient database queries, indexing, and minimizing network hops.
Optimizing system architecture also plays a key role in reducing latency.”

