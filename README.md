# **PAID Smart Agreements Protocol**

## **Chapter 1 - Verifiable credentials, attestations, proof of citizenship and smart agreements.**

### **Smart Agreements**

#### **Attestations**

An attestation is a proof issued by an attester or issuer, either human, smart contract or API.

_The attestation model for PAID_ uses W3C Verifiable Credentials Model with JSON Schemas packed as JWT. This allows us to use JWT basic features like aud, iss, nbf, exp and others sub

- _aud_: Audience
- _iss_: Issuer
- _nbf_: Not Before
- _exp_: Expiration
- _sub_: Subject

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
    "https://w3id.org/citizenship/v1"
  ],
  "type": [
    "VerifiableCredential",
    "NonDisclosureAgreement"
  ],
  "credentialSubjectA": {
    "id": "did:example:123",
    "type": [
      "NonDisclosureAgreement",
      "Discloser"
    ],
    "givenName": "JOHN",
    "familyName": "SMITH",
    "gender": "Male",
    "Discloser": "did:dpki:0x51587De731f94b69d9f956d9C736EE5B0153a170",
    "residentSince": "2015-01-01",
    "birthCountry": "Bahamas",
    "birthDate": "1958-08-17"
  },
  "credentialSubjectB": {
    "id": "did:example:123",
    "type": [
      "NonDisclosureAgreement",
      "Recipient"
    ],
    "givenName": "MARIA",
    "familyName": "STARK",
    "gender": "Female",
    "recipient": "did:dpki:0x6b3Ce64891c4D9c5C2E0072Ff682b1266497e448",
    "residentSince": "2015-01-01",
    "birthCountry": "Panama",
    "birthDate": "1958-08-17",
  },
  "conditions": {
    "Events": {
      "Notices": {
        "Discloser": "did:dpki:0x51587De731f94b69d9f956d9C736EE5B0153a170",
        "recipient": "did:dpki:0x6b3Ce64891c4D9c5C2E0072Ff682b1266497e448",
        "Message": "Message with detail of the notification form to be made within the contract",
        },
      "ReturnOfMetarials": {
        "Discloser": "did:dpki:0x51587De731f94b69d9f956d9C736EE5B0153a170",
        "recipient": "did:dpki:0x6b3Ce64891c4D9c5C2E0072Ff682b1266497e448",
        "Message": "Message with detail of the deadline to returns of materials or documents that have been furnished by Discloser to Recipient, within ten (10) days after (a) the Relationship has been rejected or concluded",
      },
      "ReturnOfMetarialsFail": {
        "Discloser": "did:dpki:0x51587De731f94b69d9f956d9C736EE5B0153a170",
        "recipient": "did:dpki:0x6b3Ce64891c4D9c5C2E0072Ff682b1266497e448",
        "Message": "Message notify that ten (10) days after finished o rejected relationship the Recipient doesn't return all the information provided within the Non Disclosure Agreement",
      },
      "RejectOrFinishRelationship": {
        "Discloser": "did:dpki:0x51587De731f94b69d9f956d9C736EE5B0153a170",
        "recipient": "did:dpki:0x6b3Ce64891c4D9c5C2E0072Ff682b1266497e448",
        "Message": "Detailed message indicating the rejection or termination of the relationship between the parties to the contract",
      }
    },
    "Function": {
      "Notification": {
        "sender": "did:dpki:0x51587De731f94b69d9f956d9C736EE5B0153a170",
        "recipient": "did:dpki:0x6b3Ce64891c4D9c5C2E0072Ff682b1266497e448",
        "message": "Message with details of notification"
      },
      "ReturnsOfMaterialsOK": {
        "Discloser": "did:dpki:0x51587De731f94b69d9f956d9C736EE5B0153a170",
        "Validation": "false" // default is false, change is Discloser Notify true
      },
      "ReturnsOfMaterialsFail": {
        "Validation": "false" // default is false, change is true if after ten 10 dias, Discloser no send true to ReturnsMaterialsOK
      },
      "TermAfterFinishRelationship": {
        "TimeStamp": "2025-01-01" // Indicate the time stamp where the period for which the information provided by the Discloser to the Recipient must be kept confidential.
      }
    }
  },
  "jurisdiction": {
    "Country": "(ISO Code Country) US",
    "Region": "(ISO Code Country/Region) US-CA",
    "Courts": {
      "Court": "Distrito, Los Angeles"
    },
    "Arbitration": {
      "Arbitration": {
        "identifier": "7465",
        "name": "PAID ADR for Non Disclouser Agreements",
        "arbitratorA": "did:dpki:0xbda5F6Ff1dAe02b006837a8E656E9644707fcEA6",
        "arbitratorB": "did:dpki:0x566f23F6c4F82E5B02eA110C8E816915a1893e1E",
        "arbitratorC": "did:dpki:0xf4D867BD19635f76196654Ef311375122aE0D5f1"
      }
    }
  },
  "issuer": "did:dpki:0xB423DD4834Be284B53d317649465d100762b838d",
  "issuanceDate": "2020-04-22T10:37:22Z",
  "identifier": "83627465",
  "name": "Non Disclosure Agreement",
  "description": "PAID Smart Agreements",
  "proof": {
    "type": "Ed25519Signature2018",
    "created": "2020-04-22T10:37:22Z",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "did:example:456#key-1",
    "jws": "eyJjcml0IjpbImI2NCJdLCJiNjQiOmZhbHNlLCJhbGciOiJFZERTQSJ9..BhWew0x-txcroGjgdtK-yBCqoetg9DD9SgV4245TmXJi-PmqFzux6Cwaph0r-mbqzlE17yLebjfqbRT275U1AA"
  }
}

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

`findDecisionFromAgreementFacts {`
<br/>

`ReturnsOfMaterialsOK(validation)`, // method to execute <br/>
`signedByDiscloser()` // Signed a Meta Transactions has Discloser accept/reject to receive of information of the Recipient in 10 days or minus <br/>
`validation == false` // default value change of the state if the Discloser notify <br/>
`ReturnsOfMaterialsFail()` // Event enabled in true if ten (10) days after finish o reject relationship the Recipient don't returned all the information provided within the Non Disclosure Agreement
<br/>
`}`

Then, each decision-making contract, based on the pre-defined conditions in the Smart Agreements previously, according to the selected template.
<br/>

<!-- debe incluir
- Prereq codificados basado en VC Model
- did-dpki
- Condiciones y Reglas (esta JEXL based)
- Cortes y Arbitrajes mapeados o lookup por medio de DID Services
--->

#### **Resolutions, courts and disputes**

Each decision-making contract, depending on the template and the conditions established therein, to make resolutions, resolve disputes or the handling of imponderables that must be processed by constituted courts, or an `Alternative Dispute Resolutions` (ADR) method, automated or semi -automated that allows quickly and decentralized to resolve disputes outside the scope of the contract but defined within it as an oracle to handle such disagreements between the signing parties.
<br/>

Additionally, Paid Smart Agreement, allows through Verifiable Credentials and to execute the authentication in two steps 'Proof of Citizenship', together with the pre-selected template at the time of establishing the contract between the parties, to validate and define as viable a jurisdiction for the resolution. of controversies and / or disputes in the execution of said contract. Allowing that prior to the selection of the court or ADR to be defined for the handling of disputes, it can be verified that the signing parties have the legal quality to participate in said litigation, eg. such as nationality or legal residence in that region or country, to which the selected court belongs or in the event of arbitration that is within the jurisdiction defined by this entity.
<br/>

Along with this PAID Smart Agreement proposed to offer a mapping or lookup system that allows offering signature parties, Courts or `Alternative Dispute Resolutions` (ADR) method the most appropriate according to the type of pre-selected template and the result of the execution of the two-step verification. authentication `Proof of Citizenship`, facilitating its selection by users of the protocol <br/>

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
- [Alternative Dispute Resolution](https://en.wikipedia.org/wiki/Alternative_dispute_resolution)
- [Ricardian contract](https://en.wikipedia.org/wiki/Ricardian_contract)
