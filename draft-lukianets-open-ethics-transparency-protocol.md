---
title: "Open Ethics Transparency Protocol"
abbrev: "OETP"
docname: draft-lukianets-open-ethics-transparency-protocol-latest
category: exp

ipr: trust200902
area: General
workgroup: 
keyword: Internet-Draft

stand_alone: yes
smart_quotes: no
pi:
    toc: yes
    tocdepth: 4
    sortrefs: yes
    symrefs: yes

author:
 -
    ins: N. Lukianets
    name: Nikita Lukainets
    organization: Open Ethics
    email: n.lukianets@openethics.ai

normative:

informative:


--- abstract

The Open Ethics Transparency Protocol (OETP) is an application-level protocol for publishing and accessing ethical Disclosures of IT Products and their Components. The Protocol is based on HTTP exchange of information about the ethical &quot;postures&quot;, provided in an open and standardized format. The scope of the Protocol covers Disclosures for systems such as Software as a Service (SaaS) Applications, Software Applications, Software Components, Application Programming Interfaces (API), Automated Decision-Making (ADM) systems, and systems using Artificial Intelligence (AI). OETP aims to bring more transparent, predictable, and safe environments for the end-users. The OETP Disclosure Format is an extensible JSON-based format.

--- middle

# Introduction

The Open Ethics Transparency Protocol (OETP or Protocol) describes the creation and exchange of voluntary ethics Disclosures for IT products. It is brought as a solution to increase the transparency of how IT products are built and deployed. This document provides details on how disclosures for data collection and data processing practice are formed, stored, validated, and exchanged in a standardized and open format.

OETP provides facilities for:

* **Informed consumer choices** : End-users able to make informed choices based on their own ethical preferences and product disclosure.
* **Industrial-scale monitoring** : Discovery of best and worst practices within market verticals, technology stacks, and product value offerings.
* **Legally-agnostic guidelines** : Suggestions for developers and product-owners, formulated in factual language, which are legally-agnostic and could be easily transformed into product requirements and safeguards.
* **Iterative improvement** : Digital products, specifically, the ones powered by artificial intelligence could receive nearly real-time feedback on how their performance and ethical posture could be improved to cover security, privacy, diversity, fairness, power balance, non-discrimination, and other requirements.
* **Labeling and certification** : Mapping to existing and future regulatory initiatives and standards.

The Open Ethics Transparency Protocol (OETP) is an application-level protocol for publishing and accessing ethical Disclosures of IT products and their components. The Protocol is based on HTTP exchange of information about the ethical &quot;postures&quot;, provided in an open and standardized format. The scope of the Protocol covers Disclosures for systems such as Software as a Service (SaaS) Applications, Software Applications, Software Components, Application Programming Interfaces (API), Automated Decision-Making (ADM) systems, and systems using Artificial Intelligence (AI). OETP aims to bring more transparent, predictable, and safe environments for the end-users. The OETP Disclosure Format is an extensible JSON-based format.

# Requirement Levels

{::boilerplate bcp14-tagged}

# Terminology

Disclosure
: Disclosure (Ethics Disclosure, or self-disclosure) is application-specific information about the data collection, data-processing, and decision-making practices of a Product, provided by the Product Vendor (an individual developer or an organization).

Disclosure Feed
: A historical sequence of Disclosures, made for a specific Product.

Vendor
: A legal person (an individual developer or an organization) that owns one or several end-user Products, or acts as a Supplier and provides Components for other Vendors.

Integrator
: A legal person (an individual developer or an organization) that deploys technology-powered services to the end-users based on Product(s) from third-party Vendors.

Product
: An IT system in the form of software, software as a service system, application, software component, application programming interface, or a physically embodied automated decision-making agent.

Component
: An IT system supplied by Vendor and integrated/embedded into end-user Products. Components themselves do not necessarily interface with end-users.

Upstream Component
: A Component that sends its outputs to the Product Downstream in the data processing chain. Disclosure for the Upstream Component is represented as a Child relative to the Disclosure node of the Downstream Product.

Downstream Component
: A Component that receives inputs from the Components Upstream in the data processing chain. Disclosure for the Downstream Component is represented as a Parent relative to the Disclosure node of the Upstream Component.

Automated Decision-Making (ADM)
: The automated decision-making is the process of making a decision by automated means without any human involvement. These decisions can be based on factual data, as well as on digitally created profiles or inferred data.

OETP Disclosure Format
: A machine-readable Disclosure with predefined structure, supplied in the JSON format.

Validation
: A sequence of automated software-based checks to control validity and security elements in the OETP Disclosure.

Auditor
: A third-party legal person trusted to perform Verification checks and to issue Verification Proofs.

Auditing software
: An automated software-based tool authorized to perform Verification checks and to issue Verification Proofs.

Verification
: A procedure to control the correspondence of the elements in the OETP Disclosure and the actual data processing and data collection practices of the Vendors.

Verification Proof
: A result of the formal Disclosure Verification procedure presented to a requestor.

Chaining
: A process of combining Disclosures of individual Components into a composite high-level Disclosure for a Product.

Label
: User-facing graphical illustrations and textual descriptions of the Product that facilitate understanding of the values and risks the Product carries.

# Security Considerations

## Response content

OETP exchanges data using JSON ([RFC159](https://www.rfc-editor.org/rfc/rfc7159)) which is a lightweight data-interchange format. A JSON-based application can be attacked in multiple ways such as sending data in an improper format or embedding attack vectors in the data. It is important for any application using JSON format to validate the inputs before being processed. To mitigate this attack type, the JSON Key Profile is provided for OETP responses.

## Spoofing

OETP Processors should be aware of the potential for spoofing attacks where the attacker publishes an OETP disclosure with the `OETP.snapshot` value from another product, or, perhaps with an outdated `OETP.snapshot.label` element. For example, an OETP Processor could suppress the display of falsified entries by comparing the snapshot integrity from the submission database and a calculated hash for the `OETP.snapshot` object. In that situation, the OETP Processor might also take steps to determine whether the disclosures originated from the same publisher require further investigation of the Disclosure Feed and alert the downstream OETP Processors.

## Falsification

Dishonest or falsified Disclosures is a problem that is hard to address generally. The approach to it is public control and systematic checks. Vendors or user-facing applications and services could further raise the level of trust in their Disclosures by implementing programmatic control scoring mechanisms, as well as the external verification by trusted Auditors.


# IANA Considerations

This document has no IANA actions.



--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
