# system-design-lld-hld-complete-resources

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
