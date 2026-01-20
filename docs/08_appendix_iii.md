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
