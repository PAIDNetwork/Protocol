# PAID Smart Agreements Protocol 

## Chapter 1 - Verifiable credentials, attestations, proof, quorum signatures and oraclized data feeds

### Smart Agreements

#### Attestations
An attestation is a proof issued by an attester or issuer, either human, smart contract or API.

*The attestation model for PAID* uses W3C Verifiable Credentials Model with JSON Schemas packed as JWT. This allows us to use JWT basic features like aud, iss, nbf, exp and others sub

- *aud*: Audience
- *iss*: Issuer
- *nbf*: Not Before
- *exp*: Expiration
- *sub*: Subject

Attestations must be single clause and composable. They are either part of VC or subset of VC Model, JSON Schemas converted to JWT using `did-jwt`, in order to provide a self-contained token that can be optionally signed using JSON Web Signature (JWS) and/or encrypted using JSON Web Encryption (JWE).

## Components of Attestations
 Proof issued by attesters (ie issuer attests a set of attributes or values).

 - Full Legal Name.
 - country and region (encoded under the ISO 3166 standard for storage in a Solidity Contract).
 - rating (non-accredited, accredited, QIB, etc.varies by issuer & jurisdiction).
 - One or more public blockchain addresses a required renewal date.

An example of a birth certificate clause might be eg Are you older than 18?, this attestation, because is a precondition, is attested off-chain with traditional APIs instead of using on-chain transactions. It means most of a Smart Agreement prerequisites will be proofs inside a Verifiable Credentials model. These proofs can also be used in conjunction Zero Knowledge technology.


## Example of VC Model using Javascript
```javascript
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "type": ["VerifiableCredential", "UniversityDegreeCredential"],
  "credentialSchema": {
    "id": "did:example:cdf:35LB7w9ueWbagPL94T9bMLtyXDj9pX5o",
    "type": "did:example:schema:22KpkXgecryx9k7N6XN1QoN3gXwBkSU8SfyyYQG"
  },
  "issuer": "did:example:Wz4eUg7SetGfaUVCn8U9d62oDYrUJLuUtcy619",
  "credentialSubject": {
    "givenName": "Jane",
    "familyName": "Doe",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts",
      "college": "College of Engineering"
    }
  },
  "proof": {
    "type": "CLSignature2019",
    "issuerData": "5NQ4TgzNfSQxoLzf2d5AV3JNiCdMaTgm...BXiX5UggB381QU7ZCgqWivUmy4D",
    "attributes": "pPYmqDvwwWBDPNykXVrBtKdsJDeZUGFA...tTERiLqsZ5oxCoCSodPQaggkDJy",
    "signature": "8eGWSiTiWtEA8WnBwX4T259STpxpRKuk...kpFnikqqSP3GMW7mVxC4chxFhVs",
    "signatureCorrectnessProof": "SNQbW3u1QV5q89qhxA1xyVqFa6jCrKwv...dsRypyuGGK3RhhBUvH1tPEL8orH"
  }
}}

```
#### Agreements

A Smart Agreements is build using the Verifiable Credentials, and contains:

- A set of one more `Prerequisites` (see Attestations)
- A set of Agreement `Conditions`, which can be DOM tagged (see JSON Schema and Meta transacciones)
- A set of resolutions which are mapped to a court and dispute Smart Contracts representing a DAO/LAO like construct.

A `PAID Smart Agreement` is then based of a root JSON Schema and inherited schemas, these specific for each industry.

Thus, a PAID Smart Agreement is:

- A JSON Schema construct
- Has the full JSON schema specs, which includes extensions using other schemas, where each schema permit to the protocol taken a right decision based in a algorithm preestablished.
- Verifiable Credentials compatible
- Decentralized Identity DID compatible
- Reputation Score.

To make Solidity Smart Contract make decisiones using a rules engine like code, we classify or transform a matrix of options to boolean.

##### **Use Case / Example 1 -  Limited Liability Autonomous Organizations**

The PAID Smart Agreements allow an organization where the management of digital assets as a representation of physical assets to carry out agreements of a different nature where the verification of credentials of the signatories of the agreements is required, in addition to the attestation of the data indicated in the moment of entering into such agreements. In addition to allowing the verification of the legal jurisdiction of the signatories and validating it with that of the conclusion of the contract.

PAID Smart Agreements, allows the verification of credentials in a decentralized way and with the use of APIs and Oracles available for these functions, taking advantage of incentive schemes such as DeFi and Chainlink, allowing the attestation of:
- Full Legal Name
- Country and Region
- A Biometric / PKI infrastructure how two-step authentication
- Decentralized Identity DID supported

Because a contract can contain myriads of terms and conditions, a condition being a boolean value or some other value that requires ML data like classification.

Then you could send it to Smart Routing:

findDecisionFromAgreementFacts { <br/>
<br/>
  smartAgreement, // as metadata oracleFacts <br/>
  signed(hash [1,0]) // has Alice accept a penalty for late payment to Bob `[Alice, Bod]`, <br/>
  PayOnTime() == false // from real time data sources = yes <br/>
  ExecutePenalty(Alice) // anyExistingSignatures <br/>
<br/>
}

Then, each decision-making contract, based on the pre-defined conditions in the Smart Agreements previously, according to the selected template.

#### **Resolutions, courts and disputes**

Each decision-making contract, depending on the template and the conditions set forth in them, to make resolutions, resolve disputes or the handling of imponderables that must be handled by hybrid or physical courts outside the scope of the contract but defined within it as a oracle to handle such disagreements between signature parties.

All this logic will be managed from the selected Smart Agreements template, and the particular conditions or events adjusted and sent through meta-transactions based on the EIP712 standard, to the Smart Routers with the actions to be executed according to the conditions and events. pre-established in the Smart Agreements. eg.:

1. EIP712 Domain Name -- LeasingDecisionMaker
2. EIP712 Method implemented -- PenaltyforLatePayment()
3. Pending define eg a. signed(hash [0,0]) === signed(address)

### **Smart Routers, math constructs and digital signatures**

PAID Smart Agreements, do not interact directly with the smart contracts deployed in onchain, instead it connects with a secondary network that in addition to performing the corresponding credential verifications to guarantee my identity through my signature (s) will verify others Security elements already mentioned as part of PAID Smart Agreements that allow guaranteeing that each interaction is secure after executing actions within the PAID Smart Agreements.

After this secondary network of Smart Routers has guaranteed the legitimacy of the communication between the signature Parties and the Smart Agreements, they will allow the execution of the actions pre-established by the signature Parties in said Smart Agreements, guaranteeing the assurance of the communication and the identity of the same without compromising your privacy.

All this supported by standards such as EIP712, for meta transactions sign with ECDSA, Decentralized Identifier with EdDSA Keypairs and Biometric Verification offchain.

### **Introducing did-dpki, a decentralized identity method for PAID network**

PAID Smart Agreements (Proposal DID-DPKI-v1) need verifiable proof of identity to work well with legal contracts. Legal contracts, because they are binding, need a way to ensure all parties are accountable under a jurisdiction. In a simple legal agreement workflow, a off-chain KYC solution might be enough. But considering PAID Smart Agreements is a decentralized based protocol, using smart contracts and oracles, we'll need a good set of technology stack that supports enough data sources and still keep the level of decentralization required, being the ideal gateway to manage contracts in the real world through legally recognized structures and Ricardian Contract provided by services such as that offered by PAID Smart Agreements


### **PAID Oracles, Incentivized Oracles and other constructs**

PAID Smart Agreements, in a first phase, foresees the use of oracles to improve the quality in the verification of credentials and the attestation of the physical and legal location of the signature Parties of the Smart Agreements, thus improving the level of security and precision of the data provided by users and verified by the platform, guaranteeing their legitimacy.

PAID Smart Agreements, in a second phase, provides for the management of an incentive model for users of the protocol, allowing them to share aspects of the use of the platform such as reputation, transparency and compliance index in the execution of Smart Agreements made in the same, without of course being violated aspects such as the security and privacy of the information, the users having control of the data at all times, which will or will not be shared through Oracles and other constructs.

### **PAID Token**

PAID Smart Agreements Token, have a capacity to handle diferents type of token, with backward to ERC 20 and ERC 223, and to interface with offchain securities like SAFTs, follow the Claims Token Standard ERC-1843 ana the Simple Restricted Token Standard ERC1404. 

It eventually allows in the first stage, it to be the ideal gateway DeFi and OpenFinance ecosystem assets including staking, insurance and escrow, allowing users to complete business agreement process from beginning to end through the platform. These assets incur future cash flows, e.g. repayments or dividends. Currently there is no standard for efficiently distributing claims on future cash flow of financial contracts among token holders. A clear and simple standard is needed to allow Dapps and exchanges to work with cash-flow producing tokens

### **Summary**

By maintaining developer efficient processes, putting Proof of Identity and Proof of Country allows our PAID Smart Agreements Protocol, to have near identical set of requirements as those found in a KYC solution. At the same time, it doesn't disrupt the CA business, it expands the CA and digital signing for vendors. In future protocol upgrades, an incentivization model could be added to make eg a reputation scoring and voting system, to be able to have another layer of trust.

### **References**

- [ISO 3166 COUNTRY CODES](https://www.iso.org/iso-3166-country-codes.html)
- [Verifiable Credentials Data Model 1.0](https://www.w3.org/TR/vc-data-model/)
- [Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)
- [JSON Web Token (JWT) RFC7519](https://tools.ietf.org/html/rfc7519)
- [Ecdsa Secp256k1 Recovery Signature 2020](https://identity.foundation/EcdsaSecp256k1RecoverySignature2020/)
- [Edwards-Curve Digital Signature Algorithm (EdDSA)](https://tools.ietf.org/html/rfc8032)
- [DID Specification Registries](https://w3c.github.io/did-spec-registries/)
- [Delaware Limited Liability Company](https://www.cscglobal.com/service/cls/delaware-llc-guide/)
- [DID (Decentralized Identifier) Specification](https://github.com/WebOfTrustInfo/rwot3-sf/blob/master/topics-and-advance-readings/did-spec-working-draft-03.md)
- [Biometric epassport](https://en.wikipedia.org/wiki/Biometric_passport)
- [Ricardian contract](https://en.wikipedia.org/wiki/Ricardian_contract)
