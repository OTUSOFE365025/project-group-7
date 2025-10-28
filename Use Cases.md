AIDAP – Use Case Scenarios

Use Case 1 – Ask Academic Question
| **Field** | **Description** |
|------------|-----------------|
| **Use case** | Ask Academic Question |
| **Summary** | Student asks a question and receives an answer that comes in real time and is accurate. |
| **Actors** | Student, AIDAP |
| **Preconditions** | We asumme the student is logged in via SSO and AIDAP is connected to LMS and Registration systems. |
| **Basic sequence** | 1. Student opens AIDAP (text or voice).<br>2. Student asks a natural-language question.<br>3. AIDAP interprets the query using AI/NLU.<br>4. AIDAP retrieves information from the LMS/Registration system.<br>5. AIDAP responds with the requested information within two seconds. |
| **Exceptions** | Step 3: Low confidence -> AIDAP asks a clarifying question.<br>Step 4: Data source unavailable -> AIDAP shows cached information and retries later. |
| **Post conditions** | Student receives an accurate answer. interaction is logged for personalization. |
| **Related Requirements** | R1, R3, R5, R6, R7, R8, RS1, RS4, RS7, RS8, RS9, RS10, RS11, RS12 |

Use Case 2 – Receive & Export Deadline Notifications
| **Field** | **Description** |
|------------|-----------------|
| **Use case** | Receive & Export Deadline Notifications |
| **Summary** | Student is notified about new or updated deadlines and can export them to a personal calendar. |
| **Actors** | Student, AIDAP |
| **Preconditions** | Student is authenticated, preferences for language and notifications are set, and system is synced with LMS. |
| **Basic sequence** | 1. AIDAP detects new or updated deadlines.<br>2. AIDAP sends a notification according to the student’s preferences.<br>3. Student opens the notification and views details.<br>4. Student selects “Export to calendar.”<br>5. AIDAP creates and exports the event successfully. |
| **Exceptions** | Step 2: Student offline -> notification queued for later delivery.<br>Step 4: Calendar export error -> display corrective instructions and retry option. |
| **Post conditions** | Event exported to the personal calendar. interaction logged. |
| **Related Requirements** | R2, R3, R6, R7, R8, RS2, RS3, RS6, RS7, RS8, RS9, RS10, RS11, RS12, RS13, RS14, RD1, RD2 |

Use Case 3 – View Personalized Dashboard
| **Field** | **Description** |
|------------|-----------------|
| **Use case** | View Personalized Dashboard |
| **Summary** | Student views a personalized dashboard that include events, announcements, and academic performance. |
| **Actors** | Student, AIDAP |
| **Preconditions** | Student is authenticated and system has the data related to the student. |
| **Basic sequence** | 1. Student opens “My Dashboard.”<br>2. AIDAP retrieves upcoming events, announcements, and analytics.<br>3. AIDAP personalizes layout and content based on history.<br>4. Dashboard displays interactive summaries and visual indicators. |
| **Exceptions** | Step 2: Some data missing -> placeholders shown until sync completes.<br>Step 3: No prior history -> default layout displayed with setup prompt. |
| **Post conditions** | Dashboard is displayed, viewing interaction logged for personalization improvements. |
| **Related Requirements** | R1, R2, R3, R6, R7, R8, RS2, RS3, RS5, RS6, RS7, RS8, RS9, RS10, RS11, RS12, RS14, RL3 |

Use Case 4 – Post Course Announcement
| **Field** | **Description** |
|------------|-----------------|
| **Use case** | Post Course Announcement |
| **Summary** | Lecturer uses AIDAP to publish or update a course announcement via conversational command. |
| **Actors** | Lecturer, AIDAP, LMS |
| **Preconditions** | Lecturer authenticated and authorized to modify the course, LMS integration active. |
| **Basic sequence** | 1. Lecturer issues announcement command (course + message).<br>2. AIDAP verifies permissions.<br>3. AIDAP previews message and target.<br>4. Lecturer confirms.<br>5. AIDAP posts the announcement to LMS and notifies students. |
| **Exceptions** | Step 2: No permission -> notify lecturer and stop action.<br>Step 5: LMS API failure -> queue and retry announcement later. |
| **Post conditions** | Announcement posted successfully and visible to students, audit entry recorded. |
| **Related Requirements** | R1, R3, R6, R8, RL1, RL2, RL8, RS2 |

Use Case 5 – Configure LMS/Calendar Integration
| **Field** | **Description** |
|------------|-----------------|
| **Use case** | Configure LMS/Calendar Integration |
| **Summary** | Administrator connects AIDAP to institutional systems such as LMS, Registration, and Calendar. |
| **Actors** | Administrator, AIDAP, LMS, Registration System |
| **Preconditions** | Administrator authenticated and has valid API credentials and policy permissions. |
| **Basic sequence** | 1. Administrator opens Integrations Console.<br>2. Enters API endpoint, keys, and sync intervals.<br>3. AIDAP validates credentials and connectivity.<br>4. Administrator saves configuration.<br>5. AIDAP enables ongoing data synchronization and monitoring. |
| **Exceptions** | Step 3: Connection fails -> show diagnostics and rollback changes.<br>Step 4: Policy violation detected -> block save and notify admin. |
| **Post conditions** | Integration successfully configured with automatic sync and monitoring enabled. |
| **Related Requirements** | R3, R7, R8, RA1, RA2, RA4, RA5, RA6, RA7, RD1, RD2, RD3, RD4, RM2, RM5 |
