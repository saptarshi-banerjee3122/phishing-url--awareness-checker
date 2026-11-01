# Test Results
Python version used: 3.13 | Operating system: Windows
Date: 29.10.2026

| # | Input | Expected result | Actual result | Pass/Fail |
|---|---|---|---|---|
| 1 | https://www.example.com/login | No listed warning signs | As Expected | Pass |
| 2 | http://192.0.2.10/account | IP address + HTTP | Uses an IP address instead of a familiar domain. Uses HTTP. HTTPS alone does not prove trust.| Pass |
| 3 | http://example.com@sample.invalid/login | @symbol + HTTP | Contains an @ symbol; inspect carefully. Uses HTTP. HTTPS alone does not prove trust.| Pass |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments | Contains many hostname segments/subdomains. | Pass|
| 5 | https://xn--example.invalid/ | Punycode-style hostname | Contains a punycode-style hostname | Pass |

