# The Govt.nz app wallet
## Purpose
The Govt.nz app wallet ("the wallet") is operated as part of the [Digital Public Infrastructure](https://github.com/NZ-Digital-Public-Infrastructure/.github/blob/main/profile/README.md) (DPI) to provide means for New Zealanders to hold digital credentials.

In the digital credentials ecosystem, the wallet is the component responsible for receiving a credential from an issuer, securely storing it for the user (the "holder"), and presenting the credential to a verifier at the holder's request. 

![Digital credential ecosystem diagram](/assets/ecosystem-diagram-wallet-highlight.png "Digital credential ecosystem diagram")

The wallet is a key component of the [Govt.nz app](https://www.govt.nz/about/the-govt-nz-app) that is available for iOS and Android devices.

## How does the wallet work?
The wallet follows the [OpenID for Verifiable Credential Issuance (OID4VCI)](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html) standard to accept credentials offered by an issuer, with the holder's permission. The wallet receives a cryptographically signed credential that is:

* **Tamper-evident:** Any modification invalidates the signature.
* **Verifiable:** Any relying party can confirm authenticity against the issuer's certificate chain without contacting the issuer.
* **Portable:** Stored in the user's wallet and presentable across contexts.
* **Revocable:** Status can be updated after issuance.

The DISTF Draft Reference Architecture provides more details on the [digital credential trust model](https://github.com/nz-trust-framework/DISTF-reference-architecture/blob/main/7-TRUST.md), with particular reference to the New Zealand context.

## Who should use the wallet?
Any New Zealand government agency or other organisation that issues digital credentials accredited under the [Digital Identify Services Trust Framework (DISTF)](https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation) can add their credential into the wallet. Example types of credential include: 

* Personal identification
* Educational qualifications
* Health records
* Proof of role in a public register
* Licences 
* Financial information 
* Proof of address 
* Travel documents 
* Delegated authority 

### Trusted issuers

The wallet refers to a trusted issuers list maintained by the DPI team, which contains all the Issuing Authority Certificate Authority certificates (IACAs) used to issue accredited credentials, and the URLs of the credential issuance services. Credentials may be added to the wallet if their URL and IACA are in the list.

## Using the Wallet

### Onboarding

Contact the DPI team at [governmentapp@gdda.govt.nz](mailto:governmentapp@gdda.govt.nz) to begin the onboarding process. This will involve testing the functionality and appearance of the new credential in a test environment.

Once the credential accreditation process is completed, the DPI team will add the IACA and URL of the production service into the trusted issuers list so users of the Govt.nz app can be offered and issued the credential.

> [!IMPORTANT]
> The IACA for an accredited credential must not be used for issuance of non-accredited credentials. 

### Development

New Zealand government agencies that provide digital credential must use the All of Government [Digital Credential Issuance Platform (DCIP)](https://github.com/NZ-Digital-Public-Infrastructure/nz-digital-credential-issuance-platform). 

The DPI team will be able to configure the wallet trusted issuer details for any agency using the DCIP.

Other types of organisations using alternative credential systems will need to provide the IACA and URL details to be added to the wallet trusted issuer list.

### Testing

A sandbox test tenancy is provided for use during development and testing. This can be used in conjunction with sandbox versions of other DPI products, including the Govt.nz app wallet, and NZ Verify.

See our [DPI Sandbox Guide](https://github.com/NZ-Digital-Public-Infrastructure/.github/blob/main/profile/sandbox/Sandbox%20User%20Guide.md) for details of the test products.

The sandbox version of the iOS or Android Govt.nz app can be deployed to the mobile devices of requested users in the issuing organisation for testing the credential.

### Costs
There is no fee for use of the wallet.

### Support

Contact the DPI team at [governmentapp@gdda.govt.nz](mailto:governmentapp@gdda.govt.nz) for assistance during development and testing, or operational support of production services.

## Links
[Digital Public Infrastructure](https://github.com/NZ-Digital-Public-Infrastructure/.github/blob/main/profile/README.md)

[Digital Identify Services Trust Framework (DISTF)](https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation)

[DISTF Draft Reference Architecture](https://github.com/nz-trust-framework/DISTF-reference-architecture/blob/main/README.md)
