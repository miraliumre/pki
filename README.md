# Miralium Research PKI

This repository provides an overview of the Miralium Research Public Key
Infrastructure (PKI) and hosts the Root and Leaf Certification Authorities
(CAs), their respective Certificate Revocation Lists (CRLs), and other relevant
artifacts.

## Project URLs

The official and authoritative source of information for the Miralium Research
PKI project is the project repository, accessible via the canonical URL
[https://pki.miralium.re](https://pki.miralium.re). In the event that this URL
is not accessible, [https://pki.miralium.net](https://pki.miralium.net) serves
as the fallback URL.

As of now, both URLs redirect users to the project's official repository hosted
on GitHub at
[https://github.com/miraliumre/pki](https://github.com/miraliumre/pki). If
GitHub or the specific repository becomes unavailable at any time, the canonical
URL and its fallback SHALL be updated to reflect the new location of the
official project repository.

## Scope

The initial scope of this PKI project is limited to the distribution of
certificates for personal identification. Future expansions to other uses, such
as website authentication, are possible but not covered in this document.

## Certification Authorities

### Root Certification Authorities

#### Miralium Research Personal ID Root CA P1

Currently, the **Miralium Research Personal ID Root CA P1** is the single
trusted root CA for the Miralium Research PKI. The "P" in the name indicates its
use for personal identification, and the "1" indicates that this is the first
version of this CA.

Non-CA leaf certificates issued under this root CA are restricted to the
following usages:

- **Digital Signature**: This usage is essential for the certificate holder to
  prove their identity by signing digital documents and communications.

- **Key Encipherment**: Enables the certificate holder to encipher cryptographic
  keys, ensuring that encrypted communications can be securely exchanged.

- **Client Authentication**: This usage explicitly permits the certificate to be
  used for the authentication of clients in network and online services,
  verifying the identity of the individual holder.

Certificates not adhering to these specified usages SHALL NOT be issued under
the **Miralium Research Personal ID Root CA P1** to maintain the integrity and
purpose of the PKI system.

### Leaf Certification Authorities

#### Miralium Research Staff Authentication CA P1

This is a leaf CA of **Miralium Research Personal ID Root CA P1**. This CA is
responsible for issuing leaf certificates that identify individual employees and
subcontractors of Miralium Research.

In the future, other leaf CAs may be created for other purposes, such as to
authenticate members of other organizations. Any organization operating a leaf
CA MUST undergo an audit for trust and security practices according to Miralium
Research's standards.

## Certificate Revocation

Due to the dynamic nature of personnel changes, the frequent revocation of leaf
certificates is expected. For instance, the termination of an employee's
relationship with the organization operating the leaf CA SHOULD result in the
revocation of their certificate. Therefore, verifying CRLs is crucial for
establishing the trust of a leaf certificate.

## Distribution

Root and leaf CA certificates, along with their CRLs, are distributed through
the GitHub repository. Updates to the list of trusted root and leaf CAs, as well
as CRLs, SHALL be committed to the master branch of the repository.

## Certificate Structure

### Common Name (CN)

Leaf certificates SHALL contain a Common Name (CN) corresponding to a
personally-identifying name chosen by the certificate holder. This name does not
necessarily correspond to their legal name.

### Subject Alternative Names

The certificate's Subject Alternative Names MAY include an email address and
MUST include an "other names" property with an OID of `1.3.6.1.4.1.61960.1.1`.
This property MUST be encoded as UTF-8 and contain a JSON object. The JSON
object's root keys SHALL correspond to an ISO 3166-1 alpha-3 country code, and
their value SHALL be an object including the subject's LegalName and a
government-issued ID.

For the country code `BRA`, the ID MAY be a CPF, Passport, or both. For other
countries, only a Passport is supported.

#### Example JSON Schema

```json
{
  "BRA": {
    "LegalName": "John Doe",
    "CPF": "0123456789",
    "Passport": "XXXXXXXXX"
  }
}
```

## Contributions

The repository is managed by Miralium Research and does not accept external
contributions.

## Conclusion

This document provides an overview of the Miralium Research PKI project,
outlining its structure, scope, and operational procedures. All users and
participants MUST adhere to the guidelines and requirements specified herein to
ensure the security and integrity of the PKI.
