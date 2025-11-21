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

# Step 4: Choose One or More Design Concepts That Satisfy the Selected Drivers

| **Design Decision and Location** | **Rationale** |
|----------------------------------|---------------|
| **Use a modular NLP pipeline** | Breaking the NLP Engine into modules such as Intent Classifier, Entity Extractor, and Response Generator improves usability (QA-5) and modifiability (QA-4). Each module will can be updated or replaced without having to impact the rest of the subsystem. |
| **Add multilingual processing support** | Introducing a language-handling layer will enable AIDAP to be more versatile. Making this modular also enhances long-term maintainability. |
| **Implement caching for repeated AI/NLP operations** | Caching model outputs reduces repeated computation. This improves performance (QA-1), especially under high load. |
| **Introduce an internal privacy filter** | A component that will preprocess all data to remove or masks sensitive information in user queries supports QA-2 (Security & Privacy) and CON-7. This will ensures no sensitive data enters logs or training feedback. |
| **Allow configurable AI model versions inside the subsystem** | A configuration approach (e.g., selecting intent model v1.2, entity model v1.1) supports QA-4 (Modifiability) by enabling safe model updates without disrupting other system components. |

# Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

| **Design Decision and Location** | **Rationale** |
|----------------------------------|---------------|
| **Create an Intent Classification Module** | This module will be responsible for identifying what the user is trying to do. Accurate intent classification directly impacts usability (QA-5) and is essential for UC-1. |
| **Create an Entity Extraction Module** | This module will extracts key details from the user query. This will help allows the Application Layer to request the correct data from external systems. Supports usability (QA-5) and performance (QA-1) by narrowing the context. |
| **Create a Multilingual Preprocessing Component** | Handles language detection and normalizing it, enabling AIDAP to support multi-language queries. Keeping this separate increases modifiability (QA-4). |
| **Create a Privacy Filter** | Removes or masks sensitive information before the query is logged or processed further. Supports QA-2 (Security & Privacy) and helps meet CON-7. |
| **Create a Response Generation Component** | Converts structured data from the Application Layer into a clear, conversational response. This maintains usability (QA-5) and improves consistency. |
| **Create a Model Configuration** | Allows the component to load specific intent/entity model versions. Supports QA-4 (Modifiability) by enabling safe upgrades without having to affect the overall system. |
| **Create Caching Support for NLP Outputs** | Caches repeated computations such as embeddings or frequent intents to help reduce processing time. Supports QA-1 (Performance) and ensures faster response times during peak usage. |

# Step 6: Sketch and record the design decisions

<img width="766" height="375" alt="image" src="https://github.com/user-attachments/assets/877ed1dd-5538-47bc-abe0-3ea15a392e00" />

# Step 7: Perform Analysis of Current Design and Review Iteration Goal and Achievement of Design Purpose

| Not Addressed | Partially Addressed | Completely Addressed | Design Decisions Made During the Iteration |
|---------------|----------------------|------------------------|--------------------------------------------|
|               |                      | **UC-1**                  | By refining the NLP Engine, we support the UC-1 by improving the intent detection and entity extraction, which in hand will allow AIDAP to better interpret academic questions. |
|               |                      | **RS4**                   | The addition of a language handler component, we are fully supporting the multi-language query handling capabilities. |
|               | **QA-1**             |                           | Performance is partially addressed through NLP caching. |
|               |                      | **QA-5**                  | Usability is fully supported by introducing accurate intent classification, entity extraction, sanitization, and structured response generation. |
|               | **QA-4**             |                           | Modifiability is partially addressed by modularizing the NLP pipeline and adding model versioning. |
|               |                      | **QA-2**                  | Security and privacy are fully supported through the privacy filter. |
|               |                      | **CON-7**                 | The privacy filter ensures compliance with institutional data-protection rules within the NLP subsystem. |

