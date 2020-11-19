# PAID Protocol (DID-DPKI Proposal v1)

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
- Proof issued by attesters (ie issuer attests a set of attributes or values).

 - full legal name
 - country and region (encoded under the ISO 3166 standard for storage in a Solidity Contract).
 - rating (non-accredited, accredited, QIB, etc.varies by issuer & jurisdiction)
 - One or more public blockchain addresses a required renewal date.
 - the KECCAK256 hash of a subset of the  foregoing PII (the IDHash)

An example of a birth certificate clause might be eg Are you older than 18?, this attestation, because is a precondition, is attested off-chain with traditional APIs instead of using on-chain transactions. It means most of a smart agreement prerequisites will be proofs inside a Verifiable Credentials model. These proofs can also be used in conjuction Zero Knowledge technology.


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
- A set of Agreement `Conditions`, which can be DOM tagged (see Solido EVM Forms)
- A set of resolutions which are mapped to a court and dispute Smart Contracts representing a DAO like construct.

A `PAID Smart Agreement` is then based of a root JSON Schema and inherited schemas, these specific for each industry.

Thus, a PAID Smart Agreement is:

- A JSON Schema construct
- Has the full JSON schema specs, which includes extensions using other schemas, where each schema permit to the protocol taken a right decision based in a algorithm preestablished.
- Verifiable Credentials compatible
- A Biometric/PKI infraestructura how two-step authentication
- Decentralized Identity DID compatible

To make Solidity Smart Contract make decisiones using a rules engine like code, we classify or transform a matrix of options to boolean.

##### **Use Case / Example 1 -  Limited Liability Autonomous Organizations**

The PAID Smart Agreements allow an organization where the management of digital assets as a representation of physical assets to carry out agreements of a different nature where the verification of credentials of the signatories of the agreements is required, in addition to the attestation of the data indicated in the moment of entering into such agreements. In addition to allowing the verification of the legal jurisdiction of the signatories and validating it with that of the conclusion of the contract.

PAID Smart Agreements, allows the verification of credentials in a decentralized way and with the use of APIs and Oracles available for these functions, taking advantage of incentive schemes such as DeFi and Chainlink, allowing the attestation of:
- full legal name
- Country and Region
- A Biometric / PKI infrastructure how two-step authentication
- Decentralized Identity DID supported

Because a contract can contain myriads of terms and conditions, a condition being a boolean value or some other value that requires ML data like classification.

Then you could send it to Smart Routing:

findDecisionFromAgreementFacts { 
  - smartAgreement, // as metadata oracleFacts
  // has Alice accept a penalty for late payment to Bob, // from real time data sources = yes // anyExistingSignatures <br/>
}

Then, each decision-making contract, based on the pre-defined conditions in the Smart Agreements previously, according to the selected template.

#### **Resolutions, courts and disputes**

Each decision-making contract, in function of the resolutions, disputes or management of imponderables that must be handled by cutting hybrids or physics outside the scope of the contract but defined in it as an oracle to handle disputes, all this is created as a meta transaction and uses EIP712

1. EIP712 Domain Name -- LeasingDecisionMaker
2. EIP712 Method implemented -- PenaltyforLatePayment()
3. Pending define eg a. signed(hash [0,0]) === signed(address)

### **Smart Routers, math constructs and digital signatures**

PAID Smart Agreements, 


### **Introducing did-dpki, a decentralized identity method for PAID network**

PAID Smart Agreements (Proposal DID-DPKI-v1) need verifiable proof of identity to work well with legal contracts. Legal contracts, because they are binding, need a way to ensure all parties are accountable under a jurisdiction. In a simple legal agreement workflow, a off-chain KYC solution might be enough. But considering PAID is a decentralized based protocol, using smart contracts and oracles, we'll need a good set of technology stack that supports enough data sources and still keep the level of decentralization required, being the ideal gateway to manage contracts in the real world through legally recognized structures and Ricardian Contract provided by services such as that offered by PAID Smart Agreements


### **PAID Oracles, Incentivized Oracles and other constructs**



### **PAID Token**

PAID Smart Agreements Token, have a capacity to handle differents type of token, with backward to ERC 20 and ERC 223, and to interface with offchain securities like SAFTs, follow the Claims Token Standard ERC-1843 ana the Simple Restricted Token Standard ERC1404. It eventually allows it to be the ideal gateway DeFi and OpenFinance ecosystem assets such as debt positions, loans, derivatives and bonds are emerging. These assets incur future cash flows, e.g. repayments or dividends. Currently there is no standard for efficiently distributing claims on future cash flow of financial contracts among token holders. A clear and simple standard is needed to allow Dapps and exchanges to work with cash-flow producing tokens

### **Summary**

By maintaining developer efficient processes, putting Proof of Identity and Proof of Address allows our smart agreements protocol, to have near identical set of requirements as those found in a KYC solution. At the same time, it doesn't disrupt the CA business, it expands the CA and digital signing for vendors. In future protocol upgrades, an incentivization model could be added to make eg a reputation voting system, to be able to have another layer of trust.

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
