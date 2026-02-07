# SOC Incident Investigation Report

## Incident: Multiple Failed Login Attempts

1. Executive Summary
On 12 January 2026, multiple failed login attempts were detected on the internal company authentication server from a single external IP address over a 15-minute period. The activity pattern suggests a potential brute-force attack attempt targeting user credentials.
Immediate monitoring and log analysis were conducted to assess risk and determine whether unauthorized access was achieved.
2. Incident Details
Date Detected: 12 January 2026
Time Window: 14:05–14:20 UTC
Affected System: Internal Authentication Server (Linux-based)
Detection Method: Log Monitoring / SIEM Alert
Source IP: 185.203.116.45
Event Type: Repeated Failed Login AttemptsLog Evidence (Sample)
Jan 12 14:05:11 server sshd[1024]: Failed password for invalid user admin from 185.203.116.45 port 51422 ssh2
Jan 12 14:06:03 server sshd[1028]: Failed password for invalid user root from 185.203.116.45 port 51433 ssh2
Jan 12 14:07:45 server sshd[1031]: Failed password for invalid user test from 185.203.116.45 port 51451 ssh2
Jan 12 14:09:12 server sshd[1034]: Failed password for invalid user guest from 185.203.116.45 port 51466 ssh2
Jan 12 14:15:22 server sshd[1040]: Failed password for invalid user admin from 185.203.116.45 port 51501 ssh2
4. Analysis
The repeated login attempts targeting multiple common account names (admin, root, guest, test) indicate automated credential guessing behavior. The consistent external IP address and short time intervals suggest a brute-force or scripted attack attempt.
No successful login events were recorded during this time window.
### 5. Risk Assessment

| Category     | Assessment |
|--------------|------------|
| Likelihood   | Medium     |
| Impact       | High (if successful) |
| Status       | No confirmed breach |

Although no successful authentication occurred, the repeated attempts indicate reconnaissance activity and potential brute-force automation.
6. Recommendations
Block the source IP address at firewall level.
Enable account lockout policies after multiple failed attempts.
Implement multi-factor authentication (MFA).
Review SSH configuration and disable root login.
Continue log monitoring for similar patterns.
### 7. Lessons Learned

- SSH services exposed to the internet require strict access controls.
- Default or common usernames increase attack surface.
- Continuous monitoring and alerting are critical for early detection.
- Multi-factor authentication significantly reduces brute-force success rates.
