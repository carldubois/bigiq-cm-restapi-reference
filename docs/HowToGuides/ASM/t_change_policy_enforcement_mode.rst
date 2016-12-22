Changing a policy enforcement mode.
-----------------------------------

Overview
~~~~~~~~

Describes how you use the REST API to view and change the policy
enforcement mode.

Prerequisites
~~~~~~~~~~~~~

Retrieve a policy selfLink using the policy name, as shown on other
examples in this chapter. ### Description Describes how you use the REST
API to view and change the policy enforcement mode. 1. Perform a GET
operation on the policy selfLink 1. Perform a PATCH operation on the
policy selfLink.

The following extended example shows each of these REST API actions. ###
Example #### 1. Perform a GET operation on the policy selfLink. Perform
a GET operation on the policy selfLink, selecting only the
'enforcementMode' field to be retrieved.

::

    GET: https://<mgmtip>/mgmt/cm/asm/working-config/policies/<policy id>?$select=enforcementMode

The following is the JSON response from the GET operation:

::

    {
        "enforcementMode": "transparent"
    }

2. Perform a PATCH operation on the policy selfLink.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a PATCH operation on the policy selfLink. The data being sent to
the server includes the new enforcementMode ('blocking').

::

    PATCH: https://<mgmtip>/mgmt/cm/asm/working-config/policies/<policy id>
    {
        "enforcementMode": "blocking"
    }

The following is the JSON response from the PATCH operation (the server
returns the updated attributes of the policy):

::

    {
        "allowedResponseCodes": [
            400,
            401,
            404,
            407,
            417,
            503
        ],
        "createdDatetime": "2016-11-20T11:37:32Z",
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
        "fullPath": "/Common/Policy_3",
        "versionDeviceName": "Policy_3",
        "versionLastChange": "POST Policy_3",
        "versionPolicyName": "/Common/Policy_3",
        "versionDatetime": "2016-11-20T11:37:32Z",
        "trustXff": false,
        "disallowedGeolocationReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/disallowed-geolocations",
            "isSubcollection": true
        },
        "signatureReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/signatures",
            "isSubcollection": true
        },
        "csrfProtectionReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/csrf-protection",
            "isSubcollection": true
        },
        "methodReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/methods",
            "isSubcollection": true
        },
        "sessionTrackingReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/session-tracking",
            "isSubcollection": true
        },
        "parameterReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/parameters",
            "isSubcollection": true
        },
        "ipIntelligenceReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/ip-intelligence",
            "isSubcollection": true
        },
        "policyBuilderReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/policy-builder",
            "isSubcollection": true
        },
        "dataGuardReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/data-guard",
            "isSubcollection": true
        },
        "webScrapingReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/web-scraping",
            "isSubcollection": true
        },
        "headerReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/headers",
            "isSubcollection": true
        },
        "responsePageReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/response-pages",
            "isSubcollection": true
        },
        "xmlProfileReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/xml-profiles",
            "isSubcollection": true
        },
        "urlReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/urls",
            "isSubcollection": true
        },
        "sensitiveParameterReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/sensitive-parameters",
            "isSubcollection": true
        },
        "loginPageReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/login-pages",
            "isSubcollection": true
        },
        "xmlValidationFileReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/xml-validation-files",
            "isSubcollection": true
        },
        "cookieReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/cookies",
            "isSubcollection": true
        },
        "characterSetReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/character-sets",
            "isSubcollection": true
        },
        "loginEnforcementReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/login-enforcement",
            "isSubcollection": true
        },
        "bruteForceAttackPreventionReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/brute-force-attack-preventions",
            "isSubcollection": true
        },
        "redirectionProtectionReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/redirection-protection",
            "isSubcollection": true
        },
        "whitelistIpReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/whitelist-ips",
            "isSubcollection": true
        },
        "gwtProfileReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/gwt-profiles",
            "isSubcollection": true
        },
        "signatureSetReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/signature-sets",
            "isSubcollection": true
        },
        "jsonProfileReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/json-profiles",
            "isSubcollection": true
        },
        "filetypeReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/filetypes",
            "isSubcollection": true
        },
        "hostNameReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/host-names",
            "isSubcollection": true
        },
        "violationsReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/violations",
            "isSubcollection": true
        },
        "evasionsReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/evasions",
            "isSubcollection": true
        },
        "httpProtocolsReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/http-protocols",
            "isSubcollection": true
        },
        "webServicesSecurityReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/web-services-securities",
            "isSubcollection": true
        },
        "extractionsReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/extractions",
            "isSubcollection": true
        },
        "plainTextProfileReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/plain-text-profiles",
            "isSubcollection": true
        },
        "websocketUrlReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/websocket-urls",
            "isSubcollection": true
        },
        "sectionReference": {
            "link": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40/sections",
            "isSubcollection": true
        },
        "type": "security",
        "hasParent": false,
        "partition": "Common",
        "name": "Policy_3",
        "description": "",
        "id": "ae0dedd4-56dd-32c3-9910-a29937d7db40",
        "generation": 1,
        "lastUpdateMicros": 1479641852337670,
        "kind": "cm:asm:working-config:policies:policystate",
        "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/ae0dedd4-56dd-32c3-9910-a29937d7db40"
    }

API reference used to support this workflow:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Api reference - virtual server
management <../html-reference/virtual-server-management.html>`__ `Api
reference - asm policy
management <../html-reference/asm-policies.html>`__
