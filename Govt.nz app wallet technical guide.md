# Govt.nz App Wallet Technical Guide
This page describes technical details and configuration requirements organisations issuing credentials into the [Govt.nz app wallet](/README.md).

* [User experience](#user-experience)
* [Credential requirements](#credential-requirements)
  * [Status list distribution](#status-list-distribution)
  * [Status list requirements](#status-list-requirements)
  * [Optional credential claims](#optional-credential-claims)
  * [Deep links for issuance](#deep-links-for-issuance)
* [Credential presentation](#credential-presentation)
  * [In-person presentation](#in-person-presentation)
  * [Deep links for presentation](#deep-links-for-presentation)
  * [References](#references)

## Background
The wallet uses the [MATTR Pi mDocs Holder SDK](https://learn.mattr.global/docs/holding/sdk-overview) within the [Govt.nz app](https://www.govt.nz/about/the-govt-nz-app/). 

## User experience
Examples of the wallet appearance for users during all phases of credential management, including issuance, presentation, and viewing credentials and usage history, are shown in the [Govt.nz wallet credential flows](/Govt.nz%20wallet%20-%20credential%20flows.pdf) document. 

## Credential requirements
The wallet is based on the [ISO/IEC 18013-5](https://www.iso.org/standard/69084.html) standard, including aspects of the draft second edition. It accepts mDoc format credentials.

### Status list distribution
All DISTF accredited credentials with an expiry period of over 72 hours must provide means for revoking the credential. The wallet supports this through use of the [Token Status List](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-status-list-14) mechanism. 

Credential issuers must communicate the status list distribution point for a credential in the IACA:

* Include a non-critical extension with `extnID 1.3.6.1.4.1.61546.100`
* `extnValue` is the BER encoding of an ASN1 UTF8String of the status list distribution URI

### Status list requirements
Status List Tokens must be encoded in CBOR Web Token (CWT) format and meet all the REQUIRED parts of [Token Status List section 5.2](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-status-list-21#section-5.2), including labels:

* 16 (protected header, type) =  `application/statuslist+cwt`
* 2 (subject)
* 6 (issued at)

The CWT shall contain the `x5chain` in the protected header that contains the certificate or chain of certificates used to verify the signature of the revocation status list.

### Optional credential claims
During a verification request, the wallet will select a credential for presentation where there is an exact match on all requested claim labels. A credential that omits an optional claim label, for example where that claim is not applicable to the holder, will not be returned in response to a request for that claim. Credentials should be issued with all defined claim labels present, using blank or null values for non-applicable optional claims, rather than omitting those claims entirely.

### Deep links for issuance
The wallet is registered with the `openid-credential-offer://` URL scheme for maximum interoperability, allowing the device holder to select the Govt.nz app wallet during credential issuance.

It is possible to deep link directly into the Govt.nz app to specifically issue into its wallet. A generic credential offer URI can be transformed into a form that will open the Govt.nz app on a user's device, either by scanning a QR code with the device camera or by opening a link on the device.

**Sandbox**  

Replace `openid-credential-offer://` with `https://sandbox.m.app.govt.nz/openid-credential-offer` 

**Production**  

Replace `openid-credential-offer://` with `https://m.app.govt.nz/openid-credential-offer`

For example, a sandbox credential offer would start with: 

    https://sandbox.m.app.govt.nz/openid-credential-offer?credential_offer=%7B%22credential_issuer… 

## Credential presentation
The wallet supports in-person presentation, e.g. to point-of-sale terminals or verifying apps, and online presentation following [ISO/IEC 18013-7:2025 Annex B](https://www.iso.org/standard/91154.html), which profiles [OpenID for Verifiable Presentations (OpenID4VP) Draft 18](https://openid.net/specs/openid-4-verifiable-presentations-1_0-ID2.html).

Support for the [Digital Credentials API (DC API)](https://w3c-fedid.github.io/digital-credentials/) will be added by the end of 2026. In a presentation using the DC API, the wallet will support [OpenID4VP v1.0](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html).

When a verification request is initiated, the wallet will select a credential that matches the request document type and that contains all requested claims. If there are multiple matching credentials, the most recent is selected by default and the wallet holder may choose to switch to another credential for presentation.

The app displays the selected credential to the wallet holder, along with the claims that are requested to be shared, and shows which claims the verifier has indicated will be retained. The user must approve the sharing of the credential by using 3D facial recognition or fingerprint scanning, as managed by the device. Using the device's PIN or password as a fallback authentication method is not permitted. 

### In-person presentation

Device engagement during in-person verification can be initiated through scanning a QR code presented in the wallet iOS and Android versions, or through NFC engagement on Android devices. Device retrieval transport is through BLE, with the wallet in `mDoc peripheral server mode`. 

### Deep links for presentation

The wallet is registered with the `mdoc-openid4vp://` URL scheme for maximum interoperability, allowing the device holder to select the Govt.nz app wallet during presentation for verification.

It is possible to deep link directly into the Govt.nz app to specifically request a credential from its wallet. A generic verifiable presentation URI can be transformed into a form that will open the Govt.nz app on a user's device, either by scanning a QR code with the device camera or by opening a link on the device.

**Sandbox**  

Replace `mdoc-openid4vp://` with `https://sandbox.m.app.govt.nz/mdoc-openid4vp` 

**Production**  

Replace `mdoc-openid4vp://` with `https://m.app.govt.nz/mdoc-openid4vp`

For example, a sandbox credential offer would start with: 

    https://sandbox.m.app.govt.nz/mdoc-openid4vp?client_id=genericverifier.com&client_id_scheme=x509_san_dns&request_uri=...

## References
[Digital Credential Concepts](https://learn.mattr.global/docs/concepts)

[MATTR Pi mDocs Holder SDK](https://learn.mattr.global/docs/holding/sdk-overview)

[MATTR VII API](https://learn.mattr.global/docs/api-reference)

[Open ID for Verifiable Credential Issuance (OpenID4VCI)](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html)

[OpenID for Verifiable Presentations (OpenID4VP)](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)

[Digital Identity Services Trust Framework Rules](https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation/trust-framework-rules)
