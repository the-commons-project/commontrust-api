![](../CTN_Logo_Horizontal.png)

# CommonTrust Network Registry API
The CommonTrust Network Registry API allows organizations to query the CommonTrust Network Registry to look up information about whether the issuer of a SMART Health Card is a participant in the registry.

Clients would first discover the `iss` value of the issuer of a SMART Health Card. Then, the client would make a `GET` request to the `/ctn/v1/issuer` endpoint, specifying the `iss` value as the `identifier` query parameter and `smarthealthcard` as the `system` query parameter. Clients will need to include their API Key in the `x-api-key` header as part of the request.

## Sample Request and Response
Request:
```
curl --location --request GET 'https://api.commontrustnetwork.org/ctn/v1/issuer
?system=smarthealthcard&identifier=https://spec.smarthealth.cards/examples/issuer' \
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

## Postman Collection

A Postman collection with sample queries is provided in this repository. To authenticate the requests to respective environments, populate a Postman environment with `x-api-key-sandbox` and `x-api-key-production` values, if available.
