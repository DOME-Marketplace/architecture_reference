# 8 Appendix III: remote Digital Signature Service (rDSS)

## 8.1 Introduction

The DSS open source library implements the standards for Advanced Electronic Signature creation, augmentation and validation. It is aligned with European legislation and eIDAS regulation. The Cloud Signature Consortium (CSC) is a global group of industry, government, and academic organisations committed to drive eIDAS-compliant standardisation of digital signatures in the cloud. The best approach to have an effective cloud signature system for DOME, mainly for JAdES signing and timestamping of Verifiable Credentials but not necessarily limited to it, would be to define an API that extends the already standardised API of the CSC to have a QTSP-independent cloud signature API.

## 8.2 JAdES cloud signature related endpoints

As explained in the [<u>CSC API v2.0 specification</u>](https://cloudsignatureconsortium.org/wp-content/uploads/2023/04/csc-api-v2.0.0.2.pdf) all the CSC endpoints are HTTP POST requests with JSON payloads and JSON responses and therefore they have the HTTP header “Content-Type: application/json”.

There are two steps when obtaining authorization to use the rDSS, service authorization and credential authorization. The latter must not be confused with Verifiable Credentials, it’s an independent concept in this case. The former gives access to the rDSS API and the latter gives authorization to use the specific keys associated with the client to ensure user control of its signing information when signing.

### 8.2.1 Service authorization and authentication

The rDSS will use OAuth 2.0 as the service auth/authz mechanism to be future proof since the CSC plans to deprecate the insecure usage of HTTP Basic authentication which is the most simple mechanism accepted as of right now..

### 8.2.2 Credential authorisation for remote signatures

To be able to remotely sign documents such as Verifiable Credentials additional authentication mechanisms MUST be used for each signing session. Several mechanisms can be used but we will use the one proposed by the CSC as explicit credential authorization for the purpose of credential authorisation for the signing session which basically entails checking if the user with access to the signing service is authorised to perform a signature as a certain legal or natural person. In our case the signing session will be just one signing operation each time since it is the most basic case proposed by the CSC.

[^1]: Note that in TM Forum recommendations the term “Product” is used instead of “Service”. This is because marketplaces relying on the specifications can be defined for different kind of products, including cloud and edge services but also any kind of physical or digital products/assets.

[^2]: [W3C Verifiable Credentials Data Model v1.1](https://www.w3.org/TR/vc-data-model/), [W3C Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)

[^3]: The following discussion is inspired by the study available at https://digital-strategy.ec.europa.eu/en/library/building-european-cloud-marketplace-conceptualisation-study

[^4]: figure taken from the conceptualization study “Building a European Cloud Marketplace”, entrusted by the European Commission to CapGemini Invent

[^5]: https://rrdg.centr.org/projects/standards/domain-industry-taxonomy/

[^6]: Taxes in Europe Database v4 - https://ec.europa.eu/taxation_customs/tedb

[^7]: Peppol BIS Billing - https://docs.peppol.eu/poacc/billing/3.0/bis/

[^8]: Understanding NLP vs NLU vs NLG,

    [<u>https://www.expert.ai/blog/dont-mistake-nlu-for-nlp-heres-why/#:~:text=While%20both%20NLP%20and%20NLU,language%2C%20NLU%20provides%20language%20comprehension</u>](https://www.expert.ai/blog/dont-mistake-nlu-for-nlp-heres-why/#:~:text=While%20both%20NLP%20and%20NLU,language%2C%20NLU%20provides%20language%20comprehension)

[^9]: Standard context topics, [<u>https://docs.expert.ai/nlapi/latest/guide/keyphrase-extraction/</u>](https://docs.expert.ai/nlapi/latest/guide/keyphrase-extraction/)

[^10]: IPTC Taxonomy [<u>https://iptc.org/standards/media-topics/</u>](https://iptc.org/standards/media-topics/)
