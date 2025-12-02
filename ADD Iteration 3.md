Include in this file the 7 steps for Iteration 3
# Step 1: Reviewing Inputs

| Category | Details |
|---------|---------|
| **Design Purpose** | The purpose of this iteration is define the Data Integration Layer in more depth, which is responsible for connecting AIDAP to systems such as LMS, Registration, Calendar, and Email.  |
| **Primary Functional Requirements** | From use cases dependent on external system data:<br/>UC-1: Ask Academic Question<br/>UC-2: Receive & Export Deadline Notifications<br/>UC-3: View Personalized Dashboard |

### Quality Attributes Relevant to This Iteration

| Scenario ID | Importance to Customer | Difficulty of Implementation |
|-------------|------------------------|-------------------------------|
| **QA-3 Availability** (system should function even when external APIs fail) | High | Medium |
| **QA-1 Performance** (fast access to LMS/Registration/Calendar data) | High | Medium |
| **QA-4 Modifiability** (adding new data sources should be easy) | Medium | Medium |
| **QA-2 Security** (ensure safe handling of API keys + secure connections) | High | Medium |

### Constraints

| Constraint Category | Description |
|---------------------|-------------|
| **CON-2** | Must integrate with LMS, Registration, Calendar, and Email using their public APIs. |
| **CON-5** | Must maintain 99.5% uptime. Integration failures must not take the whole system down. |
| **CON-6** | Must scale to support up to 5,000 concurrent users making external data requests. |
| **CON-7** | Must comply with institutional data-protection rules. API credentials must be secured. |

### Architectural Concerns

| Concern |
|---------|
| Ensuring reliable synchronization across multiple external systems. |
| Ensuring external API credentials are handled securely to protect private student data. |
| Supporting easy addition of new external systems in the future without requiring major redesign. |

# Step 2: Choose the Iteration Goal

**Iteration Goal:**  
The goal of this iteration is to define the Data Integration Layer in more depth. This subsystem is responsible for communicating with external systems, handling API calls, and providing standardized output to the Application Layer.

**Drivers:**
- **QA-3: Availability** – The system must continue functioning even when external systems aren't working.
- **QA-1: Performance** – The data layer must retrieve external data quickly to make sure we maintain the 2-second response requirement.
- **QA-4: Modifiability** – The system must be easy to extend with new external integrations.
- **QA-2: Security & Privacy** – API tokens and external credentials must be handled securely.
- **CON-2:** Must integrate with LMS, Registration, Calendar, and Email using their public APIs.
- **CON-5:** System uptime requirement (99.5%) partly depends on the handling of external API failures.
- **CON-6:** Must support scaling to accommodate high request volume during peak usage.
- **Architectural Concern:** Ensure reliable synchronization across multiple external systems and allow future integrations without redesign.
- **UC-1:** Ask Academic Question – Requires reliable LMS/Registration lookups.
- **UC-2:** Receive & Export Deadline Notifications – Requires stable communication with LMS and Calendar.
- **UC-3:** View Personalized Dashboard – Requires consistent aggregation of data across systems.

# Step 3: Choose One or More Elements in the System to Decompose

For this iteration, the element we want to refine is the **Data Integration Layer**.

This subsystem includes responsibilities such as:
- handling API calls to external university systems  
- managing retries, timeouts, and error recovery  
- caching external data to improve performance  
- validating and transforming incoming data  
- providing consistent, standardized outputs to the Application Layer  

# Step 4: Choose One or More Design Concepts That Satisfy the Selected Drivers

| **Design Decision and Location** | **Rationale** |
|----------------------------------|---------------|
| **Use an API Gateway with Adapter Modules** | This will separate the integration logic from the actual Application Layer and instead allows each external system (LMS, Registration, Calendar, Email) to have its own adapter. This will support modifiability (QA-4) and also simplifies adding new external systems in the future. |
| **Implement Retry and Timeout Policies** | Make sure the system will continue functioning even when external systems arent working. This directly supports availability (QA-3) and also aligns with the concern about unreliable external APIs. |
| **Add Response Caching for External Data** | Caching frequently accessed external data will reduces load on university systems as there are less API calls and improves performance (QA-1), helping meet the 2-second response requirement. |
| **Normalize and Standardize External Data Formats** | Since each external system may return different formats then each other, a normalization layer will help make sure the Application Layer receives a more standadized format. This improves maintainability (QA-4) and reduces logic duplication. |
| **Use Secure Credential & Token Handling** | API keys and tokens are stored and used safely. This is required for QA-2 (Security & Privacy) and CON-7 (institutional data-protection rules). |
| **Introduce Fault Isolation for Each External System** | By isolating the failures to be within eacg individual adapters instead of the whole systme, AIDAP remains functional even if one external system fails. This supports availability (QA-3) and matches the concern about one system going down affecting the whole platform. |

# Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

| **Design Decision and Location** | **Rationale** |
|----------------------------------|---------------|
| **Create an API Gateway Component** | This will serve as the entry point into the Data Integration Layer. It routes requests to the correct external system adapter. This supports QA-2 and CON-2. |
| **Create LMS, Registration, and Calendar Adapter Modules** | Each external system has its own API format, authentication, and response structure. To handle this we will make adapters to handle these differences and also to convert responses into AIDAP’s internal normalized format. This supports QA-4 (Modifiability) and the concern of adding new external systems easily. |
| **Introduce a Data Normalization Component** | This component is reponsible for converting all the varied outputs from each external systems into a stadard format for the Application Layer. This simplifies backend logic, and prevents system-wide changes when external APIs evolve. |
| **Add Retry & Timeout Logic** | This will make sure to retry failing external systems or timeout if needed. This directly supports QA-3 (Availability) and the concern of unreliable external systems. |
| **Create a Response Caching Component** | It will stores frequently accessed data to reduce API calls and improve performance. Supports QA-1 by helping maintain the 2-second response requirement, and reduces load during peak times (Scalability concern). |
| **Create Credential & Token Manager** | Stores, refreshes, and securely calls API keys and access tokens for external systems. Supports QA-2 (Security) and ensures safe handling of sensitive credentials in compliance with CON-7. |
| **Add a Fault Isolation Component** | Ensures that failures in one external system do not impact others. Prevents cascading failures by isolating adapter-level errors. Supports QA-3 (Availability) and the Data Integration concern. |

# Step 6: Sketch and record the design decisions

// Gonna insert the diagram here in a future commit

# Step 7: Perform Analysis of Current Design and Review Iteration Goal and Achievement of Design Purpose

| Not Addressed | Partially Addressed | Completely Addressed | Design Decisions Made During the Iteration |
|---------------|----------------------|---------------------|--------------------------------------------|
|               | **UC-1**             |                     | The updated integration layer makes getting LMS/Registration data more reliable, which effects asking academic questions |
|               |                      | **UC-2**            | Syncing deadlines and exporting events for UC-2 are now fully supported by the new integration layer with caching and retry logic. |
|               |                      | **UC-3**            | The dashboard's requirement to compile data from several systems is fully supported by standardized and consistent data formats. |
|               | **QA-1**             |                     | Performance is largely handled by caching and reduced API calls, although more improvements such as async batching may be explored later. |
|               |                      | **QA-3**            | Availability is fully provided by retry logic, timeout restrictions, and fault isolation, preventing failures in other systems from breaking AIDAP. |
|               | **QA-4**             |                     | Modifiability is partially addressed by employing adapters that simplify integrating additional external systems; further tooling support can be enhanced in future editions. |
|               |                      | **QA-2**            | Security is fully supported by centralizing credential handling within the Credential Manager and mandating proper token usage. |
|               |                      | **CON-2**           | All integration requirements are addressed through the API Gateway and adapters. |
|               |                      | **CON-5**           | Availability expectations (99.5%) are supported through fault isolation and retry strategies. |
|               |                      | **CON-6**           | Scalability needs are supported by caching and reducing reliance on external APIs during peak load. |
