
# 📡 Telstra Cybersecurity Simulation – Spring4Shell Incident

Hands‑on simulation completed through the Telstra Cybersecurity Virtual Experience Program.  
It covers the full incident‑response life‑cycle: **alert triage ➜ threat analysis ➜ defensive engineering ➜ post‑incident review**.

---

## 🚦 Task 1 — Threat Triage & Immediate Notification

| Item | Details |
|------|---------|
| **Threat** | *Spring4Shell* ( `CVE‑2022‑22965` ) remote‑code‑execution exploit |
| **Detected @** | **2022‑03‑20 03 : 16 : 34 UTC** via firewall anomaly alert |
| **Impacted Service** | `NBN Connectivity – External Spring Framework stack` |
| **Business Priority** | **High** — national backbone connectivity |
| **Owning Team** | **NBN Operations** (John Doe – nbn@email) |

### ✉️ Incident Notification (sent)

```
From: Telstra Security Operations Centre  
To: NBN Operations (nbnoteam@email)  
Subject: ⚠️ MALWARE INCIDENT — Spring4Shell on NBN Services (03:16 UTC)

Hi NBN Ops,

At **03 : 16 UTC 20‑Mar‑2022** we detected active exploitation of the Spring4Shell
zero‑day against the NBN external Spring stack. The service is currently impaired.

**Impact** – RCE confirmed, malware dropper observed; connectivity degraded.  
**Next Step** – please place SREs on standby while containment is underway.
We will share IOCs and mitigation guidance shortly.

— Telstra SOC
```

---

## 🔍 Task 2 — Log Analysis & Firewall Rule Request

### Key Indicators Extracted from Logs
| Field | IOC / Pattern |
|-------|---------------|
| **Request Path** | `/tomcatwar.jsp` (POST) |
| **Header** | `class.module.classLoader.resources.context.parent.pipeline.first.pattern` |
| **Payload Regex** | `Runtime\.exec\(request\.getParameter\(cmd\)\)` |

### ✉️ Firewall Rule Creation Request (sent)

```
From: Telstra Security Operations Centre  
To: Networks Team (networks@email)  
Subject: URGENT — Block Spring4Shell Payload (IOC details inside)

Hi Networks,

Requesting an immediate egress/ingress filter:

1. **Deny** any HTTP POST to **/tomcatwar.jsp**
2. **Drop** requests containing header
   `class.module.classLoader.resources.context.parent.pipeline.first.pattern`
3. Monitor for payload regex
   `Runtime\.exec\(request\.getParameter\(cmd\)\)` and alert on match

Target: Spring Framework 5.3.x exposed nodes (NBN stack).  
Objective: stop malware loader while patching is in progress.

Thanks – Telstra SOC
```

---

## 🛡️ Task 3 — Python Firewall Rule (abridged)

> File: `firewall_server.py`

```python
#!/usr/bin/env python3
from http.server import BaseHTTPRequestHandler, HTTPServer
import re

HOST, PORT = "localhost", 8000
MALICIOUS = re.compile(
    rb"(?:/tomcatwar\.jsp|class\.module\.classLoader\.resources\.context\.parent\.pipeline\.first\.pattern|Runtime\.exec\(request\.getParameter\(cmd\)\))"
)

class WAFHandler(BaseHTTPRequestHandler):
    def do_POST(self):
        length = int(self.headers.get("Content-Length", 0))
        body   = self.rfile.read(length)
        if MALICIOUS.search(self.path.encode() + body):
            self.send_error(403, "Blocked by Telstra WAF")
            return
        self._ok()

    # allow benign GET/POST
    do_GET = do_POST
    def _ok(self):
        self.send_response(200)
        self.end_headers()

if __name__ == "__main__":
    print(f"[+] WAF running on {HOST}:{PORT}")
    HTTPServer((HOST, PORT), WAFHandler).serve_forever()
```

*Tested with `test_requests.py` — malicious traffic returns **403**, legitimate traffic **200**.*

---

## 📝 Task 4 — Incident Post‑mortem

### 1. Overview
|                                |                                    |
|--------------------------------|------------------------------------|
| **Incident ID**                | TEL‑INC‑20220320‑SPR4              |
| **Start**                      | 20‑Mar‑2022 03 : 16 UTC            |
| **Mitigated**                  | 20‑Mar‑2022 05 : 22 UTC            |
| **Duration**                   | 2 h 06 m                           |
| **Severity**                   | High                               |
| **Root Cause**                 | Unpatched Spring4Shell RCE         |

### 2. Timeline
| Time (UTC) | Event |
|------------|-------|
| 03 : 16    | SOC alert — unusual POST bursts to `/tomcatwar.jsp` |
| 03 : 25    | Malware loader hash identified; NBN Ops notified |
| 03 : 55    | Log review confirmed Spring4Shell exploit pattern |
| 04 : 15    | Networks received WAF rule request |
| 05 : 05    | Python WAF rule deployed, blocking traffic |
| 05 : 22    | Service health restored; IOC monitoring active |

### 3. Impact
- **NBN Connectivity Services** — intermittent outages, up to 18 % packet loss  
- **External Spring Infrastructure** — RCE foothold; no lateral movement detected

### 4. Root‑Cause Analysis
- Exploited `CVE‑2022‑22965` in **Spring 5.3.0** running on publicly accessible Tomcat.
- Payload delivered via crafted header + JSP endpoint; achieved remote shell.

### 5. Actions Taken
1. Triage & stakeholder notification (Task 1)  
2. IOC extraction and WAF recommendation (Task 2)  
3. Rapid WAF patch via Python rule (Task 3)  
4. Post‑incident forensics confirmed no data exfiltration.

### 6. Lessons & Recommendations
| Area | Recommendation |
|------|----------------|
| **Patch Management** | Enforce 7‑day SLA for critical CVEs; auto‑deploy Spring >= 5.3.18 |
| **Perimeter Defense** | Migrate custom WAF rules to central policy repo; integrate CI/CD tests |
| **Monitoring** | Add Spring4Shell SIGMA rule to SIEM for early detection |
| **Readiness** | Conduct red‑team drill simulating Spring4Shell each quarter |

_For questions contact **Telstra SOC** (soc@email)._  

---


---

### ✅ Outcome

The simulation demonstrates end‑to‑end incident handling:

- **Detect → Communicate → Contain → Review**  
- Coordinated response cut attacker dwell‑time to **< 2 hours**.  
- Post‑mortem drives continuous hardening of Telstra’s security posture.
