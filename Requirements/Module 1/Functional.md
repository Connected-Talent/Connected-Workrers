### Module 1: Administrative Request Management

**Overview:**
Module 1 of the Connected Worker solution at APTIV focuses on streamlining and digitalizing administrative processes. By transitioning from paper-based to digital platforms, it enhances efficiency, reduces delays, and minimizes unnecessary employee movements, particularly for team leaders who frequently visit the HR office. This module supports APTIV’s vision for a digital, data-driven future by providing a centralized platform for managing various administrative requests.

The key features include the digitalization of administrative documents, which are accessible via kiosks and mobile devices, ensuring easy access and management. It also aims to avoid delays in document delivery, ensuring timely processing and reducing the waiting period for employees. Additionally, it reduces the need for employees, especially team leaders, to visit the HR office, saving time and increasing productivity by allowing employees to handle requests remotely.

The types of administrative requests managed include absence authorization, inter-site movement permits, travel orders, requests for outside work, corrections of clocking errors, changes in clocking in and out times, holiday leave requests, declarations of lost badges, and requests for medical certificates. These features collectively enhance the efficiency and effectiveness of administrative processes at APTIV.

**Key Features:**

1. **Digitalization of Administrative Documents:** 
   - **Platforms:** Accessible via kiosks and mobile devices.
   - **Purpose:** To replace physical documents with digital versions, ensuring easy access and management.

2. **Efficiency in Document Delivery:**
   - **Objective:** To avoid delays in the delivery of administrative documents.
   - **Benefit:** Ensures timely processing and reduces the waiting period for employees.

3. **Reduction of Employee Movements:**
   - **Focus:** Limits the need for employees, especially team leaders, to visit the HR office.
   - **Advantage:** Saves time and increases productivity by allowing employees to handle requests remotely.

**Key User Categories:**

1. **Direct Hourly Employees (DH):**
   - Production Operator (PO): the skilled workers working on production lines.
   - Can connect only to Kiosk
     
   **InDirect Hourly Employees (IH):**
   - Shift Leader (SL)*: leading the team leaders and so several production lines.
   - Team Leader (TL): leading a team in a production line (PO N+1). A team leader might lead more than one production line.
   - Support Techniciens (Maintenance, support, quality...) payed on hourly based.They can be assigned to multiple tasks per demand
   - Quatity auditor payed on hourly based.They can be assigned to multiple tasks per demand
   - Can connect to kiosk and tablet
   
3. **Indirect Salaries (IS):** Those are full time employees at APTIV
   - Production Cordinator: The shift leaders Manager. 
   - Department Manager:
   - Plant Manager: The exactuve manager of the plant/factory.

**For more details, see ListOfRoles page in the same folder (to add link)**

   ![image](https://github.com/user-attachments/assets/bf86088c-382a-441b-9479-2547a7f5601d)
  - All other Aptiv FTEs like managers, HR,....
    
## Administrative Document Requests:
   
   There are 3 types of requests to be considered:

   ### 1. Employee Administrative Documents requested only on Kiosk:*** Those are mainly administrative documents related to emplyee evidence. Those can be requested by all employee categories. Example: Work Certificate, Wage Certificate, Salary Domiciliation,..... 
   ### 2. Employee Requests:*** Those requests done by employees either from Tablets (Line Team leaders) or Desktops (Office Employees) 
         Exp: Vacacion request, Leave request, Travel Order, Outsite request, Clocking Adjustment.... 
   ### 3. Doc Templates:*** For non Digitalised documents
   
a completer par hajar et manal avec le detail des types de documents et liste des documents

## Administrative Process Descriptions:

1. **Leave Request (Autorisation d'abscence)**
   - **Description:** Request for approval of planned absences during a working day. It might be 1 or few hours of autorised time off that a worker can request. 
   - **Purpose:** Ensures that absences are documented and approved by the relevant team leader.
   - **Workflow Steps:**
      - For DH: Team Leader initiate the Leave Request via Inter-active Bornes with the presence of his Team Member.
      - For FTE they can request it directely from CW-App  
      - Manager (N+1) Approves the request once notified.
      - HR Manager Approves the request once notified.
      - A Event/notification is sent to TKS.
      - A notification is sent to Guardhouse “Poste de Grade” through email.

2. **Inter-site Movement Permit**
   - **Description:** Request for permission to move between different company sites.
   - **Purpose:** Manages and tracks employee movements for security and logistical purposes.
   - **Workflow Steps:**
      - Supervisor initiate Document Request via Inter-active Bornes with the presence of his Team Member
      - Manager Approves the request once notified
      - HR Manager Approves the request once notified
      - Install an application linked with the new system of all Guardhouse.
      - Notification be sent to the relevant Guardhouse
      
3. **Travel Order**
   - **Description:** Request for authorization to travel for work-related purposes.
   - **Purpose:** Ensures that travel is necessary and approved, and helps in planning and budgeting.
   - **Workflow Steps:**

4. **Request for Outside Work**
   - **Description:** Request to perform work outside the usual workplace.
   - **Purpose:** Facilitates remote work or off-site assignments while ensuring proper authorization.
   - **Workflow Steps:**

5. **Request for Correction of Clocking**
   - **Description:** Request to correct errors in clocking in or out times.
   - **Purpose:** Ensures accurate recording of working hours for payroll and attendance tracking.

6. **Change of Clocking In and Out**
   - **Description:** Request to change the recorded times of clocking in or out.
   - **Purpose:** Adjusts working hours to reflect actual time worked, correcting any discrepancies.

7. **Request for Leave (Holidays)**
   - **Description:** Request for approval of holiday leave.
   - **Purpose:** Manages and schedules employee holidays to ensure adequate staffing.

8. **Declaration of Loss of Badge**
   - **Description:** Report the loss of an employee identification badge.
   - **Purpose:** Ensures security by deactivating lost badges and issuing replacements.

9. **Issue of Medical Certificate**
   - **Description:** Request for a medical certificate to validate sick leave or fitness for work.
   - **Purpose:** Provides official documentation for health-related absences.

10. **Pay Slip**
    - **Description:** Request for a copy of an employee's pay slip.
    - **Purpose:** Provides employees with detailed information about their earnings and deductions.

11. **Work Certificate**
    - **Description:** Request for a certificate confirming employment status.
    - **Purpose:** Provides official proof of employment for various purposes.
    - **Workflow Steps:**
       - Supervisor initiate Document Request via Inter-active Bornes
       - Document Request should not exceed 2 Request per Month (flexible number to be introduced IN Configuration step)
       - If More, HR Approval is Mandatory
       - A message will appear indicating the data that will be inserted on the certificate according to the date of printing


12. **Wage Certificate**
    - **Description:** Request for a document attesting to an employee's wages.
    - **Purpose:** Used for financial or legal purposes, such as loan applications.
    - **Workflow Steps:**
       - Supervisor initiate Document Request via Inter-active Bornes with the presence of his Team Member
       - Document Request should not exceed 2 Request per Month
       - If More, HR Approval is Mandatory
       - A message will appear indicating the data that will be inserted on the certificate according to the date of printing

13. **Salary Domiciliation**
    - **Description:** Request to change the bank account where salary is deposited.
    - **Purpose:** Ensures that salary payments are directed to the correct bank account.
    - **Workflow Steps:**
       - Supervisor scanes Request Legalized and the RIB certificate after insert them in the Plateform
       - HR Analyst Double Checked and Approve the Request after receiving a Notification
       - Supervisor initiate Document Request via Inter-active Bornes after receiving approval from HR Analyst via Plateform
       - Print Salary Domiciliation
       - Document Request should not exceed 1 Request per Month
       - If More, HR Approval is Mandatory


14. **Request for Salary Domiciliation**
    - **Description:** Similar to Salary Domiciliation, this request is for setting up or changing the bank account for salary deposits.
    - **Purpose:** Manages the bank account details for salary payments.

15. **Position Confirmation**
    - **Description:** Request for confirmation of an employee's job position.
    - **Purpose:** Provides official documentation of an employee's role within the company.

16. **Confirmation Letter of Work Contract**
    - **Description:** Request for a letter confirming the terms of an employment contract.
    - **Purpose:** Provides official confirmation of employment terms and conditions.

17. **Prolongation of Trial Period**
    - **Description:** Request to extend the trial period of an employee.
    - **Purpose:** Allows for additional evaluation time before confirming permanent employment.

18. **Work & Salary Certificate (Anapec)**
    - **Description:** Request for a certificate detailing work and salary information, often required by Anapec (National Agency for the Promotion of Employment and Skills).
    - **Purpose:** Provides necessary documentation for employment-related processes.

19. **Request for Account Transfer**
    - **Description:** Request to transfer an employee's account details.
    - **Purpose:** Manages changes in account information for administrative purposes.

20. **Work Certificate (Leaving)**
    - **Description:** Request for a certificate confirming employment details upon leaving the company.
    - **Purpose:** Provides official documentation for former employees.

21. **Payment Request (Salary Anticipation)**
    - **Description:** Request for an advance on salary.
    - **Purpose:** Provides financial assistance to employees before the regular payday.

22. **Document for Withdrawal from the Caisse**
    - **Description:** Request for documents related to withdrawing funds from the company’s savings or pension fund.
    - **Purpose:** Manages the withdrawal process for employee savings or pension funds.

23. **Cheque Request**
    - **Description:** Request for issuing a cheque for various purposes.
    - **Purpose:** Facilitates financial transactions requiring a cheque.

24. **Request for Sanction**
    - **Description:** Request to impose a disciplinary action on an employee.
    - **Purpose:** Manages and documents disciplinary procedures.

25. **CNSS Slips Request**
    - **Description:** Request for slips from the National Social Security Fund (CNSS).
    - **Purpose:** Provides employees with official documentation of their social security contributions.

26. **Request for Use of Pool Car**
    - **Description:** Request to use a company pool car for business purposes.
    - **Purpose:** Manages the allocation and use of company vehicles.

27. **Request for Reimbursement of Taxi Expenses**
    - **Description:** Request for reimbursement of taxi expenses incurred for work-related travel.
    - **Purpose:** Ensures that employees are reimbursed for travel expenses.

**Cancelled Requests (Replaced by Desktop):**
- **Planning de Transport**
- **Demande de Changement d'Adresse**

This module is designed to enhance the overall efficiency of administrative processes, ensuring that employees can focus more on their core tasks rather than administrative formalities. By integrating these features, the Connected Worker solution aims to create a more streamlined and productive work environment.
