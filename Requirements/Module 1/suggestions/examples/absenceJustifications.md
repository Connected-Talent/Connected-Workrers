### **Process Overview**

This process manages the submission and validation of medical certificates for absence justifications. The flow begins when the **operator** physically submits their medical certificate to the **nurse**, who scans, validates, and initiates the digital workflow.

---

### **Step-by-Step Workflow**

#### **1. Operator Submission:**

- **Actor:** Operator
- **Action:** Submits a physical medical certificate to the Nurse at the site/factory.
- **Outcome:** Physical handoff of the certificate.

---

#### **2. Medical Certificate Handling (Nurse):**

1. **Scanning and Uploading:**

   - **Actor:** Nurse
   - **Action:**
     - Scans the physical medical certificate.
     - Uploads the scanned document to the system.
   - **Microservice:** **Document Service**
     - **Function:** Handles the scanned document, applies OCR to extract key details (e.g., absenteeism period, employee name).
     - **Event Published:** `DocumentUploaded`
     - **Data Stored:** Scanned certificate, extracted absenteeism period, employee ID.

2. **Absenteeism Period Input:**
   - **Actor:** Nurse
   - **Action:**
     - Confirms or adjusts the absenteeism period suggested by OCR.
     - Inputs the absenteeism period into the system.
   - **Microservice:** **Request Service**
     - **Function:** Creates a new absence justification request.
     - **Event Published:** `AbsenceRequestCreated`
     - **Data Stored:** Request details, absenteeism period, operator details.

---

#### **3. Workflow Initiation (System):**

- **Microservice:** **Workflow Service**
  - **Function:** Subscribes to `AbsenceRequestCreated`.
  - **Action:**
    - Initiates an approval workflow with tasks for HR and the operator’s N+1 Manager.
    - Updates the workflow instance with the statuses.
  - **Event Published:** `WorkflowStarted`

---

#### **4. Stakeholder Notifications:**

- **Notification Triggered Automatically:**
  - **Stakeholders Notified:**
    - **TKS Responsible:** For updating external systems like Optitime (time management system).
    - **Team Leader:** For informational purposes about the operator's absence.
  - **Microservice:** **Notification Service**
    - **Function:** Sends real-time notifications to stakeholders.

---

#### **5. HR and Manager Approvals:**

1. **HR Analyst Approval:**

   - **Actor:** HR Analyst
   - **Action:**
     - Logs into the system and reviews the absence justification.
     - Approves or rejects the justification.
   - **Microservice:** **Workflow Service**
     - **Function:** Updates the workflow status based on HR’s decision.

2. **N+1 Manager Approval:**
   - **Actor:** N+1 Manager
   - **Action:**
     - Logs into the system, reviews the absence details, and approves/rejects.
   - **Microservice:** **Workflow Service**
     - **Function:** Updates the workflow status to "Approved" after final approval.
     - **Event Published:** `WorkflowApproved`

---

#### **6. Attendance Record Update:**

- **Microservice:** **Time & Services Service**
  - **Function:** Subscribes to `WorkflowApproved`.
  - **Action:**
    - Updates the operator’s attendance records to reflect the approved absence period in the time management system (Optitime).
  - **Event Published:** `AttendanceUpdated`

---

#### **7. Request Completion:**

- **Actor:** System
- **Microservice:** **Request Service**
  - **Function:** Marks the absence request as "Completed."
  - **Outcome:** Workflow is closed.

---

### **Key Functionalities and Microservices Involved**

#### **1. Document Service**

- Scans and stores medical certificates.
- Integrates OCR for automated data extraction.
- Publishes events such as `DocumentUploaded`.

#### **2. Request Service**

- Creates and manages absence justification requests.
- Publishes `AbsenceRequestCreated`.

#### **3. Workflow Service**

- Manages the approval process.
- Subscribes to events like `AbsenceRequestCreated`.
- Publishes workflow-related events such as `WorkflowStarted` and `WorkflowApproved`.

#### **4. Notification Service**

- Sends notifications to stakeholders (HR, Team Leader, TKS Responsible).
- Ensures stakeholders are informed about critical updates.

#### **5. Time & Services Service**

- Updates attendance and absenteeism records in external systems (e.g., Optitime).
- Ensures accurate tracking of absences.

---

### **Microservices Communication Flow**

1. **Document Service** → Publishes `DocumentUploaded` → **Request Service**
2. **Request Service** → Publishes `AbsenceRequestCreated` → **Workflow Service**
3. **Workflow Service** → Initiates approval tasks → **Notification Service**
4. **Notification Service** → Notifies HR, N+1 Manager, and Team Leader
5. **HR and Manager Approvals** → Update workflow status → **Workflow Service**
6. **Workflow Service** → Publishes `WorkflowApproved` → **Time & Services Service**
7. **Time & Services Service** → Updates attendance records
8. **Notification Service** → Sends final notification to stakeholders
9. **Request Service** → Marks request as "Completed"

---

### **Key User Stories**

1. **Nurse Scanning and Uploading:** Simplifies digitization of physical medical certificates with OCR support.
2. **Stakeholder Notifications:** Ensures HR, TKS Responsible, and Team Leader are kept informed in real-time.
3. **Accurate Attendance Updates:** Automates attendance records to minimize errors and delays.

This revised process ensures a smooth workflow from certificate submission to request completion while maintaining communication across all stakeholders.
