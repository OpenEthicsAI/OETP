# Open Ethics Transparency Protocol - Internet Draft

Version: 0.9.3

Format: [IETF](https://www.ietf.org/) Request for Comments (RFC)

State: [Internet Draft](https://www.ietf.org/standards/ids/)

Last update: 2020-12-18

Authors: Nikita Lukianets

***

## Status of this Memo

This document is the Internet Draft, it contains a Proposed Standard description for the Internet community, and requests discussion and suggestions for improvements.

This document is planned to be brought in accordance with the RFC publication requirements for the Internet Standards Track protocol as described in [RFC322](https://www.rfc-editor.org/rfc/rfc7322) and [RFC841](https://www.rfc-editor.org/rfc/rfc7841).

Information about the current status of this document, any errata, and how to provide feedback on it may be obtained at [https://openethics.ai/oetp/](https://openethics.ai/oetp/).

## Copyright Notice

Copyright (C) 2020 Open Ethics and the persons identified as the document authors. All Rights Reserved.

## Abstract

The Open Ethics Transparency Protocol (OETP) is an application-level protocol for publishing and accessing ethical disclosures. The protocol is based on HTTP transfer of OETP-formatted information about the ethical &quot;postures&quot; of Automated Decision-Making (ADM) systems to allow more transparent, predictable, and safe environments for the end-users. The OETP Disclosure Format is an extensible JSON-based format.

***

## Contents

1. [Introduction](#introduction)

2. [Requirement Levels](#requirement-levels)

3. [Terminology](#terminology)

      1. [Automated Decision-Making (ADM)](#automated-decision-making-(adm))

      2. [Disclosure](#disclosure)

      3. [Disclosure Feed](#disclosure-feed)

      4. [Product](#product)

      5. [Vendor](#vendor)

      6. [Integrator](#integrator)

      7. [OETP Disclosure Format](#oetp-disclosure-format)

      8.  [Validation](#validation)

      9.  [Auditor](#auditor)

      10. [Verification](#verificatino)

      11. [Chaining](#chaining)

      12. [Label](#label)

4.  [Protocol Model](#protocol-model)

    1.  [Initial Disclosure](#initial-disclosure)

        1.  [Disclosure Signature](#disclosure-signature)

        2.  [Storage](#storage)

        3.  [Labeling](#labeling)

    2.  [Access to Disclosure](#access-to-disclosure)

    3.  [Automated Disclosure processing](#automated-disclosure-processing)

    4.  [End-to-end transparency and formation of the composite Disclosure](#end-to-end-transparency-and-formation-of-the-composite-disclosure)

        1.  [Open Vendor Policy](#open-vendor-policy)

        2.  [Request for Vendor&#39;s Disclosures](#request-for-vendors-disclosures)

        3.  [Validation of Vendor&#39;s Disclosures](#validation-of-vendors-disclosures)

        4.  [Verification of Vendor&#39;s Disclosures](#verification-of-vendors-disclosures)

        5.  [Disclosure Chaining](#disclosure-chaining)

5.  [Example OETP Disclosure File](#example-oetp-disclosure-file)

6.  [Security Considerations](#security-considerations)

    1.  [Response content](#response-content)

    2.  [Spoofing](#spoofing)

    3.  [Falsification](#falsification)

7.  [IANA Considerations](#iana-considerations)

8.  [Areas for Future Study](#areas-of-future-study)

9.  [References](#references)

    1.  [Normative References](#normative-references)

    2.  [Informative References](#informative-references)

10. [Author&#39;s Address](#authors-address)

## Introduction

The Open Ethics Transparency Protocol (OETP) is brought as a solution to increase transparency of products and services of the IT sector. The introduction of the protocol targets enabling the concept of Ethical Operations (EthOps) where every Automated Decision-Making system (ADM) can disclose its data collection and data processing practice as Open Data in a standardized format.

The protocol supports ethical disclosure of ADMs and provides facilities for:

- **Informed consumer choices** : End-users able to make informed choices based on their own ethical preferences and ADM disclosure.
- **Industrial scale monitoring** : Discovery of best and worst practices within market verticals, technology stacks, and product value offerings.
- **Legally-agnostic guidelines** : Suggestions for developers and product-owners, formulated in factual language, which are legally-agnostic and could be easily transformed into product requirements and safeguards.
- **Iterative improvement** : Digital products, specifically, the ones powered by artificial intelligence could receive a nearly real-time feedback on how their performance and ethical posture could be improved to cover security, privacy, diversity, fairness, power-balance, non-discrimination, and other requirements.
- **Labeling and certification** : Mapping to existing and future regulatory initiatives and standards.

OETP is an application-level protocol for publishing and accessing ethical disclosures. The protocol is based on HTTP transfer of OETP-formatted information about the ethical &quot;postures&quot; of ADMs to allow more transparent, predictable, and safe environments for the end-users. The OETP Disclosure Format is an extensible JSON-based format.

## Requirement Levels

The key words &quot;MUST&quot;, &quot;MUST NOT&quot;, &quot;REQUIRED&quot;, &quot;SHALL&quot;, &quot;SHALL NOT&quot;, &quot;SHOULD&quot;, &quot;SHOULD NOT&quot;, &quot;RECOMMENDED&quot;, &quot;MAY&quot;, and &quot;OPTIONAL&quot; in this document are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

## Terminology

### Automated Decision-Making (ADM)

Automated decision-making is the process of making a decision by automated means without any human involvement. These decisions can be based on factual data, as well as on digitally created profiles or inferred data.

### Disclosure

Disclosure, or &quot;self-disclosure&quot; is the application-specific information about the data collection, data-processing, and decision-making practices of the ADM Product, provided by its Vendor (a company) or a developer (an individual).

### Disclosure Feed

A historical sequence of Disclosures, made by and for a specific ADM Product.

### Product

An ADM system in the form of a software, service, application, or a physically embodied autonomous decision-making agent.

### Vendor

A legal entity (an organization) that owns one or several ADM products and provides services for the end-users or for other Vendors.

### Integrator

An organization that deploys services based on product(s) from 3rd party Vendors to the end users.

### OETP Disclosure Format

A machine-readable Disclosure with predefined structure, supplied in the JSON format.

### Validation

A sequence of automated software-based checks to control validity and security elements in the OETP Disclosure.

### Auditor

A third-party organization, trusted to perform verification checks.

### Verification

A procedure to control the correspondence of the elements in the OETP Disclosure and the actual data processing and data collection practices of the Vendors.

### Chaining

A process of combining Vendor Disclosures into a composite high-level ADM disclosure.

### Label

A user-facing graphical and textual descriptions of the ADM Product facilitating understanding of the values and risks it is carrying.

## Protocol Model

### Initial Disclosure

The initial ADM Product disclosure is performed using a standardized disclosure form (for Example, see 1. [https://openethics.ai/label/](https://openethics.ai/label/)). The Developer or a Product Owner MUST submit data-processing and data-collection information on behalf of the Vendor. The information about the end-point URL, as well as a contact email address MUST be specified.

#### Disclosure Signature

The Disclosure is organized into a predefined data schema and MUST be cryptographically signed using standard SHA3-512 hash implementation by the Disclosure recepient (Open Ethics). The integrity hash MUST be appended to a disclosure as OETP.shcema.integrity element.

#### Storage

Both the signature integrity hash and the Disclosure is stored in the log-centric Open Ethics database and MAY be mirrored by other distributed databases for redundancy and safety.

#### Labeling

Open Ethics Label SHOULD be automatically formed by mirroring the submitted Disclosure into a set of graphical icons and simple user-facing descriptions. Additional Labels MAY be formed by mapping of the regulatory requirements to Disclosures.

### Access to Disclosure

The OETP file SHOULD be stored in the root of the product&#39;s end-point URL. When establishing vendor relationship, Integrator or a downstream Vendor may examine their Vendors disclosure using the following HTTP request: `GET https://testexample.com/oetp.json`, where *testexample.com* is the URL of the sub-processor&#39;s end-point.

### Automated Disclosure processing

The automated disclosure processing is enabled by requests to both Open Ethics Disclosure database and the Product&#39;s OETP Disclosure.

### End-to-end transparency and formation of the composite Disclosure

A surface-level transparency is not sufficient as IT industry is getting more mature with more specialized Vendors, that are providing more narrow ADM Products to Integrators and to bigger Vendors. The following steps MUST be satisfied for end-to-end transparency:

#### Open Vendor Policy

Every Integrator or a Vendor SHOULD supply the URLs of their sub-processing Vendors, indicating the scope of the data processing.

#### Request for Vendor&#39;s Disclosures

The OETP Processing system MUST crawl the URLs of the expected sub-processing Vendors disclosures and specifies which of them have Disclosures.

#### Validation of Vendor&#39;s Disclosures

The OETP Processing system MUST compare integrity hashes in Open Ethics Disclosure database and entries that arrive from Disclosure Requests

#### Verification of Vendor&#39;s Disclosures

Every disclosure MAY be checked for the existence of the external verification from Auditors for the entire Disclosures or for one of their elements.

#### Disclosure Chaining

The same procedure is being repeated recursively for Vendors of the Vendors, and for the Vendors of the Vendors of the Vendors, etc.

## Example OETP Disclosure File

```javascript
{
    "schema": {
        "name": "Open Ethics Transparency Protocol",
        "version": "0.9.3 RFC",
        "integrity": "156d624b8f2dbea87128a2147f255842652475c5dc595c79f64c90c7ff486d59007c3e18c993e3163395812e26b70ea70dfc413f7ca128869d115f12e5699bf2"
    },
    "snapshot": {
        "product": {
            "url": "testexample.com",
            "description": ""
        },
        "timestamp": 1608273946,
        "generator": {
            "name": "Open Ethics",
            "alias": "oe",
            "type": "root",
            "website": "https://openethics.ai"
        },
        "label": {
            "data": {
                "type": "open",
                "practice": ""
            },
            "source": {
                "type": "open",
                "practice": ""
            },
            "decision": {
                "type": "restricted",
                "practice": ""
            }
        }
    }
}
```

## Security Considerations

### Response content

OETP exchanges data using JSON ([RFC159](https://www.rfc-editor.org/rfc/rfc7159)) which is a light weight data-interchange format. JSON-based application can be attacked in multiple ways such as, sending data in an improper format or embedding attack vectors in the data. It is important for any applications using JSON format to validate the inputs before being processed. To mitigate this attack type, the JSON Key Profile is provided for OETP responses.

### Spoofing

OETP Processors should be aware of the potential for spoofing attacks where the attacker publishes an OETP disclosure with the OETP.snapshot value from another product, or, perhaps with an outdated OETP.snapshot.label element. For example, an OETP Processor could suppress display of falsified entries by comparing the snapshot integrity from the submission database and a calculated hash for the OETP.snapshot object. In that situation, the OETP Processor might also take steps to determine whether the disclosures originated from the same publisher require further investigation of the Disclosure Feed and alert the downstream OETP Processors.

### Falsification

Dishonest or falsified Disclosures is the problem that is hard to address generally. The approach to it is the public control and systematic checks. Vendors or user-facing applications and services could further raise the level of trust to their Disclosures by implementing programmatic control scoring mechanisms, as well as the external verification by trusted Auditors.

## IANA Considerations

This document has no IANA actions.

## Areas for Future Study

The following topics not addressed in this version of LDP are possible areas for future study:

- IANA requests for the Data Processor identity management.
- Extensibility if the OETP Disclosure Format.
- Disclosure Chaining mechanisms and various use-cases.
- Typical scenarios and templates for Disclosure submissions.
- Mapping of the regulatory requirements and future Disclosure elements.
- Standardizing privacy Disclosure and PII data-collection practices.

## References

### Normative References

- TBD

### Informative References

- The JavaScript Object Notation (JSON) Data Interchange Format [https://www.rfc-editor.org/rfc/rfc7159](https://www.rfc-editor.org/rfc/rfc7159)
- RFC Style Guide [https://www.rfc-editor.org/rfc/rfc7322](https://www.rfc-editor.org/rfc/rfc7322)
- RFC Streams, Headers, and Boilerplates [https://www.rfc-editor.org/rfc/rfc7841](https://www.rfc-editor.org/rfc/rfc7841)

## Author&#39;s Address

Nikita Lukianets

[n.lukianets@openethics.ai](mailto:n.lukianets@openethics.ai)
