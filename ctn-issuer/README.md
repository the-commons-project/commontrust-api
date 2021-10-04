# CommonTrust Network Issuer Lookup API
The CommonTrust Network Issuer Lookup API allows clients to query the CommonTrust Network Directory for information about the issuer of a SMART Health Card. Clients would first discover the `iss` value of the issuer of a SMART Health Card. Then, the client would make a `GET` request to the `v1/ctn-issuer` endpoint, specifying the `iss` value as the `identifier` query parameter and `smarthealthcard` as the `system` query parameter. Clients will need to include their API Key in the `x-api-key` header as part of the request.

## Sample Request and Response
Request:
```
curl --location --request GET 'https://api.commontrustnetwork.org/v1/ctn-issuer?system=smarthealthcard&identifier=https://spec.smarthealth.cards/examples/issuer' \
--header 'x-api-key: {{ API_KEY }}'
```

Response:
```
{
    "id": "56ac650b-2f67-44f5-a38e-c306325a8116",
    "name": "SHC Example Issuer",
    "environment": "PROD"
}
```

## API Definition

A more detailed API definition can be found in [`issuer.yml`](issuer.yml), including information about potential errors.