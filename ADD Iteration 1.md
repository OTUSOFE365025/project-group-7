Include in this file the 7 steps for Iteration 1

# Step 1: Reviewing Inputs

| **Category** | **Details** |
|---------|---------|
| **Design Purpose** | AIDAP is a greenfield system that is used to help connect academic, administrative, and campus information into a single interface that can be accesed by asking question using the systems AI> The goal of this iteration 1 is to establish a high-level archectecture that will support our system needs like cloud-native, scalable, and secure system capable of integrating with multiple university platforms. |
| **Primary Functional Requirements** | From the use cases:<br>**UC-1: Ask Academic Question**.<br>**UC-2: Receive & Export Deadline Notifications**.<br>**UC-3: View Personalized Dashboard** |
| **Quality Attribute Scenarios** | See table below. |

### Quality Attribute Scenarios

| **Scenario ID** | **Importance to Customer** | **Difficulty of Implementation** |
|-------------|------------------------|-------------------------------|
| **QA-1 Performance** (respond in ≤ 2s) | High | Medium |
| **QA-2 Security & Privacy** (SSO + data protection) | High | High |
| **QA-3 Availability** (99.5% uptime) | High | Medium |
| **QA-4 Modifiability** (easy to add new integrations) | Medium | Medium |
| **QA-5 Usability** (natural-language chat experience) | High | High |

### Constraints

| Constraint Category | Description |
|---------------------|-------------|
| **CON-1** | Must be cloud-based so that it can be accessible via browser, mobile, and voice platforms. |
| **CON-2** | Must connect with LMS, Registration, Calendar, and Email using each system's public APIs. |
| **CON-3** | Must use institutional Single Sign-On (SSO). |
| **CON-4** | Must achieve 2-second average response time. |
| **CON-5** | Must maintain >= 99.5% uptime per month. |
| **CON-6** | Must support scalability for up to 5,000 concurrent users. |
| **CON-7** | Must comply with institutional privacy/security policies. |

### Architectural Concerns

| Concern |
|---------|
| Reliable synchronization between multiple external systems (LMS, Registration, Calendar). |
| Scalability during peak load (exams, registration). |
| Ensuring strict privacy and role-based access. |
| Balancing personalization with minimal sensitive data storage. |
| Designing for easy future expansion to new systems (library, email, analytics). |
