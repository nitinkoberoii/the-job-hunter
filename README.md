# 🤖 Automated Job-Hunting Workflow (n8n + AI)

This project is an **end-to-end automated job-hunting assistant** built with [n8n](https://n8n.io).  
It runs daily, scrapes LinkedIn for fresh jobs, evaluates them using **Google Gemini AI**, writes tailored cover letters, and sends the best matches to **Telegram** — completely hands-free.

---

## 🧠 Overview

**Workflow:**
<img width="1756" height="783" alt="Screenshot 2025-10-30 170758" src="https://github.com/user-attachments/assets/7218b48f-1192-47a8-923d-2038b0279401" />

🎥 **Watch the video walkthrough:** [Google Drive Video Link](https://drive.google.com/file/d/1cdOf60Nj9X1pxR84WCJPxm2G3J0LK2iT/view?usp=sharing)

---

## ⚙️ How It Works

### 1. Setup & Data Collection

The workflow starts with a **Schedule Trigger** that runs every day at `5 PM`.

- **Download File** → Fetches the latest resume from Google Drive.
- **Extract From File** → Converts your PDF resume to raw text (used by AI later).
- **Get Rows in Sheet** → Reads your job preferences (keywords, location, etc.) from Google Sheets.

---

### 2. LinkedIn Scraping

- **Create Search URL** → Builds a LinkedIn job search URL with your filters (custom JS).
- **Fetch Jobs from LinkedIn** → Sends an HTTP request to download the HTML of search results.
- **HTML Extractor** → Parses out all job posting links.
- **Split Out** → Splits the list of jobs into individual items for looping.

---

### 3. Job Analysis Loop

Each job goes through a structured loop:

- **Wait (2s)** → Prevents rate-limiting.
- **HTTP Request** → Fetches job details page.
- **HTML Parser** → Extracts title, company, location, and job description.
- **Edit Fields** → Cleans and formats the extracted data.

---

### 4. AI Evaluation & Cover Letter Generation

- **AI Agent (Google Gemini Chat Model)** → Compares the job with your resume and:
  - Calculates a **Job Match Score** (1–100)
  - Writes a **personalized cover letter**
- **Edit Fields** → Parses the AI response (JSON).
- **Append or Update Row** → Logs results to your Google Sheet with job data, score, and cover letter.

---

### 5. Smart Notifications

- **If Node** → Checks if the AI score ≥ 50.
- **Send Message (Telegram)** → Alerts you instantly with job details and your auto-generated cover letter.
- **Loop Over Items** → Continues to the next job until the list is done.

---

## 🧩 Tech Stack

| Tool                         | Purpose                                 |
| ---------------------------- | --------------------------------------- |
| **n8n**                      | Automation and orchestration            |
| **Google Drive**             | Resume storage                          |
| **Google Sheets**            | Preference & results database           |
| **LinkedIn**                 | Job data source                         |
| **Google Gemini Chat Model** | AI analysis and cover letter generation |
| **Telegram Bot**             | Real-time job alerts                    |

---

## 🗓️ Automation Flow

1. Trigger → Resume + Preferences
2. LinkedIn Scrape → Job Listings
3. AI Evaluation → Match Score + Cover Letter
4. Save to Sheet → Structured Results
5. Telegram Alert → Best Matches

---

## 🔒 Security Notice

All OAuth and API credentials have been **removed** from the exported workflow JSON for security reasons.  
After importing this workflow into n8n, you’ll need to **reconnect your own Google Drive, Google Sheets, and Telegram credentials**.
