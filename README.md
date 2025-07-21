<img width="382" height="902" alt="Image" src="https://github.com/user-attachments/assets/2cc475ad-ef11-4263-81d8-bd83944e228c" />

# 🛡️ Teams Chat Content Moderation Service – CST8917 Lab 3

## 📘 Overview

This project implements a **Teams Chat Content Moderation Service** using **Azure Logic Apps**, optionally integrated with **Azure Functions** and **Azure Cognitive Services**. It monitors Microsoft Teams chat messages for inappropriate content and triggers email alerts to administrators when violations are detected.

---

## 🎯 Objective

- Monitor Teams channel messages in real-time.
- Detect inappropriate content using optional Azure Functions and Azure Cognitive Services.
- Automatically notify administrators via email on policy violations.
- Demonstrate orchestration with Logic Apps and optional intelligent analysis using Cognitive Services.

---

## 🧱 Technologies Used

- **Azure Logic Apps**
- **Azure Functions** (optional)
- **Azure Cognitive Services for Language/Content Moderator** (optional)
- **Microsoft Teams**
- **Office 365 Outlook / Gmail** (for email notifications)

---

## 🔄 Workflow Flowchart

<img width="382" height="902" alt="Image" src="https://github.com/user-attachments/assets/2cc475ad-ef11-4263-81d8-bd83944e228c" />

---

## ⚙️ Logic App Setup

1. **Trigger**:
   - When a new message is posted in a Microsoft Teams channel.
2. **(Optional) Azure Function**:
   - Preprocess the message content for additional formatting or cleaning.
3. **(Optional) Azure Cognitive Services**:
   - Analyze message using Language or Content Moderator API.
4. **Condition**:
   - Check if inappropriate content is detected.
5. **Email Notification**:
   - If flagged, send an alert email to the admin.

---

## 🔌 Azure Function (Optional)

**Function Name**: `PreprocessMessage`

```python
import azure.functions as func
import json

def main(req: func.HttpRequest) -> func.HttpResponse:
    message = req.get_json().get("message", "")
    cleaned_message = message.lower().strip()
    return func.HttpResponse(
        json.dumps({ "cleanedMessage": cleaned_message }),
        mimetype="application/json"
    )
```

---

## 🧠 Azure Cognitive Services Integration (Optional)

- **Service**: Content Moderator / Language
- **Endpoint**: `{YourServiceEndpoint}`
- **Key**: `{YourAPIKey}`
- **Response Field**: `Classification.ReviewRecommended == true` or `Terms != null`

---

## ✉️ Email Notification Logic

- **Condition**: If `ReviewRecommended == true`, then:
- **Action**: Send email using Office 365 Outlook/Gmail connector
- **Email Format**:
  ```
  Subject: Policy Violation Detected
  Body:
  Message: [Original Text]
  Sender: [User Name]
  Timestamp: [Time Sent]
  ```

---

## 🧪 Testing the Workflow

1. Send test messages in the configured Teams channel.
2. Triggered Logic App checks message.
3. If violation is detected, an email is sent to the admin.
4. Verified all steps in Logic App Run History.

---

## 🛠️ Challenges Encountered

- Connecting to Teams requires valid Microsoft 365 account permissions.
- Logic App trigger delays when Teams is inactive.
- Parsing and validating API response fields from Azure Cognitive Services.
- Rate limits on Content Moderator API (20/sec).

---

## 🚀 Recommendations for Future Improvement

- Log all messages to Azure Storage for audit.
- Use Power BI or Log Analytics for violation trends.
- Integrate with Microsoft Defender for policy enforcement.
- Implement retry policies for failed email sends.

---

## 📹 Demo Video

[![Watch Demo](https://img.shields.io/badge/YouTube-Click%20Here-red)](https://youtube.com/your-demo-link)

---

## 📁 Repository Structure

```
├── README.md
├── logic-app-definition.json
├── azure-function/
│   └── preprocess_message.py
├── images/
│   └── teams_moderation_flowchart.png
```

---

## 📅 Submission Info

- **Course**: CST8917
- **Lab**: Lab 3 – Teams Chat Moderation
- **Student**: [Your Full Name]
- **Date**: July 21, 2025
