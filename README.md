# 🚨 AWS Security Monitoring System Using Secrets Manager, CloudTrail, CloudWatch & SNS

A fully automated, real-time security alerting system built using AWS native services.
This project helps you detect, monitor, and alert any unauthorized or unexpected access to sensitive secrets stored in AWS Secrets Manager.
This project demonstrates:
- AWS security fundamentals
- CloudTrail logging and governance
- CloudWatch log monitoring + metric filters
- Real-time alerting using SNS (Email/SMS)
- Practical cloud security automation techniques


▶️ Watch the Project Demo

(https://youtu.be/zz6p88RGqsw)


### 📌 Project Overview

This project provides end-to-end monitoring on:
- Who accessed your Secrets
- When they accessed it
- What API calls were made
- Instant alerts to your email
- Complete audit trail of all activities


It uses a combination of:
- AWS Secrets Manager
- AWS CloudTrail
- CloudWatch Logs
- CloudWatch Metric Filters
- CloudWatch Alarms
- Amazon SNS (Email Notifications)
- AWS KMS (Encryption and Auditability)


### 🎯 Why This Project?

Storing secrets is not enough —
you must also track every access.

This setup ensures:

✔ Only authorized users access your secrets
✔ Every secret access is logged
✔ Suspicious access immediately triggers an alert
✔ You maintain compliance & audit visibility



### 🛠️ Services Used
**🔐 AWS Secrets Manager**
- Securely stores sensitive data (DB passwords, API keys, tokens).
- Encrypts via AWS KMS for strong security.
- Every secret access generates a CloudTrail event.


**🗝️ AWS KMS (Encryption)**
- Encrypts the secret at rest.
- Ensures only KMS-allowed users can decrypt secrets.
- Logs KMS usage (optional to exclude from CloudTrail to avoid noise).


**🕵️ AWS CloudTrail**
- Records every API call.
- Tracks GetSecretValue events.
- Streams logs to CloudWatch for real-time filtering.


**📊 AWS CloudWatch**
- Stores CloudTrail logs.
- Metric Filter detects secret access.
- CloudWatch Alarm notifies via SNS.


**📩 Amazon SNS**
- Sends email notifications when secret access is detected.
- Not recommended for CloudTrail log delivery (floods inbox), but perfect for **alerts**.



### 🏗️ AWS Architecture Diagram
<p align="center"> <img src="https://github.com/Tanomichikki/AWS-Security-Monitoring-System/blob/main/Security%20Monitoring.png" width="60%" /> </p>



### ⭐ Key Features
✔ Real-Time Monitoring
Instantly detects **GetSecretValue** access.

✔ Email Alerts
Receive a message within seconds when someone retrieves your secret.

✔ Fully Encrypted
All secrets secured using KMS keys.

✔ Complete Auditing
Each access visible in:
- CloudTrail Event History
- CloudWatch Logs
- SNS Notifications

✔ Custom Alerts
- You can expand it for:
- IAM role usage
- Unauthorized access attempts
- Network security events



### 📌 Detailed Workflow (From Script)
**1️⃣ Store a Secret in Secrets Manager**
- Save a database password/API key.
- Enable encryption using AWS-managed or customer-managed KMS key.

**2️⃣ CloudTrail Captures Access**
CloudTrail logs events like:
- Read Events (e.g., GetSecretValue)
- Write Events
- Management Events
- Data Events

**➡️ These logs are pushed to CloudWatch Logs.**

**3️⃣ Set Up a CloudWatch Metric Filter**

Define a filter pattern:
``` bash
"GetSecretValue"
```

Define:
- Metric Name: SecretAccessDetected
- Namespace: SecurityMonitoring
- Metric Value: 1
- This triggers whenever your secret is accessed.

**4️⃣ Create CloudWatch Alarm**
- Alarm threshold = 1
- Whenever metric is triggered → send notification

**5️⃣ SNS Notification**
- Subscribe your email
- Confirm the email from your inbox
- You will now receive alerts like:
**“ALERT: Your secret was accessed — review CloudTrail for details.”**




### 🚀 Deployment Steps
**Step 1 — Enable CloudTrail**
- Log all management events
- Store logs in S3
- Send logs to CloudWatch Logs

**Step 2 — Create CloudWatch Log Group**
- Connected to CloudTrail.

**Step 3 — Create Metric Filters**
- Root login
- Unauthorized actions
- IAM changes
- Access key activity

**Step 4 — Create CloudWatch Alarms**
- Link alarms to metric filters.

**Step 5 — Configure SNS Topic**
- Create security-alerts topic
- Subscribe email
- Attach to alarm actions
