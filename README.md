# 🛡️ AWS Security Monitoring System – CloudTrail, CloudWatch & SNS Alerts

A fully automated real-time security monitoring system built on AWS that tracks critical account activities, analyzes CloudTrail logs, and sends instant alerts using SNS.

This project demonstrates:

AWS security fundamentals

CloudTrail logging and governance

CloudWatch log monitoring + metric filters

Real-time alerting using SNS (Email/SMS)

Practical cloud security automation techniques

▶️ Watch the Project Demo

(Replace with your video thumbnail once uploaded)


### 📌 About the Project

This AWS Security Monitoring System is designed to detect sensitive AWS account events and notify the administrator instantly.

The system protects your AWS account by alerting for:

Root user logins

Console logins without MFA

Unauthorized API calls

IAM policy or role changes

Access key creation or deletion

It follows real industry practices used by Cloud Security, DevOps, and SOC teams.

### ✨ Key Features
🔍 CloudTrail Activity Logging

Records every API call in the AWS account

Detects security-critical events

Delivers logs to CloudWatch for monitoring

### 📊 CloudWatch Monitoring

Metric filters analyze log patterns

Alarms trigger based on thresholds

Real-time threat detection

### 🔔 SNS Instant Notifications

Email/SMS alerts

Notifies admins immediately

Helps respond to risky activities quickly

### 🏗️ AWS Architecture Diagram
<p align="center"> <img src="https://github.com/Tanomichikki/AWS-Security-Monitoring-System/blob/main/Security%20Monitoring.png" width="60%" /> </p>
☁️ AWS Monitoring Breakdown
🛡️ AWS CloudTrail — API Activity Logging

CloudTrail records all API calls in your account:
Who did what → From where → With which permissions.

🔹 Why CloudTrail?

Centralized auditing

Detect suspicious actions

Required for security & compliance (SOC2, PCI, ISO)

🔹 How It Works

Creates a trail

Sends logs to S3

For real-time monitoring: sends logs to CloudWatch Logs

### 📊 Amazon CloudWatch — Log Monitoring & Alerts

Raw logs from CloudTrail are analyzed using Metric Filters.

Examples:

Root Login Filter
{ $.userIdentity.type = "Root" }

Unauthorized API Call Filter
{ $.errorCode = "*Unauthorized*" || $.errorCode = "AccessDenied*" }

Console Login Without MFA
{ $.additionalEventData.MFAUsed = "No" }

Why Metric Filters?

Search logs for event patterns

Convert patterns → Metrics

Trigger alarms automatically

### 🚨 CloudWatch Alarms — Real-Time Threat Detection

Used to detect:

Root Login

Access key deletion/creation

IAM role/policy changes

Failed console logins

MFA disabled/ignored

When an event occurs → Alarm → SNS → Email/SMS

### 📩 Amazon SNS — Instant Notifications

SNS delivers the security alert to your email or mobile.

🔹 Why SNS?

Instant notification

Supports multiple subscribers

Used in production security workflows

🛠️ Tech Stack

Monitoring Services: CloudTrail, CloudWatch Logs, CloudWatch Metrics, Alarms
Notification System: Amazon SNS
Storage: Amazon S3
Tools: AWS Console, IAM, JSON policies
Environment: VS Code, AWS CLI (optional)

📂 Project Structure
AWS-Security-Monitoring/
├── cloudtrail/
│   └── trail-configuration.json
├── cloudwatch/
│   ├── metric-filters.md
│   └── alarms.md
├── sns/
│   └── sns-topic-details.md
├── architecture-diagram.png
└── README.md

🧪 Testing the System

Trigger test alerts by:

🔐 Signing in with the root user

→ Should trigger immediate SNS alert.

❌ Making an Unauthorized API Call

(e.g., using insufficient IAM permissions)

🔑 Creating or Deleting Access Keys

→ Security-critical action detected.

👤 Modifying IAM Roles/Policies

→ Alarm activated.

### 🚀 Deployment Steps
Step 1 — Enable CloudTrail

Log all management events

Store logs in S3

Send logs to CloudWatch Logs

Step 2 — Create CloudWatch Log Group

Connected to CloudTrail.

Step 3 — Create Metric Filters

Root login

Unauthorized actions

IAM changes

Access key activity

Step 4 — Create CloudWatch Alarms

Link alarms to metric filters.

Step 5 — Configure SNS Topic

Create security-alerts topic

Subscribe email

Attach to alarm actions
