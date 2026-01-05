SIEM Log Monitoring with Splunk
📌 Project Overview
This project demonstrates hands-on experience with SIEM log monitoring using Splunk, focusing on Linux SSH authentication logs. The goal is to simulate real-world SOC analyst activities such as log ingestion, failed login detection, brute force attack identification, alert creation, dashboard monitoring, and basic incident investigation.

This project is designed for entry-level SOC Analyst roles and reflects tasks commonly performed in a Security Operations Center.

🛠️ Tools & Technologies Used

Splunk Enterprise (Free License)

Ubuntu Linux (Log Source & Target System)

SSH Service

Linux Authentication Logs (/var/log/auth.log)

VirtualBox / VMware (Virtual Lab)

🧪 Lab Setup
Component	Description
SIEM	Splunk Enterprise running on Ubuntu
Log Source	Ubuntu Linux authentication logs
Attack Simulation	SSH failed login attempts

Log File Monitored:

/var/log/auth.log
📥 Log Ingestion

Configured Splunk to monitor Linux authentication logs

Verified successful log ingestion into the main index

Validated logs using Splunk Search & Reporting

Sample Search:

index=main
🚨 Detection Use Cases
1️⃣ Failed SSH Login Detection

Detects unsuccessful SSH login attempts.

Query:

index=main "Failed password"
2️⃣ SSH Brute Force Detection

Identifies potential brute force attacks by detecting multiple failed login attempts from the same source IP.

Query:

index=main "Failed password"
| rex field=_raw "from (?<src_ip>[a-fA-F0-9:.]+)"
| stats count by src_ip
| where count > 3
🔔 Alert Configuration

Alert Name: Linux SSH Brute Force Attempt
Trigger Condition: If results > 0
Trigger Type: Once
Severity: High
Expiration: 24 hours

The alert triggers when multiple failed SSH login attempts are detected from a single source IP.

📊 Dashboard: Linux SSH Security Monitoring

A Splunk dashboard was created to provide real-time visibility into SSH authentication activity.

Dashboard Panels

1️⃣ Failed SSH Logins Over Time

index=main "Failed password"
| timechart count

2️⃣ Top Attacking Source IPs

index=main "Failed password"
| rex field=_raw "from (?<src_ip>[a-fA-F0-9:.]+)"
| stats count by src_ip
| sort - count
🕵️ Incident Investigation Summary

Incident Type: SSH Brute Force Attempt
Severity: High
Affected System: Ubuntu Linux Server

Investigation Steps

Alert triggered for multiple failed SSH logins

Reviewed raw authentication logs

Extracted attacker source IP

Analyzed frequency of failed attempts

Verified no successful authentication

Classified activity as brute force attack

Status: No successful compromise detected

🎯 Skills Demonstrated

SIEM log ingestion and monitoring

Linux authentication log analysis

SSH brute force detection techniques

Splunk search (SPL) and field extraction

Alert creation and tuning

Dashboard creation for SOC monitoring

Incident investigation and documentation

📌 Key Takeaway

This project showcases practical SOC Analyst skills including threat detection, alerting, visualization, and incident analysis using Splunk SIEM. It reflects real-world SOC workflows and is suitable for showcasing hands-on experience in cybersecurity job applications.

✅ Status: Completed
🔐 Domain: Security Operations Center (SOC)
