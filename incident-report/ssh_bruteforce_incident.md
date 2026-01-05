# Incident Report: SSH Brute Force Attempt


## Incident Summary
- **Incident Type:** SSH Brute Force Attempt
- **Severity:** High
- **Detection Tool:** Splunk SIEM
- **Affected System:** Ubuntu Linux Server
- **Log Source:** /var/log/auth.log


## Detection Details
The incident was detected through Splunk SIEM by monitoring Linux authentication logs. Multiple failed SSH login attempts were observed from the same source IP within a short time window, indicating a potential brute force attack.


## Evidence
- Repeated "Failed password" events
- Same source IP attempting multiple logins
- No successful authentication observed


## Analysis
The activity pattern matched common SSH brute force behavior. The number of failed login attempts exceeded the defined threshold, triggering a high-severity alert.


## Impact Assessment
- No successful login detected
- No system compromise observed
- Attack limited to authentication attempts


## Action Taken
- Alert generated in Splunk
- Source IP identified and flagged
- Incident documented for SOC records


## Recommendations
- Implement SSH rate limiting
- Disable password-based SSH login
- Enable key-based authentication
- Monitor repeated authentication failures


## Incident Status
**Closed – No compromise detected**
