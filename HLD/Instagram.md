## Design an Instagram-like Reels System

An Instagram-like application allows users to upload short video reels and watch reels uploaded by others.

The system must:

* Handle millions of users daily
* Support fast upload and playback
* Store user and reel data permanently
* Reduce repeated database access for popular reels
* Handle background tasks (video processing, notifications)
* Work under high traffic, low latency, and limited budget

### Assumptions:

* DAU = 1 million
* Each user uploads 2 reels/day
* Average reel size = 20 MB


---

## 1. Client vs Server

“The client is the mobile app or web app used by users to upload and watch reels.
The server consists of backend services that handle uploads, store videos, process them, and serve them for playback.”

---

## 2. SQL vs NoSQL for Metadata

“I would prefer NoSQL because:

* Data is large-scale and grows rapidly
* Schema can evolve (likes, comments, shares)
* High read/write throughput is needed

However, SQL can still be used for structured user data if strong consistency is required.”

---

## 3. What should be cached?

“To reduce latency:

* Popular reels (video URLs / metadata)
* User feed (precomputed or recent reels)
* Frequently accessed user profiles

Caching avoids repeated DB queries and improves playback speed.”

---

## 4. What should go to Queue?

“Non-critical operations should be async:

* Video processing (compression, thumbnails)
* Notifications
* Like/comment count updates
* Analytics

Queues help in handling spikes and improving system responsiveness.”

---

## 5. Daily Storage Estimation

**Step-by-step:**

* Users = 1M

* Reels per user = 2
  → Total reels/day = 2M

* Size per reel = 20 MB
  → Total storage/day =

**2M × 20 MB = 40 TB/day**

**Answer:**
“The system needs approximately **40 TB of storage per day**, so we must use scalable object storage like S3.”

---

## 6. Traffic & Latency Impact

“This is a read-heavy system with high traffic during peak hours.

To handle this:

* Use CDN for video delivery
* Cache hot content
* Use load balancers
* Keep APIs lightweight

Low latency is critical because video playback must be smooth and instant.”

---

## 7. Budget Constraints Impact

“With limited budget:

* Avoid over-provisioning servers
* Use auto-scaling instead of fixed infrastructure
* Cache only hot data instead of everything
* Use object storage instead of expensive DB storage
* Optimize video size (compression)

Trade-off is between cost vs performance.”

