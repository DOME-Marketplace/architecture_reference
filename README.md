![](src/assets/media/image163.png)

This document describes the Reference Architecture and Technical Specifications of the DOME Marketplace system.

## Structure of the document

This document is divided into the following sections:

[DOME General Overview](docs/02_dome_general_overview.md) - describes the overall structure of the project, including different roles of users, the overall technical approach and the user journeys.

[DOME Trust and IAM Framework](docs/identity/identity.md) - provides a description of the decentralised Trust and Identity and Access Management (IAM) framework which are implemented in DOME.

[DOME Marketplace Persistence Layer](docs/04_persistence_layer.md) - provides a description of the DOME Persistence Layer, focusing on the specific goals and priorities associated with its implementation, including the Shared Catalog and the Transactions Layer.

[DOME marketplace features](docs/05_features.md) - provides a description of the DOME marketplace, including the design of the processes involved in a federated procurement scenario and high-level architecture of the various subsystems delivering such features.

[DOME APIs](docs/tmfapis/index.md) - provides a description of the APIs used in DOME used by providers or federated marketplaces to integrate with the DOME ecosystem.

[Appendix I: example of onboarding of organisations in DOME](docs/06_appendix_i.md) - provides examples with detailed technical descriptions of some user journeys in DOME..

[Appendix II: JAdES signatures of Verifiable Credentials](docs/07_appendix_ii.md) - provides a description of the approach to digital signatures of Verifiable Credentials in DOME, to achieve high legal certainty and alignment with the EU eIDAS (and upcoming eIDAS2) regulatory framework..

[Appendix III: remote Digital Signature Service (rDSS)](docs/08_appendix_iii.md) - provides a description of the approach to remote/cloud digital signatures, enabling the use of advanced and qualified signatures for Verifiable Credentials and other types of documents, increasing legal certainty and making Verifiable Credentials equivalent to handwritten signed documents.

## Related documents and resources

Following is a list of valuable links to relevant documents and resources:

- [EU Digital Identity Wallet Architecture and Reference Framework](https://digital-strategy.ec.europa.eu/en/library/european-digital-identity-wallet-architecture-and-reference-framework)

- [DSBA Technology Convergence: Discussion Document](https://data-spaces-business-alliance.eu/dsba-releases-technical-convergence-discussion-document/)

- [Digital Signature Service - DSS](https://ec.europa.eu/digital-building-blocks/wikis/display/DIGITAL/Digital+Signature+Service+-++DSS)

- [DID ETSI Legal person Semantic Identifier Method Specification (did:elsi)](https://alastria.github.io/did-method-elsi/)

## How to contribute

Just create a pull request with your changes to the documents in the `src` directory. Those are written in [Pandoc Markdown](https://pandoc.org/) format and converted to Github GFM (GitHub Flavored Markdown) format in the `docs` directory, which is where the user reads the documentation.

The script to convert the documents from `src` to `docs` is `publish.py`.
