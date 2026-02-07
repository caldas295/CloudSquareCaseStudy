**🚀 Deployment & Configuration Guide**

**1\. Deploy Metadata**

**Deploy the following components to the target Salesforce org:**

**🌐 Experience Cloud Site**

- **CloudsquareGustavoCaldasStudyCase**

**🧠 Apex Classes**

- **ApplicationFormController**
- **ApplicationFormBO**
- **AccountDAO**
- **ApplicationServiceWebHook**
- **FormDTO**
- **ApplicationException**

**⚡ Lightning Web Components**

- **applicationHomeScreen**
- **applicationFormScreen**

**🧩 Custom Fields**

**Account**

- **FederalTaxId_\_c (Text, External ID)**
- **CompanyName_\_c (Text)**

**Lead**

- **FederalTaxId_\_c (Text)**

**2\. Guest User Configuration**

**To allow public access:**

- **Go to Setup → Digital Experiences → All Sites**
- **Open the site → Administration → Members**
- **Ensure Guest User Access is enabled**
- **Open the Guest User Profile**
- **Grant access to:**

**Apex Classes**

- **ApplicationFormController**
- **ApplicationFormBO**
- **AccountDAO**
- **ApplicationServiceWebHook**
- **FormDTO**
- **ApplicationException**

**Objects**

- **Lead (Create)**
- **Opportunity (Create)**
- **Account (Read)**

**3\. Webhook (REST API) Configuration**

**After deployment, the webhook endpoint will be available at:**

**https://&lt;your-domain&gt;.my.salesforce.com/services/apexrest/applications**

**or for Experience Cloud:**

**https://&lt;site-domain&gt;/services/apexrest/applications**

**HTTP Method**

- **POST**

**Request Body (JSON)**

**{**

**"companyName": "Acme Corp",**

**"email": "<contact@acme.com>",**

**"phone": "123456789",**

**"firstName": "John",**

**"lastName": "Doe",**

**"federalTaxId": "123456789",**

**"annualRevenue": 1000000**

**}**

**4\. Testing**

**LWC / UI**

- **Access the Experience Cloud site URL**
- **Fill in the application form**
- **Verify Lead or Opportunity creation**

**Webhook**

- **Use Postman or a similar tool**
- **Send a POST request to the REST endpoint**
- **Validate response status and created records**

**5\. Notes & Considerations**

- **The webhook is public and unauthenticated for the scope of this exercise**
- **In production, authentication mechanisms such as OAuth 2.0 or API keys should be implemented**
- **All business logic and validations are enforced server-side**
