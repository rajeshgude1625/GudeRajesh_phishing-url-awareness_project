# Test Results

Python version used: 3.14.4 | Operating system: Windows | Date: 2026-11-01

| # | Input | Expected result | Actual result | Pass/Fail |
|---|-------|-----------------|---------------|-----------|
| 1 | https://www.example.com/login | No listed warning signs | No listed warning signs found. This does NOT prove safety. | PASS |
| 2 | http://192.0.2.10/account | IP address + HTTP | Uses an IP address instead of a familiar domain. / Uses HTTP. HTTPS alone does not prove trust. | PASS |
| 3 | http://example.com@sample.invalid/login | @ symbol + HTTP | Contains an @ symbol; inspect carefully. / Uses HTTP. HTTPS alone does not prove trust. | PASS |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments | Contains many hostname segments/subdomains. | PASS |
| 5 | https://xn--example.invalid/ | Punycode-style hostname | Contains a punycode-style hostname. | PASS |

## Bonus checks

| Input | Actual result | Pass/Fail |
|-------|---------------|-----------|
| (empty, just Enter) | No URL entered. | PASS |
| www.example.com | Uses HTTP. HTTPS alone does not prove trust. | PASS |
| https://secure-login.example.invalid | No listed warning signs found. This does NOT prove safety. | PASS |
| http://[bad | This text is not a valid URL format. (no crash after Improvement C) | PASS |
| https://www.example.com/ + 90 letters "a" | Unusually long URL (over 100 characters). | PASS |

## Notes

The program ran the same way for all five samples after I added the four improvements, so none of them broke the original checks.
A URL like https://secure-login.example.invalid has no warning signs even though the name looks suspicious, which shows that "no warnings" does not mean "safe".
Before Improvement C, typing http://[bad crashed the program with a ValueError; now it prints a friendly message instead.
