*Intuz — Your automation partner, one workflow at a time.*

<p align="center">
  <picture>
    <img alt="Banner Image" src="https://github.com/user-attachments/assets/210f97fc-0fce-404a-b647-7dfe1302cd37" />
  </picture>
</p>

[Intuz](https://www.intuz.com) helps organizations orchestrate AI, automation, and enterprise systems through scalable workflows. Our repository showcases proven implementations across healthcare, operations, customer support, document processing, sales, and back-office functions, enabling teams to accelerate automation initiatives without starting from scratch.

[N8N Creator](https://n8n.io/creators/intuz/) · [AI Consulting](https://www.intuz.com/ai-transformation-services/) · [AI Workflow Automation](https://www.intuz.com/workflow-automation-services/) · [For Custom Workflow Automation](https://www.intuz.com/get-started/)

# Screen and rank CVs using Gmail, OpenAI, Airtable, and Slack

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

- [ScopeStorage](https://github.com/Intuz-production/ScopeStorage)
- [Enrich LinkedIn leads with Apify career data, then draft Gemini-personalized outreach emails into Google Sheets — research to campaign-ready drafts, automatically.](https://github.com/Intuz-production/LinkedIn-Lead-Generation-Automation)
- [Audio Trimmer Android](https://github.com/Intuz-production/Audio-Trimmer-Android)

[See all of Intuz's free n8n templates](https://www.intuz.com/n8n-workflow-automation-templates/)

## Connect with us

Intuz is a USA-based AI & workflow automation company with 16+ years of experience building custom AI-enabled workflow automations for SMBs and Enterprises, specializing in agentic AI, LLM integrations, and CRM/ERP sync across Healthcare, FinTech, eCommerce, Manufacturing, and Real Estate.

* **Website:** [https://www.intuz.com](https://www.intuz.com)
* **Email:** [getstarted@intuz.com](mailto:getstarted@intuz.com)
* **LinkedIn:** https://www.linkedin.com/company/intuz/
* **Get Started:** https://n8n.partnerlinks.io/intuz

## For Custom Workflow Automation

[Click here - Get Started](https://www.intuz.com/get-started/)
