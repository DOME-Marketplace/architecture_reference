# 7 Appendix II: JAdES signatures of Verifiable Credentials

## 7.1 Introduction

Verifiable Credentials are typically signed using JWS when using JWT VCs or LD-Proofs when using JSON-LD VCs, the latter being discouraged by the ARF. JWS signatures can be used as per the ARF but since this kind of signatures are not done according to the ETSI Advanced Electronic Signature creation standards those can’t be recognized as Advanced Signatures and are therefore considered Simple Signatures. In those cases that an Advanced Signature or a Qualified Signature are required or beneficial, Credentials can be signed using [<u>JAdES</u>](https://www.etsi.org/deliver/etsi_ts/119100_119199/11918201/01.01.01_60/ts_11918201v010101p.pdf) or JSON Advanced Electronic Signatures. For more details regarding Electronic Signatures refer to the 3.2.1.1 Legal basis section or the [<u>European eSignature FAQ</u>](https://ec.europa.eu/digital-building-blocks/wikis/display/DIGITAL/eSignature+FAQ).

Along this section when talking about electronic signatures we are talking about electronic seals too unless otherwise specified.

## 7.2 Choosing between Qualified and Advanced Signatures

The first step when signing using JAdES is to consider whether to do an Advanced Signature or a Qualified one. Using Qualified Signatures makes the signature of the data legally equivalent to its handwritten counterpart, as said in the European eSignature FAQ “<span class="mark">only qualified electronic signatures are explicitly recognized to have the equivalent legal effect of hand-written signatures all over EU Member States.”</span> This means that this kind of signatures provide the highest legal certainty to the involved parties.

For a signature to be considered Qualified it MUST comply with the following:

- It was created by a qualified seal creation device (QSCD). The simplest way would be to use it as a rQSCD or remote QSCD provided by a QTSP.

- Is based on a qualified certificate for electronic seals/signatures.

- Complies with the requisites of previous signature levels, which are those of Simple Electronic Signatures and Advanced electronic signatures (AdES).

Another key point is that the signed data can be time stamped too. The timestamp aims to bind the time stamped data to a particular time establishing evidence that the data existed at that time. Again we have non Qualified and Qualified Timestamps In this case the advantage of Qualified Timestamps is the presumption of the accuracy of the date and the time it indicates and the integrity of the data to which the date and time are bound. Qualified timestamping MUST be done by a QTSP.

To keep a clear separation between legal-grade production operations and testing activities, non-production environments will use non-qualified certificates. This reduces compliance risk and prevents confusion about the legal level of the generated signatures. The following text describes how we implement this separation.

## 7.3 Signing using JAdES

The simplest way to do a JAdES signature is by using the [<u>European DSS library</u>](https://ec.europa.eu/digital-building-blocks/DSS/webapp-demo/doc/dss-documentation.html) which covers both the signature creation, validation and timestamping of every ETSI standardised AdES signature type. Other libraries could be used theoretically but this is the recommended approach. The Cloud Signature Consortium is standardising an API to do everything related to the signatures with the same interface independently of the chosen QTSP to provide that remote services. That API and other DSS related information can be read in the section 8 Appendix III: remote Digital Signature Service (rDSS).

### 7.3.1 Timestamping of JWTs

When signing JWT Credentials only JAdES Baseline-B can be used for compatibility reasons with JWTs and JAdES which means that a JWT can’t be time stamped directly. Documentation related to this aspect will be elaborated in the future.

### 7.3.2 Example of a JWT Credential signed using JAdES

In the following example extracted from EBSI’s website we can see a VerifiableID signed using JAdES:

{

"alg": "RS256",

"cty": "json",

"kid": "MGcwYKReMFwxCzAJBgNVBAYTAlNJMRQwEgYDVQQKEwtIYWxjb20gZC5kLjEXMBUGA1UEYRMOVkFUU0ktNDMzNTMxMjYxHjAcBgNVBAMTFUhhbGNvbSBDQSBQTyBlLXNlYWwgMQIDEPSP",

"x5t#S256": "-zpb6qm4B4NrqhEhjoloohMtoj9jRm7BJXG3jkWB4EQ",

"x5c": \[

"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"

\],

"typ": "jose",

"sigT": "2022-04-13T07:18:32Z",

"crit": \[

"sigT"

\]

}

.

{

"iss": "did:ebsi:z219z1CJKSbtFc69M2jHcFmq",

"sub": "did:ebsi:zsSgDXeYPhZ3AuKhTFneDf1",

"jti": "urn:ebsi:status:identity:verifiableID#1dee355d-0432-4910-ac9c-70d89e8d674e",

"iat": 1638316800,

"nbf": 1638316800,

"exp": 1953849600,

"vc": {

"@context": \[

"[<u>https://www.w3.org/2018/credentials/v1</u>](https://www.w3.org/2018/credentials/v1)"

\],

"id": "urn:ebsi:status:identity:verifiableID#1dee355d-0432-4910-ac9c-70d89e8d674e",

"type": \[

"VerifiableCredential",

"VerifiableAttestation",

"VerifiableId"

\],

"issuer": "did:ebsi:z219z1CJKSbtFc69M2jHcFmq",

"issued": "2021-12-01T12:00:00.0Z",

"issuanceDate": "2021-12-01T12:00:00.0Z",

"validFrom": "2021-12-01T12:00:00.0Z",

"validUntil": "2031-12-01T12:00:00.0Z",

"expirationDate": "2031-12-01T12:00:00.0Z",

"credentialSubject": {

"id": "did:ebsi:zsSgDXeYPhZ3AuKhTFneDf1",

"familyName": "Doe",

"firstName": "John",

"dateOfBirth": "1999-03-22",

"personalIdentifier": "ES/AT/123456789"

},

"credentialSchema": {

> "id": "[<u>https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0x14b05b9213dbe7d343ec1fe1d3c8c739a3f3dc5a59bae55eb38fa0c295124f49#</u>](https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0x14b05b9213dbe7d343ec1fe1d3c8c739a3f3dc5a59bae55eb38fa0c295124f49)",

"type": "FullJsonSchemaValidator2021"

},

"credentialStatus": {

> "id": "urn:ebsi:status:identity:verifiableID#1dee355d-0432-4910-ac9c-70d89e8d674e",

"type": "CredentialStatusList2020"

},

"evidence": \[{

"type": \[

"DocumentVerification"

\],

"verifier": "did:ebsi:z219z1CJKSbtFc69M2jHcFmq",

"evidenceDocument": \[

"Passport"

\],

"subjectPresence": "Physical",

"documentPresence": \[

"Physical"

\]

}\]

}

}.\<signature\>
