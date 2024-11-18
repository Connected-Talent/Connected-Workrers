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
  - Issue of Medical Certificate
  - Declaration of Loss of Badge

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

## 8. Event and Commands
- **Events:**
  - DocumentCreated
  - DocumentUpdated
  - MovementPermitCreated
  - LeaveRequestCreated
  - BadgeDeclared
  - TravelOrderApproved
  - SalaryDomiciliationInitiated
- **Event Handlers:** Listens to events and triggers necessary actions (e.g., sending notifications).
- **Commands:** CreateLeaveRequest, ApproveTravelOrder, InitiateSalaryDomiciliation, etc.

## 9. Cross-Cutting Concerns
- **Logging:** Implement logging for tracking and debugging.
- **Security:** Ensure secure access to APIs and data.
- **Monitoring:** Set up monitoring for system health and performance.

## 10. Use Cases for Each Feature

- **Leave Request:**
  - InitiateLeaveRequest: Employee initiates a leave request.
  - ApproveLeaveRequest: Manager and HRManager approve the leave request.
  - NotifyLeaveRequestStatus: Send notifications to Employee and relevant parties.

- **Travel Order:**
  - InitiateTravelOrder: Employee initiates a travel order request.
  - ApproveTravelOrder: Manager and HRManager approve the travel order.
  - NotifyTravelOrderStatus: Send notifications to Employee and relevant parties.

- **Salary Domiciliation:**
  - InitiateSalaryDomiciliation: Employee initiates a salary domiciliation request.
  - ApproveSalaryDomiciliation: HR Analyst double-checks and approves the request.
  - NotifySalaryDomiciliationStatus: Send notifications to Employee and relevant parties.

- **Position Confirmation:**
  - InitiatePositionConfirmation: Employee initiates a position confirmation request.
  - ApprovePositionConfirmation: Manager and HRManager approve the request.
  - NotifyPositionConfirmationStatus: Send notifications to Employee and relevant parties.

- **Work & Salary Certificate (Anapec):**
  - InitiateWorkSalaryCertificate: Employee initiates a request for a work and salary certificate.
  - ApproveWorkSalaryCertificate: HRManager approves the request.
  - NotifyWorkSalaryCertificateStatus: Send notifications to Employee and relevant parties.

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
