# PriceTracker — Automated Price & Availability Monitoring Service

An asynchronous price and stock monitoring backend built with **FastAPI**, **PostgreSQL**, **Celery**, and **Redis**. Users register product watches with target price or restock conditions, while scheduled background workers poll sources, record historical price observations, and trigger deduplicated alerts.

## Architecture

```text
Client / API Consumers
        │
        ▼
   FastAPI (apps/api)  ──────────►  PostgreSQL (Products, Watches, Price History, Alerts)
        │
        ▼
      Redis (Broker / State)
        │
        ▼
 Celery Worker & Beat Scheduler  ─►  Price Providers & Alert Deduplication

 

 