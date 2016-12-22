Listing Web Application Security policies and searching for a specific policy by name.
--------------------------------------------------------------------------------------

Overview
~~~~~~~~

Describes how you use the REST API to list all policies and to retrieve
a link to an existing policy by a policy name.

Prerequisites
~~~~~~~~~~~~~

None. ### Description Describes how you use the REST API to list all
policies and to retrieve a link to an existing policy by a policy name.
Perform the REST API actions in the following order: 1. Perform a GET
operation to return all policies. 2. Perform a GET operation to return a
specific policy using a filter.

The following extended example shows each of these REST API actions. ###
Example #### 1. Perform a GET operation to return all policies. Perform
a GET operation on the policies collection, limiting the result to show
specific fields that are defining those resources, together with a link
to retrieve all the policy properties (selfLink). In this example two
policies are retrieved named name Policy\_1 and Policy\_2. Both exist in
the Common partition, as can be seen in the fullPath field value in the
example).

::

    GET: https://<mgmtip>/mgmt/cm/asm/working-config/policies?$select=name,fullPath,selfLink

The following is the JSON response from the GET operation:

::

    {
        "items": [
            {
                "fullPath": "/Common/Policy_1",
                "name": "Policy_1",
                "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef"
            },
            {
                "fullPath": "/Common/Policy_2",
                "name": "Policy_2",
                "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/240b8504-53df-322f-9faa-008b5f0bc988"
            }
        ],
        "generation": 9,
        "kind": "cm:asm:working-config:policies:policycollectionstate",
        "lastUpdateMicros": 1478688837870194,
        "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies"
    }

2. Perform a GET operation to return a specific policy using a filter.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a GET operation on the policies collection, filtering the
results by a name and limiting the result to show specific fields that
are defining the resource, together with a link to retrieve all the
policy properties (selfLink). In this example the name being searched
for is 'Policy\_1'.

::

    GET: https://<mgmtip>/mgmt/cm/asm/working-config/policies?$filter=name eq 'Policy_1'&$select=name,fullPath,selfLink

The following is the JSON response from the GET operation:

::

    {
        "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies",
        "totalItems": 1,
        "items": [
            {
                "fullPath": "/Common/Policy_1",
                "name": "Policy_1",
                "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef"
            }
        ],
        "generation": 9,
        "kind": "cm:asm:working-config:policies:policycollectionstate",
        "lastUpdateMicros": 1478688837870194
    }

API reference used to support this workflow:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Api reference - asm policies <../html-reference/asm-policies.html>`__
