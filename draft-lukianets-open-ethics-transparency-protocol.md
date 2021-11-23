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

Disclosure:
: Disclosure (Ethics Disclosure, or self-disclosure) is application-specific information about the data collection, data-processing, and decision-making practices of a Product, provided by the Product Vendor (an individual developer or an organization).

Disclosure Feed:
: A historical sequence of Disclosures, made for a specific Product.

Vendor:
: A legal person (an individual developer or an organization) that owns one or several end-user Products, or acts as a Supplier and provides Components for other Vendors.

Integrator:
: A legal person (an individual developer or an organization) that deploys technology-powered services to the end-users based on Product(s) from third-party Vendors.

Product:
: An IT system in the form of software, software as a service system, application, software component, application programming interface, or a physically embodied automated decision-making agent.

Component:
: An IT system supplied by Vendor and integrated/embedded into end-user Products. Components themselves do not necessarily interface with end-users.

Upstream Component:
: A Component that sends its outputs to the Product Downstream in the data processing chain. Disclosure for the Upstream Component is represented as a Child relative to the Disclosure node of the Downstream Product.

Downstream Component:
: A Component that receives inputs from the Components Upstream in the data processing chain. Disclosure for the Downstream Component is represented as a Parent relative to the Disclosure node of the Upstream Component.

Automated Decision-Making (ADM):
: The automated decision-making is the process of making a decision by automated means without any human involvement. These decisions can be based on factual data, as well as on digitally created profiles or inferred data.

OETP Disclosure Format:
: A machine-readable Disclosure with predefined structure, supplied in the JSON format.

Validation:
: A sequence of automated software-based checks to control validity and security elements in the OETP Disclosure.

Auditor:
: A third-party legal person trusted to perform Verification checks and to issue Verification Proofs.

Auditing software:
: An automated software-based tool authorized to perform Verification checks and to issue Verification Proofs.

Verification:
: A procedure to control the correspondence of the elements in the OETP Disclosure and the actual data processing and data collection practices of the Vendors.

Verification Proof:
: A result of the formal Disclosure Verification procedure presented to a requestor.

Chaining:
: A process of combining Disclosures of individual Components into a composite high-level Disclosure for a Product.

Label:
: User-facing graphical illustrations and textual descriptions of the Product that facilitate understanding of the values and risks the Product carries.

# Protocol Model

The Disclosure creation and delivery consist of the two parts, starting from (I) the submission of the Disclosure form, chaining of the Suppliers' Disclosures, Signature of the disclosed information, and to the delivery part (II) that first checks that the Disclosure is Valid, and then that the information specified in it is Verified by the third-parties. {{figure-disclosure-creation}} shows disclosure creation steps.

<!-- <img src="../diagrams/images/disclosure-creation/disclosure-creation.svg" alt="Creation of the Disclosure"> -->

## Creation of the Disclosure

The initial Disclosure is created by filling a standardized disclosure form (for example, see 1. [https://openethics.ai/label/](https://openethics.ai/label/)). A Vendor representative, a Product Owner, or a Developer, MUST submit data-processing and data-collection information about the Product. The information about the end-point URL, as well as a contact email address, MUST be specified. Disclosure MAY also be created in a fully automated way as a part of the CI/CD DevOps pipeline. {{figure-disclosure-submission-basic}} shows basic disclosure submission process.


<!-- <img src="../diagrams/images/disclosure-submission-basic/disclosure-submission-basic.svg" alt="Basic Disclosure Submission"> -->

### Cryptographic Signature

The Disclosure is organized into a predefined data schema and MUST be cryptographically signed by the Signature Generator (Open Ethics or federated providers) using standard SHA3-512 hash implementation. The integrity hash MUST be appended to a disclosure as the `OETP.schema.integrity` element.

### Immutable Storage

Both the signature integrity hash and the Disclosure SHOULD be stored in the log-centric root database and MAY be mirrored by other distributed databases for redundancy and safety.

### Visual Labeling

Open Ethics Label SHOULD be automatically generated by mirroring the submitted Disclosure into a set of graphical icons and simple human-readable descriptions. Additional Labels MAY be generated following successful third-party Verification and by mapping the regulatory requirements to Verified Disclosures.

## Access to Disclosure

### Initial Request to a Disclosure file

The most recent OETP file SHOULD be stored in the root of the Product's specified end-point URL, allowing requests to the OETP file from third-party domains. When establishing a Vendor relationship, the Integrator or a downstream Vendor MAY examine the Disclosure for their Components using the following HTTP request: `GET https://testexample.com/oetp.json`, where *testexample.com* is the URL of the Supplier&#39;s end-point.

### Access to Visual Trust Labels

A Vendor SHOULD place a visual Label generated as a result of the Disclosure process in the Product informational materials (for example Marketing Materials, User Guides, Safety Instructions, Privacy Policy, Terms of Service, etc). The Label reflects the content of the Disclosure and SHOULD be displayed in any digital media by embedding a software widget. Visual labels in the print media SHOULD carry a visually distinguishable Integrity signature to enable manual Validation by the User.

### Requirements for placement of Integrity Signature in Visual Label

* **Labels in the online digital media** MUST be generated automatically based on the content of the Disclosure and MUST contain a URL allowing to check the complete Integrity hash and explore more detailed information about the Disclosure.
* **Labels in the offline media** MUST be generated automatically based on the content of the Disclosure and should carry the first 10 digits of the corresponding Integrity hash.

### Conformity assessment marks

Based on the Verification performed for the OETP Disclosure file, the labels MAY include Conformity assessment marks, Certification marks, as well as marks showing adherence to certain standards. These marks MAY be generated and displayed automatically based on the Verification Proofs.

### Accessibility considerations
Accessibility of the Labels for the sight-impaired Users SHOULD be considered. The OETP Processing system MUST provide alternative forms of the Label, so that voice-reading software could be used to narrate the Label.


## Verification and Validation of Disclosure

### Automated Disclosure processing

The automated Disclosure processing is enabled by requests to both the Open Ethics Disclosure database powered by Disclosure Identity Providers and the Product's OETP Disclosure file.

### Validation of Vendor&#39;s Disclosures

The OETP Processing system MUST compare integrity hashes in the Open Ethics Disclosure database and entries that arrive as a result of the Disclosure Request response.

### Verification of Vendor&#39;s Disclosures

Every disclosure SHOULD be checked for the existence of the external Verification from Auditors for the entire Disclosures or one of Disclosure elements.

### Progressive Verification

To raise a level of trust to a Disclosure, a Vendor MAY decide to opt-in for a third-party Disclosure Verification. OETP suggests a Progressive Verification scheme where multiple independent external Verification Proofs COULD be issued by third parties to confirm the information specified in the Disclosure.

The Progressive Verification applies to a whole Disclosure, or to specific elements of the Disclosure.

{{figure-disclosure-progressive-verification}} displays a general scheme for Disclosure requests and responses.

<!-- <img src="../diagrams/images/disclosure-progressive-verification/disclosure-progressive-verification.svg" style="float: left; margin-right: 10px;" alt="Progressive Verification Scheme for Disclosures" /> -->

The following elements MAY serve as sources for various kinds of Verification proofs:
* Qualified Auditor reports
* Qualified Vendor of Auditing software tests
* Certification Authority assessments
* Conformity assessments
* User Feedback
* Market Brokers
* Real-time Loggers

## End-to-end transparency and formation of the composite Disclosure

IT industry is getting more mature with Vendors becoming more specialized. Surface-level transparency is not sufficient as supply chains are becoming more complex and distributed across various Components. The following steps MUST be satisfied for the end-to-end transparency:

### Open Supplier Policy

Every Integrator or a Vendor SHOULD disclose the information about their Suppliers (sub-processing Vendors), indicating the scope of the data processing in the Components they provide. 

If the Supplier information is not provided, Disclosure SHOULD contain information that a Vendor (Integrator) has not provided Supplier information.

##### First-party Components
For greater transparency, Vendors may decide to reveal Components even if they originate from themselves (first-party Components). For the first-party Component, the Supplier identity information SHOULD NOT be provided because it was already disclosed earlier.

Required: ({{component-information}}) only

#### Third-party Components

When disclosing Components originating from the third-party Vendors SHOULD provide both the Supplier identity information and Component information

Required: ({{supplier-identity}}, {{component-information}})

#### Elements of Supplier disclosure

##### Supplier identity
* Vendor Name
* Vendor URL
* Vendor ID
* Vendor DPO Contact Email

##### Component information
* Component Scope of use
* Personal Data Being Processed by Component
* Is a Safety Component (YES)/(NO)
* Component URL (if different from the Vendor URL)
* Component Disclosure URL (if different from the default `Component URL/oetp.json`)
* Component DPO Contact (if different from Vendor DPO Contact Email)

### Request for Supplier&#39;s Disclosures

The OETP Processing system MUST send GET requests to the URLs of each Component to obtain their Disclosures. Based on the response to each Disclosure request, the OETP Processing system MUST specify which Components have Disclosures and which don't have Disclosures.

{{figure-disclosure-chaining-request}} shows the process how Disclosure Chaining request and response happen.

<!-- <img src="../diagrams/images/disclosure-chaining-request/disclosure-chaining-request.svg" alt="Disclosure Chaining: Request-Response"> -->


### Disclosure Chaining

The same Request-response operation applies recursively for Components of the Components, and for the Components of the Components of the Components, etc. It is proposed to view the supply chain as a tree-like hierarchical data structure, where the information about Components is assembled using Level Order Tree Traversal algorithm.

In this tree:
* Node is a structure that contains Component's Disclosure;
* Root is the top Node representing a Product's Disclosure information;
* Edge is the connection between one Node and another, representing the scope of the Data Processing by the Component.

{{figure-disclosure-chaining-tree}} displays the order of the Disclosure Chaining with Level Order Tree Traversal algorithm.

<!-- <img src="../diagrams/images/disclosure-chaining-tree/disclosure-chaining-tree.svg" alt="Disclosure Chaining: Level Order Traversal"> -->

### Generation of the Composite Disclosure

The current consensus from the user & developer community suggests that Composite Disclosure should follow The "Weakest Link" model. According to this model, the risk that the Product is carrying should not be considered any less than the risk for each of the Components.

Formally this approach could be illustrated with the use of a conjunction table for risk modeling (see {{conjunction-table-risk-modeling}}). The Truth Table for Logical AND operator below takes one risk factor and evaluates risk outcomes as High (H) or Low (L) for hypothetical Disclosure options of the Product(P) and its Component(C).

|Disclosed risk of P |Disclosed risk of  C | Composite P & C |
|:-----:|:-----:|:--------------------:|
| L     | L     | **L**                |
| L     | H     | **H**                |
| H     | L     | **H**                |
| H     | H     | **H**                |
{: #conjunction-table-risk-modeling title="Conjunction Table for Risk Modeling"}

Further evaluation of this approach is required.

# Example OETP Disclosure File

~~~~ JSON
{::include examples/basic disclosure/oetp.json}
~~~~
{: #figure-example-oetp-json title="Example OETP Disclosure File"}

# Security Considerations

## Response content

OETP exchanges data using JSON {{?RFC7159}} which is a lightweight data-interchange format. A JSON-based application can be attacked in multiple ways such as sending data in an improper format or embedding attack vectors in the data. It is important for any application using JSON format to validate the inputs before being processed. To mitigate this attack type, the JSON Key Profile is provided for OETP responses.

## Spoofing

OETP Processors should be aware of the potential for spoofing attacks where the attacker publishes an OETP disclosure with the `OETP.snapshot` value from another product, or, perhaps with an outdated `OETP.snapshot.label` element. For example, an OETP Processor could suppress the display of falsified entries by comparing the snapshot integrity from the submission database and a calculated hash for the `OETP.snapshot` object. In that situation, the OETP Processor might also take steps to determine whether the disclosures originated from the same publisher require further investigation of the Disclosure Feed and alert the downstream OETP Processors.

## Falsification

Dishonest or falsified Disclosures is a problem that is hard to address generally. The approach to it is public control and systematic checks. Vendors or user-facing applications and services could further raise the level of trust in their Disclosures by implementing programmatic control scoring mechanisms, as well as the external verification by trusted Auditors.


# IANA Considerations

This document has no IANA actions.

# Areas for Future Study

The following topics not addressed in this version of LDP are possible areas for future study:

* IANA requests for the Data Processor identity management.
* Extensibility of the OETP Disclosure Format.
* Evaluate other methods of Generation of the Composite Disclosure based on the Disclosure Tree
* Disclosure Chaining mechanisms and various use-cases.
* Typical scenarios and templates for Disclosure submissions.
* Mapping of the regulatory requirements and future Disclosure elements.
* Standardizing Privacy Disclosure and PII data-collection practices.
* Enchancing Label accessibility with ARIA W3C Recommendation and other approaches




--- back



# Appendix

## Figures

Diagrams could be built from code using below `*.puml` files automatically using [PlantUML](https://plantuml.com/).


### Creation of the Disclosure
~~~~ PUML
{::include docs/diagrams/src/disclosure-creation.puml}
~~~~
{: #figure-disclosure-creation title="Creation of the Disclosure"}

### Basic Disclosure Submission
~~~~ PUML
{::include docs/diagrams/src/disclosure-submission-basic.puml}
~~~~
{: #figure-disclosure-submission-basic title="Basic Disclosure Submission"}

### Progressive Verification Scheme for Disclosures
~~~~ PUML
{::include docs/diagrams/src/disclosure-progressive-verification.puml}
~~~~
{: #figure-disclosure-progressive-verification title="Progressive Verification Scheme for Disclosures"}

### Disclosure Chaining: Request-Response
~~~~ PUML
{::include docs/diagrams/src/disclosure-chaining-request.puml}
~~~~
{: #figure-disclosure-chaining-request title="Disclosure Chaining: Request-Response"}

### Disclosure Chaining: Level Order Traversal
~~~~ PUML
{::include docs/diagrams/src/disclosure-chaining-tree.puml}
~~~~
{: #figure-disclosure-chaining-tree title="Disclosure Chaining: Level Order Traversal"}

# Acknowledgments
{:numbered="false"}

TODO acknowledge.