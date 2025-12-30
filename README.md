# Lead-qualification-agent

# 📝 Form Submission → AI Processing → Sheets Automation (n8n Workflow)

This workflow automatically captures form submissions, cleans the data, optionally validates existing rows in Google Sheets, and then sends processed information to Google Gemini AI for structured output — which is finally saved back to Google Sheets.

# 🚀 What This Workflow Does

Listens for form submissions (e.g., Webhooks, Typeform, Google Form frontend)

Cleans & formats the submitted data

Checks Google Sheets to see if the entry already exists (duplicate prevention)

Uses Google Gemini AI to:

extract structured info

enrich the data

generate formatted final output

Saves results to Google Sheets (append row)

Ignores duplicate or invalid entries via a “do nothing” branch

# 🧩 Workflow Logic
Step	Description
🟢 On Form Submission	Trigger – workflow starts when someone submits a form
✏️ Clean Data	Standardizes input fields before use
📄 Get Row(s) in Sheet	Checks Google Sheet for matching data (duplicates)
🔀 IF Condition	If form entry already exists → stop workflow
⛔ No Operation	Ends execution cleanly if duplicate / false branch
🤖 AI Agent (Gemini)	Processes and structures submission using AI
<> Structured Output Parser	Converts AI text output → usable JSON
📊 Append Row in Sheet	Saves cleaned + AI-enhanced data

# 🛠️ Requirements
Service Needed	Purpose
n8n (self-hosted or cloud)	Automation engine
Google Sheets API credentials	Read + write spreadsheet data
Google Gemini API Key	AI data enrichment
(Optional) Form Webhook URL	To connect UI form to this workflow

# 🔧 Setup Instructions

1️⃣ Import JSON file of this workflow into n8n
2️⃣ Configure:Google Sheets credentials Gemini API credentials Form POST/Webhook connection
3️⃣ Update Google Sheet fields:
Sheet ID Columns mapping in Get Row(s) and Append Row
4️⃣ Test: submit a form → AI result should be appended to sheet

# 🧠 AI Output Example

Gemini transforms input like this:
Input:
Name: Ajay
Email: ajay@example.com
Message: I’m interested in AI automation

Output Parsed JSON:

{
  "name": "Ajay",
  "email": "ajay@example.com",
  "category": "AI lead",
  "priority": "Medium",
  "notes": "Interested in automation services"
}

# 🐞 Troubleshooting
Issue	Solution
Data not writing to sheet	Verify credentials + sheet column names
Duplicate entries still being added	Adjust IF condition matching field
AI output empty	Check Gemini API key & structured parser
Wrong sheet being referenced	Update spreadsheet ID in nodes
