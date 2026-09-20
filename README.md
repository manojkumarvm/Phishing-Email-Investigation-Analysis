# Threat-Intelligence-IOC-Email-Investigation
Phishing email investigation, IOC extraction, and threat intelligence analysis using VirusTotal and URLScan.io.

## 1. Project Overview

This project demonstrates a phishing email investigation workflow using email header analysis, IOC extraction, and threat intelligence tools.

A sample phishing email was analyzed to identify suspicious sender information, domain spoofing, authentication failures, embedded URLs, IP addresses, and a suspicious attachment.

The extracted indicators were investigated using VirusTotal and URLScan.io, and the findings were documented in an incident report with recommended remediation steps.

---

## 2. Objectives

The main objectives of this project are:

* Analyze a suspicious phishing email.
* Examine email headers and authentication results.
* Identify sender-domain spoofing and lookalike domains.
* Extract URLs and IP addresses as potential indicators of compromise (IOCs).
* Investigate suspicious URLs using VirusTotal and URLScan.io.
* Investigate suspicious IP addresses using VirusTotal.
* Analyze suspicious email attachments safely.
* Document identified IOCs.
* Prepare an incident investigation report.
* Provide recommended remediation actions.

---

## 3. Tools Used

| Tool           | Purpose                                    |
| -------------- | ------------------------------------------ |
| `.eml` file    | Source phishing email                      |
| Notepad        | Email source and header inspection         |
| Microsoft Word | Investigation documentation                |
| VirusTotal     | URL, IP and email-file threat intelligence |
| URLScan.io     | URL and web infrastructure investigation   |
| GitHub         | Project documentation and evidence         |

---

## 4. Investigation Methodology

The investigation followed this workflow:

```text
Phishing Email (.eml)
        |
        v
Email Header Analysis
        |
        v
Sender & Domain Analysis
        |
        v
IOC Extraction
        |
        +----------> URL
        |              |
        |              v
        |        VirusTotal
        |              |
        |              v
        |        URLScan.io
        |
        +----------> IP
        |              |
        |              v
        |        VirusTotal
        |
        +----------> Attachment
                       |
                       v
                 Safe Analysis
        |
        v
IOC Summary
        |
        v
Phishing Indicators
        |
        v
Incident Report
        |
        v
Remediation
```

---

# 5. Email Header Analysis

The `.eml` file was examined to identify the sender, Reply-To address, Return-Path, sending infrastructure, and email authentication results.

### Observed Header Information

| Header      | Observed Value                                 |
| ----------- | ---------------------------------------------- |
| From        | `security-alert@paypa1-secure-verify.com`      |
| Reply-To    | `paypal-support-case@mail-response-center.com` |
| Return-Path | `security-alert@paypa1-secure-verify.com`      |
| Sending IP  | `185.220.101.47`                               |
| SPF         | FAIL                                           |
| DKIM        | FAIL                                           |
| DMARC       | FAIL                                           |

### Analysis

The email claimed to represent PayPal but used the domain:

```text
paypa1-secure-verify.com
```

The use of `paypa1` instead of `paypal` is a lookalike-domain indicator.

The Reply-To address also used a different domain:

```text
mail-response-center.com
```

These differences were documented as suspicious indicators.

![Email Header Analysis](evidence/01-email-header-an<img alysis.png)width="1920" height="1080" alt="01-email-header-analysis png" src="https://github.com/user-attachments/assets/3df0c666-0aed-4250-a369-d41e862f492e" />


---

# 6. Sender Domain Analysis

The sender information was compared with the Reply-To and Return-Path values.

### Sender

```text
security-alert@paypa1-secure-verify.com
```

### Reply-To

```text
paypal-support-case@mail-response-center.com
```

### Domain Indicators

The sender domain contains:

```text
paypa1
```

where the number `1` is used in place of the letter `l`.

The Reply-To address also uses a different domain.

### Authentication Results

```text
SPF  = FAIL
DKIM = FAIL
DMARC = FAIL
```

These authentication failures provide additional evidence that the message requires security investigation.<img width="1920" height="1080" alt="04-virustotal-email" src="https://github.com/user-attachments/assets/c3bfb796-a78b-48fd-8145-871eaff3c7c7" />


---

# 7. URL IOC Extraction

The email body contained a suspicious URL:

```text
http://paypa1-secure-verify.com.account-confirm.info/login.php?id=8827x9j2&session=expired
```

The URL was not opened directly during the investigation.

For safe documentation, the URL is represented in defanged form:

```text
hxxp://paypa1-secure-verify[.]com.account-confirm[.]info/login.php
```

The URL uses a deceptive domain structure designed to make the link appear associated with PayPal.

![URL Extraction](evidence/03-url-extraction.png)

---

# 8. VirusTotal Email Analysis

The `.eml` sample was submitted to VirusTotal for file-level analysis.

The observed result was:

```text
2 / 54 security vendors flagged the file as malicious
```

The VirusTotal report also showed email-related threat labels including:

```text
mail/nametrick
```

The SHA-256 hash observed for the submitted sample was:

```text
3e2bce0ee01f9a44ebb857826928684ef7f906b4d2344afc42597a07cd9c7203
```

Two vendors produced detections for the submitted email file, while other vendors reported the file as undetected, timed out, or unable to process the file.

This result was treated as supporting threat-intelligence evidence rather than as the sole basis for the investigation.

![VirusTotal Email Analysis](evidence/04-virustotal-email.png)<img width="1920" height="1080" alt="04-virustotal-email" src="https://github.com/user-attachments/assets/5be4bd11-786c-4701-aaca-4930461d7442" />


---

# 9. VirusTotal URL Investigation

The suspicious URL extracted from the email was investigated using VirusTotal.

The investigation examined:

* Detection results
* Security vendor classifications
* Domain information
* Threat categories
* Available reputation information

The observed VirusTotal findings were documented in the investigation report.

![VirusTotal URL Investigation](evidence/05-virustotal-url.png)<img width="1920" height="1080" alt="05-virustotal-url" src="https://github.com/user-attachments/assets/4e5658d9-6967-4491-a668-6726fa1f9619" />


---

# 10. VirusTotal IP Investigation

The sending IP identified from the email header was:

```text
185.220.101.47
```

The IP address was investigated using VirusTotal.

The investigation examined:

* Security vendor detections
* Reputation
* Associated domains
* Network/ASN information
* Available threat intelligence

The observed findings were documented in the investigation report.

![VirusTotal IP Investigation](evidence/06-virustotal-ip.png)<img width="1920" height="1080" alt="06-virustotal-ip" src="https://github.com/user-attachments/assets/ad8e776c-696d-440f-a3c1-1a27a6bde567" />


---

# 11. URLScan.io Investigation

The suspicious URL was investigated using URLScan.io.

The investigation examined available information including:

* Domain
* IP address
* HTTP requests
* Redirects
* Page information
* Technologies
* Available screenshot information

The URLScan.io findings were compared with the email and VirusTotal evidence.

![URLScan.io Investigation](evidence/07-urlscan-analysis.png)
<img width="1920" height="1080" alt="07-urlscan-analysis" src="https://github.com/user-attachments/assets/43c4f828-ad41-4394-8d7d-31395b831ef4" />


---

# 12. Attachment Analysis

The email contained the following attachment:

```text
Account_Statement.pdf.exe
```

The MIME information identified the attachment as:

```text
application/octet-stream
```

The filename uses a double extension:

```text
.pdf.exe
```

The final extension is `.exe`, indicating that the file is an executable rather than a normal PDF document.

The attachment was not executed during the investigation.

![Attachment Analysis](evidence/08-attachment-analysis.png)<img width="778" height="281" alt="08-attachment-analysis" src="https://github.com/user-attachments/assets/fad12599-3093-42de-8ba6-55bdc519bdd5" />


---

# 13. IOC Summary

| IOC Type      | Indicator                                                          | Source           |
| ------------- | ------------------------------------------------------------------ | ---------------- |
| Sender Email  | `security-alert@paypa1-secure-verify.com`                          | Email header     |
| Reply-To      | `paypal-support-case@mail-response-center.com`                     | Email header     |
| Sender Domain | `paypa1-secure-verify.com`                                         | Email header     |
| URL           | `hxxp://paypa1-secure-verify[.]com.account-confirm[.]info/...`     | Email body       |
| IP Address    | `185.220.101.47`                                                   | Received header  |
| Attachment    | `Account_Statement.pdf.exe`                                        | Email attachment |
| Email SHA-256 | `3e2bce0ee01f9a44ebb857826928684ef7f906b4d2344afc42597a07cd9c7203` | VirusTotal       |

![IOC Summary](evidence/09-ioc-summary.png)<img width="1920" height="1080" alt="09-ioc-summary" src="https://github.com/user-attachments/assets/ad35b7ab-9cc0-433f-830d-894686403098" />


---

# 14. Phishing Indicators Identified

The investigation identified the following indicators requiring security attention:

1. Lookalike sender domain using `paypa1`.
2. Different Reply-To domain.
3. SPF authentication failure.
4. DKIM authentication failure.
5. DMARC authentication failure.
6. Deceptive URL structure.
7. Urgent account-verification request.
8. Threat of account suspension.
9. Suspicious `.pdf.exe` attachment.
10. External sending IP identified in the email headers.

![Phishing Indicators](evidence/10-phishing-indicators.png)
<img width="1303" height="637" alt="10-phishing-indicators" src="https://github.com/user-attachments/assets/b01ac7e5-e1a1-49f6-ae43-a33012133e7e" />


---

# 15. Threat Intelligence Findings

Threat intelligence analysis was performed using VirusTotal and URLScan.io.

The email file received detections from 2 of 54 security vendors in the VirusTotal analysis.

The URL and IP address were separately investigated to identify available reputation, detection, and infrastructure information.

The results were documented as supporting evidence alongside the email header and content analysis.

---

# 16. Recommended Remediation

Recommended defensive actions include:

* Block confirmed malicious URLs and domains.
* Block confirmed malicious IP addresses where appropriate.
* Quarantine similar phishing emails.
* Search mailboxes for the identified IOCs.
* Review security logs for users who interacted with the email.
* Reset credentials if credentials were submitted to a confirmed phishing page.
* Educate users about lookalike domains and suspicious attachments.
* Maintain effective SPF, DKIM, and DMARC controls.
* Monitor for additional activity associated with identified IOCs.

---

# 17. Incident Report

The detailed investigation report is available below:

[View Phishing Investigation Report](report/phishing-investigation-report.pdf)

---

# 18. Project Evidence

All investigation screenshots are available in the `evidence` directory.

The evidence demonstrates:

* Email header analysis
* Sender-domain analysis
* IOC extraction
* VirusTotal investigation
* URLScan.io investigation
* Attachment analysis
* IOC documentation
* Phishing indicator identification

---

# 19. Conclusion

The investigation demonstrated a structured phishing-email analysis workflow involving email-header examination, sender-domain analysis, IOC extraction, threat-intelligence investigation, and incident documentation.

Multiple suspicious characteristics were identified in the sample, including a lookalike sender domain, authentication failures, a deceptive URL, and a suspicious executable attachment.

The identified indicators were documented for further defensive investigation and remediation.

---

## Disclaimer

This project is intended for cybersecurity education, laboratory practice, and portfolio demonstration.

The indicators and analysis should not be treated as evidence of compromise in another environment without independent verification.
