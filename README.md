![](./CTN_Logo_Horizontal.png)

# CommonTrust Network Registry APIs

## Welcome to the CommonTrust Network Registry APIs

The CommonTrust Network Registry APIs enable organizations to build scalable solutions for verifying COVID-19 health credentials issued for testing and vaccination. 

These APIs are powered by the CommonTrust Network, a registry of trusted data sources that are issuing verifiable credentials such as SMART Health Cards. Issuers include health systems, testing providers, vaccination providers, and public health registries.

## Project Goal

Using the CommonTrust Network Registry APIs, you can build enterprise solutions to verify issued health credentials within your existing platforms.

## Projects

### CommonTrust Network Registry API

The CommonTrust Network Registry API allows organizations to query the CommonTrust Network Registry to look up information about whether the issuer of a SMART Health Card is a participant in the registry.

See [here](ctn-issuer/README.md) for more detailed information about the CommonTrust Network Registry API.

### SMART Health Card Verifier API
The SMART Health Card Verifier API provides organizations an interface to check that a SMART Health Card is valid (i.e. not tampered with) and was issued by an issuer in the CommonTrust Network Registry. If the SMART Health Card passes validation, the payload of the SMART Health Card, containing the patient’s name, the vaccine’s CVX code, and the date of each dose, will be returned to the organization seeking to verify the credential. If the issuer of the SMART Health Card is registered in the CommonTrust Network Registry, the issuer information is returned alongside the SMART Health Card payload.

See [here](shc-verifier/README.md) for more detailed information about the SMART Health Card Verifier API.
