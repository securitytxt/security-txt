---
title: A File Format to Aid in Security Vulnerability Disclosure
abbrev: security.txt
docname: draft-foudil-securitytxt-12
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

informative:
    ISO.8601:
      title: ISO/IEC 8601, Date and time - Representations for information interchange - Parts 1 and 2
      author:
          org: International Organization for Standardization (ISO)
      date: 2019
    ISO.29147.2018:
      title: ISO/IEC 29147:2018, Information technology - Security techniques - Vulnerability disclosure
      author:
          org: International Organization for Standardization (ISO)
      date: 2018
    CERT.CVD:
      title: The CERT Guide to Coordinated Vulnerability Disclosure (CMU/SEI-2017-SR-022)
      author:
          org: Software Engineering Institute, Carnegie Mellon University
      date: 2017


--- abstract
When security vulnerabilities are discovered by
researchers, proper reporting channels are often lacking. As a result,
vulnerabilities may be left unreported. This document defines a machine-parsable format
("security.txt") to help organizations describe their vulnerability disclosure practices
to make it easier for researchers to report vulnerabilities.

--- middle

# Introduction

## Motivation, Prior Work and Scope {#motivation}

Many security researchers encounter situations where they are unable
to report security vulnerabilities to organizations because there are
no reporting channels to contact the owner of a particular
resource and no information available about the vulnerability disclosure practices
of such owner.

As per section 4 of {{?RFC2142}}, there is an existing convention
of using the \<SECURITY@domain\> email address for communications regarding
security issues. That convention provides only a single, email-based
channel of communication per domain, and does not provide
a way for domain owners to publish information about their security disclosure
practices.

There are also contact conventions prescribed for Internet Service Providers (ISPs)
in section 2 of {{?RFC3013}}, for Computer Security Incident Response Teams (CSIRTs)
in section 3.2 of {{?RFC2350}} and for site operators in section 5.2 of
{{?RFC2196}}. As per {{?RFC7485}}, there is also contact information provided by
Regional Internet Registries (RIRs) and domain registries for owners of IP
addresses, autonomous system numbers (ASNs), and domain names. However, none of
these tackle the issue of how security researchers can locate contact information
and vulnerability disclosure practices for organizations in order to report
vulnerabilities.

In this document, we define a richer, machine-parsable and more extensible way
for organizations to communicate information about their security disclosure
practices and ways to contact them. Other details of vulnerability disclosure
are outside the scope of this document. Readers are encouraged to consult other
documents such as {{ISO.29147.2018}} or {{CERT.CVD}}.

As per {{CERT.CVD}}, "vulnerability response" refers to reports of product vulnerabilities
which is related but distinct from reports of network intrusions and compromised
websites ("incident response"). The mechanism defined in this document is intended
to be used for the former ("vulnerability response"). If implementors want
to utilize this mechanism for incident response, they should be aware of additional
security considerations discussed in {{compromise}}.

The "security.txt" file is intended to be complementary and not as a substitute
or replacement for other public resources maintained by organizations regarding
their security disclosure practices.

## Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
BCP 14 {{!RFC2119}} {{!RFC8174}} when, and only when, they appear in all
capitals, as shown here.

The term "researcher" corresponds
to the terms "finder" and "reporter" in {{ISO.29147.2018}} and {{CERT.CVD}}.
The term "organization" corresponds to the term "vendor"
in {{ISO.29147.2018}} and {{CERT.CVD}}.

The term "implementors" includes all parties involved in
the vulnerability disclosure process.

# Note to Readers

> **Note to the RFC Editor:**  Please remove this section prior
> to publication.

Development of this draft takes place on Github at: https://github.com/securitytxt/security-txt

# The Specification

This document defines a text file to be placed in a known location
that provides information about vulnerability disclosure practices of a particular organization.
The format of this file is machine-parsable following the ABNF grammar defined in
{{abnf}}. This file is intended to help security researchers when
disclosing security vulnerabilities.

By convention, the file is named "security.txt". Location and scope are described
in {{location}}.

This text file contains multiple fields with different values. A field contains a "name" which is the first part of a field all the way up
to the colon (for example: "Contact:") and follows the syntax defined for "field-name" in section 3.6.8
of {{!RFC5322}}. Field names are case-insensitive (as per section 2.3 of {{!RFC5234}}).
The "value" comes after the field name (for example: "mailto:security@example.com") and follows the syntax
defined for "unstructured" in section 3.2.5 of {{!RFC5322}}. The file MAY also contain blank lines.

A field MUST always consist of a name and a value
(for example: "Contact: mailto:security@example.com"). A security.txt file
can have an unlimited number of fields. Each field MUST appear on
its own line. Unless specified otherwise by the field definition,
multiple values MUST NOT be chained together for a single field.
Unless otherwise indicated in a definition of a particular field, a field MAY appear
multiple times.

Implementors should be aware that some of the fields may
contain URIs using percent-encoding (as per section 2.1 of {{!RFC3986}}).

## Comments

Any line beginning with the "#" (%x23) symbol MUST be interpreted as a comment.
The content of the comment may contain any ASCII or Unicode characters in the
%x21-7E and %x80-FFFFF ranges plus the tab (%x09) and space (%x20) characters.

Example:

~~~~~~~~~~
# This is a comment.
~~~~~~~~~~

## Line Separator

Every line MUST end either with a carriage return and line feed
characters (CRLF / %x0D %x0A) or just a line feed character (LF / %x0A).

## Digital signature {#signature}

It is RECOMMENDED that a security.txt file be digitally signed
using an OpenPGP cleartext signature as described in
section 7 of {{!RFC4880}}. When digital signatures are used, it is also
RECOMMENDED that organizations use the "Canonical" field (as per {{canonical}}),
thus allowing the digital signature to authenticate the location of the file.

When it comes to verifying the key used to generate the signature, it is always
the security researcher's responsibility to make sure the key being
used is indeed one they trust. Researchers should use other ways to obtain
and verify the key (such as {{?I-D.koch-openpgp-webkey-service}}).

## Extensibility {#extensibility}

Like many other formats and protocols, this format may need to be extended
over time to fit the ever-changing landscape of the Internet. Therefore,
extensibility is provided via an IANA registry for fields as defined
in {{registry}}. Any fields registered via that process MUST be
considered optional. To encourage extensibility and interoperability,
researchers MUST ignore any fields they do not explicitly support.

In general, implementors should "be conservative in what you do,
be liberal in what you accept from others" (as per {{?RFC0793}}).

## Field Definitions

Unless otherwise stated, all fields MUST be considered optional.

### Acknowledgments {#acknowledgments}

This field indicates a link to a page where security
researchers are recognized for their reports. The page being referenced
should list security researchers that reported security vulnerabilities
and collaborated to remediate them. Organizations should be careful
to limit the vulnerability information being published in order
to prevent future attacks.

If this field indicates a web URI, then it MUST begin with "https://"
(as per section 2.7.2 of {{!RFC7230}}).

Example:

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

### Canonical {#canonical}

This field indicates the canonical URIs where the security.txt file is located,
which is usually something like "https://example.com/.well-known/security.txt".
If this field indicates a web URI, then it MUST begin with "https://"
(as per section 2.7.2 of {{!RFC7230}}).

While this field indicates that a "security.txt" retrieved from a given URI
is intended to apply to that URI, it MUST NOT be interpreted to apply to
all canonical URIs listed within the file. Researchers SHOULD use an additional
trust mechanism such as a digital signature (as per {{signature}}) to make the
determination that a particular canonical URI is applicable.

If this field appears within a "security.txt" file, and the URI used to
retrieve that file is not listed within any canonical fields,
then the contents of the file SHOULD NOT be trusted.

~~~~~~~~~~
Canonical: https://www.example.com/.well-known/security.txt
Canonical: https://someserver.example.com/.well-known/security.txt
~~~~~~~~~~

### Contact {#contact}

This field indicates an address that researchers
should use for reporting security
vulnerabilities such as an email address, a phone number and/or a
web page with contact information. The "Contact" field MUST
always be present in a security.txt file. If this field indicates a web URI,
then it MUST begin with "https://" (as per section 2.7.2 of {{!RFC7230}}).
Security email addresses should use the conventions defined in section
4 of {{!RFC2142}}.

The value MUST follow the URI syntax described in section 3 of {{!RFC3986}}.
This means that "mailto" and "tel" URI schemes must be used
when specifying email addresses and telephone numbers, as defined in {{!RFC6068}}
and {{!RFC3966}}. When the value of this field is an email address,
it is RECOMMENDED that encryption be used (as per {{encryption}}).

The precedence SHOULD be in listed order. The first occurrence is the preferred
method of contact. In the example below, the first email address
("security@example.com") is the preferred method of contact.

~~~~~~~~~~
Contact: mailto:security@example.com
Contact: mailto:security%2Buri%2Bencoded@example.com
Contact: tel:+1-201-555-0123
Contact: https://example.com/security-contact.html
~~~~~~~~~~

### Encryption {#encryption}

This field indicates an encryption key that
security researchers should use for encrypted communication. Keys MUST NOT
appear in this field - instead the value of this field
MUST be a URI pointing to a location where the key can be retrieved.
If this field indicates a web URI, then it MUST begin with "https://"
(as per section 2.7.2 of {{!RFC7230}}).

When it comes to verifying the authenticity of the key, it is always the security
researcher's responsibility to make sure the key being specified is indeed one
they trust. Researchers must not assume that this key is
used to generate the digital signature referenced in {{signature}}.

Example of an OpenPGP key available from a web server:

~~~~~~~~~~
Encryption: https://example.com/pgp-key.txt
~~~~~~~~~~

Example of an OpenPGP key available from an OPENPGPKEY DNS record:

~~~~~~~~~~
Encryption: dns:5d2d37ab76d47d36._openpgpkey.example.com?type=OPENPGPKEY
~~~~~~~~~~

Example of an OpenPGP key being referenced by its fingerprint:

~~~~~~~~~~
Encryption: openpgp4fpr:5f2de5521c63a801ab59ccb603d49de44b29100f
~~~~~~~~~~

### Expires {#expires}

This field indicates the date and time after which the data contained in the "security.txt"
file is considered stale and should not be used (as per {{stale}}). The value of this field is formatted
according to the Internet profile of {{ISO.8601}} as defined in {{!RFC3339}}. It is RECOMMENDED that the value
of this field be less than a year into the future to avoid staleness.

This field MUST always be present and MUST NOT appear more than once.

~~~~~~~~~~
Expires: 2021-12-31T18:37:07z
~~~~~~~~~~

### Hiring {#hiring}

The "Hiring" field is used for linking to the vendor's security-related job positions.
If this field indicates a web URI, then it MUST begin with "https://"
(as per section 2.7.2 of {{!RFC7230}}).

~~~~~~~~~~
Hiring: https://example.com/jobs.html
~~~~~~~~~~

### Policy {#policy}

This field indicates a link to where the vulnerability disclosure policy is located.
This can help security researchers understand
the organization's vulnerability reporting practices.
If this field indicates a web URI, then it MUST begin with "https://"
(as per section 2.7.2 of {{!RFC7230}}).

Example:

~~~~~~~~~~
Policy: https://example.com/disclosure-policy.html
~~~~~~~~~~

### Preferred-Languages {#preflang}

This field can be used to indicate a set of natural languages that
are preferred when submitting security reports. This set MAY list multiple
values, separated by commas. If this field is included then at least
one value MUST be listed. The values within this set are language tags
(as defined in {{!RFC5646}}). If this field is absent, security researchers
may assume that English is the language to be used (as per section 4.5
of {{!RFC2277}}).

The order in which they appear is not an indication of priority;
the listed languages are intended to have equal priority.

This field MUST NOT appear more than once.

Example (English, Spanish and French):

~~~~~~~~~~
Preferred-Languages: en, es, fr
~~~~~~~~~~

## Example of an unsigned "security.txt" file

~~~~~~~~~~
# Our security address
Contact: mailto:security@example.com

# Our OpenPGP key
Encryption: https://example.com/pgp-key.txt

# Our security policy
Policy: https://example.com/security-policy.html

# Our security acknowledgments page
Acknowledgments: https://example.com/hall-of-fame.html

Expires: 2021-12-31T18:37:07z
~~~~~~~~~~

## Example of a signed "security.txt" file

~~~~~~~~~~
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

# Canonical URI
Canonical: https://example.com/.well-known/security.txt

# Our security address
Contact: mailto:security@example.com

# Our OpenPGP key
Encryption: https://example.com/pgp-key.txt

# Our security policy
Policy: https://example.com/security-policy.html

# Our security acknowledgments page
Acknowledgments: https://example.com/hall-of-fame.html

Expires: 2021-12-31T18:37:07z
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v2.2

[signature]
-----END PGP SIGNATURE-----
~~~~~~~~~~

# Location of the security.txt file {#location}

For web-based services, organizations MUST place the security.txt file under the "/.well-known/" path; e.g. https://example.com/.well-known/security.txt
as per {{!RFC8615}} of a domain name or IP address. For legacy compatibility, a security.txt file might be placed at the top-level path
or redirect (as per section 6.4 of {{!RFC7231}}) to the security.txt file under the "/.well-known/" path. If a "security.txt" file
is present in both locations, the one in the "/.well-known/" path MUST be used.

The file MUST be accessed via HTTP 1.0 or a higher version
and the file access MUST use "https" scheme (as per section 2.7.2 of {{!RFC7230}}).
It MUST have a Content-Type of "text/plain"
with the default charset parameter set to "utf-8" (as per section 4.1.3 of {{!RFC2046}}).

Retrieval of "security.txt" files and resources indicated within such files may result in a redirect (as per
section 6.4 of {{!RFC7231}}). Researchers should perform additional analysis (as per {{redirects}}) to make sure these redirects
are not malicious or pointing to resources controlled by an attacker.

## Scope of the File

A "security.txt" file MUST only apply to the domain
or IP address in the URI used to retrieve it, not to any of its subdomains or parent domains.
A "security.txt" file MAY also apply to products and services provided by the organization publishing the file.

As per {{motivation}}, this specification is intended for vulnerability response.
If implementors want to use this for incident response, they should be aware of additional security considerations discussed in {{compromise}}.

Organizations SHOULD use the policy directive (as per {{policy}})
to provide additional details regarding scope and details of their vulnerability disclosure process.

Some examples appear below:

~~~~~~~~~~
# The following only applies to example.com.
https://example.com/.well-known/security.txt

# This only applies to subdomain.example.com.
https://subdomain.example.com/.well-known/security.txt

# This security.txt file applies to IPv4 address of 192.0.2.0.
https://192.0.2.0/.well-known/security.txt

# This security.txt file applies to IPv6 address of 2001:db8:8:4::2.
https://[2001:db8:8:4::2]/.well-known/security.txt
~~~~~~~~~~


# File Format Description and ABNF Grammar {#abnf}

The file format of the "security.txt" file MUST be plain text (MIME type "text/plain") as defined
in section 4.1.3 of {{!RFC2046}} and MUST be encoded using UTF-8 {{!RFC3629}} in Net-Unicode form {{!RFC5198}}.

The format of this file MUST follow the ABNF definition below (using
the conventions defined in {{!RFC5234}}).

~~~~~~~~~~
body             =  signed / unsigned

signed           =  sign-header unsigned sign-footer

sign-header      =  < headers and line from section 7 of [RFC4880] >

sign-footer      =  < OpenPGP signature from section 7 of [RFC4880] >

unsigned         =  *line (contact-field eol) ; one or more required
                    *line (expires-field eol) ; exactly one required
                    *line [lang-field eol] *line ; exactly one optional
                    ; order of fields within the file is not important
                    ; except that if contact-field appears more
                    ; than once the order of those indicates
                    ; priority (see Section 3.5.3)

line             =  [ (field / comment) ] eol

eol              =  *WSP [CR] LF

field            =  ; optional fields
                    ack-field /
                    can-field /
                    contact-field / ; optional repeated instances
                    encryption-field /                         
                    hiring-field /
                    policy-field /
                    ext-field

fs               =  ":"

comment          =  "#" *(WSP / VCHAR / %x80-FFFFF)

ack-field        =  "Acknowledgments" fs SP uri

can-field        =  "Canonical" fs SP uri

contact-field    =  "Contact" fs SP uri

expires-field    =  "Expires" fs SP date-time

encryption-field =  "Encryption" fs SP uri

hiring-field     =  "Hiring" fs SP uri

lang-field       =  "Preferred-Languages" fs SP lang-values

policy-field     =  "Policy" fs SP uri

date-time        =  < imported from section 5.6 of [RFC3339] >

lang-tag         =  < Language-Tag from section 2.1 of [RFC5646] >

lang-values      =  lang-tag *(*WSP "," *WSP lang-tag)

uri              =  < URI as per section 3 of [RFC3986] >

ext-field        =  field-name fs SP unstructured

field-name       =  < imported from section 3.6.8 of [RFC5322] >

unstructured     =  < imported from section 3.2.5 of [RFC5322] >
~~~~~~~~~~

"ext-field" refers to extension fields, which are discussed in {{extensibility}}

# Security Considerations

Because of the use of URIs and well-known resources, security considerations of
{{!RFC3986}} and {{!RFC8615}} apply here, in addition to the
considerations outlined below.

## Compromised Files and Incident Response {#compromise}

An attacker that has compromised a website is able to compromise
the "security.txt" file as well or setup a redirect to their own site.
This can result in security reports not being received by the organization
or sent to the attacker.

To protect against this, organizations should use the "Canonical" field to indicate the locations
of the file (as per {{canonical}}), digitally sign their "security.txt"
files (as per {{signature}}), and regularly monitor the file and
the referenced resources to detect tampering.

Security researchers should validate the "security.txt" file including verifying
the digital signature and checking any available historical records before using the information
contained in the file. If the "security.txt" file looks suspicious or compromised,
it should not be used.

While it is not recommended, implementors may choose to use the information published
within a "security.txt" file for incident response. In such cases, extreme caution
should be taken before trusting such information, since
it may have been compromised by an attacker. Researchers should use additional methods
to verify such data including out of band verification of the PGP signature, DNSSEC-based approaches, etc.

## Redirects {#redirects}

When retrieving the file and any resources referenced in the file, researchers should record
any redirects since they can lead to a different domain or IP address controlled by an attacker. Further
inspections of such redirects is recommended before using the information contained within the file.

## Incorrect or Stale Information {#stale}

If information and resources referenced in a "security.txt" file are incorrect
or not kept up to date, this can result in security reports not being received
by the organization or sent to incorrect contacts, thus exposing possible
security issues to third parties. Not having a security.txt file may be preferable
to having stale information in this file. Organizations must use
the "Expires" field (see {{expires}}) to indicate to researchers when
the data in the file is no longer valid.

Organizations should ensure that information in this file and any referenced
resources such as web pages, email addresses, and telephone numbers
are kept current, are accessible, controlled by the organization,
and are kept secure.

## Intentionally Malformed Files, Resources and Reports

It is possible for compromised or malicious sites to create files that are extraordinarily
large or otherwise malformed in an attempt to discover or exploit weaknesses
in parsing code. Researchers should make sure that any such code
is robust against large or malformed files and fields, and may choose not to parse
files larger than 32 KBs, having fields longer than 2,048 characters or
containing more than 1,000 lines. The ABNF grammar (as defined in
{{abnf}}) can also be used as a way to verify these files.

The same concerns apply to any other resources referenced within security.txt
files, as well as any security reports received as a result of publishing
this file. Such resources and reports may be hostile, malformed or malicious.

## No Implied Permission for Testing

The presence of a security.txt file might be interpreted by researchers
as providing permission to do security testing against the domain or IP address
where it is published, or products and services provided by the organization publishing
the file.
This might result in increased testing against an organization by researchers. On the other hand, a decision not
to publish a security.txt file might be interpreted by the
organization operating that website to be a way to signal to researchers
that permission to test that particular site or project is denied. This might result in pushback against
researchers reporting security issues to that organization.

Therefore, researchers shouldn't assume that presence or absence of
a "security.txt" file grants or denies permission for security testing.
Any such permission may be indicated in the company's vulnerability disclosure policy
(as per {{policy}}) or a new field (as per {{extensibility}}).

## Multi-user Environments

In multi-user / multi-tenant environments, it may possible for a user to take
over the location of the "security.txt" file. Organizations should reserve
the "security.txt" namespace at the root to ensure no third-party can create a page with
the "security.txt" AND "/.well-known/security.txt" names.

## Protecting Data in Transit

To protect a "security.txt" file from being tampered with in transit, implementors MUST use
HTTPS (as per section 2.7.2 of {{!RFC7230}}) when serving the file itself and for retrieval of any web URIs
referenced in it (except when otherwise noted in this specification). As part of the TLS
handshake, researchers should validate the provided X.509 certificate
in accordance with {{!RFC6125}} and the following considerations:

- Matching is performed only against the DNS-ID identifiers.

- DNS domain names in server certificates MAY contain the wildcard
character '*' as the complete left-most label within the identifier.

The certificate may also be checked for revocation via the Online Certificate Status
Protocol (OCSP) {{!RFC6960}}, certificate revocation lists (CRLs), or similar mechanisms.

In cases where the "security.txt" file cannot be served via HTTPS (such as localhost) or is
being served with an invalid certificate, additional human validation is recommended since
the contents may have been modified while in transit.

As an additional layer of protection, it is also recommended that
organizations digitally sign their "security.txt" file with OpenPGP (as per {{signature}}).
Also, to protect security reports from being tampered with or observed while in transit,
organizations should specify encryption keys (as per {{encryption}}) unless
HTTPS is being used for report submission.

However, the determination of validity of such keys is out of scope
for this specification. Security researchers need to establish other secure means to
verify them.

## Spam and Spurious Reports

Similar to concerns in {{!RFC2142}}, denial of service attacks via spam reports
would become easier once a "security.txt" file is published by
an organization. In addition, there is an increased likelihood of reports
being sent in an automated fashion and/or as result of automated scans without
human analysis. Attackers can also use this file as a way to spam unrelated
third parties by listing their resources and/or contact information.

Organizations need to weigh the advantages of publishing this file versus
the possible disadvantages and increased resources required to analyze
security reports.

Security researchers should review all information within the "security.txt"
file before submitting reports in an automated fashion or as resulting from automated scans.

# IANA Considerations

Implementors should be aware that any resources referenced within
a security.txt file MUST NOT point to the Well-Known URIs namespace unless
they are registered with IANA (as per {{?RFC8615}}).

## Well-Known URIs registry

The "Well-Known URIs" registry should be updated with the following additional
values (using the template from {{?RFC8615}}):

URI suffix: security.txt

Change controller: IETF

Specification document(s): this document

Status: permanent

## Registry for security.txt Fields {#registry}

IANA is requested to create the "security.txt Fields" registry in
accordance with {{?RFC8126}}. This registry will contain fields for
use in security.txt files, defined by this specification.

New registrations or updates MUST be published in accordance with the
"Expert Review" guidelines as described in sections 4.5 and 5 of
{{?RFC8126}}. Any new field thus registered is considered optional
by this specification unless a new version of this specification is published.

Designated Experts are expected to check whether a proposed registration or update
makes sense in the context of industry accepted vulnerability disclosure processes
such as {{ISO.29147.2018}} and {{CERT.CVD}}, and provides value to organizations
and researchers using this format.

New registrations and updates MUST contain the following information:

   1.  Name of the field being registered or updated
   2.  Short description of the field
   3.  Whether the field can appear more than once
   4.  The document in which the specification of the field is published (if available)
   5.  New or updated status, which MUST be one of:
       - current: The field is in current use
       - deprecated: The field has been in use, but new usage is discouraged
       - historic: The field is no longer in current use
   6. Change controller

An update may make a notation on an existing registration indicating
that a registered field is historical or deprecated if appropriate.

The initial registry contains these values:

       Field Name: Acknowledgments
       Description: link to page where security researchers are recognized
       Multiple Appearances: Yes
       Published in: this document
       Status: current
       Change controller: IETF

       Field Name: Canonical
       Description: canonical URI for this file
       Multiple Appearances: Yes
       Published in: this document
       Status: current
       Change controller: IETF

       Field Name: Contact
       Description: contact information to use for reporting vulnerabilities
       Multiple Appearances: Yes
       Published in: this document
       Status: current
       Change controller: IETF

       Field Name: Expires
       Description: date and time after which this file is considered stale
       Multiple Appearances: No
       Published in: this document
       Status: current
       Change controller: IETF

       Field Name: Encryption
       Description: link to a key to be used for encrypted communication
       Multiple Appearances: Yes
       Published in: this document
       Status: current
       Change controller: IETF

       Field Name: Hiring
       Description: link to the vendor's security-related job positions
       Multiple Appearances: Yes
       Published in: this document
       Status: current
       Change controller: IETF

       Field Name: Policy
       Description: link to security policy page
       Multiple Appearances: Yes
       Published in: this document
       Status: current
       Change controller: IETF

       Field Name: Preferred-Languages
       Description: list of preferred languages for security reports
       Multiple Appearances: No
       Published in: this document
       Status: current
       Change controller: IETF

# Contributors

The authors would like to acknowledge the help provided during the
development of this document by Tom Hudson, Jobert Abma,
Gerben Janssen van Doorn, Austin Heap, Stephane Bortzmeyer, Max Smith, Eduardo Vela, and Krzysztof Kotowicz.

The authors would also like to acknowledge the feedback provided by multiple members of IETF's
LAST CALL, SAAG, and SECDISPATCH lists.

Yakov would like to also thank L.T.S. (for everything).

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

The full list of changes can be viewed via the IETF document tracker:
https://tools.ietf.org/html/draft-foudil-securitytxt-02

## Since draft-foudil-securitytxt-02
- Use "mailto" and "tel" (#62)
- Fix typo in the "Example" section (#64)
- Clarified that the root directory is a fallback option (#72)
- Defined content-type for the response (#68)
- Clarify the scope of the security.txt file (#69)
- Cleaning up text based on the NITS tools suggestions (#82)
- Added clarification for newline values
- Clarified the encryption field language, added examples
of DNS-stored encryption keys (#28 and #94)
- Added "Hiring" field

## Since draft-foudil-securitytxt-03
- Added "Hiring" field to the registry section
- Added an encryption example using a PGP fingerprint (#107)
- Added reference to the mailing list (#111)
- Added a section referencing related work (#113)
- Fixes for idnits (#82)
- Changing some references to informative instead of normative
- Adding "Permission" field (#30)
- Fixing remaining ABNF issues (#83)
- Additional editorial changes and edits

## Since draft-foudil-securitytxt-04
- Addressing IETF feedback (#118)
- Case sensitivity clarification (#127)
- Syntax fixes (#133, #135 and #136)
- Removed permission field (#30)
- Removed signature field and switched to inline signatures (#93 and #128)
- Adding canonical field (#100)
- Text and ABNF grammar improvements plus ABNF changes for comments (#123)
- Changed ".security.txt" to "security.txt" to be consistent

## Since draft-foudil-securitytxt-05
- Changing HTTPS to MUST (#55)
- Adding language recommending encryption for email reports (#134)
- Added language handling redirects (#143)
- Expanded security considerations section and fixed typos (#30, #73, #103, #112)

## Since draft-foudil-securitytxt-06
- Fixed ABNF grammar for non-chainable fields (#150)
- Clarified ABNF grammar (#152)
- Clarified redirect logic (#143)
- Clarified comments (#158)
- Updated references and template for well-known URI to RFC 8615
- Fixed nits from the IETF validator

## Since draft-foudil-securitytxt-07
- Addressing AD feedback (#165)
- Fix for ABNF grammar in lang-values (#164)
- Fixing idnits warnings
- Adding guidance for designated experts

## Since draft-foudil-securitytxt-08
- Added language and example regarding URI encoding (#176)
- Add "Expires" field (#181)
- Changed language from "directive" to "field" (#182)
- Addressing last call feedback (#179, #180 and #183)
- Clarifying order of fields (#174)
- Revert comment/field association (#158)

## Since draft-foudil-securitytxt-09
- Adjust ABNF to allow blank lines between directives (#191)
- Make "Expires" field required (#190)
- Adding a warning about the well-known URI namespace (#188)
- Adding scope language around products/services (#185)
- Addressing last call feedback (#189)

## Since draft-foudil-securitytxt-10
- Changes addressing IESG feedback
- Removed language regarding file systems (#201)
- Adding language to explain alignment with the CERT CVD guide (#202)

## Since draft-foudil-securitytxt-11
- Changed date format from RFC 5322 to RFC 3339 / ISO 8601 (#208)
- Added clarification in "canonical" field regarding the URI used to retrieve the file
- Added language about machine-
- Added a reference to the PGP webkey draft

Full list of changes can be viewed via the IETF document tracker:
https://tools.ietf.org/html/draft-foudil-securitytxt
