# task-2

### 1. Obtain a Sample Phishing Email

Collected a phishing email sample from an open-source repository (PhishTank/GitHub). The email was saved as a `.txt` / `.eml` file for analysis. This sample impersonates a legitimate organization to trick the user into clicking malicious links or revealing credentials.

---

### 2. Examine Sender's Email Address for Spoofing

**Finding:** The display name shows a trusted brand (e.g., "PayPal Support") but the actual email address is `support@paypa1-secure.com` — note the **"1" instead of "l"** in the domain. This is a classic **typosquatting** technique used to deceive victims at a glance.

---

### 3. Check Email Headers for Discrepancies

**Tool Used:** MXToolbox Header Analyzer

**Findings:**

- `Return-Path` does not match the `From` address
- **SPF:** Fail — sender IP not authorized
- **DKIM:** Not signed
- **DMARC:** Fail — no policy enforced
- Originating IP traced to an unknown/suspicious server

*(Add your MXToolbox screenshot here)*

---

### 4. Identify Suspicious Links or Attachments

**Tool Used:** VirusTotal / URLScan.io

**Finding:** The email contained a button labeled "Verify Your Account" which on hover reveals the actual URL as `http://malicious-login.xyz/paypal` instead of `paypal.com`. VirusTotal flagged this URL as **malicious** by multiple vendors.

*(Add VirusTotal screenshot here)*

---

### 5. Look for Urgent or Threatening Language

**Finding:** The email body contained phrases like:

- *"Your account will be suspended within 24 hours"*
- *"Immediate action required"*

This is a **social engineering tactic** designed to create panic and make the victim act without thinking critically.

---

### 6. Note Any Mismatched URLs

**Finding:** Visible link text says `www.paypal.com/verify` but the actual hyperlink destination is `http://malicious-login.xyz/paypal`. This mismatch is a strong phishing indicator — always hover before clicking.

---

### 7. Verify Spelling or Grammar Errors

**Findings:**

- "Dear Costumer" instead of "Customer"
- "Please to verify your account informations"
- Inconsistent fonts and formatting throughout the email

These errors are common in phishing emails, often because they are written by non-native speakers or auto-generated.

## Interview Quetions ans Answers

1) What is phishing?

"Phishing is a social engineering attack where attackers impersonate legitimate entities through fake emails or websites to steal credentials, financial data, or personal information. It exploits human trust rather than technical vulnerabilities."

---

2) How to identify a phishing email?

"Look for these red flags:

- Suspicious sender email address (not just display name)
- Urgent or threatening language
- Unexpected attachments or links
- Requests for sensitive information
- Poor grammar or spelling
- Generic greetings like 'Dear Customer'

Always hover over links before clicking and verify through official channels when in doubt."

---

3) What is email spoofing?

"Email spoofing is forging the sender's address to make emails appear from trusted sources. SMTP doesn't verify sender identity by default. We prevent this using SPF, DKIM, and DMARC protocols that authenticate legitimate senders and reject spoofed emails."

---

4) Why are phishing emails dangerous?

"Phishing emails are dangerous because they:

- Bypass technical security controls by targeting humans
- Can lead to credential theft and account compromise
- Enable malware delivery through attachments
- Result in financial fraud and wire transfer scams
- Provide initial access for larger breaches
- Only need one employee to click to succeed"

---

5) How can you verify the sender's authenticity?

"Verify senders by:

- Checking the full email address, not just the display name
- Contacting the sender through a separate, known-good channel
- Calling official company numbers from their website
- Checking email headers for routing information
- Looking for SPF, DKIM, and DMARC authentication results
- Never using contact info from the suspicious email itself"

---

6) What tools can analyze email headers?

"Common tools include:

- **MXToolbox** - web-based header analyzer
- **Google's Message Header Analyzer** - checks Gmail headers
- **Microsoft Message Header Analyzer** - for Outlook
- **Mail Header Analyzer by MHA** - detailed breakdown
- **Built-in email client options** - most email clients show raw headers

These reveal routing information, authentication results, originating IP addresses, and help identify spoofed or malicious emails."

---

7) What actions should be taken on suspected phishing emails?

"Immediate actions:

1. **Don't click** any links or open attachments
2. **Don't reply** or provide any information
3. **Report** to IT security team immediately
4. **Mark as phishing** using your email client's reporting feature
5. **Delete** after reporting
6. **Verify independently** if it claims to be urgent
7. **Warn colleagues** if it's targeted at your organization

---

8) How do attackers use social engineering in phishing?

"Attackers exploit psychological triggers:

- **Authority** - impersonating executives or officials
- **Urgency** - creating false deadlines and threats
- **Fear** - account suspension or legal consequences
- **Curiosity** - enticing subject lines or offers
- **Trust** - appearing as known contacts or brands
- **Helpfulness** - posing as IT support needing credentials
- **Greed** - fake prizes, bonuses, or opportunities