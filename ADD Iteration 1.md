Include in this file the 7 steps for Iteration 1

# Step 1: Reviewing Inputs

| **Category** | **Details** |
|---------|---------|
| **Design Purpose** | AIDAP is a greenfield system that is used to help connect academic, administrative, and campus information into a single interface that can be accesed by asking question using the systems AI> The goal of this iteration 1 is to establish a high-level archectecture that will support our system needs like cloud-native, scalable, and secure system capable of integrating with multiple university platforms. |
| **Primary Functional Requirements** | From the use cases:<br>**UC-1: Ask Academic Question**.<br>**UC-2: Receive & Export Deadline Notifications**.<br>**UC-3: View Personalized Dashboard** |

### Quality Attribute Scenarios

| **Scenario ID** | **Importance to Customer** | **Difficulty of Implementation** |
|-------------|------------------------|-------------------------------|
| **QA-1 Performance** (respond in ≤ 2s) | High | Medium |
| **QA-2 Security & Privacy** (SSO + data protection) | High | High |
| **QA-3 Availability** (99.5% uptime) | High | Medium |
| **QA-4 Modifiability** (easy to add new integrations) | Medium | Medium |
| **QA-5 Usability** (natural-language chat experience) | High | High |

### Constraints

| **Constraint Category** | **Description** |
|---------------------|-------------|
| **CON-1** | Must be cloud-based so that it can be accessible via browser, mobile, and voice platforms. |
| **CON-2** | Must connect with LMS, Registration, Calendar, and Email using each system's public APIs. |
| **CON-3** | Must use institutional Single Sign-On (SSO). |
| **CON-4** | Must achieve 2-second average response time. |
| **CON-5** | Must maintain >= 99.5% uptime per month. |
| **CON-6** | Must support scalability for up to 5,000 concurrent users. |
| **CON-7** | Must comply with institutional privacy/security policies. |

### Architectural Concerns

| **Concern** |
|---------|
| Reliable synchronization between multiple external systems (LMS, Registration, Calendar). |
| Scalability during peak load (exams, registration). |
| Ensuring strict privacy and role-based access. |
| Balancing personalization with minimal sensitive data storage. |
| Designing for easy future expansion to new systems (library, email, analytics). |

# Step 2: Establish Iteration Goal by Selecting Drivers

**Iteration Goal:**  
This is the first iteration in the design of a greenfield system, so the goal of this iteration is to define the overall system structure for AIDAP.

**Drivers:**
- **QA-1: Performance** – System must respond within 2 seconds.
- **QA-2: Security & Privacy** – SSO required; user data must remain protected.
- **QA-3: Availability** – System must maintain 99.5% uptime.
- **CON-1:** Must be cloud-based and accessible via browser, mobile, and voice platforms.
- **CON-2:** Must integrate with LMS, Registration, and Calendar using their APIs.
- **CON-3:** Must use institutional Single Sign-On (SSO).
- **CON-6:** Must scale to at least 5,000 concurrent users.
- **UC-1:** Ask Academic Question.
- **UC-2:** Receive & Export Deadline Notifications (sync + notifications).
- **Architectural Concern:** Ensure reliable multi-system integration and scalable data access.

# Step 3: Choosing one or more elements in the system to decompose
As this is the first interaction, the element we want to refine is the AIDAP system.

# Step 4: Choose one or more design concepts that satisfy the selected drivers

| **Design Decision and Location** | **Rationale** |
|------------------------------|-----------|
| **Use a layered architecture** | We plan on dividing AIDAP using the a three-layered system into Presentation, Application, and Data+Intergration layers. This supports security (QA-2), performance (QA-1), and modifiability (QA-4) by isolating the UI logic from backend services and external integrations. |
| **Adopt a cloud-native model** | By running AIDAP using a cloud service we can enable automatic scaling which will help us meet our CON-6 (5,000+ users) and ensures availability targets (QA-3). This cloud infrastructure will also help support rapid updates, monitoring, and continuous deployment to help maintain and upgrade our system. |
| **Use an API Gateway within an integration layer** | Routing all LMS, Registration, Calendar, and Email requests through a dedicated integration layer will help ensure reliability and consistent error handling. This will also directly support the architectural concern of multi-system synchronization and aligns with CON-2. |
| **Use an AI-driven NLP processing pipeline** | By implementing a modular NLP pipeline (intent detection, entity extraction, dialog management), we will be able to support usability (QA-5) by improving the natural-language understanding and will allow future enhancements without redesigning the whole system. |
| **Cache frequently accessed data** | Using caching reduces response times and helps achieve the performance requirement of 2 seconds (QA-1). It also improves availability (QA-3) by allowing the system to respond even when some external services are temporarily unavailable. |
| **Implement secure authentication using SSO** | Integrating institutional Single Sign-On satisfies CON-3 and ensures that sensitive academic data remains protected (QA-2). This also will help simplify the user experience and enforces role-based access. |

# Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

| Design Decision and Location | Rationale |
|------------------------------|-----------|
| **Create a Presentation Layer** | This layer will handle all the required user interactions for students, lecturers, and administrators. It also collects natural-language input like text or voice and displays responses, notifications, and dashboards. This will supports UC-1, UC-2, and UC-3 by providing a simple interface for all user roles. |
| **Create a Data Integration Layer** | This will layer manages all communications with external systems such as LMS, Registration, Calendar, and Email. It also handles services like API calls, retries, caching, and error recovery. This directly supports CON-2 (API integration) and QA-3 (Availability). |
| **Create an NLP & AI Processing Component** | This component will be responsible for the intent detection, entity extraction, dialog management, and generating context-aware responses. It fulfills QA-5 (Usability), by enabling natural-language conversation, and supports UC-1 as the core mechanism for interpreting user questions. |
| **Database** | Stores user profiles, past interactions, preferences, cached events, and notification history. This supports R2 (historical interactions) and RS5 (personalization). Local caching improves response time (QA-1). |
| **Create an Application / Backend Logic Layer** | It will coordinates the workflows between the Presentiation Layer, the data integration layer, NLP and databases. It will contain all system logic needed. Centralizing logic here supports maintainability (QA-4) and security (QA-2). |
| **Create a Notification & Event Sync Service** | Responsible for detecting new deadlines, syncing schedules, generating reminders, and pushing notifications. This fulfills RS2, RS3, and UC-2 and ensures data consistency with external systems. |
| **Create Monitoring & Logging Services** | Tracks system health, model accuracy, latency, and error rates. This supports RM2, RM4, QA-3 (Availability), and institutional security requirements. |
