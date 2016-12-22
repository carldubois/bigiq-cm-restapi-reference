#Enable, Disable, and Force Offline Pool Members
------------------------------------------------

This topic describes how to control the state of pool members, to enable
pool members to take traffic for the application, disable pool members
to drain down existing traffic, or force offline pool members to stop
serving traffic.

##Prerequisites
---------------

The following prerequisites are required to complete this task.

-  An account with administrator privileges is used for accessing APIs.
-  The BIG-IP devices are already discovered on BIG-IQ with at least
   Local Traffic (LTM) configuration imported, and desired pool members
   exist at last import time.

##1. Find Pool Members
----------------------

If already know the ``selfLink`` of pool members to operate on and
desired state to change to, please skip Step 1 and proceed directly to
Step 3. Otherwise send a GET request to pool collection to read pools
that are in the BIG-IQ repository.

::

    GET https://ip_address/mgmt/cm/adc-core/working-config/ltm/pool

The JSON in the body of the response can look similar to the following.

::

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
          "loadBalancingMode": "least-sessions",
          "minActiveMembers": 0,
          "queueDepthLimit": 0,
          "enableQueueOnConnectionLimit": false,
          "queueTimeLimit": 0,
          "reselectTries": 0,
          "serviceDownAction": "none",
          "slowRampTime": 10,
          "membersCollectionReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/df237cb1-e272-3de9-8de3-a1afae6d6503/members",
            "isSubcollection": true
          },
          "partition": "Common",
          "deviceReference": {
            "id": "174ad39d-47b8-4b33-80fa-809532cd8ad9",
            "name": "bigip224.pdsea.f5net.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "174ad39d-47b8-4b33-80fa-809532cd8ad9",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/174ad39d-47b8-4b33-80fa-809532cd8ad9"
          },
          "name": "pool",
          "id": "df237cb1-e272-3de9-8de3-a1afae6d6503",
          "generation": 1,
          "lastUpdateMicros": 1474411642285774,
          "kind": "cm:adc-core:working-config:ltm:pool:adcpoolstate",
          "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/df237cb1-e272-3de9-8de3-a1afae6d6503"
        },
        {
          "allowNat": true,
          "allowSnat": true,
          "ignorePersistedWeight": false,
          "ipTosToClientControl": "pass-through",
          "ipTosToServerControl": "pass-through",
          "linkQosToClient": 65535,
          "linkQosToServer": 65535,
          "loadBalancingMode": "ratio-least-connections-node",
          "minActiveMembers": 0,
          "queueDepthLimit": 0,
          "enableQueueOnConnectionLimit": false,
          "queueTimeLimit": 0,
          "reselectTries": 0,
          "serviceDownAction": "none",
          "slowRampTime": 10,
          "membersCollectionReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/f17b91d9-6e1f-3974-aeb4-8dac762ffcaf/members",
            "isSubcollection": true
          },
          "partition": "Common",
          "deviceReference": {
            "id": "174ad39d-47b8-4b33-80fa-809532cd8ad9",
            "name": "bigip224.pdsea.f5net.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "174ad39d-47b8-4b33-80fa-809532cd8ad9",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/174ad39d-47b8-4b33-80fa-809532cd8ad9"
          },
          "name": "a-pool",
          "id": "f17b91d9-6e1f-3974-aeb4-8dac762ffcaf",
          "generation": 1,
          "lastUpdateMicros": 1474411642322329,
          "kind": "cm:adc-core:working-config:ltm:pool:adcpoolstate",
          "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/f17b91d9-6e1f-3974-aeb4-8dac762ffcaf"
        }
      ],
      "generation": 7,
      "kind": "cm:adc-core:working-config:ltm:pool:adcpoolcollectionstate",
      "lastUpdateMicros": 1474411642564892,
      "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool"
    }

Note the value of selfLink for pools where the target pool members
belong to, which will be used in the next step.

##2. Review Current State of Pool Members
-----------------------------------------

Send a GET request to the pool member sub-collections of the specific
pools.

::

    GET https://ip_address/mgmt/cm/adc-core/working-config/ltm/pool/df237cb1-e272-3de9-8de3-a1afae6d6503/members

The JSON in the body of the response can look similar to the following.
Note the value of selfLink for pool members to operate on, which will be
used in the next step.

::

    {
      "items": [
        {
          "connectionLimit": 0,
          "port": 0,
          "priorityGroup": 0,
          "rateLimit": "disabled",
          "ratio": 1,
          "sessionConfig": "user-enabled",
          "stateConfig": "user-up",
          "nodeReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/0409b7ec-686f-3dae-bde4-da72ad4947b2"
          },
          "monitorHttpReferences": [
            {
              "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/monitor/http/a9e6b8ab-2d94-3a0c-bc5d-06286f1db9fb"
            }
          ],
          "partition": "Common",
          "name": "a1-node:0",
          "id": "e6b49485-6abe-39db-831b-4c4e8afb463c",
          "generation": 1,
          "lastUpdateMicros": 1474411643854263,
          "kind": "cm:adc-core:working-config:ltm:pool:members:adcpoolmemberstate",
          "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/df237cb1-e272-3de9-8de3-a1afae6d6503/members/e6b49485-6abe-39db-831b-4c4e8afb463c"
        },
        {
          "connectionLimit": 0,
          "port": 0,
          "priorityGroup": 0,
          "rateLimit": "disabled",
          "ratio": 1,
          "sessionConfig": "user-disabled",
          "stateConfig": "user-up",
          "nodeReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/feb0d32e-e3c7-3179-b849-a0bf201bee2a"
          },
          "monitorHttpReferences": [
            {
              "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/monitor/http/a9e6b8ab-2d94-3a0c-bc5d-06286f1db9fb"
            }
          ],
          "partition": "Common",
          "name": "f5net.com:0",
          "id": "a33ca82b-2e6f-3d9d-a24e-fbed3c3f9e76",
          "generation": 1,
          "lastUpdateMicros": 1474411643760479,
          "kind": "cm:adc-core:working-config:ltm:pool:members:adcpoolmemberstate",
          "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/df237cb1-e272-3de9-8de3-a1afae6d6503/members/a33ca82b-2e6f-3d9d-a24e-fbed3c3f9e76"
        }
      ],
      "generation": 3,
      "kind": "cm:adc-core:working-config:ltm:pool:members:adcpoolmembercollectionstate",
      "lastUpdateMicros": 1474411644499775,
      "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/df237cb1-e272-3de9-8de3-a1afae6d6503/members"
    }

##3. Set New State for Pool Members
-----------------------------------

Send a POST request to set new state for each pool member. The pool
member will be set to the new state regardless of the previous state.

::

    POST https://ip_address/mgmt/cm/adc-core/tasks/self-service

The JSON in the body of the request can look similar to the following
example. The ``operation`` can be ``enable``, ``disable``, or
``force-offline`` for pool members.

.. code:: json

    {
       "operation":"enable",
       "resourceReference":{
          "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/f17b91d9-6e1f-3974-aeb4-8dac762ffcaf/members/c481eb1b-32f2-3b5a-80f1-2628c1c48212"
       }
    }

The JSON in the body of a successful response will look similar to the
following example.

.. code:: json

    {
      "resourceReference": {
        "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/f17b91d9-6e1f-3974-aeb4-8dac762ffcaf/members/c481eb1b-32f2-3b5a-80f1-2628c1c48212"
      },
      "operation": "enable",
      "id": "31bdbb35-1b98-4bb6-9791-624743c11c7f",
      "status": "STARTED",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "ownerMachineId": "9f21f7f4-06a1-4fcf-abe7-2b75cf78fadc",
      "taskWorkerGeneration": 1,
      "generation": 1,
      "lastUpdateMicros": 1474416152551850,
      "kind": "cm:adc-core:tasks:self-service:selfservicetaskitemstate",
      "selfLink": "https://localhost/mgmt/cm/adc-core/tasks/self-service/31bdbb35-1b98-4bb6-9791-624743c11c7f"
    }

Note the value of selfLink for pools and wait for the task to complete.
Upon completion, the task would reach FINISHED in status.

.. code:: json

    {
      "deviceReference": {
        "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/174ad39d-47b8-4b33-80fa-809532cd8ad9"
      },
      "endDateTime": "2016-09-20T17:02:32.694-0700",
      "generation": 2,
      "id": "31bdbb35-1b98-4bb6-9791-624743c11c7f",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:adc-core:tasks:self-service:selfservicetaskitemstate",
      "lastUpdateMicros": 1474416152744916,
      "operation": "enable",
      "ownerMachineId": "9f21f7f4-06a1-4fcf-abe7-2b75cf78fadc",
      "resourceReference": {
        "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/f17b91d9-6e1f-3974-aeb4-8dac762ffcaf/members/c481eb1b-32f2-3b5a-80f1-2628c1c48212"
      },
      "selfLink": "https://localhost/mgmt/cm/adc-core/tasks/self-service/31bdbb35-1b98-4bb6-9791-624743c11c7f",
      "startDateTime": "2016-09-20T17:02:32.569-0700",
      "status": "FINISHED",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

Result
------

The pool members are enabled, disabled or forced offline, and the change
is synchronized if the devices is in config sync group with either
manual or automatic sync mode.

API references that support this workflow:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Api reference - pool member
management <../html-reference/pool-member-management.html>`__ `Api
reference - adc self service
task <../html-reference/adc-self-service.html>`__
