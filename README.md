# HVAC Business Automation — n8n AI Workflow

## Function
Automatically captures client inquiries submitted through the website consultation form, classifies the request using AI, logs all client information into the Notion CRM database, and sends a personalized confirmation email, ensuring every lead is recorded and acknowledged instantly.

## Workflow
<img width="1647" height="372" alt="image" src="https://github.com/user-attachments/assets/5dfaa871-e0ae-4241-b1ba-224fbd4b92e7" />

## Showcase Video: https://youtu.be/JieOKJ_F2bg

## How it works
**Trigger:** Customer submits an inquiry simulating real form posted on the website via hosted n8n form

1. **Form Submission Node**: Captures structured inquiry data from a branded contact form (Name, Company, Role, Email, Phone, Project Details)
2. **1st AI Agent Node**: This agent classifies the inquiry and extracts three fields: Job Title (2-3 words), Service Type (Installation / Repair / Maintenance), and Job Type (Residential / Commercial)
3. **Code Node**: A JavaScript Code node parses the AI output into structured fields
4. **Notion Job Record Node**: Creates a detailed job record in Notion with all extracted and form fields populated automatically
5. **2nd AI Agent Node**: This agent generates a warm, personalized acknowledgement email written as a Customer Representative (e.g, Sarah M.) from the company
6. **Gmail Node**: Sends the email to the customer via Gmail
7. **Notion Job Update Node:** Update job status in Notion

**Error Handling:**

- Notion Create retries up to 3 times on failure
- Gmail retries up to 2 times on failure

## Technical Highlights
- **Local AI inference:** used Ollama with llama3.1 running locally inside Docker, keeping the entire stack free and private
- **Structured AI output parsing:** prompted the AI to return multi-field structured data and parsed it with a custom JavaScript Code node

## Stack Breakdown
| Tool    | Role | Cost |
| :-------- | :------- | :------- |
| n8n (self-hosted) |	Workflow automation engine | Free
Ollama + llama3.1	| Local AI model for email generation and classification	| Free
Notion | CRM database and job logging	 | Free
Gmail API |	Sending automated emails via OAuth2 |	Free
Google Cloud Console | OAuth2 credentials for Gmail	| Free
Docker |	Running n8n container with persistent volume | Free
