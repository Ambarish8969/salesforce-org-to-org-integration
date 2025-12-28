# Salesforce Org-to-Org Integration

📌 Project Overview

This project demonstrates a secure Salesforce-to-Salesforce integration where Cases created in Org A are sent to Org B using OAuth-based authentication and REST Apex.

The integration follows Salesforce-recommended best practices by leveraging:

* Connected App (Org B)

* Auth Provider (Org A)

* Named Credentials (Org A)

* REST Apex (@RestResource)

* JSON-based data exchange

This is a real-world, enterprise-level integration pattern commonly used in multi-org Salesforce implementations.

🏗️ Architecture Overview

Org A (Source Org)

* Detects newly created Case records

* Sends Case data via REST callout

* Uses Named Credential for authentication

⬇️

Org B (Target Org)

* Exposes REST endpoint using Apex

* Receives Case data

* Inserts records into Salesforce

Authentication is handled using OAuth 2.0, ensuring secure communication between both orgs.

<img width="900" height="700" alt="Org to Org Architecture Daigram" src="https://github.com/user-attachments/assets/f38f36c0-13af-42ba-8e03-d74438fc2c47" />

🔐 Authentication & Security Design
1️⃣ Connected App (Org B)

* Acts as the OAuth client

* Provides Consumer Key & Consumer Secret

* Controls API access scope

2️⃣ Auth Provider (Org A)

* Stores Consumer Key & Secret securely

* Handles OAuth authorization and token management

* Represents Org B inside Org A

3️⃣ Named Credential (Org A)

* Uses Auth Provider for authentication

* Eliminates hardcoded credentials

* Automatically injects access tokens during callouts

This design ensures:
✔ No credentials in code
✔ Centralized authentication
✔ Easy token refresh & maintenance

🔄 Integration Flow

1. A Case is created in Org A

2. Apex service queries newly created Cases

3. Case data is serialized into JSON

4. REST callout is made using Named Credential

5. Org B receives the request via REST Apex

6. Cases are created in Org B

7. Optional post-processing can be triggered using Queueable Apex

📤 Org A – Source Org Logic

Purpose

* Fetch newly created Case records

* Prepare JSON payload

* Send data securely to Org B

Key Concepts Used

* Named Credential

* HTTP Callout

* JSON Serialization

* Bulk-safe processing

📌 Source Code
org-a-source/apex/SendCasesToOrgBService.cls

📥 Org B – Target Org Logic

Purpose

* Expose REST API endpoint

* Deserialize incoming Case data

* Insert records into Salesforce

* Return success or error response

Key Concepts Used

* REST Apex (@RestResource)

* JSON Deserialization

* Bulk record insertion

* Error handling

📌 Source Code
org-b-target/apex/CaseInboundService.cls

🔍 Verifying the Integration Output

To verify the project output:

1. Create a test Case in Org A

2. Execute the SendCasesToOrgBService class manually

3. Navigate to Org B and confirm the Case has been created

For automation, this process can also be scheduled to run at defined intervals instead of manual execution.

🧠 Key Learnings

* How to integrate two Salesforce orgs securely

* Practical use of Connected Apps and OAuth

* Benefits of Auth Providers over hardcoded credentials

* How Named Credentials simplify callouts

* Designing scalable REST Apex integrations

* Real-world enterprise integration patterns

🎯 Use Cases

* Multi-org Salesforce architecture

* Centralized case management

* Salesforce system integrations

* Interview and portfolio demonstration

* Enterprise-grade API design examples

🚀 Enhancements (Future Scope)

* Add HttpCalloutMock test classes

* Schedule integration using Scheduled Apex

* Bi-directional org synchronization

* Add retry logic and logging framework

* Flow-triggered integration
