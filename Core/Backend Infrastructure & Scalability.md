**Infra**: like roads, power, water supply, pipelines etc. In software world, we have data center, network cable, database etc.

**Scalability**: often comes with "peak time", when it is high volume, we need **more server instances** for that particular period, but **not always**.

# What is the scalability issue
Given a scenario, during a sudden rainstorm in KL, high volume of **matching drivers** & passengers raised up in **Grab** app, while user profile & reward page are remain as normal usage.   

# How Grab handle it
- **microservice:** modular services (e.g. rides, payments, location, drivers, user profile & reward)
- **load balancing** & containerization (Docker & Kubernetes for different microservices)
- **Dynamic recourse adjustment**: Grab's "Trident" system adjusts the active **goroutine** based on events from **Kafka** 
