List virtual servers with a web application policy associated.
--------------------------------------------------------------

Overview
~~~~~~~~

Describes how you use the REST API to list all virtual servers with a
Web Application Security policy associated with them.

Prerequisites
~~~~~~~~~~~~~

Device configuration discovered and imported to Web Application
Security. Description describes how you use the REST API to list all
virtual servers with a Web Application Security policy associated with
them. 

Perform the REST API actions: 

1. Perform a GET operation to the Web Application Security virtual server collection.

The following extended example shows each of these REST API actions.

1. Perform a GET operation to the Web Application Security virtual server collection. 
2. Perform a GET operation to the Web Application Security virtual server collection, 
   selecting only the 'name', 'attachedPolicyReferences', 'address' and 'isInactivePoliciesHolder' 
   fields, and filtering the results to include virtual servers that have a security 
   policy associated with them.


Description
~~~~~~~~~~~

A list of virtuals associated to a web application security policy.

::

    GET: https://<mgmtip>/mgmt/cm/asm/working-config/virtual-servers?$select=name,address,attachedPoliciesReferences,isInactivePoliciesHolder&$filter=attachedPoliciesReferences/link eq '*'

The following is the JSON response from the GET operation:

::

    {
        "selfLink": "https://localhost/mgmt/cm/asm/working-config/virtual-servers",
        "totalItems": 2,
        "items": [
            {
                "address": "0.0.0.0",
                "isInactivePoliciesHolder": true,
                "attachedPoliciesReferences": [
                    {
                        "link": "https://localhost/mgmt/cm/asm/working-config/policies/68981f45-00a0-35d8-947b-4741ead42012"
                    },
                    {
                        "link": "https://localhost/mgmt/cm/asm/working-config/policies/034e195d-5267-3c6c-bf1d-28a117f3fc87"
                    },
                    {
                        "link": "https://localhost/mgmt/cm/asm/working-config/policies/95d37173-5c5d-32de-b6a3-59094e0b99cd"
                    }
                ],
                "name": "inactive"
            },
            {
                "address": "1.1.1.1:80",
                "attachedPoliciesReferences": [
                    {
                        "id": "1005831c-7e40-30ed-bd0d-f8068526d7ef",
                        "name": "Policy_1",
                        "kind": "cm:asm:working-config:policies:policystate",
                        "partition": "Common",
                        "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef"
                    }
                ],
                "isInactivePoliciesHolder": false,
                "name": "Virtual_1"
            }
        ],
        "generation": 8,
        "kind": "cm:asm:working-config:virtual-servers:asmvirtualservercollectionstate",
        "lastUpdateMicros": 1479388471928975
    }

Note: There are two types of virtual servers in Web Application
Security: inactive policies holder, and regular. The inactive policies
holder can have multiple policies associated with it, and is used to
deploy policies to devices without using them to enforce rules on
traffic for that device. The regular virtual servers can only have one
policy associated with them, and are used to enforce rules on traffic.

API references
~~~~~~~~~~~~~~
:doc:`../../ApiReferences/virtual-server-management`
