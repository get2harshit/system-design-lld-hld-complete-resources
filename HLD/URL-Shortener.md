# Design a simple URL Shortener

### Core Answer

“In a URL shortener, the client sends a long URL to the server.
The server generates a unique short key, stores the mapping of short URL to long URL in a database, and returns the shortened URL to the client.

When a user accesses the short URL, the server looks up the original URL using the key and redirects the user.
To improve performance, frequently accessed URLs are cached.”


## Follow-up Questions (Integrated Answers)


### 1. In this system, what is the client and what is the server?

**Answer:**

“The client is typically a browser or mobile app that sends requests to shorten or access URLs.
The server is the backend service that generates short URLs, stores mappings, and handles redirection.”

---


### 2. SQL or NoSQL — which database is more suitable?

**Answer:**

“NoSQL is generally more suitable because:

* The data model is simple key-value (short → long URL)
* We need high scalability and high read throughput
* Schema flexibility is not critical here

However, SQL can also be used if strong consistency or relational features are required.”

---

### 3. Where should caching be used and what should be cached?

**Answer:**

“Caching should be used in the read path, especially during redirection.
Frequently accessed short URLs should be cached in a fast in-memory store like Redis.

This avoids repeated database lookups and significantly reduces latency.”

---

### 4. Which operations should use a queue?

**Answer:**

“Operations that are not critical to immediate response should be handled asynchronously using a queue. For example:

* Analytics (click tracking)
* Logging
* Expiration cleanup
* Spam detection

These can be processed in the background without blocking the user request.”

---

### 5. How do traffic and latency constraints influence design?

**Answer:**

“URL shorteners are read-heavy systems with very high redirection traffic.
So the design must prioritize low latency and high availability.

To handle this:

* Use caching for fast lookups
* Use horizontally scalable databases
* Use load balancers to distribute traffic
* Keep redirection logic lightweight

Even small latency increases can impact user experience since redirects happen in real-time.”

---



```text
START
│
├── Requirement?
│     ├── Convert long URL → short URL
│     ├── Redirect short URL → original URL
│     └── High read traffic (redirects)
│
├── Core Design
│     └── Client → API → Service → DB
│
├── Key Problem?
│     └── How to generate unique short IDs
│
├── ID Generation Strategies
│     ├── Option 1: Auto-increment ID + Base62 encoding
│     ├── Option 2: Random string
│     └── Option 3: Hash (MD5/SHA + truncation)
│
├── Preferred Approach
│     └── Auto-increment + Base62
│           ├── Simple
│           ├── Guaranteed uniqueness
│           └── Short readable URLs
│
├── DB Design
│     ├── id (PK)
│     ├── short_code (unique)
│     ├── long_url
│     ├── created_at
│     └── expiry (optional)
│
├── Read Flow (Redirect)
│     ├── User hits short URL
│     ├── Lookup DB / cache
│     └── Redirect (HTTP 301/302)
│
├── Write Flow (Create Short URL)
│     ├── Receive long URL
│     ├── Generate short code
│     └── Store mapping in DB
│
├── Performance Optimization?
│     ├── Cache (Redis) for fast lookups
│     └── CDN for global access
│
├── Scaling?
│     ├── Read-heavy → caching
│     ├── DB sharding by ID
│     └── Load balancer
│
├── Edge Cases
│     ├── Duplicate URLs?
│     ├── Collision in random/hash?
│     ├── Expired links?
│
├── Follow-ups
│     ├── Analytics? → store click data async
│     ├── Custom alias? → user-defined short code
│     └── Abuse? → rate limiting
│
END
```

# HLD of URL Shortener
<img width="721" height="423" alt="Screenshot 2026-04-23 at 10 34 20 AM" src="https://github.com/user-attachments/assets/0803d827-5944-4b44-83ce-4016e9d82c1e" />


