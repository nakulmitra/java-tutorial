# Handling 1 Lakh Likes in 1 Minute using Redis + Spring Boot

In modern social media platforms like Instagram, posts can go viral in seconds, generating **massive write loads** (likes, comments, shares, etc.).
If every single action directly hits the **relational database**, the system can:

* Become **unresponsive** due to overwhelming I/O
* Suffer from **locks and contention**
* Eventually **crash or degrade in performance**

Under this section, we will presents a **high-level conceptual architecture** of how such spikes in like activity can be **buffered using Redis** and **processed in batches**, significantly reducing pressure on the backend database.

> **Disclaimer**: This architecture is **not an exact replica** of how companies like Instagram operate. It is a **simplified and practical design** to demonstrate scalable principles in system design.

## Watch the Full Tutorial on YouTube

[How Instagram Handles 1 Lakh Likes in 1 Minute | Redis Bulk Update System Design](https://youtu.be/ChyRAH-0xGE)

## Problem Statement

Imagine RCB wins the IPL 2025 and posts about it on Instagram. The post goes viral and gets:

* **1,00,000 likes in 1 minute**
* That's approx **1,667 likes per second**

If each like makes a direct write to the database:

* It creates **enormous write traffic**
* The **RDBMS can lock up**, affecting user experience
* System **scalability becomes limited**

## High-Level Solution

We break the problem into **two stages**:

1. **Record likes in Redis** (an in-memory data store with high throughput)
2. **Flush likes to the database** periodically in **bulk**

### Redis as Like Buffer

* Every like increments a **Redis counter key**: `post:like:{postId}`
* No DB writes happen immediately
* Every 30 seconds, a scheduled job reads all counters and performs **one DB update per post**
* Redis keys are deleted/reset after flushing

## Components in the Code

### 1. **PostController.java**

Handles incoming like requests via:

```java
@PostMapping(value ="/{postId}/like", produces = "application/text")
public String likePost(@PathVariable Integer postId) {
	service.recordLike(postId);
	return "Liked successfully!!!";
}
```

### 2. **LikeService.java**

Uses `RedisTemplate` to increment counters:

```java
public void recordLike(Integer postId) {
	String key = "post:like:" + postId;
	redisTemplate.opsForValue().increment(key);
}
```

### 3. **LikeAggregator.java**

Flushes Redis counters to the DB every 30 seconds:

```java
@Scheduled(fixedRate = 30000)
public void aggregateLike() {
	Set<String> keys = redisTemplate.keys("post:like:*");
	if (null == keys) {
		return;
	}

	for (String key : keys) {
		Long postId = Long.valueOf(key.split(":")[2]);
		String likeCountStr = redisTemplate.opsForValue().get(key);
		Long count = likeCountStr != null ? Long.valueOf(likeCountStr) : 0;

        if (count > 0) {
            repo.findById(postId).ifPresent(post -> {
                post.setLikeCount(post.getLikeCount() + count);
                repo.save(post);
                redisTemplate.delete(key);
            });
        }
    }
}
```

## Architectural Diagram

```
Client
  |
  |------> POST /posts/123/like
             |
             V
        [PostController]
             |
             V
     [Redis: post:like:123] <- +1
             |
      (No DB write yet)
             |
   [LikeAggregator @ every 30s]
             |
             V
      SELECT + UPDATE in DB
             |
             V
         Reset Redis Key
```

## Benefits

* High Performance
* Minimal DB contention
* Scalable for viral spikes
* Efficient batch writes
* Fast user feedback

## Without This Architecture?

If every like -> direct DB write:

* High chance of lock contention
* Increased latency
* Potential DB outage

## Limitations & Next Steps

| Limitation              | Solution                                      |
| ----------------------- | --------------------------------------------- |
| Redis crash = data loss | Use Redis persistence or Kafka for durability |
| No retry mechanism      | Add a failure queue                           |
| Counter overwrites      | Use atomic increments or pub-sub              |

## Tech Stack

* Java 8
* Spring Boot
* Redis (in-memory store)
* PostgreSQL
* Spring Scheduler

## Extending This Design

For more resilience and durability:

* Use **Kafka**: Each like is a message -> consumer -> DB write
* Use **Write-Ahead Logs** in Redis (AOF/RDB)
* Add **metrics and dashboards**

## Conclusion

This repo demonstrates **how we can design scalable systems** to handle high-throughput user interactions like likes or views.
Using **Redis as a buffer** drastically reduces DB load while maintaining real-time responsiveness.