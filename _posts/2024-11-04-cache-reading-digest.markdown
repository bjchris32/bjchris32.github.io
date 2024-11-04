---
layout: post
title:  "Common Caching Strategies and How to Choose"
date:   2024-11-04 11:40:34 -0500
categories: cache
---

I recently read an [article](https://medium.com/ssense-tech/cache-me-if-you-can-a-look-at-common-caching-strategies-and-how-cqrs-can-replace-the-need-in-the-65ec2b76e9e) that introduces various caching strategies. This was also my first time using NotebookLM. This tool significantly enhanced my understanding of the topic. You can ask questions in this notebook: [NotebookLM](https://notebooklm.google.com/notebook/91bfc8ff-5d25-4793-9a9e-95fe572bae33)


## Common Caching Strategies and How to Choose

### 1. **Read-Through Caching**

*   With read-through caching, the application first checks the cache for the requested data.
*   If the data is not in the cache, it's fetched from the original source, added to the cache, and then returned to the client.
*   **Benefits**: This approach ensures data is always available, even if it's not initially in the cache. It also allows for an eviction strategy to remove old or infrequently accessed data.
*   **Drawbacks**: It can lead to slower response times when data is not in the cache.

### 2. **Write-Through Caching**

*   This strategy writes data to both the cache and the origin simultaneously during every write operation.
*   Reads are performed solely from the cache.
*   **Benefits**:  Eliminates stale data by keeping the cache consistently in sync with the origin.
*   **Drawbacks**:  The cache must be large enough to hold the entire dataset, and writes become slower and more complex due to the need to update both the cache and the origin.

### 3. **Write-Behind Caching**

*   In this approach, data is first written to the cache, which acts as the temporary source of truth.
*   A separate process asynchronously synchronizes the cache with the origin.
*   **Benefits**: Offers the fastest read times as data is always up-to-date in the cache.
*   **Drawbacks**:  Requires a resilient cache to prevent data loss before it's written to the origin and involves an additional synchronization process that adds complexity. 

### Choosing the Right Strategy

The best caching strategy depends on factors like:

*   **Data Freshness**: If your application requires extremely up-to-date data, write-through or write-behind caching might be more suitable. If eventual consistency is acceptable, read-through caching could be sufficient.
*   **Read/Write Ratio**:  If your application has a high read-to-write ratio, read-through caching is typically a good choice. For applications with frequent writes, write-through or write-behind might be more appropriate.
*   **Data Size**:  Write-through and write-behind caching require the cache to hold the entire dataset. If your data is too large, read-through caching with a selective caching strategy might be a better option.
*   **Complexity**:  Read-through caching is generally simpler to implement than write-through or write-behind. Consider the complexity and maintenance overhead when choosing a strategy.

## Alternative cache - CQRS

**CQRS (Command Query Responsibility Segregation)** is a design pattern that separates the responsibilities of reading and writing data in an application. It acknowledges that interactions for retrieving information (queries) are different from those that change the system's state (commands). 

**Key Concepts:**

*   **Commands:**  Actions that modify the state of the system. They are typically asynchronous and do not return data. 
*   **Queries:**  Operations that retrieve data from the system without altering its state. They are typically synchronous and return data.
*   **Separate Persistence:** CQRS implementations often use different persistence solutions for the read (query) and write (command) sides. This allows each side to be optimized for its specific purpose.


**Advantages of CQRS as a Caching Mechanism:**

*   **Event-Driven Architecture:** In CQRS, the write side emits events representing state changes, which are used to populate and update the read side. This eliminates the need for traditional caching mechanisms like TTL management and stampede handling.
*   **Planned From the Beginning:**  Unlike traditional caching, which is often added as an afterthought, CQRS is designed into the system from the start.
*   **Simplified Read Side:** The read side doesn't need complex logic like repositories or entity manipulation, making it simpler to implement.

**Comparison to Traditional Caching:**

The sources explain that CQRS offers benefits similar to traditional caching methods: 

*   **Eventual Consistency:** Both CQRS and caching accept the possibility of serving slightly outdated data. 
*   **Pre-computed Results:** CQRS's read side provides pre-computed results based on events from the write side, much like how a cache stores pre-fetched data.
*   **Low-Latency Reads:** CQRS, like caching, aims to provide fast read operations by optimizing the read side for data retrieval. 


## Reference
* https://medium.com/ssense-tech/cache-me-if-you-can-a-look-at-common-caching-strategies-and-how-cqrs-can-replace-the-need-in-the-65ec2b76e9e
* https://notebooklm.google.com/notebook/91bfc8ff-5d25-4793-9a9e-95fe572bae33
