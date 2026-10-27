# Test Results

Python version used: 3.12 | Operating system: Linux | Date: 2026-10-27

| # | Input | Expected result | Actual result | Pass/Fail |
|---|-------|-----------------|---------------|-----------|
| 1 | https://www.example.com/login | No listed warning signs | No listed warning signs found. This does NOT prove safety. | PASS |
| 2 | http://192.0.2.10/account | IP address + HTTP | Uses an IP address instead of a familiar domain. / Uses HTTP. HTTPS alone does not prove trust. | PASS |
| 3 | http://example.com@sample.invalid/login | @ symbol + HTTP | Contains an @ symbol; inspect carefully. / Uses HTTP. HTTPS alone does not prove trust. | PASS |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments | Contains many hostname segments/subdomains. | PASS |
| 5 | https://xn--example.invalid/ | Punycode-style hostname | Contains a punycode-style hostname. | PASS |

## Bonus checks

| Input | Actual result |
|-------|---------------|
| (just Enter) | No URL entered. |
| www.example.com | Uses HTTP (missing scheme is treated as http://) |
| https://secure-login.example.invalid | No listed warning signs found. (A tricky name can slip through.) |
| http://[bad | This text is not a valid URL format. (no crash after Improvement C) |

## Notes

I re-ran all five tests after adding my four improvements (loop, summary, error handling, explanations) and every test still passed.
The surprising part was https://secure-login.example.invalid: it looks suspicious to a human but has none of the six signs, so "no warnings" really does not mean "safe".
Before Improvement C, typing http://[bad crashed the program with a ValueError; now it shows a friendly message.
