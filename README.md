# Phishing-Email-Detector

## Project Description

The Phishing Email Detector Tool is a Python-based command-line utility designed to analyze the content of an email and determine whether it is potentially a phishing attempt. It employs a set of rule-based detection criteria to identify suspicious elements such as urgent language, requests for sensitive information, dubious links, spoofed sender addresses, and common spelling/grammar mistakes.

The tool provides a clear classification (Safe, Suspicious, or Phishing), explains which criteria triggered the detection, and offers actionable safety suggestions to the user.

## Features

* **Input Flexibility:**
    * Accepts email content directly pasted into the terminal.
    * Can read email content from a specified text file (`.txt`).
    * (Optional future enhancement) Simulate sender email and attachments via command-line arguments.
* **Rule-Based Detection:**
    * Flags **urgent or threatening language** (e.g., "act now", "account suspended").
    * Identifies **requests for sensitive information** (e.g., "password", "credit card number").
    * Detects **suspicious links** (mismatched text/URL, shortened URLs, IP addresses in URLs, keywords in URLs).
    * Checks for **spoofed sender domains** (e.g., `paypai.com` instead of `paypal.com`).
    * Identifies **spelling and grammar mistakes**.
    * Flags **unusual attachment extensions** (e.g., `.exe`, `.js`).
* **Clear Output:**
    * **Classification:** Displays a prominent status: Safe | Suspicious | Phishing.
    * **Explanation:** Lists the specific criteria that triggered the detection, indicating their severity.
    * **Safety Suggestions:** Provides practical advice based on the detected threats (e.g., "Do not click suspicious links").
* **Bonus Feature:**
    * **Content Highlighting:** Markdown-formatted output that visually highlights suspicious phrases, keywords, and URLs within the email body.

## Tech Stack

* **Language:** Python 3.x
* **Core Libraries:**
    * `re` (built-in): For regular expressions (link and keyword detection).
    * `urllib.parse` (built-in): For parsing URLs.
    * `os` (built-in): For path manipulation (attachment extension checking).
    * `argparse` (built-in): For command-line argument parsing.
    * `textblob`: For natural language processing (spell/grammar checking).

## Setup Instructions

Follow these steps to get the Phishing Email Detector Tool up and running on your local machine.

### 1. Prerequisites

* Python 3.6 or higher installed on your system.

### 2. Clone the Repository (or Download Files)

If you have Git installed, you can clone the repository:

```bash
git clone [https://github.com/yourusername/phishing-email-detector.git](https://github.com/yourusername/phishing-email-detector.git)
cd phishing-email-detector
(If you don't have a Git repository, ensure you have both phishing_detector.py and rules.py in the same directory.)

3. Install Dependencies
Navigate to the project directory in your terminal and install the required Python libraries:

Bash

pip install textblob
After installing textblob, you also need to download its corpora (data files for NLP tasks like spell checking):

Bash

python -m textblob.download_corpora
4. Create sample_phishing.txt (Optional, but Recommended)
For easy testing, create a text file named sample_phishing.txt in the same directory as phishing_detector.py. You can paste example email content into this file.

Example sample_phishing.txt content:

Subject: Urgent: Your Account Has Been Suspended! Act NOW!!!

Dear Customer,

We regret to inform you that your PayPal account has been temporary suspended due to suspicious activity. We have detected unusal login attempts from an unknown location. To ensure the security of your account, you must immdiately verify your account details.

Please click on the link below to update your information:

Click Here To Verify Your Account: [http://paypal-security.xyz/login?id=12345](http://paypal-security.xyz/login?id=12345)

Failure to do so within 24 hours will result in permanent account closure.

Thank you for your cooperation.

Sincerely,
The PayPal Security Team
How to Use
You can use the tool in two main ways: by pasting content directly or by providing a file.

Option 1: Paste Email Content Directly (Interactive Mode)
Run the script without any file arguments. The tool will prompt you to enter the email content.

Bash

python phishing_detector.py
After running the command, you will see a prompt: Enter email content:.

Paste or type your email content.

To signal the end of input:

On Windows: Press Ctrl+Z, then press Enter.

On Linux/macOS: Press Ctrl+D.

Option 2: Analyze Email Content from a File
Provide the path to a .txt file containing the email content using the -f or --file flag.

Bash

python phishing_detector.py -f sample_phishing.txt
You can also include optional sender information and simulated attachments:

-s or --sender: Specify the sender's email address (e.g., support@example.com).

-a or --attachments: Provide a space-separated list of attachment filenames (e.g., document.exe invoice.pdf).

Example Output
Here's an example of the tool's output for a typical phishing email (like the sample_phishing.txt content provided above):

--- Analyzing email from file: sample_phishing.txt ---

Classification: Phishing

Explanation:
- [PHISHING] Use of urgent/threatening language: 'urgent'
- [PHISHING] Use of urgent/threatening language: 'act now'
- [PHISHING] Use of urgent/threatening language: 'account suspended'
- [PHISHING] Use of urgent/threatening language: 'verify your account'
- [PHISHING] Request for sensitive information: 'account details'
- [PHISHING] Suspicious link: Mismatched link text 'Click Here To Verify Your Account' and URL '[http://paypal-security.xyz/login?id=12345](http://paypal-security.xyz/login?id=12345)'
- [SUSPICIOUS] Spoofed sender domain detected: 'security@paypai.com' resembles 'paypal.com'
- [SUSPICIOUS] Multiple spelling/grammar mistakes detected (e.g., 'unusal', 'immdiately', 'temporary')
- [PHISHING] Suspicious attachment extension detected: 'report.exe'

Suggestions for User Safety:
- ACTION REQUIRED: This is highly likely a phishing email. DO NOT click any links, open attachments, or reply. Delete it immediately.
- Never share passwords, credit card numbers, or other sensitive personal information via email.
- Always hover over links to see the real URL before clicking. If it doesn't match the description or looks suspicious, don't click.
- The sender's domain looks like a legitimate one but is slightly off. This is a common phishing tactic.
- Phishing emails often contain spelling and grammar errors.
- Never open attachments with suspicious extensions (.exe, .zip, .js, etc.) unless you are absolutely sure of their origin.

--- Highlighted Suspicious Elements (Markdown formatted) ---
Subject: **Urgent**: Your Account Has Been **Suspended**! **Act NOW**!!!

Dear Customer,

We regret to inform you that your PayPal **account** has been temporary **suspended** due to suspicious activity. We have detected unusal login attempts from an unknown location. To ensure the security of your **account**, you must immdiately **verify your account** **details**.

Please **click here** on the link below to **update your information**:

**Click Here To Verify Your Account** (URL: *[http://paypal-security.xyz/login?id=12345](http://paypal-security.xyz/login?id=12345)*)

Failure to do so within 24 hours will result in permanent **account** closure.

Thank you for your cooperation.

Sincerely,
The PayPal Security Team
