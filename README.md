# 🌐 Website Status Monitor — n8n AI Agent

An automated monitoring agent built with **n8n** that continuously checks whether a website is online or offline, then sends instant email alerts via Gmail.

---

## 📌 Overview

This workflow automates website uptime monitoring without any manual effort. It runs on a schedule, pings your target website, evaluates the HTTP response, and routes the result to one of two Gmail notifications — one for "site is up" and one for "site is down."

---

## 🔄 Workflow

<img width="803" height="263" alt="n8n workflow diagram" src="https://github.com/user-attachments/assets/1ca6c78e-db34-4cdb-829d-161cda653b82" />

```
Schedule Trigger → HTTP Request → If (status check)
                                     ├── true  → Edit Fields → Gmail (Site is UP)
                                     └── false → Edit Fields → Gmail (Site is DOWN)
```

### Node breakdown

| Node | Type | Purpose |
|------|------|---------|
| Schedule Trigger | Trigger | Runs the workflow at a fixed interval (e.g., every 5 minutes) |
| HTTP Request | Action | Sends a GET request to the target website |
| If | Logic | Checks if the HTTP status code is 200 (OK) |
| Edit Fields (true) | Transform | Formats the "Site is UP" message |
| Gmail (send message) | Action | Sends uptime alert email to recipient |
| Edit Fields1 (false) | Transform | Formats the "Site is DOWN" message |
| Gmail1 (send message1) | Action | Sends downtime alert email to recipient |

---

## ⚙️ Setup Instructions

### Prerequisites

- [n8n](https://n8n.io) installed (self-hosted or cloud)
- A Gmail account with OAuth2 credentials configured in n8n
- The target website URL you want to monitor

### Steps

1. **Import the workflow**
   - Open your n8n instance
   - Go to **Workflows → Import from file**
   - Upload `workflow.json`

2. **Configure the HTTP Request node**
   - Set the URL to your target website (e.g., `https://yourwebsite.com`)
   - Method: `GET`

3. **Configure the Gmail credentials**
   - In both Gmail nodes, connect your Gmail OAuth2 credentials
   - Set the **To** field to the recipient's email address

4. **Set the schedule**
   - Open the Schedule Trigger node
   - Set your preferred interval (e.g., every 5 or 10 minutes)

5. **Activate the workflow**
   - Toggle the workflow to **Active**
   - The agent will now run automatically on schedule

---

## 📧 Email Alerts

**When the site is UP:**
> Subject: ✅ Website Status: Online  
> Body: Your website is up and running normally.

**When the site is DOWN:**
> Subject: ❌ Website Status: Down  
> Body: Alert! Your website appears to be offline. Please check immediately.

<img width="308" height="172" alt="Email alert preview" src="https://github.com/user-attachments/assets/05c4ddcf-9a93-46de-ad7d-3a6fc5431b24" />

*(You can customize these messages inside the Edit Fields nodes.)*

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| [n8n](https://n8n.io) | Workflow automation platform |
| Gmail API (OAuth2) | Email notifications |
| HTTP Request node | Website ping / health check |

---

## 📁 Repository Structure

```
├── workflow.json       # n8n workflow export
├── README.md           # Project documentation
└── screenshots/        # (optional) workflow screenshots
```

---

## 🚀 Future Improvements

- Add Slack/Telegram notification support
- Track response time and log to a database
- Monitor multiple websites in one workflow
- Send daily uptime summary reports
- Add retry logic before triggering a "down" alert

---

## 👤 Author

**Muhammad Zuhaib**  
Computer Systems Engineering Student — Sukkur IBA University  
GitHub: [@Zuhaib23](https://github.com/Zuhaib23)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
