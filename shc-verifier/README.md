![](../CTN_Logo_Horizontal.png)

# SMART Health Card Verifier API
The SMART Health Card Verifier API provides organizations an interface to check that a SMART Health Card is valid (i.e. not tampered with) and was issued by an issuer in the CommonTrust Network Registry. If the SMART Health Card passes validation, the payload of the SMART Health Card, containing the patient’s name, the vaccine’s CVX code, and the date of each dose, will be returned to the organization seeking to verify the credential. If the issuer of the SMART Health Card is registered in the CommonTrust Network Registry, the issuer information is returned alongside the SMART Health Card payload.

The SMART Health Card Verifier API accepts SMART Health Cards either encoded as a JSON Web Signature (JWS) or a numeric encoded JWS as defined in the [SMART Health Card specification](https://spec.smarthealth.cards/#creating-a-qr-code-or-a-set-of-qr-codes-from-a-health-card-jws), the encoding used when the SMART Health Card is represented as a QR code.

Is addition to signature validation, the SMART Health Card verifier performs the following conformance checks:
 - `nbf` is less than or equal to the current time (with nominal leeway to account for clock skew)
 - `vc.type` is present and contains an array of strings
 - `vc.credentialSubject.fhirVersion` is present and contains a string
 - `vc.credentialSubject.fhirBundle` is present and contains an object

## Sample Requests and Response

The following requests are equivalent and return the same response:
```
curl --location --request POST 'https://api.commontrustnetwork.org/shc/v1/verifier' \
--header 'x-api-key: {{ API_KEY }}' \
--header 'Content-Type: application/json' \
--data-raw '{
   "shc_jws":"eyJ6aXAiOiJERUYiLCJhbGciOiJFUzI1NiIsImtpZCI6IjNLZmRnLVh3UC03Z1h5eXd0VWZVQUR3QnVtRE9QS01ReC1pRUxMMTFXOXMifQ.3ZJLb9swEIT_SrC9yhIlJzGsW50CfRyKAk17KXygqbXFgg-BpIS4gf57d2kHbYMkp5yq24rDjzND3oOOEVroUxpiW1VxQFVGK0PqUZrUl0qGLlZ4J-1gMFakHjFAAW63h7a-Xi6X10I06_JydVXApKC9h3QcENoff5iPcW9Ow4IHQj2v09aOTv-SSXv3olD5SXf1GrYFqIAduqSl-TrufqJKbGnf6_AdQ2ROC5elKGvi8d_N6DqDrAkY_RgU3mb7cF4oznFAeWOIdnJCB4QjZSTyaMy3YEjwsL8VJHgYngB_oTi0nzuUFk8QabUhHrx1pAkxn3HQEzru8ZPved6UsJ0p4E5T-HcyMateX9ULUS8aAfNcPOmmftnNx38rjkmmMea4fOEJ-YImqZR2eOO7TFC-0-6QjcdjTGjP74dupjer0odDxc1WUXeVmu4IoPJOaMQK5u1cwHCuINvZY0DH3v5ukEReqTHkJQ57q-0J0eTAgmNRVXsfLL1H9iJV8oGRnY6DkbnOzc3Fe3QYpLn44OOgkzRUFJVofPo82h1vBZG_-tkGm_-ywWb92g2ueGGm7zc.5jM9qq_jL7fZbgCrg-RPeDBrd7i7P6k5jDSZV4irBXLgfUqAwnSGuh1VfZi8g-0W7qUygyf5qns5dZ_7uidcfg"
}'
```

```
curl --location --request POST 'https://api.commontrustnetwork.org/shc/v1/verifier' \
--header 'x-api-key: {{ API_KEY }}' \
--header 'Content-Type: application/json' \
--data-raw '{
   "shc_numeric":"shc:/5676290952432060346029243740446031222959532654603460292540772804336028702864716745222809286133314564376531415906402203064504590856435503414245413640370636654171372412363803043756220467374075323239254334433260573601064529315312707424283950386922127659286329772670420803225737763020620410304376586853432558580021672838075857081055056227534432626708766805076923617733230666343424416966407567604204417536254126300335684045694063036826316345072900045832255262276125202042090659105200436009430403280309502976554143206730221259063654243366575708603554421234740728273661057303125234397300383843730666632308384357042669442568282055726838630039697257682930532665570950205536053734220856633026736011555033092368236920624450375840066453105425076677652520564234285565292221073661453839765232760644246174703111412927584465582150663960036577724025621136525340592769750467206275650627362477697211453573565509407029036707240839002754763252715643124031403811522057335435346464577165337506116961626464325652075734242900442864684537055634341039252200030009366154556139266135100755726761566903665523755404424043564164720728663529345232363008720454742722722833734544032327067308726224375668392762293608106800032903563920586433374143705731310427126029411166263765440923625365347754062556063644673165070734345862773740252941665735661105590473214526500071622664500076744253120558057256262664107754010861321268685061311057455358226958003735562321695510601035096208612338454107606921433158574068207465382672590441574560115800034210684076587657086865700855455010726055545758"
}'
```

Response:
```
{
    "payload": {
        "iss": "https://spec.smarthealth.cards/examples/issuer",
        "nbf": 1633360029.475,
        "vc": {
            "type": [
                "https://smarthealth.cards#health-card",
                "https://smarthealth.cards#immunization",
                "https://smarthealth.cards#covid19"
            ],
            "credentialSubject": {
                "fhirVersion": "4.0.1",
                "fhirBundle": {
                    "resourceType": "Bundle",
                    "type": "collection",
                    "entry": [
                        {
                            "fullUrl": "resource:0",
                            "resource": {
                                "resourceType": "Patient",
                                "name": [
                                    {
                                        "family": "Anyperson",
                                        "given": [
                                            "John",
                                            "B."
                                        ]
                                    }
                                ],
                                "birthDate": "1951-01-20"
                            }
                        },
                        {
                            "fullUrl": "resource:1",
                            "resource": {
                                "resourceType": "Immunization",
                                "status": "completed",
                                "vaccineCode": {
                                    "coding": [
                                        {
                                            "system": "http://hl7.org/fhir/sid/cvx",
                                            "code": "207"
                                        }
                                    ]
                                },
                                "patient": {
                                    "reference": "resource:0"
                                },
                                "occurrenceDateTime": "2021-01-01",
                                "performer": [
                                    {
                                        "actor": {
                                            "display": "ABC General Hospital"
                                        }
                                    }
                                ],
                                "lotNumber": "0000001"
                            }
                        },
                        {
                            "fullUrl": "resource:2",
                            "resource": {
                                "resourceType": "Immunization",
                                "status": "completed",
                                "vaccineCode": {
                                    "coding": [
                                        {
                                            "system": "http://hl7.org/fhir/sid/cvx",
                                            "code": "207"
                                        }
                                    ]
                                },
                                "patient": {
                                    "reference": "resource:0"
                                },
                                "occurrenceDateTime": "2021-01-29",
                                "performer": [
                                    {
                                        "actor": {
                                            "display": "ABC General Hospital"
                                        }
                                    }
                                ],
                                "lotNumber": "0000007"
                            }
                        }
                    ]
                }
            }
        }
    },
    "issuer": {
        "id": "56ac650b-2f67-44f5-a38e-c306325a8116",
        "name": "SHC Example Issuer",
        "environment": "PROD"
    }
}
```

## API Definition

A more detailed API definition can be found in [`shc-verifier.yml`](shc-verifier.yml), including information about potential errors.

## Postman Collection

A Postman collection with sample queries is provided in this repo. To authenticate the requests to respective environments, populate a Postman environment with `x-api-key-sandbox` and `x-api-key-production` values, if available.

## Testing Considerations

The test environment only supports a limited number of known issuers of sample SMART Health Cards, including `https://spec.smarthealth.cards/examples/issuer`. Example SMART Health Cards issued by `https://spec.smarthealth.cards/examples/issuer` can be found [here](https://spec.smarthealth.cards/examples/). If you need any additional issuers of sample SMART Health Cards added to this list in order to support your testing, please reach out.
