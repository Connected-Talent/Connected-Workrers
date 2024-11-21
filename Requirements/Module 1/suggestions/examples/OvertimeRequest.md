### Refactored Process: Overtime Request by Team Leader on Behalf of Operator

**Domain:** Time & Services (T&S)  
**Document Type:** Workflow document requiring approval.

---

### **Step-by-Step Process**

---

#### **1. Request Initiation**

1. **Actor:** Team Leader
2. **Action:**

   - Logs into the system via a tablet/kiosk.
   - Selects the "Overtime Request" option.
   - Enters the operator's details, specifies the date and overtime hours, and provides a justification.

3. **Microservice Involved:** **Request Service**

   - **Function:**
     - Creates a new overtime request.
     - Links the request to the operator and stores overtime details.

4. **Data Stored:** Operator ID, request details (date, overtime hours, justification), and timestamps.
5. **Event Published:** `OvertimeRequestCreated`

---

#### **2. Workflow Initiation**

1. **Microservice:** **Workflow Service**

   - **Function:**
     - Subscribes to `OvertimeRequestCreated` events.
     - Initiates a two-step approval workflow involving:
       - N+1 Manager.
       - HR Analyst.

2. **Data Stored:** Workflow instance details, SLA timers, approval progress.

---

#### **3. Approval Process - N+1 Manager**

1. **Microservice:** **Notification Service**

   - **Function:**
     - Sends a notification to the N+1 Manager about the pending overtime request.

2. **Actor:** N+1 Manager

   - **Action:**
     - Logs into the system.
     - Reviews the request and provides approval/rejection along with comments.

3. **Microservice:** **Workflow Service**
   - **Function:**
     - Updates the workflow status based on the N+1 Manager's decision.

---

#### **4. Approval Process - HR Analyst**

1. **Microservice:** **Notification Service**

   - **Function:**
     - Sends a notification to the HR Analyst once the N+1 Manager approves.

2. **Actor:** HR Analyst

   - **Action:**
     - Logs into the system.
     - Reviews the request and provides final approval/rejection.

3. **Microservice:** **Workflow Service**
   - **Function:**
     - Updates the workflow status to "Approved" or "Rejected."
     - Publishes `WorkflowApproved` if approved.

---

#### **5. Payroll Records Update**

1. **Microservice:** **Payroll Service**

   - **Function:**
     - Subscribes to `WorkflowApproved` events.
     - Updates payroll records to include approved overtime hours.

2. **Data Stored:** Operator's overtime details, date, approved hours, and payroll adjustments.

---

#### **6. Notification to Stakeholders**

1. **Microservice:** **Notification Service**

   - **Function:**
     - Sends a notification to the Team Leader and Operator about the final decision (approved or rejected).

2. **Event Published:** `NotificationSent`

---

#### **7. Request Completion**

1. **Microservice:** **Request Service**
   - **Function:**
     - Marks the overtime request as "Completed" in the system.

---

---

### **Microservices Communication Flow**

1. **Request Service** → Publishes `OvertimeRequestCreated` → **Workflow Service**
2. **Workflow Service** → Initiates workflow → Sends tasks → **Notification Service**
3. **Notification Service** → Notifies N+1 Manager and HR Analyst
4. **N+1 Manager and HR Analyst** → Interact with **Workflow Service**
5. **Workflow Service** → Publishes `WorkflowApproved` → **Payroll Service**
6. **Payroll Service** → Updates payroll records
7. **Notification Service** → Sends final notifications to Team Leader and Operator
8. **Request Service** → Marks request as "Completed"

---

### **Summary of Microservices Involvement**

#### **1. Request Service**

- Handles request creation and updates request statuses.
- Publishes `OvertimeRequestCreated` and `RequestCompleted`.

#### **2. Workflow Service**

- Manages approval workflows (steps, SLA timers, escalations).
- Publishes `WorkflowApproved` or `WorkflowRejected`.

#### **3. Notification Service**

- Sends notifications to relevant actors (Team Leader, N+1 Manager, HR Analyst, Operator).

#### **4. Payroll Service**

- Updates payroll records for approved overtime requests.

#### **5. Analytics Service**

- Tracks workflow durations, approvals, and SLA compliance for overtime requests.

---

### **Key Adjustments Made**

1. **Operator Involvement Removed:**

   - Team Leader manages all interactions with the system on behalf of the operator.

2. **Workflow Optimization:**

   - Focused on essential actors (Team Leader, N+1 Manager, HR Analyst).

3. **Enhanced Communication:**

   - Notifications ensure all stakeholders remain informed throughout the process.

4. **Event-Driven Architecture:**
   - Decoupled services rely on published events for seamless integration and extensibility.
