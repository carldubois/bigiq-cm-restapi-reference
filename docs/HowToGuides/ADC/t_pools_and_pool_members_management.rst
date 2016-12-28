Pool and Pool Members Management Overview
-----------------------------------------

BIG-IQ allows users to progammatically enabled/disable/force offline
pools and pool members through the use of REST API calls.

Overview
~~~~~~~~
Pool and pool memeber management.


Prerequisites
~~~~~~~~~~~~~

-  The BIG-IQ Centralized Management system is operational by completing
   the initial setup wizard.
-  Discovery and establishing trust with one BIG-IP with LTM Services
   enabled.
   
Description
~~~~~~~~~~~

This workflow will allow the user to manage pools and pool members.

Pools
^^^^^

A user may view and filter the Pools collection if they have the proper
RBAC permissions to perform GETs on
'/mgmt/cm/adc-core/working-config/ltm/pool'. Permissions can be setup so
users may only see Pool and Pool Member objects if they have been
granted permission. Permission could look like:

::

    GET /mgmt/cm/adc-core/working-config/ltm/pool/{id1}
    GET /mgmt/cm/adc-core/working-config/ltm/pool/{id1}/members
    GET /mgmt/cm/adc-core/working-config/ltm/pool/{id2}

Viewing active Pools on BIG-IQ.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

GET ``/mgmt/cm/adc-core/working-config/ltm/pool``

Response: 200

.. code:: json

    {
      "items": [
        {
          "allowNat": true,
          "allowSnat": true,
          "ignorePersistedWeight": false,
          "ipTosToClientControl": "pass-through",
          "ipTosToServerControl": "pass-through",
          "linkQosToClient": 65535,
          "linkQosToServer": 65535,
          "loadBalancingMode": "round-robin",
          "minActiveMembers": 0,
          "queueDepthLimit": 0,
          "enableQueueOnConnectionLimit": false,
          "queueTimeLimit": 0,
          "reselectTries": 0,
          "serviceDownAction": "none",
          "slowRampTime": 10,
          "membersCollectionReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/b045388c-a454-3b53-a190-940d665d0a1a/members",
            "isSubcollection": true
          },
          "partition": "Common",
          "deviceReference": {
            "id": "eb0f77b6-ee63-449c-8e90-ce5498926a1c",
            "name": "ip65.f5.pd.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "eb0f77b6-ee63-449c-8e90-ce5498926a1c",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/eb0f77b6-ee63-449c-8e90-ce5498926a1c"
          },
          "name": "pool-east",
          "description": "LAB",
          "id": "b045388c-a454-3b53-a190-940d665d0a1a",
          "generation": 1,
          "lastUpdateMicros": 1480628497415304,
          "kind": "cm:adc-core:working-config:ltm:pool:adcpoolstate",
          "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/b045388c-a454-3b53-a190-940d665d0a1a"
        },
        {
          "allowNat": true,
          "allowSnat": true,
          "ignorePersistedWeight": false,
          "ipTosToClientControl": "pass-through",
          "ipTosToServerControl": "pass-through",
          "linkQosToClient": 65535,
          "linkQosToServer": 65535,
          "loadBalancingMode": "round-robin",
          "minActiveMembers": 0,
          "queueDepthLimit": 0,
          "enableQueueOnConnectionLimit": false,
          "queueTimeLimit": 0,
          "reselectTries": 0,
          "serviceDownAction": "none",
          "slowRampTime": 10,
          "membersCollectionReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/dcf33ae3-ac2e-3984-95cf-6afd341e90e7/members",
            "isSubcollection": true
          },
          "partition": "Common",
          "deviceReference": {
            "id": "00b1ece7-c700-47ab-8ce0-4bcea4b3b9e9",
            "name": "ip223.f5.pd.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "00b1ece7-c700-47ab-8ce0-4bcea4b3b9e9",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/00b1ece7-c700-47ab-8ce0-4bcea4b3b9e9"
          },
          "name": "pool-west",
          "description": "RESERVE",
          "id": "dcf33ae3-ac2e-3984-95cf-6afd341e90e7",
          "generation": 1,
          "lastUpdateMicros": 1480628465441408,
          "kind": "cm:adc-core:working-config:ltm:pool:adcpoolstate",
          "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/dcf33ae3-ac2e-3984-95cf-6afd341e90e7"
        }
      ],
      "generation": 7,
      "kind": "cm:adc-core:working-config:ltm:pool:adcpoolcollectionstate",
      "lastUpdateMicros": 1480628497456842,
      "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool"
    }

Searching for Pools By Fields
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Users are able to search the pool collection for a value in a field
using exact or wildcard matching by appending "?$filter=PROPERTYNAME eq
'searchValue'".

Searching for any Pool objects that contain "LAB" in the description
would look like

GET
``/mgmt/cm/adc-core/working-config/ltm/pool?$filter=description eq '*LAB*'``

Response: 200

.. code:: json

    {
      "totalItems": 1,
      "items": [
        {
          "ignorePersistedWeight": false,
          "membersCollectionReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/b045388c-a454-3b53-a190-940d665d0a1a/members",
            "isSubcollection": true
          },
          "linkQosToServer": 65535,
          "slowRampTime": 10,
          "reselectTries": 0,
          "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/b045388c-a454-3b53-a190-940d665d0a1a",
          "ipTosToServerControl": "pass-through",
          "kind": "cm:adc-core:working-config:ltm:pool:adcpoolstate",
          "deviceReference": {
            "id": "eb0f77b6-ee63-449c-8e90-ce5498926a1c",
            "name": "ip65.f5.pd.com",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/eb0f77b6-ee63-449c-8e90-ce5498926a1c",
            "machineId": "eb0f77b6-ee63-449c-8e90-ce5498926a1c",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate"
          },
          "minActiveMembers": 0,
          "id": "b045388c-a454-3b53-a190-940d665d0a1a",
          "loadBalancingMode": "round-robin",
          "partition": "Common",
          "lastUpdateMicros": 1480628497415304,
          "allowSnat": true,
          "enableQueueOnConnectionLimit": false,
          "ipTosToClientControl": "pass-through",
          "description": "LAB",
          "name": "pool-east",
          "serviceDownAction": "none",
          "queueTimeLimit": 0,
          "linkQosToClient": 65535,
          "allowNat": true,
          "generation": 1,
          "queueDepthLimit": 0
        }
      ],
      "generation": 7,
      "kind": "cm:adc-core:working-config:ltm:pool:adcpoolcollectionstate",
      "lastUpdateMicros": 1480628497456842,
      "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool"
    }

Creating A Pool Object With A Monitor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

POST ``/mgmt/cm/adc-core/working-config/ltm/pool``

BODY

.. code:: json

    {
       "allowNat":true,
       "allowSnat":true,
       "description":"",
       "ignorePersistedWeight":false,
       "ipTosToClient":null,
       "ipTosToServer":null,
       "linkQosToClient":65535,
       "linkQosToServer":65535,
       "loadBalancingMode":"round-robin",
       "monitorReferences":[],
       "minActiveMembers":0,
       "minUpMembers":null,
       "queueDepthLimit":0,
       "enableQueueOnConnectionLimit":false,
       "queueTimeLimit":0,
       "serviceDownAction":"none",
       "slowRampTime":10,
       "reselectTries":0,
       "membersReference":{
          "link":""
       },
       "profiles":[],
       "requestQueueTimeLimit":0,
       "deviceReference":{
          "link":"https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/465b8fe0-4441-4ece-a8b6-04fcd613ff83"
       },
       "partition":"Common",
       "kind":"cm:adc-core:working-config:ltm:pool:adcpoolstate",
       "name":"new-pool-with-http-monitor",
       "monitorHttpReferences":[
          {
             "name":"http",
             "partition":"Common",
             "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/monitor/http/ad348aed-0309-36d5-b5cd-c5b9e00cbb26"
          }
       ],
       "ipTosToClientControl":"pass-through",
       "ipTosToServerControl":"pass-through"
    }

Response: 200

.. code:: json

    {
       "allowNat":true,
       "allowSnat":true,
       "ignorePersistedWeight":false,
       "ipTosToClientControl":"pass-through",
       "ipTosToServerControl":"pass-through",
       "linkQosToClient":65535,
       "linkQosToServer":65535,
       "loadBalancingMode":"round-robin",
       "minActiveMembers":0,
       "queueDepthLimit":0,
       "enableQueueOnConnectionLimit":false,
       "queueTimeLimit":0,
       "reselectTries":0,
       "serviceDownAction":"none",
       "slowRampTime":10,
       "membersCollectionReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/56e0bcd8-b3e7-358b-bf0f-965fc798e507/members",
          "isSubcollection":true
       },
       "monitorHttpReferences":[
          {
             "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/monitor/http/ad348aed-0309-36d5-b5cd-c5b9e00cbb26"
          }
       ],
       "partition":"Common",
       "deviceReference":{
          "id":"465b8fe0-4441-4ece-a8b6-04fcd613ff83",
          "name":"ip66.f5.pd.com",
          "kind":"shared:resolver:device-groups:restdeviceresolverdevicestate",
          "machineId":"465b8fe0-4441-4ece-a8b6-04fcd613ff83",
          "link":"https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/465b8fe0-4441-4ece-a8b6-04fcd613ff83"
       },
       "name":"new-pool-with-http-monitor",
       "id":"56e0bcd8-b3e7-358b-bf0f-965fc798e507",
       "generation":1,
       "lastUpdateMicros":1480549590312880,
       "kind":"cm:adc-core:working-config:ltm:pool:adcpoolstate",
       "selfLink":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/56e0bcd8-b3e7-358b-bf0f-965fc798e507"
    }

Deploying A Pool Object To A Device
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This requires a deviceReference and the Rest Reference for the Pool
object to be deployed. Users can configure the task verification by
toggling the boolean attribute "skipVerifyConfig". Users may also pause
the deployment after evaluation by setting the property
"skipDistribution" to "true".

POST ``/mgmt/cm/adc-core/tasks/deploy-configuration``

BODY

.. code:: json

    {
       "skipVerifyConfig":false,
       "skipDistribution":false,
       "snapshotReference":null,
       "objectsToDeployReferences":[
          {
             "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/e80bf7e0-41ac-3056-a114-4a1b2ddc0b6c"
          }
       ],
       "name":"add",
       "deploySpecifiedObjectsOnly":false,
       "deviceReferences":[
          {
             "link":"https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/00b1ece7-c700-47ab-8ce0-4bcea4b3b9e9"
          }
       ]
    }

Response: 202

.. code:: json

    {
       "skipDistribution":false,
       "deviceReferences":[
          {
             "link":"https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/00b1ece7-c700-47ab-8ce0-4bcea4b3b9e9"
          }
       ],
       "skipVerifyConfig":false,
       "objectsToDeployReferences":[
          {
             "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/e80bf7e0-41ac-3056-a114-4a1b2ddc0b6c"
          }
       ],
       "deploySpecifiedObjectsOnly":false,
       "id":"2120a0bc-b311-407e-844f-f89e151f0bb5",
       "status":"STARTED",
       "name":"add",
       "userReference":{
          "link":"https://localhost/mgmt/shared/authz/users/admin"
       },
       "identityReferences":[
          {
             "link":"https://localhost/mgmt/shared/authz/users/admin"
          }
       ],
       "ownerMachineId":"3b786166-8069-45ae-b633-60e7416ef7a0",
       "taskWorkerGeneration":1,
       "generation":1,
       "lastUpdateMicros":1480703520843810,
       "kind":"cm:adc-core:tasks:deploy-configuration:deployconfigtaskstate",
       "selfLink":"https://localhost/mgmt/cm/adc-core/tasks/deploy-configuration/2120a0bc-b311-407e-844f-f89e151f0bb5"
    }

The 202 response contains details about the self service task along with
the "status" of "STARTED". The selfLink should be polled with GETs
checking the "status" property to report "FINISHED" or "FAILED". If the
task was configured to have "skipVerifyConfig" to "false", the self
service task will eventually be populated with a
"verifyConfigReference". Performing a GET on the
"verifyConfigReference.link" will provide any warnings and errors found
during verification. Only critical errors will prevent users from
deploying the objects to the BIG-IP. If the task was configured to have
"skipDistribution" set to "true", the task will pause after an
evaluation has been created. This allows users to review their changes
before deployment. Users can resume the deployment by PATCHing the task
with the following body:

.. code:: json

    {"skipDistribution": false, "status": "STARTED"}

Edit A Pool Object
^^^^^^^^^^^^^^^^^^

Attaching a new health monitor to the Pool.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This requires a proper monitor name and RestReference.

PATCH ``/mgmt/cm/adc-core/working-config/ltm/pool/{id}``

BODY

.. code:: json

    {
       "monitorHttpReferences":[
          {
             "name":"http",
             "partition":"Common",
             "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/monitor/http/ad348aed-0309-36d5-b5cd-c5b9e00cbb26"
          }
       ]
    }

Response: 200

.. code:: json

    {
      "allowNat": true,
      "allowSnat": true,
      "ignorePersistedWeight": false,
      "ipTosToClientControl": "pass-through",
      "ipTosToServerControl": "pass-through",
      "linkQosToClient": 65535,
      "linkQosToServer": 65535,
      "loadBalancingMode": "round-robin",
      "minActiveMembers": 0,
      "queueDepthLimit": 0,
      "enableQueueOnConnectionLimit": false,
      "queueTimeLimit": 0,
      "reselectTries": 0,
      "serviceDownAction": "none",
      "slowRampTime": 10,
      "membersCollectionReference": {
        "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/b045388c-a454-3b53-a190-940d665d0a1a/members",
        "isSubcollection": true
      },
      "monitorHttpReferences": [
        {
          "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/monitor/http/ad348aed-0309-36d5-b5cd-c5b9e00cbb26"
        }
      ],
      "partition": "Common",
      "deviceReference": {
        "id": "eb0f77b6-ee63-449c-8e90-ce5498926a1c",
        "name": "ip65.f5.pd.com",
        "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
        "machineId": "eb0f77b6-ee63-449c-8e90-ce5498926a1c",
        "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/eb0f77b6-ee63-449c-8e90-ce5498926a1c"
      },
      "name": "pool-east",
      "description": "LAB",
      "id": "b045388c-a454-3b53-a190-940d665d0a1a",
      "generation": 2,
      "lastUpdateMicros": 1480630096304382,
      "kind": "cm:adc-core:working-config:ltm:pool:adcpoolstate",
      "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/b045388c-a454-3b53-a190-940d665d0a1a"
    }

Attaching Pool Objects To Role Permissions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Role permissions can be updated to give user roles the abilty to
view/edit/delete Pool objects and Pool Members.

PUT ``/mgmt/shared/authz/users/{user role name}``

BODY

.. code:: json

    {
    ...
        resources: [
            ...
            {resourceMask: "/mgmt/cm/adc-core/working-config/ltm/pool/{id}", restMethod: "GET"},
            {resourceMask: "/mgmt/cm/adc-core/working-config/ltm/pool/{id}/members", restMethod: "GET"},
            {resourceMask: "/mgmt/cm/adc-core/working-config/ltm/pool/{id}/members/*", restMethod: "GET"},
            {resourceMask: "/mgmt/cm/adc-core/working-config/ltm/pool/{id}/members/*/*", restMethod: "POST"},
            ...
        ]
    ...
    }

Note: Provisioning a user to GET
"/mgmt/cm/adc-core/working-config/ltm/pool/{id}" does not automatically
grant permissions to subcollections.

Removing A Pool Object And Deploying Changes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

DELETE ``/mgmt/cm/adc-core/working-config/ltm/pool/{id}``

The pool object will no longer exist in the working config of the
BIG-IQ. To deploy these changes to a device, the device reference is
needed.

POST ``/mgmt/cm/adc-core/tasks/deploy-configuration``

BODY

.. code:: json

    {  
       "skipVerifyConfig":false,
       "skipDistribution":false,
       "snapshotReference":null,
       "objectsToDeployReferences":[  

       ],
       "name":"removedPool",
       "deviceReferences":[  
          {  
             "link":"https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/00b1ece7-c700-47ab-8ce0-4bcea4b3b9e9"
          }
       ]
    }

Response: 202

.. code:: json

    {  
       "skipDistribution":false,
       "deviceReferences":[
          {
             "link":"https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/00b1ece7-c700-47ab-8ce0-4bcea4b3b9e9"
          }
       ],
       "skipVerifyConfig":false,
       "objectsToDeployReferences":[
       ],
       "id":"c1a3501f-293f-45e4-b3a0-29ff6c59203b",
       "status":"STARTED",
       "name":"removedPool",
       "userReference":{
          "link":"https://localhost/mgmt/shared/authz/users/admin"
       },
       "identityReferences":[
          {
             "link":"https://localhost/mgmt/shared/authz/users/admin"
          }
       ],
       "ownerMachineId":"3b786166-8069-45ae-b633-60e7416ef7a0",
       "taskWorkerGeneration":1,
       "generation":1,
       "lastUpdateMicros":1480705617532917,
       "kind":"cm:adc-core:tasks:deploy-configuration:deployconfigtaskstate",
       "selfLink":"https://localhost/mgmt/cm/adc-core/tasks/deploy-configuration/c1a3501f-293f-45e4-b3a0-29ff6c59203b"
    }

The 202 response contains details about the self service task along with
the "status" of "STARTED". The selfLink should be polled with GETs
checking the "status" property to report "FINISHED" or "FAILED".

API references
~~~~~~~~~~~~~~~

`Api reference - pool member
management <../html-reference/pool-member-management.html>`__ `Api
reference - deploy
configuration <../html-reference/deploy-configuration.html>`__


Pool Member enable/disable/force offline.
-----------------------------------------

Overview
~~~~~~~~
Pool and pool memeber management.

Prerequisites
~~~~~~~~~~~~~

-  A Pool object must exist.
-  A Node object must exist.

Description
~~~~~~~~~~~

This workflow will allow the user to manage pools and pool members.

Viewing Pool Members
^^^^^^^^^^^^^^^^^^^^

GET ``/mgmt/cm/adc-core/working-config/ltm/pool/{id}/members``

Response: 200

.. code:: json

    {
      "items": [
        {
          "connectionLimit": 0,
          "port": 80,
          "priorityGroup": 0,
          "rateLimit": "disabled",
          "ratio": 1,
          "sessionConfig": "user-enabled",
          "stateConfig": "user-up",
          "nodeReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/36d49760-3d0e-3368-a679-52e79ff44227"
          },
          "partition": "Common",
          "name": "testNode:80",
          "description": "a test member",
          "id": "e93af93a-c397-39ba-853f-c2808b818ef3",
          "generation": 1,
          "lastUpdateMicros": 1480551570546280,
          "kind": "cm:adc-core:working-config:ltm:pool:members:adcpoolmemberstate",
          "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/56e0bcd8-b3e7-358b-bf0f-965fc798e507/members/e93af93a-c397-39ba-853f-c2808b818ef3"
        }
      ],
      "generation": 2,
      "kind": "cm:adc-core:working-config:ltm:pool:members:adcpoolmembercollectionstate",
      "lastUpdateMicros": 1480551570582031,
      "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/56e0bcd8-b3e7-358b-bf0f-965fc798e507/members"
    }

Creating Pool Member
^^^^^^^^^^^^^^^^^^^^

POST ``/mgmt/cm/adc-core/working-config/ltm/pool/{id}/members``

BODY

.. code:: json

    {
       "nodeReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/node/36d49760-3d0e-3368-a679-52e79ff44227"
       },
       "ratio":1,
       "priorityGroup":0,
       "connectionLimit":0,
       "rateLimit":"disabled",
       "dynamicRatio":1,
       "sessionConfig":"user-enabled",
       "stateConfig":"user-up",
       "name":"testNode:80",
       "description":"a test member",
       "kind":"cm:adc-core:working-config:ltm:pool:members:adcpoolmemberstate",
       "partition":"Common",
       "port":"80"
    }

Response: 200

.. code:: json

    {
       "connectionLimit":0,
       "port":80,
       "priorityGroup":0,
       "rateLimit":"disabled",
       "ratio":1,
       "sessionConfig":"user-enabled",
       "stateConfig":"user-up",
       "nodeReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/node/36d49760-3d0e-3368-a679-52e79ff44227"
       },
       "partition":"Common",
       "name":"testNode:80",
       "description":"a test member",
       "id":"e93af93a-c397-39ba-853f-c2808b818ef3",
       "generation":1,
       "lastUpdateMicros":1480551570546280,
       "kind":"cm:adc-core:working-config:ltm:pool:members:adcpoolmemberstate",
       "selfLink":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/56e0bcd8-b3e7-358b-bf0f-965fc798e507/members/e93af93a-c397-39ba-853f-c2808b818ef3"
    }

Removing Pool Member
^^^^^^^^^^^^^^^^^^^^

DELETE
``/mgmt/cm/adc-core/working-config/ltm/pool/{pool-id}/members/{memmber-id}``

Enabling A Pool Member Using Self Service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

POST ``/mgmt/cm/adc-core/tasks/self-service``

BODY

.. code:: json

    {
       "name":"Self-Service_someNode:80",
       "resourceReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/dcf33ae3-ac2e-3984-95cf-6afd341e90e7/members/a8aedfee-722c-39e1-a464-e8a2d352d8f2"
       },
       "operation":"enable"
    }

Response: 202

.. code:: json

    {
       "resourceReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/dcf33ae3-ac2e-3984-95cf-6afd341e90e7/members/a8aedfee-722c-39e1-a464-e8a2d352d8f2"
       },
       "operation":"enable",
       "id":"865ec76a-02a2-47f1-a007-f07010b18177",
       "status":"STARTED",
       "name":"Self-Service_someNode:80",
       "userReference":{
          "link":"https://localhost/mgmt/shared/authz/users/admin"
       },
       "identityReferences":[
          {
             "link":"https://localhost/mgmt/shared/authz/users/admin"
          }
       ],
       "ownerMachineId":"3b786166-8069-45ae-b633-60e7416ef7a0",
       "taskWorkerGeneration":1,
       "generation":1,
       "lastUpdateMicros":1480632847604821,
       "kind":"cm:adc-core:tasks:self-service:selfservicetaskitemstate",
       "selfLink":"https://localhost/mgmt/cm/adc-core/tasks/self-service/865ec76a-02a2-47f1-a007-f07010b18177"
    }

The 202 response contains details about the self service task along with
the "status" of "STARTED". The selfLink should be polled with GETs
checking the "status" property to report "FINISHED" or "FAILED".

Disabling A Pool Member Using Self Service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

POST ``/mgmt/cm/adc-core/tasks/self-service``

BODY

.. code:: json

    {
       "name":"Self-Service_someNode:80",
       "resourceReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/dcf33ae3-ac2e-3984-95cf-6afd341e90e7/members/a8aedfee-722c-39e1-a464-e8a2d352d8f2"
       },
       "operation":"disable"
    }

Response: 202

.. code:: json

    {
       "resourceReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/dcf33ae3-ac2e-3984-95cf-6afd341e90e7/members/a8aedfee-722c-39e1-a464-e8a2d352d8f2"
       },
       "operation":"disable",
       "id":"40f8385a-9f76-4377-9b9e-dccfd1c0d089",
       "status":"STARTED",
       "name":"Self-Service_someNode:80",
       "userReference":{
          "link":"https://localhost/mgmt/shared/authz/users/admin"
       },
       "identityReferences":[
          {
             "link":"https://localhost/mgmt/shared/authz/users/admin"
          }
       ],
       "ownerMachineId":"3b786166-8069-45ae-b633-60e7416ef7a0",
       "taskWorkerGeneration":1,
       "generation":1,
       "lastUpdateMicros":1480632998507447,
       "kind":"cm:adc-core:tasks:self-service:selfservicetaskitemstate",
       "selfLink":"https://localhost/mgmt/cm/adc-core/tasks/self-service/40f8385a-9f76-4377-9b9e-dccfd1c0d089"
    }

The 202 response contains details about the self service task along with
the "status" of "STARTED". The selfLink should be polled with GETs
checking the "status" property to report "FINISHED" or "FAILED".

Force Offline A Pool Member Using Self Service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

POST ``/mgmt/cm/adc-core/tasks/self-service``

BODY

.. code:: json

    {
       "name":"Self-Service_someNode:80",
       "resourceReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/dcf33ae3-ac2e-3984-95cf-6afd341e90e7/members/a8aedfee-722c-39e1-a464-e8a2d352d8f2"
       },
       "operation":"force-offline"
    }

Response: 202

.. code:: json

    {
       "resourceReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/dcf33ae3-ac2e-3984-95cf-6afd341e90e7/members/a8aedfee-722c-39e1-a464-e8a2d352d8f2"
       },
       "operation":"force-offline",
       "id":"bfccaa9d-7add-4ed6-82a3-5e5026ee98a6",
       "status":"STARTED",
       "name":"Self-Service_someNode:80",
       "userReference":{
          "link":"https://localhost/mgmt/shared/authz/users/admin"
       },
       "identityReferences":[
          {
             "link":"https://localhost/mgmt/shared/authz/users/admin"
          }
       ],
       "ownerMachineId":"3b786166-8069-45ae-b633-60e7416ef7a0",
       "taskWorkerGeneration":1,
       "generation":1,
       "lastUpdateMicros":1480633122692313,
       "kind":"cm:adc-core:tasks:self-service:selfservicetaskitemstate",
       "selfLink":"https://localhost/mgmt/cm/adc-core/tasks/self-service/bfccaa9d-7add-4ed6-82a3-5e5026ee98a6"
    }

The 202 response contains details about the self service task along with
the "status" of "STARTED". The selfLink should be polled with GETs
checking the "status" property to report "FINISHED" or "FAILED".

API references
~~~~~~~~~~~~~~~

`Api reference - pool member
management <../html-reference/pool-member-management.html>`__ `Api
reference - deploy
configuration <../html-reference/deploy-configuration.html>`__
