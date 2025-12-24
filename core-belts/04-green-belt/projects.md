# 💚 Green Belt - Capstone Projects

Pick ONE project to graduate to the next belt.

## Project 1: 3-service microservices system
**Time**: 3-4 weeks
**Tech Stack**: A programming language of your choice, Docker, a message queue
**Concepts**: This project is a deep dive into microservices, service-to-service communication, and distributed tracing.
**Requirements**:
- Build a system composed of three independent microservices (e.g., user, order, and inventory).
- Services should communicate with each other, both synchronously (e.g., REST/gRPC) and asynchronously (e.g., Kafka).
- Implement distributed tracing to trace requests across all three services.
- Each service should have its own database.
- Use an API gateway to route requests to the appropriate service.

## Project 2: API gateway routing to 2+ backend services
**Time**: 2-3 weeks
**Tech Stack**: An API gateway (e.g., Kong, Traefik), two backend services
**Concepts**: This project focuses on the role of an API gateway in a microservices architecture.
**Requirements**:
- Set up an API gateway.
- Create two backend services.
- Configure the API gateway to route requests to the backend services based on the request path.
- Implement authentication and rate limiting at the gateway level.

## Project 3: Event-sourcing proof of concept
**Time**: 3-4 weeks
**Tech Stack**: A programming language of your choice, a message queue
**Concepts**: This project explores the event-sourcing pattern.
**Requirements**:
- Build a service that uses event sourcing to store the state of an aggregate.
- All changes to the state should be stored as a sequence of events.
- Implement a way to rebuild the current state of an aggregate by replaying the events.
- Implement a separate read model that is updated asynchronously from the events.

## Project 4: Database sharding for 1M+ records
**Time**: 3-4 weeks
**Tech Stack**: A database that supports sharding (e.g., Vitess, Citus), a programming language of your choice
**Concepts**: This project is about scaling a database by sharding it.
**Requirements**:
- Design a sharding strategy for a large dataset (1M+ records).
- Implement the sharding strategy.
- Write queries that span multiple shards.
- Benchmark the performance of the sharded database and compare it to a non-sharded database.
