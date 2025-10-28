1. **Platform Constraint**  
The AIDAP system must be built as a cloud-based web application so that it can be accessed on any device with a browser.

2. **Integration Constraint**  
The system must connect to existing university systems like the LMS, Registration, and Calendar using their public APIs. This means it has to follow each system’s API format and update rules.

3. **Security and Privacy Constraint**  
The AIDAP system must follow the university’s privacy and data protection policies. It has to use Single Sign-On (SSO) for authentication and ensure each user only sees their own data.

4. **Performance Constraint**  
The system should give answers quickly even when many people use it. According to requirements, AIDAP should respond to most queries in under two seconds under normal conditions.

5. **Availability Constraint**  
AIDAP must stay online almost all the time. It should have 99.5% uptime per month, and if something fails, there must be a way to recover without losing data.

6. **Scalability Constraint**  
The system should handle up to 5,000 users at once without crashing or slowing down. It should be able to scale by adding more servers or instances when usage increases.

7. **Technology Constraint**  
Only approved university tools and technologies can be used. This may include the official cloud provider, database platform, and security systems already used by the institution.

8. **Maintenance Constraint**  
Updates should be done with almost instantly using a continuous deployment pipeline. All configuration changes and backups must be managed securely.
