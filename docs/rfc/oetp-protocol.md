<style type="text/css">
  body {
    margin: auto;
    max-width: 44em;
    font-family: Calibri, sans-serif;
    font-size: 18pt;
  }

  /* automatic heading numbering */
  h1 { counter-reset: h2counter; }
  h2 { counter-reset: h3counter; }
  h3 { counter-reset: h4counter; }
  h4 { counter-reset: h5counter; }
  h5 { counter-reset: h6counter; }
  h6 { }
  h2:before {
    counter-increment: h2counter;
    content: counter(h2counter) ".\0000a0\0000a0";
  }
  h3:before {
    counter-increment: h3counter;
    content: counter(h2counter) "."
             counter(h3counter) ".\0000a0\0000a0";
  }
  h4:before {
    counter-increment: h4counter;
    content: counter(h2counter) "."
             counter(h3counter) "."
             counter(h4counter) ".\0000a0\0000a0";
  }
  h5:before {
    counter-increment: h5counter;
    content: counter(h2counter) "."
             counter(h3counter) "."
             counter(h4counter) "."
             counter(h5counter) ".\0000a0\0000a0";
  }
  h6:before {
    counter-increment: h6counter;
    content: counter(h2counter) "."
             counter(h3counter) "."
             counter(h4counter) "."
             counter(h5counter) "."
             counter(h6counter) ".\0000a0\0000a0";
  }
</style>

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

The Open Ethics Transparency Protocol (OETP) is an application-level protocol for publishing and accessing ethical Disclosures of IT Products and their Components. The Protocol is based on HTTP exchange of information about the ethical &quot;postures&quot;, provided in an open and standardized format. The scope of the Protocol covers Disclosures for systems such as Software as a Service (SaaS) Applications, Software Applications, Software Components, Application Programming Interfaces (API), Automated Decision-Making (ADM) systems, and systems using Artificial Intelligence (AI). OETP aims to bring more transparent, predictable, and safe environments for the end-users. The OETP Disclosure Format is an extensible JSON-based format.

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

The Open Ethics Transparency Protocol (OETP or Protocol) describes creation and exchange of voluntary ethics Disclosures for IT products. It is brought as a solution to increase transparency of how IT products are built and deployed. This document provides details on how disclosures for data collection and data processing practice are formed, stored, validated, and exchanged in a standardized and open format.

OETP provides facilities for:

- **Informed consumer choices** : End-users able to make informed choices based on their own ethical preferences and product disclosure.
- **Industrial scale monitoring** : Discovery of best and worst practices within market verticals, technology stacks, and product value offerings.
- **Legally-agnostic guidelines** : Suggestions for developers and product-owners, formulated in factual language, which are legally-agnostic and could be easily transformed into product requirements and safeguards.
- **Iterative improvement** : Digital products, specifically, the ones powered by artificial intelligence could receive a nearly real-time feedback on how their performance and ethical posture could be improved to cover security, privacy, diversity, fairness, power-balance, non-discrimination, and other requirements.
- **Labeling and certification** : Mapping to existing and future regulatory initiatives and standards.

The Open Ethics Transparency Protocol (OETP) is an application-level protocol for publishing and accessing ethical Disclosures of IT products and their components. The Protocol is based on HTTP exchange of information about the ethical &quot;postures&quot;, provided in an open and standardized format. The scope of the Protocol covers Disclosures for systems such as Software as a Service (SaaS) Applications, Software Applications, Software Components, Application Programming Interfaces (API), Automated Decision-Making (ADM) systems, and systems using Artificial Intelligence (AI). OETP aims to bring more transparent, predictable, and safe environments for the end-users. The OETP Disclosure Format is an extensible JSON-based format.

## Requirement Levels

The key words &quot;MUST&quot;, &quot;MUST NOT&quot;, &quot;REQUIRED&quot;, &quot;SHALL&quot;, &quot;SHALL NOT&quot;, &quot;SHOULD&quot;, &quot;SHOULD NOT&quot;, &quot;RECOMMENDED&quot;, &quot;MAY&quot;, and &quot;OPTIONAL&quot; in this document are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

## Terminology

### Disclosure

Disclosure, Ethics Disclosure, or &quot;self-disclosure&quot; is an application-specific information about the data collection, data-processing, and decision-making practices of a Product, provided by Product Vendor (an individual developer or an organization).

### Disclosure Feed

A historical sequence of Disclosures, made for a specific Product.

### Vendor

A legal person (an individual developer or an organization) that owns one or several end-user Products, or acts as a Supplier and provides Components for other Vendors.

### Integrator

A legal person (an individual developer or an organization) that deploys services to the end-users based on Product(s) from third-party Vendors.

### Product

An IT system in the form of a software, software as a service system, application, software component, application programming interface, or a physically embodied automated decision-making agent.

### Component

An IT system supplied by Vendor and integrated/embedded into end-user Products. Components themselves do not necessarily interface with end-users.

### Automated Decision-Making (ADM)

Automated decision-making is the process of making a decision by automated means without any human involvement. These decisions can be based on factual data, as well as on digitally created profiles or inferred data.

### OETP Disclosure Format

A machine-readable Disclosure with predefined structure, supplied in the JSON format.

### Validation

A sequence of automated software-based checks to control validity and security elements in the OETP Disclosure.

### Auditor

A third-party legal person, trusted to perform Verification checks and to issue Verification Proofs.

### Auditing software

An automated software-based tool authorized to perform Verification checks and to issue Verification Proofs.

### Verification

A procedure to control the correspondence of the elements in the OETP Disclosure and the actual data processing and data collection practices of the Vendors.

### Verification Proof

A result of the formal Disclosure Verification procedure presented to a requestor.

### Chaining

A process of combining Disclosures of individual components into a composite high-level Disclosure for a Product.

### Label

A user-facing graphical and textual descriptions of the Product facilitating understanding of the values and risks it carries.

## Protocol Model

### Creation of the Disclosure

The initial Disclosure is created from a standardized disclosure form (for Example, see 1. [https://openethics.ai/label/](https://openethics.ai/label/)). A Vendor representative, a Product Owner or a Developer, MUST submit data-processing and data-collection information about the Product. The information about the end-point URL, as well as a contact email address MUST be specified. Disclosure MAY also be created in a fully automated way as a part of the CI/CD DevOps pipeline.

#### Cryptographic Signature

The Disclosure is organized into a predefined data schema and MUST be cryptographically signed using standard SHA3-512 hash implementation by the Disclosure generator (Open Ethics or federated providers). The integrity hash MUST be appended to a disclosure as OETP.schema.integrity element.

#### Immutable Storage

Both the signature integrity hash and the Disclosure is stored in the log-centric Open Ethics database and MAY be mirrored by other distributed databases for redundancy and safety.

#### Label Formation

Open Ethics Label SHOULD be automatically formed by mirroring the generated Disclosure into a set of graphical icons and simple human-readable descriptions. Additional Labels MAY be formed by mapping of the regulatory requirements to Disclosures.

### Access to Disclosure

The most recent OETP file SHOULD be stored in the root of the Product's end-point URL, allowing requests to OETP file from thirt-party domains. When establishing Vendor relationship, Integrator or a downstream Vendor may examine the Disclosure for their Components using the following HTTP request: `GET https://testexample.com/oetp.json`, where *testexample.com* is the URL of the Supplier&#39;s end-point.

### Automated Disclosure processing

The automated disclosure processing is enabled by requests to both Open Ethics Disclosure database and the Product's OETP Disclosure file.

### End-to-end transparency and formation of the composite Disclosure

A surface-level transparency is not sufficient as IT industry is getting more mature with more specialized Vendors, that are providing more narrow Products to Integrators and to bigger Vendors. The following steps MUST be satisfied for end-to-end transparency:

#### Open Vendor Policy

Every Integrator or a Vendor SHOULD supply the URLs of their sub-processing Vendors, indicating the scope of the data processing.

#### Request for Vendor&#39;s Disclosures

The OETP Processing system MUST crawl the URLs of the expected sub-processing Vendors' disclosures and specifies which of them have Disclosures.

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
