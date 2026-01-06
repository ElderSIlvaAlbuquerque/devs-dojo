# 🥋 Purple Belt: Capstone Projects

Choose **one** of the following projects as your capstone. Each project requires designing a system that could handle production scale, with a written architecture document and presentation.

---

## Project 1: Design Twitter/X

**Scope**: Design the core platform for a Twitter-like social network.

**Features to Support**:

- User registration, authentication, profiles
- Create tweets (140 characters, supports images/videos)
- Feed: Users see tweets from accounts they follow
- Retweet, like, reply, quote tweets
- Search by hashtag or user
- Trending topics
- Notifications (someone liked/retweeted your tweet)
- Timeline: Show tweets in reverse chronological order

**Scale**:

- 500 million registered users
- 100 million daily active users
- 100 million tweets/day
- 5 billion reads/day (feeds, searches)
- Peak load: 500k requests/second

**Technical Requirements**:

1. Database design (schema for users, tweets, follows, likes, etc.)
2. Feed generation strategy (normalized vs denormalized, caching strategy)
3. Search capability (full-text search on 5B+ tweets)
4. Notification system (fan-out on write vs fan-out on read)
5. Real-time updates (WebSocket for live feed updates)
6. Scalability plan (load balancing, database replication, caching)
7. Consistency model (eventual consistency for feeds OK, but tweets must be immediately visible)

**Deliverables**:

- Architecture document (8-15 pages) with diagrams
- Database schema with indexes and partitioning strategy
- API design (endpoints for tweets, feed, search, etc.)
- Scaling analysis (how would you handle 10x load?)
- High-level implementation guide

---

## Project 2: Design Uber/Lyft

**Scope**: Design the core platform for a ride-sharing service.

**Features to Support**:

- User registration (riders and drivers)
- Driver location updates (real-time GPS)
- Find nearby drivers (geospatial search)
- Request ride, driver accepts
- Real-time tracking (driver and rider see each other)
- Payment processing
- Rating and reviews
- Surge pricing (supply and demand)
- Analytics (hot zones, peak hours)

**Scale**:

- 10 million drivers
- 100 million riders
- 10 million rides/day
- 100k+ concurrent rides at peak
- Driver location updates every 2-5 seconds

**Technical Requirements**:

1. Geospatial database design (storing and querying locations)
2. Real-time location tracking (WebSocket, Kafka for location streams)
3. Matching algorithm (find best driver for each request)
4. Payment system (idempotent transactions, retries)
5. Notification system (rider and driver updates)
6. Analytics (real-time heatmaps, surge pricing calculations)
7. High availability (what if a key service fails?)

**Deliverables**:

- Architecture document with focus on real-time systems
- Database schema and indexing strategy for location queries
- API design for real-time updates (WebSocket protocol or server-sent events)
- Matching algorithm explanation
- Disaster recovery plan for payment system

---

## Project 3: Design an E-Commerce Platform (like Amazon)

**Scope**: Design the core systems for a large-scale e-commerce platform.

**Features to Support**:

- Product catalog (100M+ products)
- Search and filtering
- Shopping cart
- Checkout and payment
- Order tracking
- Inventory management (real-time availability)
- Seller/vendor support (some products from third parties)
- Recommendations (related products, personalized)
- Reviews and ratings
- Returns and refunds

**Scale**:

- 1 billion product views/day
- 100 million orders/day
- 50k checkout requests/second
- Product inventory changes constantly
- Must handle Black Friday (10x normal load)

**Technical Requirements**:

1. Inventory system design (real-time stock updates, preventing overselling)
2. Product catalog (how to search 100M products fast?)
3. Checkout flow (handling payment failures, retries, concurrency)
4. Recommendation system (collaborative filtering, ML model serving)
5. Order tracking and fulfillment coordination
6. Seller integration (third-party inventory sync)
7. Cost optimization (storage, bandwidth for media)

**Deliverables**:

- Architecture document covering catalog, inventory, checkout
- Database partitioning strategy (how to shard?)
- Search architecture (Elasticsearch design)
- Checkout flow with failure handling
- Inventory management and concurrency control
- Recommendation system architecture

---

## Project 4: Design a Messaging Platform (like WhatsApp/Telegram)

**Scope**: Design a real-time messaging platform.

**Features to Support**:

- User registration and authentication
- One-to-one messaging
- Group messaging (100+ users in a group)
- Message delivery and read receipts
- Typing indicators
- Voice/video call signaling
- Message encryption (end-to-end)
- Offline support (messages delivered when user comes online)
- Media sharing (images, videos, voice notes)

**Scale**:

- 1 billion registered users
- 500 million daily active users
- 100 billion messages/day
- 10 million concurrent connections
- Must handle network failures (users often offline)

**Technical Requirements**:

1. Real-time message delivery (WebSocket or similar)
2. Offline message queue (store messages for offline users)
3. Group messaging at scale (fan-out strategy)
4. Message ordering (messages must be delivered in order)
5. Delivery receipts and acknowledgments (idempotency)
6. Encryption (how to implement end-to-end while still offering analytics?)
7. Media handling (efficient storage and delivery for 100B messages/day)

**Deliverables**:

- Architecture document focused on real-time systems
- Connection management (how to handle 10M concurrent users?)
- Message routing and delivery strategy
- Database design for ordered message storage
- Offline message queue design
- Media storage architecture (CDN strategy)

---

## Project 5: Design a Video Streaming Platform (like YouTube/Netflix)

**Scope**: Design a video streaming platform serving billions of views.

**Features to Support**:

- Video upload and encoding
- Content delivery (streaming in multiple resolutions)
- User accounts and subscriptions
- Recommendations (what to watch next)
- Search and discovery
- Comments and engagement
- Analytics (view counts, watch time, retention)
- Content protection (DRM for premium content)
- Monetization (ads for free tier, subscriptions)

**Scale**:

- 2 billion users
- 500 million daily active users
- 1 billion hours watched/day
- 500k video uploads/day
- Video files: 1-4 hours at multiple resolutions (360p to 4K)

**Technical Requirements**:
1. Video encoding pipeline (convert uploaded video to multiple resolutions)
2. CDN strategy (where to cache videos for fast delivery?)
3. Database design for metadata (user watch history, subscriptions)
4. Recommendation engine (collaborative filtering on watch history)
5. Analytics (real-time view counts, streaming analytics)
6. Search (full-text search on titles, descriptions, tags)
7. Adaptive streaming (adjust quality based on bandwidth)

**Deliverables**:
- Architecture document covering encoding, delivery, recommendations
- Video encoding pipeline design (orchestration, fault tolerance)
- CDN strategy (how many edge locations? which content to cache?)
- Database schema (users, videos, watch history, subscriptions)
- Recommendation system design
- Real-time analytics architecture
- DRM strategy for premium content

---

## Project 6: Design a Financial Trading Platform

**Scope**: Design a system for cryptocurrency or stock trading at scale.

**Features to Support**:
- User accounts and KYC (Know Your Customer)
- Order placement (buy/sell, limit orders)
- Order matching (matching buy and sell orders)
- Real-time market data (prices, charts)
- Portfolio tracking
- Transaction history and statements
- Wallet management (storing assets)
- Market surveillance (detecting manipulation)
- Compliance and audit logging

**Scale**:
- 10 million active traders
- 1 million orders/second at peak
- Microsecond latency requirements
- 24/7 availability (markets never close)
- Regulatory compliance (must preserve audit trail)

**Technical Requirements**:
1. Order matching engine (low-latency, high-throughput)
2. Real-time market data (billions of price updates)
3. Wallet/account management (tracking balances safely)
4. Transaction atomicity (preventing double-spending)
5. Audit logging (compliance requirements)
6. Fraud detection (unusual trading patterns)
7. Disaster recovery (financial data is critical)

**Deliverables**:
- Architecture document with focus on reliability and latency
- Order matching engine design (matching algorithm)
- Transaction system design (atomicity and consistency)
- Market data pipeline (real-time updates)
- Compliance and audit logging architecture
- Fraud detection system design
- Disaster recovery plan

---

## Project 7: Design a Content Delivery Network (CDN)

**Scope**: Design your own CDN (like Cloudflare, Akamai).

**Features to Support**:
- Customer dashboard (upload origins, manage DNS)
- Edge servers (cache content at 100+ locations worldwide)
- DDoS protection (identify and block malicious traffic)
- Performance analytics (latency, throughput, cache hit ratio)
- Custom rules (which content to cache, TTLs)
- Origin failover (if origin fails, serve cached content)
- Signed URLs (prevent hotlinking)

**Scale**:
- 1 million customer origins
- 10 petabytes cached content
- 10 gigabits per second throughput
- 100+ edge locations worldwide
- Handle DDoS attacks (terabits per second)

**Technical Requirements**:
1. Edge caching strategy (what content, how long, geographic awareness)
2. Origin health checks (detecting failing origins)
3. DDoS mitigation (filtering malicious traffic)
4. Geo-routing (direct user to nearest edge)
5. Cache invalidation (when customer updates content)
6. Analytics (real-time and historical)
7. Security (TLS termination, DDoS, origin privacy)

**Deliverables**:
- Architecture document covering edge servers, control plane, origin
- Global routing strategy
- Caching strategy (what to keep, TTLs, invalidation)
- DDoS detection and mitigation
- Analytics and monitoring pipeline
- Scalability analysis

---

## Grading Rubric

Your capstone will be evaluated on:

1. **Completeness** (30%):
   - Did you address all major components?
   - Are there gaps in your design?
   - Did you consider edge cases?

2. **Scalability** (25%):
   - Would your system handle the stated scale?
   - How would you scale further (10x, 100x)?
   - Identified bottlenecks and solutions

3. **Reliability** (20%):
   - How would you ensure high availability?
   - Disaster recovery and failover plans
   - Data consistency and correctness

4. **Real-World Pragmatism** (15%):
   - Are decisions practical (not over-engineered)?
   - Cost considerations
   - Operational complexity

5. **Communication** (10%):
   - Clear diagrams and documentation
   - Understandable to a peer engineer
   - Reasoning explained for key decisions

---

## Presentation

You'll present your design to a peer or mentor (30 minutes):

1. **Problem Overview** (3 min): Scale, key challenges
2. **Architecture** (10 min): High-level system design with diagrams
3. **Deep Dives** (12 min): 2-3 critical components (database, caching, real-time, etc.)
4. **Questions & Discussion** (5 min): Be ready to defend choices and explore alternatives

---

## Resources

- "System Design Interview" by Alex Xu (most relevant)
- "Designing Data-Intensive Applications" by Martin Kleppmann
- High Scalability blog (case studies)
- Papers: Bigtable, Dynamo, GFS (Google/Amazon innovations)
