# Phishing URL Awareness Checker

## Project Overview
The Phishing URL Awareness Checker is a lightweight, local Python command line program used to help individuals
recognize possible signs that a phishing attack may be taking place through the use of web links. The program was
developed with an educational focus on improving user awareness regarding phishing attacks. It does this by 
analyzing raw URL strings for common structural characteristics associated with malicious activity, including but 
not limited to, raw IP address hosting; use of the @ symbol for redirecting to another site; punycode domain spoofing; 
and excessive use of subdomains.

Crucially, the tool uses only static text parsing; it does not open links, or use DNS, or make live network calls, or test
other internet-based systems.

# Technical Specifications & Environment

**Language:** Python 3.x (Tested on Python 3.13)

**Target OS:** Microsoft Windows / Cross-platform compatible

**Dependencies:** Standard Python Library only (re, urllib.parse)

**Network Requirements:** None (100% Offline)

# Implemented Code Improvements
In order to improve both usability and application stability, two significant structural enhancements were incorporated
into the codebase, extending beyond the standard baseline scripts:
## 1. Interactive Continuous Loop (Option A)
* **Description:** Switches from a single run to a while True loop for interactive use.  
* **Impact:** Users can keep sending in and checking multiple URLs in one go, without needing to restart the script every time. 
* **User Control:** Allows for easy ending of sessions, closing smoothly when the user types q, quit, or exit.

## 2. Input Validation & Crash Protection (Option C)
* **Description:** Uses try and except blocks to wrap string parsing and urllib.parse functions, allowing solid error handling. 
* **Impact:** Stops the script from crashing when it hits bad inputs like unbalanced brackets or wrong character encodings. Instead of an unhandled exception, it gives back a clear and helpful message to the user.

# Repository & Project Structure

## The project directory is structured as follows:

```text
project/
├── phishing_checker.py        # Main Python application source file
├── README.md                 # Comprehensive project documentation
├── tests/
│   └── test_samples.md       # Standardized test suite results and execution
└── screenshots/              # Execution screenshots for verification
    ├── first_link_output.png
    ├── second_link.png
    ├── third_link.png
    ├── fourth_link.png
    └── fifth_link_output.png
```

# Detection Logic & Risk Indicators

## The tool checks candidate URLs against several known structural red flags:

## 🔍 Threat Detection Indicators

The tool analyzes URLs using the following technical checks to determine risk factors:

| Risk Indicator | Technical Check | Risk Explanation |
| :--- | :--- | :--- |
| **IP Address Host** | `\d{1,3}\.\d{1,3}\...` (Regex) | Phishing attacks often bypass domain registration by using raw IP addresses for their landing pages. |
| **User Information Symbol (@)** | `@` in URL substring search | In the context of URLs, any sequence of characters appearing before the "@" symbol within the authority section is interpreted as user credentials. These credentials are employed to direct users to the host specified immediately after the symbol. |
| **Excessive Subdomains** | `split('.') >= 5` on hostname | Cybercriminals trick people by adding real brand names to subdomains, like `://paypal.com.attacker.invalid`, to mislead users. |
| **Punycode Encodings** | `xn--` string prefix check | People can misuse Internationalized Domain Names (IDN) by using similar-looking Unicode characters for homograph attacks. |
| **Insecure Scheme** | `http://` protocol evaluation | Using HTTP without encryption or verification makes your data easy to intercept. |
| **Unusual URL Length** | `len > 100` string length check | Abnormally long URLs might hide where they really lead or contain hidden harmful query codes. |

#How to Run the Application

* Open a command-line interface or PowerShell window at the top level of the project.

* Run the main Python script:

* python phishing_checker.py

* Enter any URL string when prompted by the application.

* Review the generated list of detected structural risk factors.

* To end the session, type q, quit, or exit and press Enter.

# Verification & Testing

The application was validated against standard reserved testing domains (.example, .invalid, and 192.0.2.0/24 test net ranges) to ensure all inspection logic fires as expected.

* Detailed breakdown of input cases, expected behaviors, and actual outputs can be reviewed in tests/test_samples.md.

* Image proof for each test case is available in the screenshots/ directory.