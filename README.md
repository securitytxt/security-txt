Security.txt is a proposed standard which allows websites to define security policies. The security.txt file sets clear guidelines for security researchers on how to report security issues, and allows bug bounty programs to define a scope. Security.txt is the equivalent of `robots.txt`, but for security issues.

> “When security risks in web services are discovered by independent security researchers who understand the severity of the risk, they often lack the channels to properly disclose them. As a result, security issues may be left unreported. Security.txt defines a standard to help organizations define the process for security researchers to securely disclose security vulnerabilities.”

---

# Website

Project website: https://securitytxt.org/ (https://github.com/securitytxt/securitytxt.org)

Internet draft website: https://securitytxt.io/ (https://github.com/securitytxt/security-txt/tree/master/docs)

# Security.txt GitHub Organization

https://github.com/securitytxt/

# Internet draft

The Internet draft for security.txt can be found here: https://tools.ietf.org/html/draft-foudil-securitytxt-06.

# Building the Draft

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

No, security.txt is supposed to accompany them.

# Code of conduct

To maintain an orderly, productive, and fun environment, the _security.txt_ project have a few guidelines that we ask people to adhere to when they are participating in contributing to the project. These guidelines apply equally to everyone within the _security.txt_ project. Likewise, they apply to all spaces managed by the _security.txt_ project, both online and offline. This includes GitHub repositories, chat rooms, in-person events, and any other communication channels.

- Be welcoming, friendly, patient, and kind.
- Be respectful.
- Be cautious with how you word things. Our goal is to remain professional.
- When we disagree, try to understand why.
- Direct contributions to the specification will only be accepted from individuals <sup>[[1]](https://en.oxforddictionaries.com/definition/individual)</sup>. The _security.txt_ project will not accept contributions to the specification in the name of an organisation. This is to ensure that the specifications and tools remain as neutral as possible.
- Registering an account on any service in the name of the _security.txt_ project must be clearly communicated via the team first.

# Contributing

Contributions from the public are welcome.

### Using the issue tracker 💡

The issue tracker is the preferred channel for bug reports and features requests. [![GitHub issues](https://img.shields.io/github/issues/securitytxt/security-txt.svg?style=flat-square)](https://github.com/securitytxt/security-txt/issues)

### Issues and labels 🏷

The bug tracker utilizes several labels to help organize and identify issues.

### Guidelines for bug reports 🐛

Use the GitHub issue search — check if the issue has already been reported.
