---
title: A Method for Web Security Policies
docname: draft-foudil-securitytxt-01
ipr: trust200902
cat: info
date: 2017-10-25
pi:
  sortrefs: 'yes'
  strict: 'yes'
  symrefs: 'yes'
  toc: 'yes'
author:
- ins: E. Foudil
  name: Edwin Foudil
  email: contact@edoverflow.com

--- abstract
When security risks in web services are discovered by independent
security researchers who understand the severity of the risk, they
often lack the channels to properly disclose them. As a result,
security issues may be left unreported. security.txt defines a
standard to help organizations define the process for security
researchers to securely disclose security vulnerabilities.

--- middle

# Introduction

## Motivation

Many security researchers encounter situations where they are unable
to responsibly disclose security issues to companies because there is
no course of action laid out. security.txt is designed to help
assist in this process by making it easier for companies to designate
the preferred steps for researchers to take when trying to reach out.

## Terminology

In this document, the key words "MUST", "MUST NOT", "REQUIRED",
"SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY",
and "OPTIONAL" are to be interpreted as described in {{!RFC2119}}.

# The Specification {#specification}

security.txt is a text file that should be located under the
/.well-known/ path ("/.well-known/security.txt") {{!RFC5785}}
This text file contains 4 directives with different values.
The "directive" is the first part of a field all the way up
to the colon ("Contact:"). Directives are case-insensitive. The
"value" comes after the directive ("https://example.com/security").
A "field" always consists of a directive and a value
("Contact: https://example.com/security"). A security.txt file
can have an unlimited number of fields. It is important to note that
you need a separate line for every field. One MUST NOT chain multiple
values for a single directive. Everything MUST be in a separate field.

A security.txt file only applies to the application it is located in.

## Comments

Comments can be added using the # symbol:

~~~~~~~~~~
<CODE BEGINS>
# This is a comment.
<CODE ENDS>
~~~~~~~~~~

You MAY use one or more comments as descriptive text immediately
before the field. Parsers can then associate the comments with the
respective field.

## Separate Fields

A separate line is required for every new value and field. You MUST
NOT chain everything in to a single field. Every line must end with
a line feed character (%x0A).

## Contact:

Add an address that researchers MAY use for reporting security
issues. The value can be an email address, a phone number and/or a
security page with more information. The "Contact:" directive MUST
always be present in a security.txt file. URIs SHOULD be loaded over
HTTPS. Security email addresses SHOULD use the conventions defined
in {{!RFC2142}}.

The precedence is in listed order. The first field is the preferred
method of contact. In the example below, the e-mail address is
the preferred method of contact.

~~~~~~~~~~
<CODE BEGINS>
Contact: security@example.com
Contact: +1-201-555-0123
Contact: https://example.com/security
<CODE ENDS>
~~~~~~~~~~

## Encryption: {#encryption}

This directive allows you to add your key for encrypted
communication. You MUST NOT directly add your key. The value
MUST be a link to a page which contains your key. Keys SHOULD be
loaded over HTTPS.

~~~~~~~~~~
<CODE BEGINS>
Encryption: https://example.com/pgp-key.txt
<CODE ENDS>
~~~~~~~~~~

## Acknowledgement:

This directive allows you to link to a page where security
researchers are recognized for their reports.

~~~~~~~~~~
<CODE BEGINS>
Acknowledgement: https://example.com/hall-of-fame.html
<CODE ENDS>
~~~~~~~~~~

## Example

~~~~~~~~~~
<CODE BEGINS>
# Our security address
Contact: security@example.com

# Our PGP key
Encryption: https://example.com/pgp-key.txt
<CODE ENDS>
~~~~~~~~~~

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
                         acknowledgement-field

fs                     = ":"

comment                = "#" *(WSP / VCHAR / %xA0-E007F)

contact-field          = "Contact" fs SP (email / uri / phone)

email                  = <Email address as per {{!RFC5322}}>

phone                  = "+" *1(DIGIT / "-" / "(" / ")" / SP)

uri                    = <URI as per {{!RFC3986}}>

encryption-field       = "Encryption" fs SP uri

acknowledgement-field  = "Acknowledgement" fs SP uri

# Security considerations

Companies creating security.txt files will need to take several
security-related issues into consideration. These include exposure
of sensitive information and attacks where limited access to a server
could grant the ability to modify the contents of the security.txt
file or affect how it is served.

As stated in {{encryption}}, keys specified using the "Encryption:"
directive SHOULD be loaded over HTTPS.

# IANA Considerations

example.com is used in this document following the uses indicated in
{{!RFC2606}}.

## Well-Known URIs registry

The "Well-Known URIs" registry should be updated with the following additional
value (using the template from {{?RFC5785}}):

URI suffix: security.txt

Change controller: IETF

Specification document(s): this document

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
* Justin Calmus was always there to answer questions related to writing
this document.
* Casey Ellis had several ideas related to security.txt that helped
shape security.txt itself.
