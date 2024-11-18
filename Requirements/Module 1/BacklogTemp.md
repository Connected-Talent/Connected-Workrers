# Sprint Backlog Proposal

# Epics

### Epic 1: Requests Microservice
### Epic 2: Employee Movement
### Epic 3: Leave and Attendance 
### Epic 4: Notification Microservice
### Epic 5: Security and Access

# Sprint Backlog for Microservices

## Sprint 1: Initial Setup and Core Functionality

### Epic 1: Requests Microservice
#### Document Management Microservice
- **Task 1:** Set up project structure and repository.
  - Set up project scaffolding
- **Task 2:** Implement basic CRUD operations for Document entity.
  - Define Document schema.
  - Implement `POST /documents` endpoint.
  - Implement `GET /documents/{id}` endpoint.
  - Implement `PUT /documents/{id}` endpoint.
  - Implement `DELETE /documents/{id}` endpoint.
- **Task 3:** Integrate Azure Cosmos DB for document storage.
  - Configure connection to Azure Cosmos DB.
  - Implement data access layer.
- **Task 4:** Set up Docker and create Dockerfile.
  - Write Dockerfile for the microservice.
  - Build and test Docker image locally.
- **Task 5:** Deploy initial version to AKS.
  - Create Kubernetes deployment and service manifests.
  - Deploy Docker image to AKS.
  - Verify deployment and basic functionality.

### Epic 2: Employee Movement
#### Employee Movement Microservice
- **Task 1:** Set up project structure and repository.
  - Set up project scaffolding.
- **Task 2:** Implement basic CRUD operations for MovementPermit entity.
  - Define MovementPermit model.
  - Implement `POST /movement-permits` endpoint.
  - Implement `GET /movement-permits/{id}` endpoint.
  - Implement `PUT /movement-permits/{id}` endpoint.
  - Implement `DELETE /movement-permits/{id}` endpoint.
- **Task 3:** Integrate Azure SQL for relational data storage.
  - Configure connection to Azure SQL.
  - Implement data access layer using Entity Framework Core.
- **Task 4:** Set up Docker and create Dockerfile.
  - Write Dockerfile for the microservice.
  - Build and test Docker image locally.
- **Task 5:** Deploy initial version to AKS.
  - Create Kubernetes deployment and service manifests.
  - Deploy Docker image to AKS.
  - Verify deployment and basic functionality.

### Epic 3: Leave and Attendance
#### Leave and Attendance Microservice
- **Task 1:** Set up project structure and repository.
  - Set up project scaffolding.
- **Task 2:** Implement basic CRUD operations for LeaveRequest entity.
  - Define LeaveRequest model.
  - Implement `POST /leave-requests` endpoint.
  - Implement `GET /leave-requests/{id}` endpoint.
  - Implement `PUT /leave-requests/{id}` endpoint.
  - Implement `DELETE /leave-requests/{id}` endpoint.
- **Task 3:** Integrate Azure SQL for relational data storage.
  - Configure connection to Azure SQL.
- **Task 4:** Set up Docker and create Dockerfile.
  - Write Dockerfile for the microservice.
  - Build and test Docker image locally.
- **Task 5:** Deploy initial version to AKS.
  - Create Kubernetes deployment and service manifests.
  - Deploy Docker image to AKS.
  - Verify deployment and basic functionality.

### Epic 4: Notification Microservice
#### Notification Microservice
- **Task 1:** Set up project structure and repository.
  - Set up project scaffolding using Express.js.
- **Task 2:** Implement basic CRUD operations for Notification entity.
  - Define Notification schema.
  - Implement `POST /notifications` endpoint.
  - Implement `GET /notifications/{id}` endpoint.
  - Implement `PUT /notifications/{id}` endpoint.
  - Implement `DELETE /notifications/{id}` endpoint.
- **Task 3:** Integrate Azure Cosmos DB for flexible schema storage.
  - Configure connection to Azure Cosmos DB.
  - Implement data access layer.
- **Task 4:** Set up Docker and create Dockerfile.
  - Write Dockerfile for the microservice.
  - Build and test Docker image locally.
- **Task 5:** Deploy initial version to AKS.
  - Create Kubernetes deployment and service manifests.
  - Deploy Docker image to AKS.
  - Verify deployment and basic functionality.

### Epic 5: Security and Access
#### Security and Access Control Microservice
- **Task 1:** Set up project structure and repository.
  - Set up project scaffolding using ASP.NET Core.
- **Task 2:** Implement basic CRUD operations for BadgeDeclaration entity.
  - Define BadgeDeclaration model.
  - Implement `POST /badge-declarations` endpoint.
  - Implement `GET /badge-declarations/{id}` endpoint.
  - Implement `PUT /badge-declarations/{id}` endpoint.
  - Implement `DELETE /badge-declarations/{id}` endpoint.
- **Task 3:** Integrate DataLayer
- **Task 4:** Set up Docker and create Dockerfile.
  - Write Dockerfile for the microservice.
  - Build and test Docker image locally.
- **Task 5:** Deploy initial version to AKS.
  - Create Kubernetes deployment and service manifests.
  - Deploy Docker image to AKS.
  - Verify deployment and basic functionality.

## Sprint 2: Authentication and Event Handling

### Epic 1: Requests Microservice
#### Document Management Microservice
- **Task 1:** Integrate Microsoft Entra for authentication.
  - Configure OAuth 2.0 / JWT authentication.
  - Implement authentication middleware.
- **Task 2:** Implement event handling for DocumentCreated and DocumentUpdated events.
  - Define event schemas.
  - Implement event producers for DocumentCreated and DocumentUpdated.
  - Implement event consumers.
- **Task 3:** Set up Azure Event Hub for event-driven communication.
  - Configure connection to Event Hub.
- **Task 4:** Implement logging and monitoring.
  - Set up logging framework (e.g., Winston).
  - Integrate with Azure Monitor for monitoring and alerting.

### Epic 2: Employee Movement
#### Employee Movement Microservice
- **Task 1:** Integrate Microsoft Entra for authentication.
  - Configure OAuth 2.0 / JWT authentication.
  - Implement authentication middleware.
- **Task 2:** Implement event handling for MovementPermitCreated event.
  - Define event schema.
  - Implement event producer for MovementPermitCreated.
  - Implement event consumer.
- **Task 3:** Set up Azure Event Hub for event-driven communication.
  - Configure connection to Event Hub.
- **Task 4:** Implement logging and monitoring.
  - Set up logging framework (e.g., Serilog).
  - Integrate with Azure Monitor for monitoring and alerting.

### Epic 3: Leave and Attendance
#### Leave and Attendance Microservice
- **Task 1:** Integrate Microsoft Entra for authentication.
  - Configure OAuth 2.0 / JWT authentication.
  - Implement authentication middleware.
- **Task 2:** Implement event handling for LeaveRequestCreated event.
  - Define event schema.
  - Implement event producer for LeaveRequestCreated.
  - Implement event consumer.
- **Task 3:** Set up Azure Event Hub for event-driven communication.
  - Configure connection to Event Hub.
- **Task 4:** Implement logging and monitoring.
  - Set up logging framework (e.g., Loguru).
  - Integrate with Azure Monitor for monitoring and alerting.

### Epic 4: Notification Microservice
#### Notification Microservice
- **Task 1:** Integrate Microsoft Entra for authentication.
  - Configure OAuth 2.0 / JWT authentication.
  - Implement authentication middleware.
- **Task 2:** Implement event handling for notification events.
  - Define event schemas.
  - Implement event producers for notification events.
  - Implement event consumers.
- **Task 3:** Set up Azure Event Hub for event-driven communication.
  - Configure connection to Event Hub.
- **Task 4:** Implement logging and monitoring.
  - Set up logging framework.
  - Integrate with Azure Monitor for monitoring and alerting.

### Epic 5: Security and Access
#### Security and Access Control Microservice
- **Task 1:** Integrate Microsoft Entra for authentication.
  - Configure OAuth 2.0 / JWT authentication.
  - Implement authentication middleware.
- **Task 2:** Implement event handling for BadgeDeclared event.
  - Define event schema.
  - Implement event producer for BadgeDeclared.
  - Implement event consumer.
- **Task 3:** Set up Azure Event Hub for event-driven communication.
  - Configure connection to Event Hub.
- **Task 4:** Implement logging and monitoring.
  - Set up logging framework (e.g., Serilog).
  - Integrate with Azure Monitor for monitoring and alerting.

## Sprint 3: Advanced Features and Testing

### Epic 1: Requests Microservice
#### Document Management Microservice
- **Task 1:** Implement advanced document management features (e.g., versioning, metadata).
  - Define versioning and metadata requirements.
  - Implement versioning and metadata features.
- **Task 2:** Write unit and integration tests.
  - Write unit tests for CRUD operations.
  - Write integration tests for event handling and advanced features.
- **Task 3:** Perform load testing and optimize performance.
  - Set up load testing environment.
  - Conduct load tests and analyze results.
  - Optimize performance based on findings.
- **Task 4:** Finalize documentation.
  - Document API endpoints.
  - Document authentication and authorization setup.
  - Document event handling and advanced features.
