## Enable and enforce a specific signature in a policy by signatureId

### Overview
Describes how you use the REST API to update the attributes of a specific signature in a policy.

### Prerequisites

1. Retrieve a policy selfLink using the policy name, as shown on other examples in this chapter.
2. Find the signatureId that needs to be updated. The signatureId is shown on the BIG-IP and BIG-IQ UI and is reported in violation logs.

### Description

Describes how you use the REST API to update the attributes of a specific signature in a policy.

Perform the REST API actions in the following order:

1. Perform a GET operation to the signatures collection to retrieve a seflLink of a signature.
2. Perform a GET operation to the policy signatures to validate that the signature is listed within the security policy signatures.
3. Perform a POST operation with the new attributes to a special URI that updates policy signature attributes.

The following extended example shows each of these REST API actions.

#### 1. Perform a GET operation to the signatures collection to retrieve a seflLink of a signature.
Perform a GET operation to the signatures collection to retrieve a seflLink of a signature.
```
GET: https://<mgmtip>/mgmt/cm/asm/working-config/signatures/$filter=signatureId eq '<signatureId>'?$select=signatureId,selfLink
```
The following is the JSON response from the GET operation:
```
{
    "selfLink": "https://localhost/mgmt/cm/asm/working-config/signatures",
    "totalItems": 1,
    "items": [
        {
            "signatureId": "200010008",
            "selfLink": "https://localhost/mgmt/cm/asm/working-config/signatures/152bcf94-4ab3-3f8b-b524-4648f83249e0"
        }
    ],
    "generation": 2925,
    "kind": "cm:asm:working-config:signatures:signaturecollectionstate",
    "lastUpdateMicros": 1479385001323905
}
```
#### 2. Perform a GET operation to the policy signatures to validate that the signature is listed within the security policy signatures.
Perform a GET operation on the signatures sub collection link, with a special parameter called 'filterBySignatureSets' that limits the results to signatures that are part of the sets that are defined in the policy. The signatures sub collection link can be found in the 'signatureReference' reference structure (link attribute) in the policy above. The link can also be determined by the policy selfLink - add '/signatures' to the policy selfLink. The same logic applies to all other sub collections as listed above.
Note - further filtering by the 'enabled'/'performStaging' attributes cannot be done by the REST APIs. Such filtering should be done by the caller with the retrieved results.
To validate that the signature is used in the policy, validate that the 'selfLink' obtained in step #1 is set in one of the signatures as the value of the link attribute of the signatureReference structure.

```
GET: https://<mgmtip>/mgmt/cm/asm/working-config/policies/<id>/signatures?filterBySignatureSets=true
```
The following is the JSON response from the GET operation:
```
{
    "items": [
        {
            "signatures": [ **** Link to t_asm_signatures_reference.md **** ],
            "name": "signatures",
            "id": "006fcd4e-b57c-3714-aede-6bb66938a9a6",
            "generation": 1,
            "lastUpdateMicros": 1479388438674931,
            "kind": "cm:asm:working-config:policies:signatures:policysignaturearraystate",
            "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/signatures/006fcd4e-b57c-3714-aede-6bb66938a9a6"
        }
    ],
    "generation": 2,
    "lastUpdateMicros": 1479388438906235,
    "kind": "cm:asm:working-config:policies:signatures:policysignaturecollectionstate",
    "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/signatures"
}
```
#### 3. Perform a POST operation with the new attributes to a special URI that updates policy signature attributes.
Perform a POST operation with the new attributes to a special URI that updates policy signature attributes. The URI is the string "/signatures/update" appended to the policy selfLink. The POST data contains an array of updated signatures. Use the signature selfLink as obtained in step #1 as the link attribute of the 'signatureReference' structure. Choose the 'enabled' and 'performStaging' values as needed.
Note - the example shows one signature in the 'updatedSignatures' array, but multiple signatures can be chosen.
```
POST: https://<mgmtip>/mgmt/cm/asm/working-config/policies/<policy id>/signatures/update
{  
   "updatedSignatures":[  
      {  
         "signatureReference":{  
            "link":"https://localhost/mgmt/cm/asm/working-config/signatures/152bcf94-4ab3-3f8b-b524-4648f83249e0"
         },
         "enabled":true,
         "performStaging":true
      }
   ]
}
```
The following is the JSON response from the POST operation:
```
{
    "updatedSignatures": [
        {
            "signatureReference": {
                "link": "https://localhost/mgmt/cm/asm/working-config/signatures/152bcf94-4ab3-3f8b-b524-4648f83249e0"
            },
            "enabled": true,
            "performStaging": true
        }
    ]
}
```

### API Reference