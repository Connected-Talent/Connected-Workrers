### **Operator Training and Certification Process**

#### **Domain:** Training Management

#### **Process Type:** Training involving comprehension and practical tests, resulting in certification.

---

### **Step-by-Step Process**

---

#### **1. Training Scheduling**

1. **Actor:** Trainer
2. **Action:**

   - Logs into the system and schedules training for an operator.
   - Selects the operator, assigns the type of training (e.g., comprehension or practical), and specifies the date/time.

3. **Microservice Involved:** **Training Service**

   - **Function:**
     - Creates a training session.
     - Assigns the operator and tests to the session.

4. **Data Stored:** Training schedule, operator details, test type, and session details.
5. **Event Published:** `TrainingScheduled`

---

#### **2. Event Publication**

1. **Microservice:** **Training Service**
   - **Action:** Publishes the `TrainingScheduled` event.

---

#### **3. Notification to Team Leader**

1. **Microservice:** **Notification Service**

   - **Function:**
     - Subscribes to `TrainingScheduled`.
     - Sends a notification to the Team Leader and Trainer about the scheduled training session.

2. **Event Published:** `NotificationSent`

---

#### **4. Operator Takes the Comprehension Test (Facilitated by Trainer)**

1. **Actor:** Trainer

   - **Action:**
     - Administers the comprehension test to the operator manually or via a shared device (tablet/kiosk).
     - Records the operator’s responses in the system.

2. **Microservice:** **Training Service**

   - **Function:**
     - Presents the test interface.
     - Records the test responses and completion timestamp.

3. **Data Stored:** Operator’s test responses, test completion timestamp.
4. **Event Published:** `TestCompleted`

---

#### **5. Operator Takes the Practical Test (Observed by Trainer)**

1. **Actor:** Trainer

   - **Action:**
     - Observes the operator performing practical tasks.
     - Inputs the evaluation and practical test score into the system.

2. **Microservice:** **Training Service**

   - **Function:**
     - Stores the practical test results and evaluator comments.

3. **Data Stored:** Practical test score, evaluator comments.
4. **Event Published:** `TestCompleted`

---

#### **6. Result Evaluation and Certification**

1. **Actor:** Trainer

   - **Action:**
     - Reviews the operator’s test results (comprehension and practical).
     - Decides whether the operator qualifies for certification.

2. **Microservice:** **Training Service**

   - **Function:**
     - Updates the operator’s training record with the certification decision.
     - Publishes `OperatorCertified` if the operator passes.

3. **Event Published:** `OperatorCertified`

---

#### **7. Versatility Matrix Update**

1. **Microservice:** **Training Service**

   - **Function:**
     - Updates the versatility matrix to reflect the operator’s new skills and certification status.
     - Publishes `VersatilityMatrixUpdated`.

2. **Event Published:** `VersatilityMatrixUpdated`

---

#### **8. Notification to Stakeholders**

1. **Microservice:** **Notification Service**

   - **Function:**
     - Sends notifications to the Trainer, Team Leader, and Operator (via their Team Leader) about the certification outcome.

2. **Event Published:** `NotificationSent`

---

#### **9. Analytics and Reporting**

1. **Microservice:** **Analytics Service**
   - **Function:**
     - Subscribes to `OperatorCertified` and `VersatilityMatrixUpdated`.
     - Updates dashboards to reflect:
       - Training progress.
       - Operator skills and certification status.
       - Overall team versatility.

---

### **Microservices Communication Flow**

1. **Training Service** → Publishes `TrainingScheduled` → **Notification Service**
2. **Notification Service** → Notifies Team Leader and Trainer.
3. Trainer interacts with **Training Service** to record test results.
4. **Training Service** → Publishes `TestCompleted` → Updates training records.
5. **Training Service** → Evaluates results → Publishes `OperatorCertified` and `VersatilityMatrixUpdated`.
6. **Notification Service** → Sends certification results to stakeholders.
7. **Analytics Service** → Subscribes to events to update dashboards.

---

### **Key Adjustments for Operator's Non-System Access**

- **Trainer-Driven Interactions:**  
  Trainers handle all system inputs and interactions, acting on behalf of the operator.

- **Notifications Directed to Team Leader:**  
  Operators receive updates indirectly via their Team Leader, who is notified through the system.

- **Centralized Test Administration:**  
  Tests (both comprehension and practical) are facilitated by Trainers using shared devices (e.g., tablets, kiosks) at the factory site.

- **Simplified Operator Role:**  
  Operators focus solely on performing their tasks/tests, without the need to interact with the system.
