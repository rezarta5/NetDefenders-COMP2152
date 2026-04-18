# COMP2152 — Term Project: CTF Bug Bounty

## Team Name
NetDefenders-COMP2152

## Team Members
Sanzida Islam - 101564719
Rezarta Marku - 101402390
Wasifa Hossain - 101594842

| Member | Vulnerability Found | Branch Name |
|--------|-------------------|-------------|
| Rezarta Marku | Open Port Exposure on api.0x10.cloud| rezarta-feature|
| _______ | _______ | _______ |

## Videos

Each team member records a short video (max 3 minutes) explaining their vulnerability. Add your YouTube links below:

- Member 1: https://youtube.com/watch?v=_______
- Member 2: https://youtube.com/watch?v=_______
- Member 3: https://youtube.com/watch?v=_______

## Vulnerability Report (Rezarta Marku)
Title:

Open Port Exposure on api.0x10.cloud

Description:

Ports such as Telnet (23), FTP (21), or Redis (6379) may be open on the target server. These services are often insecure or misconfigured. For example, Telnet sends data in plaintext, and Redis may allow unauthorized access if not secured. Open ports increase the attack surface and can be exploited by attackers.

### Proof:
1. A Python script was used to scan common ports on the target server api.0x10.cloud using the socket library.

2. The script attempted connections to ports: 21, 22, 23, 80, 443, and 6379.

3. The scan result showed that ports 80 (HTTP) and 443 (HTTPS) are open, while the others are closed.

4. Port 80 allows unencrypted communication, which can expose data to interception, even though HTTPS is available on port 443.

Output:
[+] Port 21 is closed
[+] Port 22 is closed
[+] Port 23 is closed
[!] Port 80 is OPEN
    → HTTP is insecure (no encryption)
[!] Port 443 is OPEN
    → HTTPS is secure but HTTP should be redirected
[+] Port 6379 is closed

## Target

- Server: `0x10.cloud` and its subdomains
- Submission: http://submit.0x10.cloud
- Leaderboard: http://ranking.0x10.cloud

## Important: Rate Limit

The server allows **10 requests per second** per IP address. If you send requests too fast, you will get blocked (HTTP 429). Add a small delay between requests:

```python
import time
time.sleep(0.15)  # wait 150ms between requests
```

