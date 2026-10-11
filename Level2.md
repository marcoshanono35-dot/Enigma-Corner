# Level 2: Hollow Transit — Forensic Analysis Write-Up

This write-up covers the investigation into the "Hollow Transit" advanced intrusion scenario, detailing patient-zero discovery, LOLBin abuse, persistence, network evasion, and threat actor attribution.

---

## 1. Which user account was the TRUE initial-access victim (patient zero)?

Reviewing the overarching case timeline and authentication logs isolates the primary account compromised at the perimeter prior to lateral traversal.

**Answer:** `s.okafor`

<img src="image/level2-q1.png" alt="Patient Zero Account Identification" width="500" />

---

## 2. What was the initial-access vector?

Event log analysis identifies an unsigned, untrusted dynamic link library (DLL) executed via dynamic link library sideloading/proxy loading by an otherwise legitimate host executable.

**Answer:** Unsigned DLL (DLL Sideloading)

<img src="image/level2-q2.png" alt="Unsigned DLL Execution Alert" width="500" />

---

## 3. Which living-off-the-land binary (LOLBin) downloaded the second stage?

Examining process creation events shows the native Windows certificate utility being abused to retrieve remote secondary payloads directly to disk.

**Answer:** `certutil.exe`

<img src="image/level2-q3.png" alt="Certutil Stager Execution" width="500" />

---

## 4. What persistence technique was established?

Security auditing captures Windows Management Instrumentation (WMI) event subscriptions deployed on the endpoint, specifically leveraging an active **WMI event filter** bound to an event consumer.

**Answer:** WMI Event Filter (T1546.003)

<img src="image/level2-q4.png" alt="WMI Persistence Mechanism" width="500" />

---

## 5. What domain was used for DNS-tunnelling C2?

Network inspection reveals high-frequency, anomalous DNS query lengths utilized for covert data encapsulation and C2 communications.

**Answer:** `3f9a2c.sync.telemetry-cdn.io`

<img src="image/level2-q5.png" alt="DNS Tunnelling Query Telemetry" width="500" />

---

## 6. What is the C2 IP address?

Correlating the captured network flows reveals the resolved C2 IP address receiving encapsulated communications.

**Answer:** `45.83.220.19`

<img src="image/level2-q6.png" alt="C2 Network Interception Record" width="500" />

---

## 7. Which technique was used for lateral movement?

Review of Windows event telemetry identifies successful remote process instantiation and protocol binding via Windows Remote Management.

**Answer:** WinRM (Windows Remote Management)

<img src="image/level2-q7.png" alt="Lateral Movement Event Log" width="500" />

---

## 8. What intellectual property was exfiltrated?

Forensic inspection of the staging path `C:\Users\s.okafor\AppData\Local\Temp\t.cab` confirms the adversary compressed and packaged proprietary semiconductor design files for extraction.

**Answer:** Tape-out archive

<img src="image/level2-q8.png" alt="Exfiltrated Intellectual Property Archive" width="500" />

---

## 9. The insider d.raymond looks suspicious. Are they responsible for the intrusion? (yes / no)

Correlating endpoint execution logs and network telemetry confirms that `d.raymond` was not the vector or operator behind this intrusion sequence.

**Answer:** No

---

## 10. Which threat actor is attributed to this intrusion?

Threat intelligence correlation against the DNS tunneling infrastructure, WMI persistence tradecraft, and specialized payload signatures links this intrusion to the adversary group **SLATE TYPHOON**.

**Answer:** SLATE TYPHOON

<img src="image/level2-q10.png" alt="Threat Intelligence Actor Attribution" width="500" />
