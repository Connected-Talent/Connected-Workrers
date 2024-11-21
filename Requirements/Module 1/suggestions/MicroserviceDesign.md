### Microservice Design

#### 1. **Request Service**

**Purpose:**

- Manages initiation and tracking of all requests, including those made by Team Leaders on behalf of operators.
- Supports various request types: absence authorization, holiday leave, movement requests, overtime, payroll claims, clocking corrections.

**Data Handling:**

- Stores request details, including requester and target operator.
- Manages request statuses and timestamps.

**External Interactions:**

- Communicates with **Workflow Service** to initiate workflows.
- Publishes events like `RequestCreated`, `RequestOnBehalfCreated`.

---

#### 2. **Workflow Service**

**Purpose:**

- Orchestrates approval workflows involving multiple roles (Team Leader, N+1 approvers, Trainers).
- Enforces SLAs and handles escalations.

**Data Handling:**

- Stores workflow instances and approval steps.
- Tracks progression and deadlines.

**External Interactions:**

- Interfaces with **Request**, **Training**, and **Document Services**.
- Uses Azure Durable Functions for complex workflows.

---

#### 3. **Document Service**

**Purpose:**

- Generates documents (digital and physical).
- Manages templates for instantaneous documents (e.g., payslips, work certificates).
- Handles document requests requiring physical signatures (e.g., salary domiciliation).

**Data Handling:**

- Stores document templates and metadata for generated documents.

**External Interactions:**

- Retrieves data from external systems (e.g., Workday, Payroll).
- Integrates with GED for storage.

---

#### 4. **Training Service** (New)

**Purpose:**

- Manages training programs, tests, certifications, and recertifications.
- Enables Trainers, Team Leaders, and Auditors to schedule and assign tests.
- Updates the versatility matrix upon certification.

**Data Handling:**

- Stores training schedules, test results, and operator skill levels.
- Manages operator training history.

**External Interactions:**

- Interfaces with **User Service** for operator details.
- Sends notifications via **Notification Service**.
- Publishes events like `TrainingScheduled`, `TestCompleted`, `OperatorCertified`.

---

#### 5. **Notification Service**

**Purpose:**

- Sends notifications to users (Team Leaders, N+1, Trainers, Operators).
- Manages messaging between users for clarifications.
- Alerts for SLA breaches and workflow updates.

**Data Handling:**

- Stores notification preferences and logs.

**External Interactions:**

- Subscribes to events from **Request**, **Workflow**, and **Training Services**.
- Uses Azure Service Bus for message queuing.

---

#### 6. **Analytics Service**

**Purpose:**

- Provides dashboards and reports for requests, workflows, and training progress.
- Tracks SLA compliance and identifies bottlenecks.
- Monitors operator certifications and versatility matrix updates.

**Data Handling:**

- Maintains materialized views for fast querying.
- Aggregates data from various services.

**External Interactions:**

- Consumes events for real-time analytics.
- Implements CQRS pattern.

---

#### 7. **User Service**

**Purpose:**

- Manages user authentication and authorization.
- Handles role-based access control (Team Leader, Trainer, Customer Satisfaction Auditor).

**Data Handling:**

- Stores user profiles, roles, and permissions.

**External Interactions:**

- Provides identity services to other microservices.
- Integrates with Azure AD.

---

#### 8. **Time & Services Service**

**Purpose:**

- Handles T&S-specific logic, including overtime requests and clocking corrections.
- Manages absence and movement management.

**Data Handling:**

- Stores T&S request details and statuses.

**External Interactions:**

- Works with **Request** and **Workflow Services**.
- Updates operator attendance records.

---

#### 9. **Payroll Service**

**Purpose:**

- Manages payroll-related documents and claims.
- Handles salary anticipations, payslips, and salary certificates.

**Data Handling:**

- Stores payroll request data and documentation.

**External Interactions:**

- Retrieves data from Payroll systems.
- Coordinates with **Document Service** for document generation.

---

#### 10. **Administration Service**

**Purpose:**

- Manages administrative requests, including salary domiciliation.
- Handles certifications and financial requests.

**Data Handling:**

- Stores admin request information.

**External Interactions:**

- Interfaces with **Request** and **Document Services**.

---

#### 11. **Labor Relations Service**

**Purpose:**

- Manages transportation and expense-related requests.
- Handles pool car requests and expense reimbursements.

**Data Handling:**

- Stores LR request details.

**External Interactions:**

- Coordinates with **Workflow** and **Notification Services**.
