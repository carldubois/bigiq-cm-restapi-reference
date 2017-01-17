## Retrieving links to all policy sub collections and listing all parameters in the policy.

### Overview
Describes how you use the REST API to retrieve links to all policy sub collections and use of those links to retrieve the list of all parameters in the policy.

### Prerequisites
Retrieve a policy selfLink using the policy name, as shown on other examples in this chapter.

### Description
Describes how you use the REST API to retrieve links to all policy sub collections and use of those links to retrieve the list of all parameters in the policy.
Perform the REST API actions in the following order:
1. Perform a GET operation using the policy selfLink to return all the policy attributes.
2. Perform a GET operation on the parameters sub collection link.

The following extended example shows each of these REST API actions.

### Example

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

#### 2. Perform a GET operation on the parameters sub collection link.
Perform a GET operation on the parameters sub collection link. The parameters sub collection link can be found in the 'parameterReference' reference structure (link attribute) in the policy above. The link can also be determined by the policy selfLink - add '/parameters' to the policy selfLink. The same logic applies to all other sub collections as listed above.

```
GET: https://<mgmtip>/mgmt/cm/asm/working-config/policies/<id>/parameters
```
The following is the JSON response from the GET operation:
```
{
    "items": [
        {
            "allowRepeatedParameterName": false,
            "checkMaxValueLength": false,
            "metacharsOnParameterValueCheck": true,
            "attackSignaturesCheck": true,
            "isBase64": false,
            "sensitiveParameter": false,
            "allowEmptyValue": true,
            "enableRegularExpression": false,
            "performStaging": false,
            "dataType": "alpha-numeric",
            "level": "url",
            "signatureOverrides": [
                {
                    "enabled": true,
                    "signatureReference": {
                        "name": "\"open()\" execution attempt",
                        "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0d8018f7-055b-3b72-96eb-97c3e3bb3c64"
                    }
                }
            ],
            "valueMetacharOverrides": [
                {
                    "isAllowed": false,
                    "metachar": "0x4"
                }
            ],
            "valueType": "user-input",
            "urlReference": {
                "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/urls/96009cdc-01c5-37bd-a5d1-1189937a16a0"
            },
            "type": "explicit",
            "name": "Param_1",
            "id": "07a6094f-c99d-3aac-8a20-b154663a6ea8",
            "generation": 1,
            "lastUpdateMicros": 1479395792656799,
            "kind": "cm:asm:working-config:policies:parameters:parameterstate",
            "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/parameters/07a6094f-c99d-3aac-8a20-b154663a6ea8"
        },
        {
            "allowRepeatedParameterName": false,
            "checkMaxValueLength": false,
            "checkMetachars": true,
            "metacharsOnParameterValueCheck": true,
            "attackSignaturesCheck": true,
            "isBase64": false,
            "sensitiveParameter": false,
            "allowEmptyValue": true,
            "enableRegularExpression": false,
            "performStaging": true,
            "dataType": "alpha-numeric",
            "level": "global",
            "nameMetacharOverrides": [],
            "signatureOverrides": [],
            "valueMetacharOverrides": [],
            "valueType": "user-input",
            "wildcardOrder": 1,
            "type": "wildcard",
            "name": "*",
            "id": "138afd59-dc95-373f-8b73-03a871dd863f",
            "generation": 1,
            "lastUpdateMicros": 1479388438536186,
            "kind": "cm:asm:working-config:policies:parameters:parameterstate",
            "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/parameters/138afd59-dc95-373f-8b73-03a871dd863f"
        }
    ],
    "generation": 3,
    "kind": "cm:asm:working-config:policies:parameters:parametercollectionstate",
    "lastUpdateMicros": 1479395792694929,
    "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/parameters"
}
```

### API references used to support this workflow:
[Api reference - virtual server management](../html-reference/virtual-server-management.html)

[Api reference - asm policy management](../html-reference/asm-policies.html)