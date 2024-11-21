### **Work Certificate Request (Requires Printing)**

**Domain:** Administration  
**Document Type:** Physical document requiring printing and physical signature (due to legal requirements).

---

### **Step-by-Step Process**

---

#### **1. Request Initiation**

- **Actor:** Team Leader
- **Action:**

  - Logs into the system via a kiosk or tablet.
  - Selects "Work Certificate" from the list of available documents.

- **Microservice Involved:** Request Service
- **Function:**
  - Creates a new request for a work certificate, either on behalf of an operator or for themselves.
  - **Data Stored:**
    - Requester ID, operator ID (if on behalf), document type, and timestamp.

---

#### **2. Event Publication**

- **Event:** `RequestCreated`
- **Microservice:** Request Service
- **Action:** Publishes the event to the message broker (Azure Service Bus).

---

#### **3. Workflow Initiation**

- **Microservice:** Workflow Service
- **Function:**

  - Subscribes to `RequestCreated` events specific to work certificates.
  - Initiates an approval workflow if necessary.

- **Data Stored:**
  - Workflow instance details with approval steps.

---

#### **4. Approval Process**

- **Microservice:** Workflow Service
- **Action:**

  - Determines HR approval is required.
  - Sends a task to the HR Analyst for approval.

- **Notification:**
  - **Microservice:** Notification Service
  - **Function:** Sends notification to the HR Analyst.
  - **Event:** `NotificationSent`

---

#### **5. HR Approval**

- **Actor:** HR Analyst
- **Action:** Logs into the system and approves the request.
- **Microservice:** Workflow Service
- **Function:**
  - Updates workflow status upon approval.
  - **Event:** `WorkflowApproved`

---

#### **6. Document Generation**

- **Microservice:** Document Service
- **Function:**

  - Subscribes to `WorkflowApproved` events.
  - Generates the work certificate using the appropriate template.

- **Data Retrieval:** Fetches necessary data from external systems (e.g., HR system) via APIs or replicated data.
- **Data Stored:** Document metadata and the generated document (PDF ready for printing).

---

#### **7. Printing and Physical Signature**

- **Microservice:** Document Service
- **Action:**

  - Flags the document as requiring printing and a physical signature.
  - Triggers a notification to the responsible department for printing and signing.

- **Notification:**
  - **Microservice:** Notification Service
  - **Function:** Sends a notification to administrative staff.

---

#### **8. Document Ready for Pickup**

- **Actor:** Administrative Staff
- **Action:**

  - Prints the document.
  - Obtains the required physical signatures.

- **Microservice:** Document Service
- **Action:** Updates the document status to "Ready for Pickup."
- **Event:** `DocumentReady`

---

#### **9. Notification to Requester**

- **Microservice:** Notification Service
- **Function:** Sends a notification to the Team Leader that the document is ready for pickup.
- **Event:** `NotificationSent`

---

#### **10. Request Completion**

- **Actor:** Team Leader
- **Action:**

  - Picks up the document.
  - Hands it over to the operator if requested on their behalf.

- **Microservice:** Request Service
- **Function:** Marks the request as "Completed."

---

### **Microservices Communication Flow**

1. **Request Service** → Publishes `RequestCreated` → **Workflow Service**
2. **Workflow Service** → Sends task → **Notification Service** → Notifies HR Analyst
3. **Workflow Service** → Upon approval, publishes `WorkflowApproved` → **Document Service**
4. **Document Service** → Generates document, publishes `DocumentReady` → **Notification Service**
5. **Notification Service** → Notifies Team Leader

---
