# 💙 Blue Belt - Capstone Projects

Pick ONE project to graduate to the next belt.

## Project 1: Payment processing system
**Time**: 4-6 weeks
**Tech Stack**: A programming language of your choice, a database, a message queue, a payment provider (e.g., Stripe)
**Concepts**: This project is a deep dive into building a reliable and secure payment processing system.
**Requirements**:
- An API to create and manage payments.
- Idempotency for all API endpoints that create or update resources.
- A system for handling webhooks from the payment provider.
- A secure way to store and manage API keys and other secrets.
- A monitoring and alerting system to detect and respond to payment failures.

## Project 2: Real-time analytics dashboard
**Time**: 4-6 weeks
**Tech Stack**: A programming language of your choice, a real-time database (e.g., ClickHouse, Druid), a message queue
**Concepts**: This project is about building a system that can ingest and query a large volume of data in real-time.
**Requirements**:
- A data ingestion pipeline that can handle high-throughput writes.
- A real-time database to store the data.
- A dashboard to visualize the data in real-time.
- The system should be able to handle a high volume of concurrent queries.

## Project 3: Content delivery system
**Time**: 4-6 weeks
**Tech Stack**: A programming language of your choice, a CDN (e.g., Cloudflare, Fastly), a caching layer (e.g., Redis)
**Concepts**: This project is about building a system that can deliver content to users quickly and reliably.
**Requirements**:
- A system for uploading and storing content.
- A CDN to cache and deliver the content.
- A caching layer to cache frequently accessed content.
- A system for invalidating the cache when the content is updated.

## Project 4: Rate limiting at scale
**Time**: 4-6 weeks
**Tech Stack**: A programming language of your choice, a distributed caching layer (e.g., Redis)
**Concepts**: This project is about building a distributed rate limiter that can handle a large volume of requests.
**Requirements**:
- A rate limiter that can be applied to API endpoints.
- The rate limiter should be distributed and work across multiple instances of the service.
- The rate limiter should be configurable (e.g., number of requests per minute).
- The rate limiter should be able to handle a large volume of requests.
