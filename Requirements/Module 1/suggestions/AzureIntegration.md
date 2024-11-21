### Azure Integration

---

#### **Compute and Integration**

- **Azure Kubernetes Service (AKS):**

  - Hosts all microservices.
  - Ensures scalability and centralized management for the microservices architecture.

- **Azure Functions:**
  - Processes event triggers efficiently.
  - Key use cases include:
    - Handling **training completion** events.
    - Updating the **versatility matrix** when certifications are completed.

---

#### **Messaging**

- **Azure Service Bus:**

  - Provides durable messaging for commands and domain events.
  - Manages reliable communication for training-specific events, such as:
    - `TrainingScheduled`
    - `TestAssigned`
    - `TestCompleted`.

- **Azure Event Grid:**
  - Enables real-time broadcasting of training-related events.
  - Supports multiple subscribers for events like `OperatorCertified` and `SLABreached`.

---

#### **Data Storage**

- **Azure Cosmos DB:**
  - Each microservice is equipped with its own dedicated database for modularity and scalability.
  - The **Training Service** manages:
    - Training schedules.
    - Test results and operator performance data.
    - Certifications and recertifications.

---
