# 🧡 Orange Belt - Capstone Projects

Pick ONE project to graduate to the next belt.

## Project 1: Event processor
**Time**: 2-3 weeks
**Tech Stack**: Kafka/RabbitMQ, a programming language of your choice
**Concepts**: This project teaches how to build a system that processes a high volume of events asynchronously.
**Requirements**:
- A producer that sends events to a message queue.
- A consumer that reads events from the queue, processes them, and stores the result in a database.
- The system should be able to handle at least 10,000 events per second.
- Expose Prometheus metrics for event processing latency and throughput.

## Project 2: Job queue system
**Time**: 2-3 weeks
**Tech Stack**: Redis/RabbitMQ, a programming language of your choice
**Concepts**: This project is about building a system for asynchronous task processing.
**Requirements**:
- An API to enqueue new jobs.
- A worker process that dequeues jobs and executes them.
- Implement at least two different job types.
- The system should be resilient to worker crashes, with jobs being retried automatically.

## Project 3: Rate limiter with metrics dashboard
**Time**: 2-3 weeks
**Tech Stack**: A programming language of your choice, Prometheus, Grafana
**Concepts**: This project focuses on building a crucial component for system reliability and security, and monitoring it.
**Requirements**:
- A rate limiter that can be applied to API endpoints.
- The rate limiter should be configurable (e.g., number of requests per minute).
- Expose Prometheus metrics for the number of allowed and blocked requests.
- Create a Grafana dashboard to visualize the rate limiter metrics.

## Project 4: Real-time data pipeline
**Time**: 2-3 weeks
**Tech Stack**: Kafka/Kinesis, a programming language of your choice
**Concepts**: This project teaches how to build a system that collects, transforms, and stores data in real-time.
**Requirements**:
- A data source that generates a stream of events.
- A pipeline that collects the data, transforms it (e.g., filters, aggregates), and stores it in a database.
- The pipeline should be able to handle a high volume of data.
