# Domain-Driven Design for Connected Worker Solution Module-1

## 1. Core Domains and Subdomains
- **Core Domain:** Administrative Requests
- **Subdomains:**
  - Document Management
  - Employee Movement
  - Leave and Attendance
  - Security and Access Control

## 2. Bounded Contexts
- **Document Management Context:**
  - Pay Slip
  - Work Certificate
  - Wage Certificate
  - ....
- **AdministrativeRequestsContext:**
  - Manages the lifecycle and processing of administrative requests.
  - Entities: AdministrativeRequest, Notification

- **Employee Movement Context:**
  - Inter-site Movement Permit
  - Travel Order
  - Request for Outside Work

- **Leave and Attendance Context:**
  - Leave Request
  - Request for Correction of Clocking
  - Change of Clocking In and Out
  - Request for Leave (Holidays)

- **Security and Access Control Context:**
  - Declaration of Loss of Badge
  - Issue of Medical Certificate

## 3. Core Entities, Aggregates and Value Objects
- **Entities:**

  - **Employee:**
    - Attributes: EmployeeID, Name, Role, Category (DH, IHE, IS), etc.
    - Relationships: Can initiate multiple types of requests.
  
  - **AdministrativeRequest (Aggregate Root):**
    - Attributes: RequestID, Type, Status, CreatedDate, EmployeeID, etc.
    - Types: LeaveRequest, MovementPermit, TravelOrder, ClockingCorrection, BadgeDeclaration, MedicalCertificate, PaySlip, WorkCertificate, WageCertificate, SalaryDomiciliation, PositionConfirmation, etc.
    - Relationships: Contains details specific to each request type (e.g., LeaveDetails, ClockingDetails).
  
  - **Document:**
    - Attributes: DocumentID, Type, Status, CreatedDate, etc.
    - Relationships: Linked to AdministrativeRequests for document management.

  - **Notification:**
    - Attributes: NotificationID, Type, Status, SentDate, etc.
    - Relationships: Sent to relevant parties (e.g., Employee, Manager, HRManager).

- **Relationships Between Entities and Aggregates:**
    - Employee can initiate multiple AdministrativeRequests.
    - AdministrativeRequest can have multiple Documents associated with it.
    - Notification is sent to Employee, Manager, and HRManager for updates on AdministrativeRequest status.

- **Value Objects:**
  - **LeaveDetails**
    - Attributes: StartDate, EndDate, Reason
  - **ClockingDetails**
    - Attributes: ClockInTime, ClockOutTime

## 4. Repositories
- **EmployeeRepository:** Manages Employee data.
- **DocumentRepository:** Manages Document data.
- **RequestRepository:** Manages Request data.
- **NotificationRepository:** Manages Notification data.

## 5. Domain Services
- **DocumentService:** Handles operations related to digitalization and management of documents.
- **MovementService:** Manages inter-site movement permits and travel orders.
- **LeaveService:** Handles leave requests, clocking corrections, and holiday requests.
- **SecurityService:** Manages badge declarations and medical certificates.

## 6. Application Services
- **DocumentApplicationService:** Coordinates document-related use cases.
- **MovementApplicationService:** Coordinates employee movement-related use cases.
- **LeaveApplicationService:** Coordinates leave and attendance-related use cases.
- **SecurityApplicationService:** Coordinates security and access control-related use cases.

## 7. APIs
- **Document API:**
  - Endpoints: CreateDocument, GetDocument, UpdateDocument, DeleteDocument
- **Movement API:**
  - Endpoints: CreateMovementPermit, GetMovementPermit, UpdateMovementPermit, DeleteMovementPermit
- **Leave API:**
  - Endpoints: CreateLeaveRequest, GetLeaveRequest, UpdateLeaveRequest, DeleteLeaveRequest
- **Security API:**
  - Endpoints: CreateBadgeDeclaration, GetBadgeDeclaration, UpdateBadgeDeclaration, DeleteBadgeDeclaration

## 8. Event-Driven Architecture
- **Events:**
  - DocumentCreated
  - DocumentUpdated
  - MovementPermitCreated
  - LeaveRequestCreated
  - BadgeDeclared
- **Event Handlers:** Listens to events and triggers necessary actions (e.g., sending notifications).

## 9. Cross-Cutting Concerns
- **Logging:** Implement logging for tracking and debugging.
- **Security:** Ensure secure access to APIs and data.
- **Monitoring:** Set up monitoring for system health and performance.

## Example Use Case: Leave Request
1. **Initiate Leave Request:**
   - Employee initiates a leave request.
   - LeaveService validates the request.
   - LeaveApplicationService saves the request via RequestRepository.
   - NotificationService sends notifications to the Manager and HRManager for approval.
2. **Approve Leave Request:**
   - Manager receives a notification and approves the request.
   - LeaveService updates the request status.
   - NotificationService sends a notification to the HRManager.
3. **Finalize Leave Request:**
   - HRManager receives a notification and finalizes the request.
   - LeaveService updates the final status.
   - NotificationService sends a confirmation notification to the Employee and Guardhouse.
