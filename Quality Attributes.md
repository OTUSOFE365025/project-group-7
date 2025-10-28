1. Performance (Response Time)

| **Element** | **Description** |
|--------------|----------------|
| **Stimulus** | A student asks AIDAP a question like “When is my next exam?”. |
| **Environment** | Normal usage with up to 5,000 users online. |
| **Artifact** | AIDAP’s main chat system and connected APIs. |
| **Response** | The system finds and sends back the correct answer. |
| **Response Measure** | Most answers should load in about **2 seconds or less**. |

2. Security (Authentication & Privacy)

| **Element** | **Description** |
|--------------|----------------|
| **Stimulus** | A student logs in and tries to view their personal data. |
| **Environment** | Using the web, mobile, or voice version of AIDAP. |
| **Artifact** | AIDAP’s login and data protection features. |
| **Response** | The system checks login through the school’s SSO and only shows that student’s data. |
| **Response Measure** | All private info should stay protected, and any failed login attempts should be blocked and recorded. |

3. Availability

| **Element** | **Description** |
|--------------|----------------|
| **Stimulus** | A student asks something while part of the system (like the LMS) is offline. |
| **Environment** | Normal operation with a small system issue or outage. |
| **Artifact** | AIDAP’s cloud platform and backup features. |
| **Response** | The system still works by using saved or partial data instead of crashing. |
| **Response Measure** | AIDAP should stay available **99.5% of the time** each month. |

4. Modifiability (Adding New Integrations)

| **Element** | **Description** |
|--------------|----------------|
| **Stimulus** | A maintainer connects a new data source, like a library or grades system. |
| **Environment** | During a normal maintenance update. |
| **Artifact** | AIDAP’s integration and setup system. |
| **Response** | The new connection is added and goes live without downtime. |
| **Response Measure** | Updates or new integrations should take **under an hour** and not interrupt service. |

5. Usability (Conversational Experience)

| **Element** | **Description** |
|--------------|----------------|
| **Stimulus** | A student talks to AIDAP using text or voice. |
| **Environment** | Normal use on a phone, computer, or smart speaker. |
| **Artifact** | AIDAP’s chat interface and AI model. |
| **Response** | The system understands the question and answers clearly, or asks for clarification if needed. |
| **Response Measure** | About **90% of questions** should be correctly understood on the first try. |
