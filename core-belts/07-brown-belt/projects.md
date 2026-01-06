# 🤎 Brown Belt - Capstone Projects

Pick ONE project to graduate to the next belt.

## Project 1: Sharded user service
**Time**: 6-8 weeks
**Tech Stack**: A database that supports sharding (e.g., Vitess, Citus), a programming language of your choice
**Concepts**: This project is a deep dive into database sharding and building a system that can handle a massive number of users.
**Requirements**:
- Design and implement a sharded user service that can handle 100M+ users.
- Use hash-based sharding to distribute users across shards.
- Implement a shard routing layer that can route requests to the correct shard.
- Implement a system for rebalancing shards as the number of users grows.

## Project 2: Multi-region architecture
**Time**: 6-8 weeks
**Tech Stack**: A cloud provider (e.g., AWS, GCP), a database that supports multi-region replication (e.g., CockroachDB, Spanner)
**Concepts**: This project is about building a system that is highly available and resilient to regional outages.
**Requirements**:
- Deploy a service to multiple regions.
- Use a database that supports multi-region replication.
- Implement a system for failing over to another region in the event of a regional outage.
- Implement a system for routing traffic to the closest region.

## Project 3: Consensus system
**Time**: 6-8 weeks
**Tech Stack**: A programming language of your choice
**Concepts**: This project is a deep dive into distributed consensus and building a system that is fault-tolerant.
**Requirements**:
- Implement a simplified version of a consensus algorithm like Raft or Paxos.
- The system should be able to elect a leader.
- The system should be able to replicate a log of commands across all nodes.
- The system should be able to tolerate the failure of a minority of nodes.

## Project 4: Event-sourcing system with CQRS
**Time**: 6-8 weeks
**Tech Stack**: A programming language of your choice, a message queue, a database
**Concepts**: This project is about building a system that uses event sourcing and CQRS to achieve high scalability and performance.
**Requirements**:
- Build a service that uses event sourcing to store the state of an aggregate.
- All changes to the state should be stored as a sequence of events.
- Implement a separate read model that is updated asynchronously from the events (CQRS).
- Implement a system for replaying events to rebuild the read model.
