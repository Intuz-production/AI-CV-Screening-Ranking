# Screen and rank CVs using Gmail, OpenAI, Airtable, and Slack

An automated workflow that screens and ranks CVs received via Gmail or Google Drive using OpenAI, scores candidates against Airtable job descriptions, updates Airtable pipelines, and sends notifications through Slack and Gmail.

**Import this workflow:** [n8n.io template](https://n8n.io/workflows/19925-screen-and-rank-cvs-using-gmail-openai-airtable-and-slack/) · [workflow.json](workflow.json)  
**Built by [Intuz](https://www.intuz.com/n8n-workflow-automation-templates/)**, n8n Creator. Need it customized? [Talk to us](https://www.intuz.com/get-started/).

<!-- ![Screen and rank CVs using Gmail, OpenAI, Airtable, and Slack workflow in the n8n editor](workflow-canvas.png) -->

## Quick overview

This workflow screens CVs received via Gmail (or an optional Google Drive folder), extracts and parses resume text with OpenAI, scores candidates against a job description stored in Airtable, writes results to an Airtable pipeline, and posts notifications to Slack and sends booking emails.

## How it works

1. Triggers when a new Gmail message arrives with an attachment (or, if enabled, when a file is created in a specific Google Drive folder).
2. Detects whether the attachment is a PDF or DOCX and extracts the CV text accordingly.
3. Uses OpenAI to parse the CV text into structured JSON fields like experience, skills, education, and projects while discarding protected attributes.
4. Fetches the active job description (and optional booking link) from an Airtable Config table and combines it with the parsed candidate data.
5. Uses OpenAI to score the candidate against the job description and returns a score, strengths, gaps, recommendation, and screening questions.
6. Creates a new record in an Airtable Pipeline table with the candidate details, scoring output, and a mapped status.
7. Routes outcomes by recommendation: posts shortlisted and “needs review” candidates to Slack, emails shortlisted candidates a booking link via Gmail, and holds rejected candidates in Airtable without sending notifications.
8. Runs every Monday morning to pull the last 7 days of Airtable pipeline records, compute totals and average score, and post a weekly digest to Slack.

## Setup

1. Connect credentials for Gmail, OpenAI, Airtable (Personal Access Token), and Slack.
2. In Airtable, create/configure a Config table with an `active` field and a job description field (plus an optional `booking_link`), and ensure exactly one record is marked `active = 1`.
3. In Airtable, create/configure the Pipeline table with the fields mapped in the workflow (for example Name, Email, Score, Recommendation, Status, Applied At, Strengths, and Gaps) and update the base/table IDs if yours differ.
4. Choose a single intake source by keeping the Gmail trigger active or enabling the Google Drive trigger and setting the folder ID to watch.
5. Set the Slack channel used for shortlist alerts, manual review posts, and the weekly digest, and confirm the booking URL included in the Config record is the one you want candidates to use.

## Requirements

- Credentials: Gmail, OpenAI, Airtable PAT, Slack
- Airtable Config: active, job_description, optional booking_link
- Airtable Pipeline: Name, Email, Score, Recommendation, Status, Applied At, etc.
- Slack hiring channel
- Booking URL is just a link in Config — no Calendly credential

## FAQ

**What triggers the workflow to start screening CVs?**  
The workflow triggers when a new Gmail message arrives with an attachment or when a file is created in a specific Google Drive folder if enabled.

**How does the workflow score candidates?**  
It uses OpenAI to parse CV text and score candidates against a job description stored in Airtable, providing a score, strengths, gaps, recommendation, and screening questions.

**How are candidates notified about their status?**  
Shortlisted and 'needs review' candidates are posted to Slack, shortlisted candidates receive booking emails via Gmail, and rejected candidates are held in Airtable without notifications.

## Related n8n templates from Intuz

- [Review contract risks and route approvals with Google Drive, OpenAI, and Gmail](https://github.com/Intuz-production/Legal-document-review-automation)
- [Route lead reply follow-up tasks by intent with Gmail, OpenAI, Pipedrive, and Slack](https://github.com/Intuz-production/AI-Lead-Follow-Up-Routing)
- [Answer internal policy questions from Google Drive with OpenAI and Qdrant](https://github.com/Intuz-production/Policy-Q-A-with-AI)

[See all of Intuz's free n8n templates](https://www.intuz.com/n8n-workflow-automation-templates/)

## About Intuz

<p align="center">
  <img alt="Intuz: your automation partner, one workflow at a time" src="https://github.com/user-attachments/assets/210f97fc-0fce-404a-b647-7dfe1302cd37" />
</p>

Intuz is a USA-based AI & workflow automation company with 16+ years of experience building custom AI-enabled workflow automations for SMBs and Enterprises, specializing in agentic AI, LLM integrations, and CRM/ERP sync across Healthcare, FinTech, eCommerce, Manufacturing, and Real Estate.

- [Free n8n workflow templates from Intuz](https://www.intuz.com/n8n-workflow-automation-templates/)
- [Intuz on n8n.io](https://n8n.io/creators/intuz/)
- [Workflow automation services](https://www.intuz.com/workflow-automation-services/)
- [AI consulting company](https://www.intuz.com/ai-transformation-services/)
- [Try n8n Cloud (Intuz partner link)](https://n8n.partnerlinks.io/intuz)
- Email: [getstarted@intuz.com](mailto:getstarted@intuz.com)
- LinkedIn: [linkedin.com/company/intuz](https://www.linkedin.com/company/intuz/)

## Need a custom workflow?

[Talk to Intuz about a custom n8n or AI workflow](https://www.intuz.com/get-started/)
