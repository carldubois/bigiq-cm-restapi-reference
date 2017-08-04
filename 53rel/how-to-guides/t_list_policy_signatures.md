## Listing all signatures in a Web Application Security policy.

### Overview

Describes how you use the REST API to retrieve all the signatures for a specific policy, with their settings. The signatures listed are those that are part of the signature sets that are associated with the policy.

### Prerequisites

Retrieve a policy selfLink using the policy name, as shown on other examples in this chapter.

### Description

Describes how you use the REST API to retrieve all the signatures for a specific policy, with their settings. 

Perform the REST API actions in the following order:

1. Perform a GET operation using the policy selfLink to return all the policy attributes.
2. Perform a GET operation on the signatures sub collection link.

### REST API actions.

#### 1. Perform a GET operation using the policy selfLink to return all the policy attributes.
Perform a GET operation on a policy resource using the selfLink obtained from the policies collection. Note that the "localhost" host name is the link will need to be replaced with the management IP address or the DNS record of the BIG-IQ device.
```
GET: https://<mgmtip>/mgmt/cm/asm/working-config/policies/<id>
```
The following is the JSON response from the GET operation:
```
{
    "allowedResponseCodes": [
        400,
        401,
        404,
        407,
        417,
        503
    ],
    "createdDatetime": "2016-11-17T13:13:58Z",
    "creatorName": "admin",
    "customXffHeaders": [],
    "applicationLanguage": "utf-8",
    "caseInsensitive": false,
    "protocolIndependent": false,
    "enforcementMode": "transparent",
    "learningMode": "manual",
    "modifierName": "",
    "stagingSettings": {
        "signatureStaging": true,
        "placeSignaturesInStaging": false,
        "enforcementReadinessPeriod": 7
    },
    "attributes": {
        "maximumCookieHeaderLength": "8192",
        "inspectHttpUploads": false,
        "triggerAsmIruleEvent": "disabled",
        "useDynamicSessionIdInUrl": false,
        "maximumHttpHeaderLength": "8192",
        "maskCreditCardNumbersInRequest": true,
        "pathParameterHandling": "as-parameters"
    },
    "fullPath": "/Common/Policy_1",
    "versionDeviceName": "Policy_1",
    "versionLastChange": "POST Policy_1",
    "versionPolicyName": "/Common/Policy_1",
    "versionDatetime": "2016-11-17T13:13:58Z",
    "trustXff": false,
    "disallowedGeolocationReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/disallowed-geolocations",
        "isSubcollection": true
    },
    "signatureReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/signatures",
        "isSubcollection": true
    },
    "csrfProtectionReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/csrf-protection",
        "isSubcollection": true
    },
    "methodReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/methods",
        "isSubcollection": true
    },
    "sessionTrackingReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/session-tracking",
        "isSubcollection": true
    },
    "parameterReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/parameters",
        "isSubcollection": true
    },
    "ipIntelligenceReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/ip-intelligence",
        "isSubcollection": true
    },
    "policyBuilderReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/policy-builder",
        "isSubcollection": true
    },
    "dataGuardReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/data-guard",
        "isSubcollection": true
    },
    "webScrapingReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/web-scraping",
        "isSubcollection": true
    },
    "headerReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/headers",
        "isSubcollection": true
    },
    "responsePageReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/response-pages",
        "isSubcollection": true
    },
    "xmlProfileReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/xml-profiles",
        "isSubcollection": true
    },
    "urlReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/urls",
        "isSubcollection": true
    },
    "sensitiveParameterReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/sensitive-parameters",
        "isSubcollection": true
    },
    "loginPageReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/login-pages",
        "isSubcollection": true
    },
    "xmlValidationFileReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/xml-validation-files",
        "isSubcollection": true
    },
    "cookieReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/cookies",
        "isSubcollection": true
    },
    "characterSetReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/character-sets",
        "isSubcollection": true
    },
    "loginEnforcementReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/login-enforcement",
        "isSubcollection": true
    },
    "bruteForceAttackPreventionReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/brute-force-attack-preventions",
        "isSubcollection": true
    },
    "redirectionProtectionReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/redirection-protection",
        "isSubcollection": true
    },
    "whitelistIpReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/whitelist-ips",
        "isSubcollection": true
    },
    "gwtProfileReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/gwt-profiles",
        "isSubcollection": true
    },
    "signatureSetReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/signature-sets",
        "isSubcollection": true
    },
    "jsonProfileReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/json-profiles",
        "isSubcollection": true
    },
    "filetypeReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/filetypes",
        "isSubcollection": true
    },
    "hostNameReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/host-names",
        "isSubcollection": true
    },
    "violationsReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/violations",
        "isSubcollection": true
    },
    "evasionsReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/evasions",
        "isSubcollection": true
    },
    "httpProtocolsReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/http-protocols",
        "isSubcollection": true
    },
    "webServicesSecurityReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/web-services-securities",
        "isSubcollection": true
    },
    "extractionsReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/extractions",
        "isSubcollection": true
    },
    "plainTextProfileReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/plain-text-profiles",
        "isSubcollection": true
    },
    "websocketUrlReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/websocket-urls",
        "isSubcollection": true
    },
    "sectionReference": {
        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/sections",
        "isSubcollection": true
    },
    "type": "security",
    "hasParent": false,
    "partition": "Common",
    "name": "Policy_1",
    "description": "",
    "id": "1005831c-7e40-30ed-bd0d-f8068526d7ef",
    "generation": 1,
    "lastUpdateMicros": 1479388438212062,
    "kind": "cm:asm:working-config:policies:policystate",
    "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef"
}
```
#### 2. Perform a GET operation on the signatures sub collection link.
Perform a GET operation on the signatures sub collection link, with a special parameter called 'filterBySignatureSets' that limits the results to signatures that are part of the sets that are defined in the policy. The signatures sub collection link can be found in the 'signatureReference' reference structure (link attribute) in the policy above. The link can also be determined by the policy selfLink - add '/sigantures' to the policy selfLink. The same logic applies to all other sub collections as listed above.
Note - further filtering by the 'enabled'/'performStaging' attributes cannot be done by the REST APIs. Such filtering should be done by the caller with the retrieved results.

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

### API Reference