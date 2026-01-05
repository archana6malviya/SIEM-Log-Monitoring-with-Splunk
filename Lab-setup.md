1️⃣ Virtual Machine Setup

Installed Oracle VirtualBox on host system

Created an Ubuntu Linux VM (20.04/22.04)

Allocated resources:

RAM: 4 GB (minimum 2 GB)

CPU: 2 cores

Storage: 40 GB

Linux Preparation
sudo apt update && sudo apt upgrade -y
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh

SSH service enabled to generate authentication logs

Logs generated at: /var/log/auth.log

3️⃣ Splunk Enterprise Installation (Free)

Downloaded Splunk Enterprise .deb package


sudo dpkg -i splunk-*.deb
sudo /opt/splunk/bin/splunk start --accept-license

Accessed Splunk Web UI:

http://localhost:8000

4️⃣ Log Ingestion (auth.log)

Navigated to:

Settings → Add Data → Monitor

Selected Existing file

Added log source:

/var/log/auth.log

Index used: main

Verified events using:

index=main
5️⃣ Attack Simulation (Failed SSH Logins)

Generated failed login attempts:

ssh fakeuser@localhost

Multiple failed attempts created to simulate brute-force behavior

6️⃣ Detection Queries

Failed login detection:

index=main "Failed password"

Brute-force detection:

index=main "Failed password"
| rex field=_raw "from (?<src_ip>[a-fA-F0-9:.]+)"
| stats count by src_ip
| where count > 3
7️⃣ Alert Creation

Created Splunk alert for brute-force activity

Trigger condition: Number of failed attempts > threshold

Alert severity: High

8️⃣ Dashboard Creation

Dashboard Name: Linux SSH Security Monitoring

Line chart: Failed SSH logins over time

Table: Top attacking IP addresses

9️⃣ Incident Documentation

Observed alert firing

Documented incident in SOC format

Added remediation recommendations





