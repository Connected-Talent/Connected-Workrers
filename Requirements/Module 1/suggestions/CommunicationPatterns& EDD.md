### Communication Patterns and Event-Driven Design

---

#### **2. Communication Patterns**

##### **Event-Driven Architecture**

**Asynchronous Messaging:**

- Services communicate using domain events for decoupled interactions.
- New events introduced specifically for training processes (e.g., `TrainingScheduled`, `TestAssigned`, `TestCompleted`).

**Azure Service Bus:**

- Enables reliable, FIFO (First In, First Out) messaging between services.

---

##### **gRPC Direct Communication**

**Synchronous Calls:**

- Used for scenarios requiring immediate data retrieval.
- Example: **Training Service** retrieves operator profiles from the **User Service**.

---

##### **Azure Services Integration**

- **Azure Service Bus:**
  - Facilitates command and event messaging between services.
- **Azure Event Grid:**
  - Used for real-time broadcasting of training-related events.
- **Azure Functions:**
  - Processes events such as training results and updates to the versatility matrix.

---

#### **2. Event-Driven Design**

##### **Key Domain Events**

| **Event**                    | **Description**                                       |
| ---------------------------- | ----------------------------------------------------- |
| **RequestCreated**           | Triggered when a new request is initiated.            |
| **RequestOnBehalfCreated**   | When a Team Leader creates a request for an operator. |
| **WorkflowStarted**          | Indicates the start of an approval workflow.          |
| **WorkflowApproved**         | Marks the completion of an approval step.             |
| **TrainingScheduled**        | A training session has been scheduled.                |
| **TestAssigned**             | An operator has been assigned a test.                 |
| **TestCompleted**            | An operator has completed a test.                     |
| **OperatorCertified**        | An operator has been certified or recertified.        |
| **VersatilityMatrixUpdated** | Updates the versatility matrix for an operator.       |
| **SLABreached**              | SLA threshold has been breached.                      |
| **NotificationSent**         | A notification has been dispatched.                   |

---

##### **Event Propagation**

**Publishing Events:**

- **Training Service:** Publishes events related to training processes (e.g., `TrainingScheduled`, `TestCompleted`).
- **Request Service:** Publishes events for newly created requests, including `RequestOnBehalfCreated`.

**Subscribing to Events:**

- **Notification Service:** Subscribes to events like `SLABreached`, `WorkflowApproved` to send user updates.
- **Analytics Service:** Consumes all events for real-time data aggregation and visualization.

---

##### **Handling Eventual Consistency and Retries**

**Eventual Consistency:**

- Accepts temporary inconsistencies during event propagation.
- UI design accommodates potential delays in data updates (e.g., loading indicators or last updated timestamps).

**Retries:**

- Implements retry policies for transient failures to ensure reliability.
- Utilizes **dead-letter queues** for unprocessed or failed messages.
