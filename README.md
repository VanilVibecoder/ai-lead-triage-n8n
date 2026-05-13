# AI Lead Triage — n8n Workflow

## Status

Training portfolio case, not a client implementation.

This project is based on a common business process:

incoming lead → validation → duplicate check → AI qualification → Google Sheets → Telegram manager notification.

## Overview

AI Lead Triage is an n8n workflow for online schools, experts, and service businesses.

The workflow receives incoming leads through a secured webhook, validates contact data, checks duplicates, classifies the lead using AI, calculates lead score and SLA, stores the result in Google Sheets, and sends a ready-to-use Telegram card to the manager.

## Problem

Small businesses and online schools often process leads manually:

- managers read every message by hand;
- hot leads may be answered too late;
- duplicate requests are not detected;
- lead data is copied manually into spreadsheets;
- spam and irrelevant requests distract the sales team.

## Solution

The workflow automates the first stage of lead processing:

Webhook → Secret Check → Validation → Duplicate Check → AI Classification → Score/SLA → Google Sheets → Telegram Notification → Client Response

## Features

- Secured webhook with secret header
- Message/contact validation
- Phone and email normalization
- Duplicate detection by lead_key
- AI lead classification
- Priority: hot / warm / cold / unknown
- Lead score from 0 to 100
- SLA calculation and follow-up deadline
- Google Sheets storage
- Telegram manager notification
- Spam routing
- AI fallback for invalid JSON
- Error workflow for technical failures
- Retry on external API nodes

## Tech Stack

- n8n
- Mistral AI
- Google Sheets
- Telegram Bot
- JavaScript Code Node
- Webhook
- Postman

## Workflow Architecture

Webhook  
→ Validate Webhook Secret  
→ Normalize + Validate Lead  
→ Check Message  
→ Check Valid Contact  
→ Check Duplicate in Google Sheets  
→ Mark New / Duplicate  
→ Prepare AI Input  
→ AI Agent  
→ Parse + Validate AI Output  
→ Append Lead to Google Sheets  
→ Prepare Telegram Message  
→ Route Notification  
→ Respond to Client

## Test Scenarios

1. New hot lead
2. Duplicate hot lead
3. Invalid contact data
4. Unauthorized request
5. Spam or irrelevant lead
6. AI fallback / Error Workflow

## Screenshots

### Workflow architecture

![Workflow architecture](screenshots/01_workflow_schema.png)

### Successful request

![Postman success](screenshots/02_postman_success.png)

### Hot lead notification

![Telegram hot lead](screenshots/03_telegram_hot_lead.png)

### Duplicate lead notification

![Telegram duplicate lead](screenshots/04_telegram_duplicate_lead.png)

### Google Sheets storage

![Google Sheets](screenshots/05_google_sheets.png)

### Unauthorized request

![Unauthorized request](screenshots/06_unauthorized_401.png)

### Error Workflow alert

![Error Workflow alert](screenshots/07_error_workflow_alert.png)

## Repository Structure

```text
ai-lead-triage-n8n/
├─ README.md
├─ workflow-redacted.json
├─ screenshots/
└─ test-payloads/