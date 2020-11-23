# **PAID Smart Agreements Protocol**

## **Chapter 1 - Verifiable credentials, attestations, proof of citizenship and smart agreements.**

### **Smart Agreements**

#### **Attestations**
An attestation is a proof issued by an attester or issuer, either human, smart contract or API.

*The attestation model for PAID* uses W3C Verifiable Credentials Model with JSON Schemas packed as JWT. This allows us to use JWT basic features like aud, iss, nbf, exp and others sub

- *aud*: Audience
- *iss*: Issuer
- *nbf*: Not Before
- *exp*: Expiration
- *sub*: Subject

Attestations must be single clause and composable. They are either part of VC or subset of VC Model, JSON Schemas converted to JWT using `did-jwt`, in order to provide a self-contained token that can be optionally signed using JSON Web Signature (JWS) and/or encrypted using JSON Web Encryption (JWE).

#### **Components of Attestations**
 Proof issued by attesters (ie issuer attests a set of attributes or values, KYC like).

 - Full Legal Name.
 - Date and Place of Birth.
 - Country and Region (encoded under the ISO 3166 standard for storage in a Solidity Contract).
 - Rating (non-accredited, accredited, QIB, etc.varies by issuer & jurisdiction).
 - One or more public blockchain addresses a required renewal date.

An example of a birth certificate clause might be eg Are you older than 18?, this attestation, because is a precondition, is attested off-chain with traditional APIs instead of using on-chain transactions. It means most of a Smart Agreement prerequisites will be proofs inside a Verifiable Credentials model. These proofs can also be used in conjunction Zero Knowledge technology.


## **Example of VC Model using Javascript**
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
  ""
  "proof": {
    "type": "CLSignature2019",
    "issuerData": "5NQ4TgzNfSQxoLzf2d5AV3JNiCdMaTgm...BXiX5UggB381QU7ZCgqWivUmy4D",
    "attributes": "pPYmqDvwwWBDPNykXVrBtKdsJDeZUGFA...tTERiLqsZ5oxCoCSodPQaggkDJy",
    "signature": "8eGWSiTiWtEA8WnBwX4T259STpxpRKuk...kpFnikqqSP3GMW7mVxC4chxFhVs",
    "signatureCorrectnessProof": "SNQbW3u1QV5q89qhxA1xyVqFa6jCrKwv...dsRypyuGGK3RhhBUvH1tPEL8orH"
  }
}}

```
#### **Agreements**

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

To make Solidity Smart Contract make decisiones using a rules engine like code, we classify or transform a matrix of options to boolean.
<br/>

#### **Use Case / Example 1 - Mutual Non Disclosure Agreement **

<br/>

Paid Smart Agreements allow an organization where the management of digital assets as a representation of entities and physical assets, allows carrying out agreements of a different nature where the verification of credentials of the signatories of the agreements is required. In addition to the attestation of the data indicated at the time of entering into said agreements and that allows verifying the legal jurisdiction of the signatories and validating it with that of the conclusion of the contract.
<br/>

Paid Smart Agreement, allows the verification of credentials through a Decentralized Digital Identity, based on the W3C standard, and a DID METHOD developed by PAID, as a standard identifier candidate within the experimental exercise that the W3C is doing together with the Web 3 Foundation, for the evolution of the entire Blockchain Ecosystem and the Management of Decentralized Identification Systems. The `did:dpki`, is a DID Method, inspired by `did:ether` and additionally works the native library of the W3C `did-jwt`, allowing the encoding and decoding with multiple algorithms such as JsonWebKey2020 or Ed25519VerificationKey2018.
<br/>

Additionally Paid Smart Agreement, allows the establishment of conditions and validation of events or calls for execution, through a standard technology for sending gas-less transactions (`EP-712`) to smart contracts and with a scheme that allows the conversion of the conditions of the conditions of the Physical Contract in a Pseudo Code (`JEXL`/`Java Expression Language`) understandable for the Smart Contract corresponding to the pre-established template at the time of creation, fulfilling the conditions of the Ricardian Contract.
<br/>

Because smart agreements can contain numerous terms and conditions, a condition is a Boolean value or some other value that requires data machine learning for classification purposes, then it is transformed into a compressible language for smart contract (RLP Like) , and sent by meta-transactions the same for the execution of functions and events correspond to the information submitted, and actions preset template in the Smart Contract.
<br/>

Then you could send it to Smart Routing (`Smart Contract predefined according to the templates available and the courts or arbitration courts selected for its execution`):

findDecisionFromAgreementFacts {
<br/>

  smartAgreement, // as metadata oracleFacts <br/>
  signed(hash [1,0]) // has Alice accept a penalty for late payment to Bob `[Alice, Bod]`, <br/>
  PayOnTime() == false // from real time data sources = yes <br/>
  ExecutePenalty(Alice) // anyExistingSignatures
<br/>
}

Then, each decision-making contract, based on the pre-defined conditions in the Smart Agreements previously, according to the selected template.
<br/>
<!-- debe incluir
- Prereq codificados basado en VC Model
- did-dpki
- Condiciones y Reglas (esta JEXL based)
- Cortes y Arbitrajes mapeados o lookup por medio de DID Services
--->

#### **Resolutions, courts and disputes**

Each decision-making contract, depending on the template and the conditions set forth in them, to make resolutions, resolve disputes or the handling of imponderables that must be handled by hybrid or physical courts outside the scope of the contract but defined within it as a oracle to handle such disagreements between signature parties.
<br/>

Additionally, Paid Smart Agreement, allows through Verifiable Credentials and executed the two-step authentication `Proof of Citizenship`, together with the preselected template at the time of establishing the contract between the parties, to validate and define as viable a jurisdiction for the resolution of controversies and / or disputes in the execution of said contract. Allowing that prior to the selection of the court or court to define for the handling of disputes, it can be verified that the signature parties have the legal quality to participate in said litigation, eg. such as nationality or legal residence in that region or country. , to which the selected court belongs.
<br/>

Along with this PAID Smart Agreement proposed to offer a mapping or lookup system that allows offering signature parties, Courts or Arbitration Courts the most appropriate according to the type of pre-selected template and the result of the execution of the two-step verification. authentication `Proof of Citizenship`, facilitating its selection by users of the protocol <br/>

<!---  TODO 
> - Ejemplo del Smart Router, given a DID method/service eg court service
> - Por ahora, Rules builtin en la plantilla con JEXL, estos rules, investiga max 4h y me reportas si podemos  mapearlo a RLP y/o EIP712
> - Trabaja con Patricia, el schema final draft 0.1 --->

### **Summary**
<br/>
By maintaining developer efficient processes, putting Proof of Identity and Proof of Citizenship allows our PAID Smart Agreements Protocol, to have near identical set of requirements as those found in a KYC solution. At the same time, it doesn't disrupt the CA business, it expands the CA and digital signing for vendors. In future protocol upgrades, an incentivization model could be added to make eg a reputation scoring and voting system, to be able to have another layer of trust.
<br/>
<br/>

### **References**
<br/>

- [ISO 3166 COUNTRY CODES](https://www.iso.org/iso-3166-country-codes.html)
- [Verifiable Credentials Data Model 1.0](https://www.w3.org/TR/vc-data-model/)
- [Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)
- [JSON Web Token (JWT) RFC7519](https://tools.ietf.org/html/rfc7519)
- [Ecdsa Secp256k1 Recovery Signature 2020](https://identity.foundation/EcdsaSecp256k1RecoverySignature2020/)
- [Edwards-Curve Digital Signature Algorithm (EdDSA)](https://tools.ietf.org/html/rfc8032)
- [DID Specification Registries](https://w3c.github.io/did-spec-registries/)
- [Delaware Limited Liability Company](https://www.cscglobal.com/service/cls/delaware-llc-guide/)
- [DID (Decentralized Identifier) Specification](https://github.com/WebOfTrustInfo/rwot3-sf/blob/master/topics-and-advance-readings/did-spec-working-draft-03.md)
- [Ricardian contract](https://en.wikipedia.org/wiki/Ricardian_contract)
