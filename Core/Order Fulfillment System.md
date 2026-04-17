🌱 I am taking on this project to deepen my understanding of event-driven architecture.

# High-Level Architecture

The system uses a "Hybrid Event Mesh" approach.

- **EventBridge** handles "Orchestration Events" (routing between disparate services).
- **Kafka** handles "Stream Events" (detailed, high-frequency state changes).
- **Redis** acts as a shared fast-access state store (e.g., current inventory levels or payment status).

# Event Flow Design
- **Placement:** **Order Service** receives a request, generates a `UUID`, and produces an `OrderPlaced` event to the **Kafka** `orders` topic.
- **Inventory Check:** **Inventory Service** (a Lambda mapped to the Kafka topic) reads the event. It checks **Redis** for stock:
    - _If available:_ Decrements Redis and emits `InventoryReserved` to **EventBridge**.
    - _If unavailable:_ Emits `OrderFailed` to EventBridge.
- **Payment Processing:** **EventBridge** routes `InventoryReserved` to the **Payment Service**. This service simulates a bank call and emits `PaymentCompleted` or `PaymentFailed`.
- **Finalization & Alerting:** **Notification Service** has EventBridge rules to "listen" for `PaymentCompleted` or `OrderFailed` to log the final status.

# Project Tasks & Workflow
1. **EventBridge:** Create your custom EventBridge Bus first.
2. **Lambda:** Complete the Create Function process you have already started.
3. **Connectivity:**
    - Add an **EventBridge Rule** (in the EventBridge console) to trigger your Lambda from the bus.
    - Add a **Kafka Trigger** (in the Lambda console) to create the Event Source Mapping for your Kafka topic.