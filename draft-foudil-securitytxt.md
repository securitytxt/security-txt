---
title: A Method for Web Security Policies
docname: draft-foudil-securitytxt-02
ipr: trust200902
cat: info
pi:
  sortrefs: 'yes'
  strict: 'yes'
  symrefs: 'yes'
  toc: 'yes'
author:
- ins: E. Foudil
  name: Edwin Foudil
  email: contact@edoverflow.com
- ins: Y. Shafranovich
  name: Yakov Shafranovich
  organization: Nightwatch Cybersecurity
  email: yakov+ietf@nightwatchcybersecurity.com

--- abstract
When security risks in web services are discovered by independent
security researchers who understand the severity of the risk, they
often lack the channels to disclose them properly. As a result,
security issues may be left unreported. security.txt defines a
standard to help organizations describe the process for security
researchers to disclose security vulnerabilities securely.

--- middle

# Introduction

## Motivation

Many security researchers encounter situations where they are unable
to responsibly disclose security issues to companies because there is
no course of action laid out. security.txt is designed to help
assist in this process by making it easier for companies to designate
the preferred steps for researchers to take when trying to reach out.

As per section 4 of {{!RFC2142}}, there is an existing convention
of using the \<SECURITY@domain\> email address for communications regarding
security issues. That convention provides only a single, email-based
channel of communication for security issues per domain, and does not provide
a way for domain owners to publish information about their security disclosure
policies.

In this document, we propose a richer, machine-parsable and more extensible way
for companies to communicate information about their security disclosure
policies, which is not limited to email and also allows for additional features
such as encryption.

## Terminology

In this document, the key words "MUST", "MUST NOT", "REQUIRED",
"SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY",
and "OPTIONAL" are to be interpreted as described in {{!RFC2119}}.

# The Specification

security.txt is a text file that should be located under the
/.well-known/ path ("/.well-known/security.txt") {{!RFC5785}} for web
properties. For file systems and version control repositories a .security.txt
file should be placed in the root directory. This text file contains 4 directives
with different values. The "directive" is the first part of a field all the way up
to the colon ("Contact:"). Directives are case-insensitive. The
"value" comes after the directive ("https://example.com/security").
A "field" always consists of a directive and a value
("Contact: https://example.com/security"). A security.txt file
can have an unlimited number of fields. It is important to note that
you need a separate line for every field. One MUST NOT chain multiple
values for a single directive. Everything MUST be in a separate field.

A security.txt file only applies to the domain, subdomain, IPv4 or IPv6 address
it is located in.

~~~~~~~~~~
# The following only applies to example.com.
https://example.com/.well-known/security.txt

# This only applies to subdomain.example.com.
https://subdomain.example.com/.well-known/security.txt

# This security.txt file applies to IPv4 address of 192.0.2.0.
http://192.0.2.0/.well-known/security.txt

# This security.txt file applies to IPv6 address of 2001:db8:8:4::2.
http://[2001:db8:8:4::2]/.well-known/security.txt
~~~~~~~~~~

## Comments

Comments can be added using the # symbol:

~~~~~~~~~~
# This is a comment.
~~~~~~~~~~

You MAY use one or more comments as descriptive text immediately
before the field. Parsers can then associate the comments with the
respective field.

## Separate Fields

A separate line is required for every new value and field. You MUST
NOT chain everything into a single field. Every line must end with
a line feed character (%x0A).

## Contact: {#contact}

Add an address that researchers MAY use for reporting security
issues. The value can be an email address, a phone number and/or a
contact page with more information. The "Contact:" directive MUST
always be present in a security.txt file. URIs SHOULD be loaded over
HTTPS. Security email addresses SHOULD use the conventions defined
in section 4 of {{!RFC2142}}, but there is no requirement for this directive
to be an email address.

While URIs already include the ability to have both email address and phone
numbers via "mailto" and "tel" prefixes, allowing this information to be listed
without a prefix is intended for ease of use and readability.

The precedence is in listed order. The first field is the preferred
method of contact. In the example below, the e-mail address is
the preferred method of contact.

~~~~~~~~~~
Contact: security@example.com
Contact: +1-201-555-0123
Contact: https://example.com/security-contact.html
~~~~~~~~~~

## Encryption: {#encryption}

This directive allows you to add your key for encrypted
communication. You MUST NOT directly add your key. The value
MUST be a link to a page which contains your key. Keys SHOULD be
loaded over HTTPS.

~~~~~~~~~~
Encryption: https://example.com/pgp-key.txt
~~~~~~~~~~

## Signature: {#signature}

To ensure the authenticity of the security.txt file one SHOULD use the
"Signature:" directive, which allows you to link to an external signature. External signature files should be
named "security.txt.sig" and also be placed under the /.well-known/ path.
External signature files SHOULD be loaded over HTTPS.

Here is an example of an external signature file.

~~~~~~~~~~
Signature: https://example.com/.well-known/security.txt.sig
~~~~~~~~~~

## Policy: {#policy}

With the Policy directive, you can link to where your security policy and/or disclosure policy is located. This can help security researchers understand what you are looking for and how to report security vulnerabilities.

~~~~~~~~~~
Policy: https://example.com/security-policy.html
~~~~~~~~~~

## Acknowledgments: {#Acknowledgments}

This directive allows you to link to a page where security
researchers are recognized for their reports. The page should list individuals or companies
that disclosed security vulnerabilities and worked with you to remediate the issue.

~~~~~~~~~~
Acknowledgments: https://example.com/hall-of-fame.html
~~~~~~~~~~

Example security acknowledgments page:

~~~~~~~~~~
We would like to thank the following researchers:

(2017-04-15) Frank Denis - Reflected cross-site scripting
(2017-01-02) Alice Quinn  - SQL injection
(2016-12-24) John Buchner - Stored cross-site scripting
(2016-06-10) Anna Richmond - A server configuration issue
~~~~~~~~~~

## Example

~~~~~~~~~~
# Our security address
Contact: security@example.com

# Our PGP key
Encryption: https://example.com/pgp-key.txt

# Our security policy
Encryption: https://example.com/security-policy.html

# Our security acknowledgments page
Acknowledgments: https://example.com/hall-of-fame.html

# Verify this security.txt file
Signature: https://example.com/.well-known/security.txt.sig
~~~~~~~~~~

# Location of the security.txt file

~~~~~~~~~~
                          External
+---------------------------------------------------------------+
|              Default                                          |
|  +-----------------------------+          +----------------+  |
|  |                             | Redirect |                |  |
|  |  /.well-known/security.txt  <----------+  security.txt  |  |
|  |                             |          |                |  |
|  +-----------------------------+          +----------------+  |
|                                                               |
+---------------------------------------------------------------+

        Internal
+------------------------+
|                        |
|  +------------------+  |
|  |                  |  |
|  |  /.security.txt  |  |
|  |                  |  |
|  +------------------+  |
|                        |
+------------------------+
~~~~~~~~~~

## Web-based services

Web-based services SHOULD place the security.txt file under the /.well-known/ path; e.g. https://example.com/.well-known/security.txt.

## Filesystems

File systems SHOULD place the security.txt file under the root directory; e.g., /.security.txt, C:\.security.txt.

~~~~~~~~~~
user:/$ l
.security.txt
example-directory-1/
example-directory-2/
example-directory-3/
example-file
~~~~~~~~~~

## Internal hosts

A .security.txt file SHOULD be placed in the root directory of an internal host to trigger incident response.

## Extensibility {#extensibility}

Like many other formats and protocols, this format may need to be extended
over time to fit the ever-changing landscape of the Internet. Therefore,
extensibility is provided via an IANA registry for headers fields as defined
in {{registry}}. Any fields registered via that process MUST be
considered optional. To encourage extensibility and interoperability,
implementors MUST ignore any fields they do not explicitly support.

# File Format Description

The expected file format of the security.txt file is plain text as defined
in section 4.1.3 of {{!RFC2046}} and encoded in UTF-8.

The following is an ABNF definition of the security.txt format, using
the conventions defined in {{!RFC5234}}.

body                   = *line (contact-field eol) *line

line                   = *1(field / comment) eol

eol                    = *WSP \[CR\] LF

field                  = contact-field /
                         encryption-field /
                         acknowledgments-field /
                         ext-field

fs                     = ":"

comment                = "#" *(WSP / VCHAR / %xA0-E007F)

contact-field          = "Contact" fs SP (email / uri / phone)

email                  = <Email address as per {{!RFC5322}}>

phone                  = "+" *1(DIGIT / "-" / "(" / ")" / SP)

uri                    = <URI as per {{!RFC3986}}>

encryption-field       = "Encryption" fs SP uri

signature-field        = "Signature" fs SP uri

policy-field           = "Policy" fs SP uri

Acknowledgments-field  = "Acknowledgments" fs SP uri

ext-field              = field-name fs SP unstructured

field-name             = <as per section 3.6.8 of {{!RFC5322}}>

unstructured           = <as per section 3.2.5 of {{!RFC5322}}>

"ext-field" refers to extension fields, which are discussed in {{extensibility}}

# Security considerations

Organizations creating security.txt files will need to consider several
security-related issues. These include exposure
to sensitive information and attacks where limited access to a server
could grant the ability to modify the contents of the security.txt
file or affect how it is served. Organizations SHOULD also monitor
their security.txt files regularly to detect tampering.

To ensure the authenticity of the security.txt file, organizations SHOULD
sign the file and include the signature using the "Signature:"
directive.

As stated in {{encryption}} and {{signature}}, both encryption keys
and external signature files SHOULD be loaded over HTTPS.

# IANA Considerations

example.com is used in this document following the uses indicated in
{{!RFC2606}}.

192.0.2.0 and 2001:db8:8:4::2 are used in this document following
the uses indicated in {{!RFC6890}}.


## Well-Known URIs registry

The "Well-Known URIs" registry should be updated with the following additional
values (using the template from {{?RFC5785}}):

URI suffix: security.txt

URI suffix: security.txt.sig

Change controller: IETF

Specification document(s): this document

## Registry for security.txt Header Fields {#registry}

IANA is requested to create the "security.txt Header Fields" registry in
accordance with {{?RFC8126}}. This registry will contain header fields for
use in security.txt files, defined by this specification.

New registrations or updates MUST be published in accordance with the
"Specification Required" guidelines as described in section 4.6 of
{{?RFC8126}}. Any new field thus registered is considered optional
by this specification unless a new version of this specification is published.

New registrations and updates MUST contain the following information:

   1.  Name of the field being registered or updated
   2.  Short description of the field
   3.  Whether the field can appear more than once
   4.  The document in which the specification of the field is published
   5.  New or updated status, which MUST be one of:
       current:  The field is in current use
       deprecated:  The field is in current use, but its use is discouraged
       historic:  The field is no longer in current use

An update may make a notation on an existing registration indicating
that a registered field is historical or deprecated if appropriate.

The initial registry contains these values:

       Field Name: Acknowledgment
       Description: link to page where security researchers are recognized
       Multiple Appearances: Yes
       Published in: this document
       Status: current

       Field Name: Contact
       Description: contact information to use for reporting security issues
       Multiple Appearances: Yes
       Published in: this document
       Status: current

       Field Name: Encryption
       Description: link to a key to be used for encrypted communication
       Multiple Appearances: Yes
       Published in: this document
       Status: current

       Field Name: Signature
       Description: signature used to verify the authenticity of the file
       Multiple Appearances: No
       Published in: this document
       Status: current

       Field Name: Policy
       Description: link to security policy page
       Multiple Appearances: No
       Published in: this document
       Status: current

# Contributors

The editor would like to acknowledge the help provided during the
development of this document by the following individuals:

* Tom Hudson helped writing the "File Format Description" and wrote
several security.txt parsers.
* Joel Margolis was a big help when it came to wording this document
appropriately.
* Jobert Abma for raising issues and concerns that might arise when
using certain directives.
* Gerben Janssen van Doorn for reviewing this document multiple times.
* Austin Heap for helping improve the Internet drafts.
* Justin Calmus was always there to answer questions related to writing
this document.
* Casey Ellis had several ideas related to security.txt that helped
shape security.txt itself.

--- back
# Note to Readers

> **Note to the RFC Editor:**  Please remove this section prior
> to publication.

Development of this draft takes place on Github at https://github.com/securitytxt/security-txt

# Document History

> **Note to the RFC Editor:**  Please remove this section prior
> to publication.

## Since draft-foudil-securitytxt-00
- Moved to use IETF's markdown tools for draft updates
- Added table of contents and a fuller list of references
- Moved file to .well-known URI and added IANA registration (#3)
- Added extensibility with an IANA registry for fields (#34)
- Added text explaining relationship to RFC 2142 / security@ email address (#25)
- Scope expanded to include internal hosts, domains, IP addresses and file systems
- Support for digital signatures added (#19)

The full list of changes can be viewed via the IETF document tracker:
https://tools.ietf.org/html/draft-foudil-securitytxt-01

## Since draft-foudil-securitytxt-01
- Added appendix with pointer to Github and document history
- Added external signature file to the well known URI registry (#59)
- Added policy field (#53)
- Added diagram explaining the location of the file on public vs. internal systems
- Added recommendation that external signature files should use HTTPS (#55)
- Added recommendation that organizations should monitor their security.txt files (#14)

## Since draft-foudil-securitytxt-02
- Cleaning up text based on the NITS tools suggestions (#82)


The full list of changes can be viewed via the IETF document tracker:
https://tools.ietf.org/html/draft-foudil-securitytxt-02
