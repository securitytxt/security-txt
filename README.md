Security.txt is a "standard" which allows websites to define security policies. This "standard" sets clear guidelines for security researchers on how to report security issues, and allows bug bounty programs to define a scope. Security.txt is the equivalent of `robots.txt`, but for security issues.

---

# Website

https://securitytxt.org/ (https://github.com/securitytxt/securitytxt.org)

# Security.txt GitHub Organization

https://github.com/securitytxt/

# Internet draft

The Internet draft for security.txt can be found here: https://www.ietf.org/id/draft-foudil-securitytxt-00.txt.

## Building the Draft

To build the text and HTML drafts, use the following make command.

```sh
$ make clean
$ make txt
$ make html
```

This requires that you have the necessary software installed.  See [the
instructions](https://github.com/martinthomson/i-d-template/blob/master/doc/SETUP.md).


---

# FAQ

**What is the main purpose of `security.txt`?**

The main purpose of `security.txt` is to help make things easier for companies and security researchers when trying to secure platforms. Thanks to `security.txt`, security researchers can easily get in touch with companies about security issues.

**Is `security.txt` supposed to replace bug bounty platforms?**

No. Security.txt is supposed to accompany them.

# Contributing

Contributions from the public are welcome.

### Using the issue tracker 💡

The issue tracker is the preferred channel for bug reports and features requests. [![GitHub issues](https://img.shields.io/github/issues/securitytxt/security-txt.svg?style=flat-square)](https://github.com/securitytxt/security-txt/issues)

### Issues and labels 🏷

The bug tracker utilizes several labels to help organize and identify issues.

### Guidelines for bug reports 🐛

Use the GitHub issue search — check if the issue has already been reported.
