# URL Shortener


# Design a simple URL Shortener

**Answer:**

“In a URL shortener, we take a long URL and generate a unique short key for it.
This mapping is stored in a database.
When a user hits the short URL, the system looks up the original URL using the key and redirects the user.
To improve performance, frequently accessed URLs can be cached.”




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


