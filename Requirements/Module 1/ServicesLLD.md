# Module-1: Services Low Level Design

## 1. Document Management Microservice
### Responsibilities:
- Handle operations related to the digitalization and management of documents.
- Manage different types of documents such as Pay Slip, Work Certificate, and Wage Certificate.

### Core Entities:
- **Document**
  - Attributes: DocumentID, Type, Status, CreatedDate, etc.
  - Relationships: Linked to AdministrativeRequests for document management.

### APIs:
- **Document API:**
  - Endpoints:
    - `POST /documents`: Create a new document.
    - `GET /documents/{id}`: Retrieve a document by ID.
    - `PUT /documents/{id}`: Update a document by ID.
    - `DELETE /documents/{id}`: Delete a document by ID.

### Domain Services:
- **DocumentService:** Handles operations related to digitalization and management of documents.

### Repositories:
- **DocumentRepository:** Manages Document data.

### Technology Stack:
- **Programming Language:** NodeJs or C#
- **Framework:** TBD or Express.js
- **Database:** Azure Cosmos DB 
- **Messaging:** CosmosDB ChangeFeed or Azure Event Hub for event-driven communication
- **Authentication:** OAuth 2.0 / MS Entra

## 2. Employee Movement Microservice
### Responsibilities:
- Manage inter-site movement permits, travel orders, and requests for outside work.

### Core Entities:
- **AdministrativeRequest (Aggregate Root)**
  - Attributes: RequestID, Type, Status, CreatedDate, EmployeeID, etc.
  - Types: MovementPermit, TravelOrder, Request for Outside Work
  - Relationships: Contains details specific to each request type.

### APIs:
- **Movement API:**
  - Endpoints:
    - `POST /movement-permits`: Create a new movement permit.
    - `GET /movement-permits/{id}`: Retrieve a movement permit by ID.
    - `PUT /movement-permits/{id}`: Update a movement permit by ID.
    - `DELETE /movement-permits/{id}`: Delete a movement permit by ID.

### Domain Services:
- **MovementService:** Manages inter-site movement permits and travel orders.

### Repositories:
- **RequestRepository:** Manages Request data.

### Technology Stack:
- **Programming Language:** NodeJs or C#
- **Framework:** TBD
- **Database:** CosmosDB or Azure SQL
- **Messaging:** Azure Event Hub for event-driven communication
- **Authentication:** OAuth 2.0 / MS Entra

## 3. Leave and Attendance Microservice
### Responsibilities:
- Handle leave requests, clocking corrections, holiday requests, and related notifications.

### Core Entities:
- **AdministrativeRequest (Aggregate Root)**
  - Attributes: RequestID, Type, Status, CreatedDate, EmployeeID, etc.
  - Types: LeaveRequest, ClockingCorrection, Request for Leave (Holidays)
  - Relationships: Contains details specific to each request type (e.g., LeaveDetails, ClockingDetails).

### APIs:
- **Leave API:**
  - Endpoints:
    - `POST /leave-requests`: Create a new leave request.
    - `GET /leave-requests/{id}`: Retrieve a leave request by ID.
    - `PUT /leave-requests/{id}`: Update a leave request by ID.
    - `DELETE /leave-requests/{id}`: Delete a leave request by ID.

### Domain Services:
- **LeaveService:** Handles leave requests, clocking corrections, and holiday requests.

### Repositories:
- **RequestRepository:** Manages Request data.

### Technology Stack:
- **Programming Language:** NodeJs or C#
- **Framework:** TBD
- **Database:** CosmosD
- **Messaging:** Azure Event Hub for event-driven communication
- **Authentication:** OAuth 2.0 / MS Entra


### Manage badge declarations, medical certificates, and related security operations.

### Core Entities:
- **AdministrativeRequest (Aggregate Root)**
  - Attributes: RequestID, Type, Status, CreatedDate, EmployeeID, etc.
  - Types: BadgeDeclaration, MedicalCertificate
  - Relationships: Contains details specific to each request type.

### APIs:
- **Security API:**
  - Endpoints:
    - `POST /badge-declarations`: Create a new badge declaration.
    - `GET /badge-declarations/{id}`: Retrieve a badge declaration by ID.
    - `PUT /badge-declarations/{id}`: Update a badge declaration by ID.
    - `DELETE /badge-declarations/{id}`: Delete a badge declaration by ID.

### Domain Services:
- **SecurityService:** Manages badge declarations and medical certificates.

### Repositories:
- **RequestRepository:** Manages Request data.

### Technology Stack:
- **Programming Language:** NodeJs or C#
- **Framework:** TBD
- **Database:** CosmosD
- **Messaging:** Azure Event Hub for event-driven communication
- **Authentication:** OAuth 2.0 / MS Entra

## 5. Notification Microservice
### Responsibilities:
- Manage the sending of notifications to relevant parties (e.g., Employee, Manager, HRManager).

### Core Entities:
- **Notification**
  - Attributes: NotificationID, Type, Status, SentDate, etc.
  - Relationships: Sent to relevant parties.

### Domain Services:
- **NotificationService:** Manages the sending of notifications.

### APIs:
- **Notification API:**
  - Endpoints:
    - `POST /notifications`: Create a new notification.
    - `GET /notifications/{id}`: Retrieve a notification by ID.
    - `PUT /notifications/{id}`: Update a notification by ID.
    - `DELETE /notifications/{id}`: Delete a notification by ID.

### Repositories:
- **NotificationRepository:** Manages Notification data.

### Technology Stack:
- **Programming Language:** NodeJs or C#
- **Framework:** TBD
- **Database:** CosmosD
- **Messaging:** Azure Event Hub for event-driven communication
- **Notification Services:** SignalR, Azure Function/LogicApp
- **Authentication:** OAuth 2.0 / MS Entra
- **Orchestration:** Kubernetes

## 6. Administrative Requests Microservice
### Responsibilities:
- Manage the lifecycle and processing of administrative requests.

### Core Entities:
- **AdministrativeRequest (Aggregate Root)**
  - Attributes: RequestID, Type, Status, CreatedDate, EmployeeID, etc.
  - Types: LeaveRequest, MovementPermit, TravelOrder, ClockingCorrection, BadgeDeclaration, MedicalCertificate, PaySlip, WorkCertificate, WageCertificate, SalaryDomiciliation, PositionConfirmation, etc.
  - Relationships: Contains details specific to each request type.

### APIs:
- **AdministrativeRequests API:**
  - Endpoints:
    - `POST /administrative-requests`: Create a new administrative request.
    - `GET /administrative-requests/{id}`: Retrieve an administrative request by ID.
    - `PUT /administrative-requests/{id}`: Update an administrative request by ID.
    - `DELETE /administrative-requests/{id}`: Delete an administrative request by ID.

### Domain Services:
- **AdministrativeRequestsService:** Manages the lifecycle and processing of administrative requests.

### Repositories:
- **RequestRepository:** Manages Request data.

### Technology Stack:
- **Programming Language:** NodeJs or C#
- **Framework:** TBD
- **Database:** CosmosD or Azure SQL
- **Messaging:** Azure Event Hub for event-driven communication
- **Authentication:** OAuth 2.0 / MS Entra

## Cross-Cutting Concerns
- **Logging:** Implement logging for tracking and debugging.
- **Security:** Ensure secure access to APIs and data.
- **Monitoring:** Set up monitoring for system health and performance.
