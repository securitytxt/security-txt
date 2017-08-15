# Security.txt

Security.txt is a standard that allows websites to define security policies. This standard sets clear guidelines for security researchers for how to report security issues and allows bug bounty programs to define a scope. Security.txt is the equivalent of `robots.txt`, but for security issues.

# How it works

Create a `/security.txt` file in the website's top-level directory. Security.txt uses a similar syntax to `robots.txt`.

Here is a list of all available options:

**In-scope:** Define what targets are in scope. You can use wildcards and add your desktop applications, mobile applications, and open source projects to the list.

```
In-scope: *.example.com
In-scope: github.com/example-project
```

**Out-of-scope:** Define what targets are not in scope.

```
Out-of-scope: test.example.com
```

**Out-of-scope-vuln:** State what vulnerabilities will not be accepted in reports. For instance, if you do not want researchers to report [Clickjacking](https://www.owasp.org/index.php/Clickjacking) vulnerabilities you can do so as follows:

```
Out-of-scope-vuln: Clickjacking
```

**Rate-limit:** Set how many requests researchers can send per second.

```
Rate-limit: 1000
```

**Contact:** Add an address that researchers can use to report security issues.

```
Contact: security@example.com
```

**PGP:** Add your PGP key. You can directly add your PGP key or link to a page that contains your key.

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

**Currency:** Specify the currency for your rewards. Currency codes must be used here and not the symbol.

```
Currency: USD
```

**Reward:** Let security researchers know how much you will reward them based on the impact of the issue.

```
Reward: Medium-200
```

**Donate:** Set the value to `True` if you are willing to match reward donations. This means if a researcher wants to donate their bounty, you are willing to match the donation.

```
Donate: True
```

**Disallow:** If you do not want security researchers to test your platform, you can do the following:

```
Disallow: *
```

Comments can be added using the `#` symbol:

```
# This is a comment.
```

It is important to note, that you need a separate line for everything you specify. You cannot chain everything onto a single line.

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

In the top-level directory of your web server (http://example.com/security.txt)

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
