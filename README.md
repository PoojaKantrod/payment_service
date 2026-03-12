Payment Service – Idempotent Payment Processing with Redis

Overview

This project implements a Payment Processing Service built using Spring Boot, PostgreSQL, and Redis to demonstrate how idempotency can be implemented in distributed systems.

In real-world payment systems, duplicate requests may occur due to:
	•	Network retries
	•	Client timeouts
	•	API gateway retries
	•	Users clicking the payment button multiple times

Without idempotency protection, the same payment could be processed multiple times, which is unacceptable for financial transactions.

This service prevents duplicate payments using Redis-based idempotency keys.

-----
System Architecture:
Client
  │
  │  HTTP Request (Idempotency-Key)
  ▼
Spring Boot REST Controller
  │
  ▼
Payment Service
  │
  │  Check Idempotency Key
  ▼
Redis (SETNX)
  │
  ├── Key Exists → Reject Duplicate Request
  │
  └── Key Not Found
          │
          ▼
      PostgreSQL Database
          │
          ▼
      Payment Created


--------
Key Features
	•	Idempotent payment processing
	•	Redis-based duplicate request protection
	•	RESTful API using Spring Boot
	•	PostgreSQL persistence
	•	Clean layered architecture
	•	Demonstrates distributed system reliability patterns

-------
How Idempotency Works

The client sends a unique Idempotency-Key with each payment request.

Example request header: Idempotency-Key: payment-123

The system performs the following steps:
	1.	Check Redis for the key using SETNX (Set If Not Exists).
	2.	If the key already exists → request is considered a duplicate.
	3.	If the key does not exist → process the payment.
	4.	Store the key in Redis with a TTL to prevent duplicates for a time window.

This guarantees that only one payment is processed per idempotency key.

-------
Running the Application

Prerequisites
	•	Java 17
	•	Maven
	•	PostgreSQL
	•	Redis

-------


