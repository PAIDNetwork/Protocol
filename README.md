## did-dpki

### A did method to verify identity and residence using pluggable authentication sources


### Why did-dpki

PAID Smart Agreements need verifiable proof of identity to work well with legal contracts. Legal contracts, because they are binding, need a way
to ensure all parties are accountable under a jurisdiction. In a simple legal agreement workflow, a KYC solution might be enough. But considering PAID
 is a decentralized based protocol, using smart contracts and oracles, we'll need a good set of technology stack that supports enough data sources and still
 keep the level of decentralization required.
 
 ### Proposal
 
 `did-dpki` uses DID Method specification as standard to be able to integrate with other DID applications and services in the ecosystem. Based from ideas found in
 `did-ethr`, we will have the following:
 
 - `delegate`: be able to delegate to another did user
 - `add`: register public key 
 - `revoke`: unregister public key
 
 It must be resolvable, that is, be able to lookup and match by its public key.
 
 Additionally, did-dpki needs to have a decentralized KYC experience, it must be able to do:
 
 - `As a user, provision a signed well known (verifiable credentials) document based in a JSON Schema and publish it to IPFS / IPNS`
 - `As a user, approve or reject Certificate Authority keypair issuing`
 - `As a validator, validate did-dpki belongs to DNS Human Readable Link`
 - `As a validator, validate DNS Human Readable Link belongs to a did-dpki`

 Ideally, but optional, provisioning must permit users to configure a custom `verified domain name` under paidnetwork or similar DNS name, similar to `domain.kreds`. Eg we could have a party sign a smart agreement with a domain name `alice-wonderland.paid.network` and the other party signing with `bob-realworld.paid.network`.
 
 To implement this use case requires several pieces of technology:

 #### **An encrypted off-chain database of personally identifiable information (PII)** 

 - full legal name
 - country and region (encoded under the ISO 3166 standard for storage in a Solidity Contract).
 - rating (non-accredited, accredited, QIB, etc.varies by issuer & jurisdiction)
 - Tax ID #
 - One or more public blockchain addresses a required renewal date.
 - the KECCAK256 hash of a subset of the  foregoing PII (the IDHash)

 #### **JSON Schema**

 A JSON Schema construct, Has the full JSON schema specs, which includes extensions using other schemas with a Verifiable Credentials and compatible `Decentralized Identity DID compatible (W3C)`
 
 #### **P384 or secp256r1**
 
 We need to sign the wellknown document using a keypair using ECDSA NIST P384. This to be compatible with the Certificate Authority and Smart Contracts requiring to verify these signatures.
 
 #### **IPNS**
 
 Once the document is pushed to IPFS, create and publish to IPNS and optionally, use DNSLink to link to a human readable DNS name.
 
 #### **Certificate Authority**
 
 There are two different implementations here:
 
 - `Use of centralized CAs`: [Use Let's Encrypt with ECDSA Support](https://letsencrypt.org/certificates/)
 - `Use of PAID Network Decentralized CA nodes`: Using a combination of Smart Contracts and or a LB of CAs nodes
 
 #### *Option 1 - Let's Encrypt*
 
 Using the IPNS wellknown, provision ECDSA keypair and store in PAID wallet. These keypair will be used for Domain Name proof of identity.
 
 #### *Option 2 - Smart Contract*
 
 A Smart Contract in Polkadot can issue ECDSA keypairs. And either using EVM or Polkadot, be able to verify ECDSA keypairs onchain.
 
 #### **Proof of Address**
 
 Using an existing KYC provider Proof of Address service, create a Chainlink oracle that handles any KYC related actions. In this special case, because of cost, any proof of address validation must be accounted in the transaction and billed depending on token being used.

 #### **Proof of epassport** *(How two-step authentication)*

A biometric passport (also known as an e-passport, ePassport, or a digital passport) is a traditional passport that has an embedded electronic microprocessor chip which contains biometric information that can be used to authenticate the identity of the passport holder. It uses contactless smart card technology, including a microprocessor chip (computer chip) and antenna (for both power to the chip and communication) embedded in the front or back cover, or centre page, of the passport.
 
 ### **Summary**
 
 By maintaining developer efficient processes, putting Proof of Identity and Proof of Address allows our smart agreements protocol, to have near identical set of requirements as those found in a KYC solution. At the same time, it doesn't disrupt the CA business, it expands the CA and digital signing for vendors. In future protocol upgrades, an incentivization model could be added to make eg a reputation voting system, to be able to have another layer of trust.
 
 ### References
 
 - [ISO 3166 COUNTRY CODES](https://www.iso.org/iso-3166-country-codes.html)
 - [Verifiable Credentials Data Model 1.0](https://www.w3.org/TR/vc-data-model/)
 - [Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/)
 - [DID Specification Registries](https://w3c.github.io/did-spec-registries/)
 - [Delaware Limited Liability Company](https://www.cscglobal.com/service/cls/delaware-llc-guide/)
 - [Biometric epassport](https://en.wikipedia.org/wiki/Biometric_passport)
