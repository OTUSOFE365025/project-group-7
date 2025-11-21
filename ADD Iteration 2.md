Include in this file the 7 steps for Iteration 2

# Step 1: Reviewing Inputs

| Category | Details |
|---------|---------|
| **Design Purpose** | The purpose of this iteration is to define the structure of the NLP + AI Engine, which is one of our most critical component of the system responsible for intent detection, entity extraction, and generating natural-language responses. |
| **Primary Functional Requirements** | From the use cases that rely heavily on NLP:<br/>UC-1: Ask Academic Question<br/>UC-3: View Personalized Dashboard |

### Quality Attributes

| Scenario ID | Importance to Customer | Difficulty of Implementation |
|-------------|------------------------|-------------------------------|
| **QA-5 Usability** (correct understanding of natural-language queries) | High | High |
| **QA-1 Performance** (fast NLP processing under load) | High | Medium |
| **QA-2 Security** (ensure no sensitive data leaks through logs/model prompts) | Medium | Medium |
| **QA-4 Modifiability** (ability to update or replace AI models) | Medium | Medium |

### Constraints

| Constraint Category | Description |
|---------------------|-------------|
| **CON-3** | Must use institutional SSO. NLP can't be used otherwise. |
| **CON-2** | NLP outputs must work with formats required by downstream systems (LMS, registration). |
| **CON-7** | Must comply with institutional data-protection rules. NLP logs must avoid storing sensitive information. |

### Architectural Concerns

| Concern |
|---------|
| Need to make sure for consistent and accurate intent classification. |
| Ensuring AI model updates will not break the rest of the updates. |
| Avoiding privacy issues from storing raw user text in logs. |
| Supporting multilingual queries through the modular language-processing components in the NLP. |
| Ensuring the NLP component can scale independently under heavy query load. |

# Step 2: Choose the Iteration Goal

**Iteration Goal:**  
The goal of the second iteration will be to refine the actual structure of the NLP + AI engine. This is a core subsytem in our design that is responsble for handling user intent, extracting entities, and generating natural-language response.

**Drivers:**
- **QA-5: Usability** – The system must correctly understand most queries on the first attempt.
- **QA-1: Performance** – NLP processing must be fast enough to respond within 2 seconds.
- **QA-4: Modifiability** – The design must support updating or replacing AI models without affecting other components.
- **QA-2: Security** – User text must be handled in a way that will comply with the set privacy constraints.
- **CON-7:** Must comply with institutional data protection rules.
- **UC-1:** Ask Academic Question – Depends heavily on accurate intent/entity extraction.
- **RS4:** Multilingual query support – Requires modular language-processing structure.
- **Architectural Concern:** Ensure that the NLP subsystem can scale independently.

# Step 3: Choose One or More Elements in the System to Decompose

For this iteration, the element we want to refine is the NLP + AI Engine.

This subsystem has the following component:
- intent detection  
- entity extraction  
- dialog management  
- generating natural-language responses  
