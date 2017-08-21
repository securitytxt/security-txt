# Security.txt

Security.txt is a "standard" which allows websites to define security policies. This "standard" sets clear guidelines for security researchers on how to report security issues, and allows bug bounty programs to define a scope. Security.txt is the equivalent of `robots.txt`, but for security issues.

*Note:* I (@EdOverflow) am currently working on the RFC for this idea.

# How it works

The `/security.txt` file should be located under `/.well-known/` (`/.well-known/security.txt`) [[RFC5785](https://tools.ietf.org/html/rfc5785)]. Security.txt uses a similar syntax to `robots.txt`.

Here is a list of all available options:

**In-scope:** Define which targets are in scope. You can use wildcards and add your desktop applications, mobile applications, and open source projects to the list.

```
In-scope: *.example.com
In-scope: github.com/example-project
```

**Out-of-scope:** Define which targets are not in scope.

```
Out-of-scope: test.example.com
```

**Out-of-scope-vuln:** State which vulnerabilities will not be accepted in reports. For example, if you do not want researchers to report [Clickjacking](https://www.owasp.org/index.php/Clickjacking) vulnerabilities, you can do as follows:

```
Out-of-scope-vuln: Clickjacking
```

**Rate-limit:** Set how many requests researchers can send per second.

```
Rate-limit: 1000
```

**Contact:** Add an address that researchers can use for reporting security issues.

```
Contact: security@example.com
```

<!-- TODO: Add keybase. -->

**PGP:** Add your PGP key. You can directly add your PGP key or link to a page which contains your key.

```
PGP-key: -----BEGIN PGP PUBLIC KEY BLOCK-----
...
-----END PGP PUBLIC KEY BLOCK----- 
```

```
PGP-key: http://example.com/pgp-key.txt
```

**Security-page:** Link to your company's more detailed security page.

```
Security-page: http://example.com/security
```

**Platform:** If your company uses a bug bounty platform (HackerOne, Bugcrowd, etc.) you can add it with this option.

```
Platform: https://hackerone.com/example
```

**Payment-method:** State payment method your company will use when rewarding a researcher.

```
Payment-method: PayPal
```

**Currency:** Specify reward currency. Currency codes must be used here and not the symbol.

```
Currency: USD
```

**Reward:** Let security researchers know how much you will reward them based on the impact of the issue.

```
Reward: Medium-200
```

**Donate:** Set the value to `True` if you are willing to match reward donations. This means if a researcher wants to donate their bounty, you are willing to match their donation.

```
Donate: True
```

**Disclosure:** Specify your disclosure policy. This can be a disclosure type and/or a timeframe (in days).

```
Disclosure: Full-30
```

**Disallow:** If you do not want security researchers to test your platform, you can do the following:

```
Disallow: *
```

Comments can be added using the `#` symbol:

```
# This is a comment.
```

It is important to note that you need a separate line for everything you specify. You cannot chain everything onto a single line.

```
Out-of-scope-vuln: Clickjacking
Out-of-scope-vuln: Self-XSS
Out-of-scope-vuln: Open Redirect
```

# Example

```
# In scope targets
In-scope: *.example.com

# Out of scope targets
Out-of-scope: test.example.com

# Out of scope vulnerabilities
Out-of-scope-vuln: Clickjacking

# Our security address
Contact: security@example.com

# Our HackerOne program
Platform: https://hackerone.com/example
```

# FAQ

**What is the main purpose of `security.txt`?**

The main purpose of `security.txt` is to help make things easier for companies and security researchers when trying to secure platforms. Thanks to `security.txt`, security researchers can easily get in touch with companies about security issues.

**Where should I put the `security.txt` file?**

The `/security.txt` file should be located under `/.well-known/` (`/.well-known/security.txt`) [[RFC5785](https://tools.ietf.org/html/rfc5785)].

http://example.com/.well-known/security.txt

**Is `security.txt` supposed to replace bug bounty platforms?**

No. Security.txt is supposed to accompany them. You can use the `Platform:` option to link to your bug bounty program.

# Contributing

Contributions from the public are welcome.

### Using the issue tracker 💡

The issue tracker is the preferred channel for bug reports and features requests. [![GitHub issues](https://img.shields.io/github/issues/EdOverflow/security-txt.svg?style=flat-square)](https://github.com/EdOverflow/security-txt/issues)

### Issues and labels 🏷

The bug tracker utilizes several labels to help organize and identify issues.

### Guidelines for bug reports 🐛

Use the GitHub issue search — check if the issue has already been reported.
