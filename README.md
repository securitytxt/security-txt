<p align="center"><img src=https://avatars2.githubusercontent.com/u/32488600?s=100&v=4></p>

security.txt provides a way for websites to define security policies.
The security.txt file sets clear guidelines for security researchers on how to report security issues.
security.txt is the equivalent of `robots.txt`, but for security issues.

> “ When security vulnerabilities are discovered by researchers, proper reporting channels are often lacking.  As a result, vulnerabilities may be left unreported.  This document defines a format ("security.txt") to help organizations describe their vulnerability disclosure practices to make it easier for researchers to report vulnerabilities.”

---

# RFC and Registry for Extensions
The definitive reference on security.txt and how it is used can be found in
[RFC 9116](https://www.rfc-editor.org/info/rfc9116).

Extensions to security.txt can be found in
[an IANA registry](https://www.iana.org/assignments/security-txt-fields/security-txt-fields.xhtml#security-txt-fields)

# Website
Project website: https://securitytxt.org/ (https://github.com/securitytxt/securitytxt.org)

# Security.txt GitHub Organization

https://github.com/securitytxt/

# Frequently asked questions

**What is the main purpose of security.txt?**

The main purpose of security.txt is to help make things easier for companies and security researchers when trying to secure platforms. Thanks to security.txt, security researchers can easily get in touch with companies about security issues.

**Is security.txt an [RFC](https://en.wikipedia.org/wiki/Request_for_Comments)?**

Yes, it was published by the IETF as [RFC 9116](https://www.rfc-editor.org/info/rfc9116).
There is also [a related IANA registry](https://www.iana.org/assignments/security-txt-fields/security-txt-fields.xhtml#security-txt-fields).

Information about previous drafts can be found in the "archived" folder and
at [the IETF's Datatracker website](https://datatracker.ietf.org/doc/rfc9116/).

**Where should I put the security.txt file?**

For websites, the security.txt file should be placed under the `/.well-known/` path
(`/.well-known/security.txt`) [[<abbr title="Request For Comments">RFC</abbr>8615](https://tools.ietf.org/html/rfc8615)].
It can also be placed in the root directory (`/security.txt`) of a website, especially
if the `/.well-known/` directory cannot be used for technical reasons, or simply as a fallback.
Please consult [section 3 of RFC 9116 for details](https://www.rfc-editor.org/rfc/rfc9116.html#name-location-of-the-securitytxt).

**Are there any settings I should apply to the file?**

The security.txt file should have an Internet Media Type of `text/plain` and must be served over HTTPS.

**Will adding an email address expose me to spam bots?**

The email value is an optional field. If you are worried about spam, you can set a URI as the value and link to your security policy.

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
