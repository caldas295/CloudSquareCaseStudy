**📄 Salesforce Application Intake - Design & Implementation**

**1\. Design Solution**

**🌐 Experience Cloud (LWR)**

- **CloudsquareGustavoCaldasStudyCase**  
    Public Experience Cloud site developed to allow external partners to submit applications through a user-friendly interface.

**⚡ Lightning Web Components (LWC)**

- **applicationHomeScreen**  
    Home screen of the application site, providing entry point and basic information.
- **applicationFormScreen**  
    Application form screen responsible for collecting applicant data and submitting it to Salesforce.

**🧠 Apex Classes**

- **ApplicationFormController**  
    Acts as the controller for the LWC, delegating requests to the business layer.
- **ApplicationFormBO**  
    Contains the core business logic responsible for:
  - Matching existing Accounts
  - Creating an Opportunity when a match is found
  - Creating a Lead when no match exists
- **AccountDAO**  
    Responsible for querying the Account object based on matching rules (Federal Tax ID or Company Name).
- **ApplicationServiceWebHook**  
    Public REST endpoint that allows external systems to submit applications via webhook.
- **FormDTO**  
    Data Transfer Object responsible for mapping and transporting application data across layers.
- **ApplicationException**  
    Custom exception class used to handle controlled error scenarios.

**🧩 New Custom Fields**

**Account**

- **Federal Tax Id (FederalTaxId_\_c)**  
    Type: Text  
    Configuration: External ID
- **Company Name (CompanyName_\_c)**  
    Type: Text

**Lead**

- **Federal Tax Id (FederalTaxId_\_c)**  
    Type: Text

**2\. Key Tradeoffs**

The solution prioritizes clarity and maintainability over complexity.  
Business rules and matching logic were implemented in Apex rather than declarative tools to keep the behavior explicit and easy to evolve.

Both the LWC and the REST webhook reuse the same business logic to avoid duplication and ensure consistent processing across all submission channels.  
The user interface was intentionally kept simple, focusing only on data collection, while all validations and decisions are enforced server-side.

Public access is handled using controlled server-side logic, balancing simplicity and security for this exercise.

**3\. One Thing Intentionally Not Implemented**

Authentication for the REST webhook was intentionally not implemented.  
For the scope of this exercise, the endpoint is publicly accessible to simplify external integrations and focus on the core business logic and data processing flow.

All validations and decision-making are enforced server-side to ensure data consistency.  
In a real production scenario, this endpoint would be protected using authentication mechanisms such as OAuth 2.0, API keys, or a signed webhook strategy to prevent unauthorized access and abuse.
