# AI Lead Qualification & Outreach Agent

An end-to-end AI-powered lead qualification and outreach workflow built with **n8n, Google Gemini, Google Sheets, and Gmail**.

The agent receives a new business lead, evaluates its qualification signals, assigns an AI score and category, generates evidence-based reasoning and a recommended action, creates a personalized outreach email, sends the email automatically, and records the final email status.

---

## 🚀 What This Project Does

The workflow automates the early-stage lead qualification process.

Instead of manually reviewing every incoming lead, the system:

1. Detects a new lead in Google Sheets.
2. Sends the lead information to an AI Agent.
3. Evaluates the lead across multiple qualification dimensions.
4. Generates a score from **1–10**.
5. Classifies the lead as **HOT, WARM, or COLD**.
6. Generates evidence-based reasoning.
7. Recommends the next business action.
8. Creates a personalized B2B email.
9. Sends the email through Gmail.
10. Updates the lead's email status to **Sent**.

---

## 🏗️ Architecture

```text
                    New Lead
                       │
                       ▼
              ┌─────────────────┐
              │  Google Sheets  │
              │     Trigger     │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │     AI Agent    │
              └────────┬────────┘
                       │
              ┌────────┴────────┐
              ▼                 ▼
       ┌─────────────┐   ┌─────────────────┐
       │   Google    │   │    Structured   │
       │   Gemini    │   │  Output Parser  │
       └──────┬──────┘   └────────┬────────┘
              └──────────┬────────┘
                         ▼
                ┌─────────────────┐
                │  Update Lead    │
                │   in Sheets     │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │      Gmail      │
                │  Send Outreach  │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Update Status   │
                │   → Sent        │
                └─────────────────┘

## 🧠 AI Qualification Framework

The AI Agent evaluates each lead across five dimensions:

1. Decision-Making Authority

The agent considers the lead's job title and evaluates whether they appear to have purchasing influence.

Examples of stronger authority signals:

Founder
Co-Founder
CEO
Owner
Director
Head of Department
2. Business / Problem Fit

The agent evaluates whether the stated business problem is realistically suitable for AI automation.

Examples include:

Repetitive manual work
Lead qualification
Customer support
Document processing
Information extraction
Workflow coordination
Reporting
Research
Repetitive communication
3. Problem Severity & Volume

The agent considers:

Task frequency
Number of items processed
Repetitive workload
Operational complexity
Whether the problem is recurring

The agent does not invent savings, revenue, ROI, or productivity improvements.

4. Budget Signal

A stated budget is treated as a signal of purchasing intent.

The agent does not assume that the provided budget is sufficient for implementation and does not invent pricing.

5. Timeline / Urgency

The implementation timeline is evaluated as a buying-intent signal.

For example:

Immediately
This week
Within 2 weeks
Within 1 month

indicate stronger urgency than an unspecified future timeline.

📊 Lead Scoring

The agent produces a score from 1–10.

Score	Category	Meaning
9–10	HOT	Excellent qualification signals
8	HOT	Strong lead with minor uncertainty
6–7	WARM	Potentially valuable but with missing/moderate signals
4–5	WARM	Weak or uncertain qualification
1–3	COLD	Poor fit or insufficient evidence

The agent is instructed not to assign a high score simply because someone is a founder, works in SaaS, has a large company, or provides a budget.

📤 Structured AI Output

The AI Agent produces:

{
  "ai_score": 9,
  "lead_category": "HOT",
  "ai_reasoning": "...",
  "recommended_action": "...",
  "personalized_email": "..."
}

This structured output is then used by the downstream automation.

✉️ Automated Outreach

After qualification, the workflow generates a personalized B2B email using:

Lead name
Company
Stated business problem
Potential AI automation approach
Low-pressure call to action

The workflow then sends the generated email through Gmail.

After successful delivery, the Google Sheet is updated:

Email Status → Sent
🛡️ Anti-Hallucination Rules

The agent is explicitly instructed not to invent:

Company revenue
Company growth
Customer numbers
Conversion rates
ROI
Cost savings
Existing software
Technology stack
Meeting dates
Meeting times
Pricing
Implementation guarantees

When information is missing, the agent is instructed to account for the uncertainty instead of assuming the best case.

🧰 Tech Stack
n8n — Workflow orchestration
Google Gemini — LLM reasoning and generation
Google Sheets — Lead database and workflow trigger
Gmail — Automated personalized outreach
Structured Output Parser — Reliable machine-readable AI output
🔄 Workflow
New Lead
   ↓
Google Sheets Trigger
   ↓
AI Lead Qualification
   ↓
Google Gemini
   ↓
Structured Output
   ↓
Lead Database Update
   ↓
Personalized Email
   ↓
Gmail
   ↓
Email Status = Sent
🧪 Example Use Case

A business submits a lead with information such as:

Name: Alex
Company: Example SaaS
Job Title: Founder
Industry: SaaS
Company Size: 25
Problem: Manually qualifying 100 leads every week
Budget: ₹50,000
Timeline: Within 1 month

The agent evaluates the available evidence and produces a qualification score, category, reasoning, recommended next action, and personalized outreach.

📁 Repository Structure
ai-lead-qualification-agent/
│
├── README.md
│
└── ai-lead-qualification-agent.json

The JSON file contains the sanitized n8n workflow that can be imported into an n8n environment and connected to the user's own credentials and Google Sheet.

⚙️ Setup
1. Import the workflow

Import:

ai-lead-qualification-agent.json

into n8n.

2. Configure credentials

Connect your own:

Google Sheets credential
Google Gemini credential
Gmail credential
3. Configure Google Sheets

Replace:

YOUR_GOOGLE_SHEET_ID

with your own Google Sheet.

4. Configure the lead columns

The workflow expects fields including:

name
email
company
job title
Industry
Company size
problem
budget
time line
AI score
AI category
AI reasoning
recommended action
Personalized Email
Lead ID
Email Status
created at
5. Test

Add a test lead to the configured Google Sheet and verify:

Lead detected
    ↓
AI qualification
    ↓
Sheet updated
    ↓
Email generated
    ↓
Email sent
    ↓
Status = Sent
🔐 Security

The workflow repository does not contain the actual Google, Gemini, or Gmail credentials.

Users should configure their own credentials when importing the workflow.

Never commit:

API keys
OAuth secrets
Passwords
Access tokens
.env files
Private credentials
Real customer data
🎯 Project Outcome

This project demonstrates how an LLM can be integrated into a real business workflow rather than being used only as a standalone chatbot.

The agent combines:

Reasoning + Structured Output + Workflow Automation + External Actions + State Updates

to create an end-to-end AI-powered business process.

👩‍💻 Author

Karunya

AI Automation Developer
