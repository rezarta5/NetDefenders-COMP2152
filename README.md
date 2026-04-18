# COMP2152 — Term Project: CTF Bug Bounty

## Team Name
NetDefenders-COMP2152

## Team Members
Sanzida Islam - 101564719
Rezarta Marku - 101402390
Wasifa Hossain - 101594842

| Member | Vulnerability Found | Branch Name |
|--------|-------------------|-------------|
| Sanzida Islam | No HTTPS on api.0x10.cloud| sanzida-feature |
| Rezarta Marku | Open Port Exposure on api.0x10.cloud| rezarta-feature|
| _______ | _______ | _______ |

## Videos

Each team member records a short video (max 3 minutes) explaining their vulnerability. Add your YouTube links below:

- Member 1: https://youtube.com/watch?v=_______
- Member 2: https://youtube.com/watch?v=_______
- Member 3: https://youtube.com/watch?v=_______

## Vulnerability Report (Sanzida Islam)

### Title:
No HTTPS on api.0x10.cloud

### Description:
The website allows communication over HTTP instead of HTTPS. This means data transmitted between the user and the server is not encrypted. An attacker can intercept sensitive information such as login credentials using a man-in-the-middle (MITM) attack.

### Proof:
Final URL: http://api.0x10.cloud
[!] VULNERABILITY: Site does NOT use HTTPS
→ Data can be intercepted (MITM attack)

## Vulnerability Report (Rezarta Marku)
Title:

Open Port Exposure on api.0x10.cloud

Description:

Ports such as Telnet (23), FTP (21), or Redis (6379) may be open on the target server. These services are often insecure or misconfigured. For example, Telnet sends data in plaintext, and Redis may allow unauthorized access if not secured. Open ports increase the attack surface and can be exploited by attackers.

1. A Python script was used to scan common ports on the target server api.0x10.cloud using the socket library.

2. The script attempted connections to ports: 21, 22, 23, 80, 443, and 6379.

3. The scan result showed that only port 80 (HTTP) is open, while all other tested ports are closed.

4. Since port 80 uses HTTP, communication is not encrypted and can be intercepted by attackers.

Output:
[+] Port 21 is closed
[+] Port 22 is closed
[+] Port 23 is closed
[!] Port 80 is OPEN
    → HTTP is insecure (no encryption)
[+] Port 443 is closed
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

## Getting Started

1. Look at the three example scripts:
   - `example_http_check.py` — checks if a site uses HTTPS (uses `urllib`)
   - `example_port_check.py` — checks if a port is open (uses `socket`)
   - `example_header_check.py` — reads HTTP response headers for info leaks (uses `urllib`)
2. Run all examples: `python3 main.py`
3. Create your own branch: `git checkout -b your_vuln_name`
4. Write a Python script that finds and demonstrates a vulnerability
5. Submit your finding at http://submit.0x10.cloud
6. Merge your branch into master when done

## Rules

- **Python standard library only** — `socket`, `urllib`, `ssl`, `json`, `base64`, `time`. No pip packages.
- **Only scan `*.0x10.cloud`** — do not scan any other domain.
- **Respect the rate limit** — 10 requests/second max.
