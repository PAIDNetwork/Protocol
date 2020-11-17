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
 - Tax ID #
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

##### Use Case / Example 1 - Car Insurance

You sign up for a car insurance, in the contract, the following prerequisites are required:

- `Must be 18 years old or more`
- `Must have valid license`
- `Must have insurance worthiness`

Because a contract can contain myriads of terms and conditions, a condition being a boolean value or some other value that requires ML data like classification. 

##### Insurance terms and condition

- `Collision`: Deductible, Full, ... terms and conditions
- `Crashed`
- ...more

These conditions must be validated and coded in packaged forms. Solido Forms are then formatted either as protocol onchain format, or stored offline.

 Given the following matrix:
 
 [signature],
 [has Alice crashed Bob and accept to have court settlement]
 [has Alice crashed Bob and accepted crash accident]
 

Turn this to a matrix, where vertical are the `claims`, and horizontal are the different `actors` involved
[Alice, Bob]
[0, 1]    - has Alice crashed Bob
[0, 0]    - has Bob crashed Alice
[0, 0]    - has Alice accepted accident
[0, 0]    - has Bob accepted accident


Thus, we get a way to calculate decision making using digital signatures, what we call Smart Agreements, using smart contracts with digital signatures features. 
Using digital signatures signing, we can transform clauses to Solidity/RLP compatible packaged data.

A packed message with VC digital signatures, can be translated to xxHash operations (AND, OR, XOR):

[Alice, Bob]
[hash_0_0, hash_0_1]
[...]

Once PAID Solido Forms generates the matrix to ABIEncode or RLP, it is used in 2 scenarios:

1. xxHash are used as hash verifications (boolean algebra)
2. Because a hash, in this case non-cryptography, we can sign that with EdDSA/ECDSA and use that for Smart Routing purposes and/or rules engine.

In this case:

- "Has Alice crashed Bob: [$true]"  -> xxHash -> xxHash signed with ECDSA
- "Has Alice crashed Bob: [$false]" -> xxHash -> xxHash signed with ECDSA

Then you could send it to Smart Routing:


findDecisionFromAgreementFacts(
   smartAgreement,   // as metadata
   oracleFacts,      // has Alice crashed Bob from real time data sources = yes
   anyExistingSignatures
)

Then each decision making contract is created as a Metatransaction and uses EIP712:

1. EIP712 Domain Name -- CarInsuranceDecisionMaker
2. EIP712 Method implemented -- handleCarCollisionBetweenTwoParties()
3. Pending define eg
    a. signed(hash [0,0]) === signed(address)

#### Resolutions, courts and disputes



### **Introducing Solido Forms, an agnostic template framework to stored JSON Schema mapped data**

*** TODO Define JSON Schema Interface for Solido Forms, migrate ABIForms documentation ***


### **Smart Routers, math constructs and digital signatures**

PAID Smart Agreements, In accordance with our development, two options are presented for the deployment of Smart Routers:

- Smart routers based on Upgradable Smart Contracts, or contract proxy management, using did: dpki: id as the user of the contracts to adjust their operation, allowing to delegate, approve or revoke permissions. These would be displayed through Solang (Solidity / Substrate Compiler), as if they were written in RUST.
- Substrate Runtime Module development has the intention of producing lean, performant, and fast nodes. It affords none of the protections or overhead of transaction reverting and does not implicitly introduce any fee system to the computation which nodes on your chain run, and Provide low-level access to your entire blockchain, remove the overhead of built-in safety for performance, and besides require a high level to entry for developers.Has no inherent economic incentives to repel bad actors.


### Introducing did-dpki, a decentralized identity method for PAID network

PAID Smart Agreements (Poroposal DID-DPKI-v1) need verifiable proof of identity to work well with legal contracts. Legal contracts, because they are binding, need a way to ensure all parties are accountable under a jurisdiction. In a simple legal agreement workflow, a KYC solution might be enough. But considering PAID is a decentralized based protocol, using smart contracts and oracles, we'll need a good set of technology stack that supports  enough data sources and still keep the level of decentralization required.


### PAID Oracles, Incentivized Oracles and other constructs


### PAID Token

PAID Smart Agreements 

### **Summary**

By maintaining developer efficient processes, putting Proof of Identity and Proof of Address allows our smart agreements protocol, to have near identical set of requirements as those found in a KYC solution. At the same time, it doesn't disrupt the CA business, it expands the CA and digital signing for vendors. In future protocol upgrades, an incentivization model could be added to make eg a reputation voting system, to be able to have another layer of trust.

### References

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
