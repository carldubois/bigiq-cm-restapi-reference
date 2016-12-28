Create Simple Application
-------------------------

Overview
~~~~~~~~

Using the BIG-IQ REST API, you can create a simple application and then
deploy such aplication to BIG-IP devices. A typical simple application
includes the following four LTM objects: virtual-server, pool, pool
member, node. Therefore in order to create a simple application, all of
those four LTM objects are required.

Virtual-server is an entry point to a simple application. A
virtual-server references a pool. A pool includes a list of pool member
objects. A pool member is dependent on a node object.

Description
~~~~~~~~~~~

In general, you create a simple application following the below steps: -
step 1: create a node - step 2: create a pool - step 3: add a pool
member to a pool - step 4: create a virtual server - step 5: attach the
pool to virtual server

Prerequisites
~~~~~~~~~~~~~

You should be sure the following prerequisites have been met.

-  All BIG-IP devices are operational and have the services provisioned
   that will be managed by the BIG-IQ Centralized Management system.
-  The BIG-IQ Centralized Management system is operational, has
   completed the setup wizard, and completed any other needed
   configuration.
-  Trust has been established between the BIG-IP device and the BIG-IQ
   Centralized Management system and the current configuration of the
   BIG-IP device has been discovered on the BIG-IQ Centralized
   Management system.
-  When performing the tasks in this example, review the listed IP
   addresses and change them as appropriate for your environment. For
   example, if you are not running the script directly on the BIG-IQ
   system, you should change localhost to be the IP address of the
   BIG-IQ Centralized Management system.

Examples creating simple application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Below are a few examples showing how a simple application can be
created.

Create a node:
^^^^^^^^^^^^^^^^^

::

    POST https://ip/mgmt/cm/adc-core/working-config/ltm/node

    Request body:
    {
        "partition": "Common",
        "name": "myNode",
        "address": "20.20.20.20",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/4fcf3469-f9ca-4a51-80d0-3336f779f949"
        }
    }

When the POST command is completed successfully, it will create a node
in working config and responds with the selfLink of the object. Here is
the POST response example,

::

    {
        "address": "20.20.20.20",
        "connectionLimit": 0,
        "isEphemeral": false,
        "rateLimit": "disabled",
        "fqdn": {
            "addressFamily": "ipv4",
            "isAutoPopulate": false,
            "downInterval": 5,
            "interval": "3600"
        },
        "partition": "Common",
        "deviceReference": {
            "id": "4fcf3469-f9ca-4a51-80d0-3336f779f949",
            "name": "bigip12-swu.f5.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "4fcf3469-f9ca-4a51-80d0-3336f779f949",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/4fcf3469-f9ca-4a51-80d0-3336f779f949"
        },
        "name": "myNode",
        "id": "17345a11-9d4d-3545-8d75-200e1fb50d10",
        "generation": 1,
        "lastUpdateMicros": 1481060607706179,
        "kind": "cm:adc-core:working-config:ltm:node:adcnodestate",
        "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/bcad3364-7481-3c1c-b4cf-093486816a48"
    }

Take a note on the self Link. Doing a GET on the selfLink will get the
object created in working config. It looks like,

::

    GET https://ip/mgmt/cm/adc-core/working-config/ltm/node/bcad3364-7481-3c1c-b4cf-093486816a48
    {
        "address": "20.20.20.20",
        "connectionLimit": 0,
        "isEphemeral": false,
        "rateLimit": "disabled",
        "fqdn": {
            "addressFamily": "ipv4",
            "isAutoPopulate": false,
            "downInterval": 5,
            "interval": "3600"
        },
        "partition": "Common",
        "deviceReference": {
            "id": "4fcf3469-f9ca-4a51-80d0-3336f779f949",
            "name": "bigip12-swu.f5.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "4fcf3469-f9ca-4a51-80d0-3336f779f949",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/4fcf3469-f9ca-4a51-80d0-3336f779f949"
        },
        "name": "myNode",
        "id": "bcad3364-7481-3c1c-b4cf-093486816a48",
        "generation": 1,
        "lastUpdateMicros": 1481060607706179,
        "kind": "cm:adc-core:working-config:ltm:node:adcnodestate",
        "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/bcad3364-7481-3c1c-b4cf-093486816a48"
    }

Create a pool
^^^^^^^^^^^^^^^^

::

    POST https://ip/mgmt/cm/adc-core/working-config/ltm/pool

    Request Body:
    {
        "partition": "Common",
        "name": "myPool",
        "loadBalancingMode": "round-robin",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/4fcf3469-f9ca-4a51-80d0-3336f779f949"
        }
    }

After a successful creation, a new pool is created and it looks like,

::


    Results:
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
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1/members",
            "isSubcollection": true
        },
        "partition": "Common",
        "deviceReference": {
            "id": "4fcf3469-f9ca-4a51-80d0-3336f779f949",
            "name": "bigip12-swu.f5.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "4fcf3469-f9ca-4a51-80d0-3336f779f949",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/4fcf3469-f9ca-4a51-80d0-3336f779f949"
        },
        "name": "myPool",
        "id": "db935eaf-69b8-34b1-8c0c-d61d665698c1",
        "generation": 1,
        "lastUpdateMicros": 1481060913788697,
        "kind": "cm:adc-core:working-config:ltm:pool:adcpoolstate",
        "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1"
    }

Create a pool member
^^^^^^^^^^^^^^^^^^^^^^^

In order to create a pool member, you must create a pool and a node
first. Here is an example showing we create a pool member using the node
created in step 1 and pool created in step 2.

::

    POST https://ip/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1/members

    Request Body:
    {
        "partition": "Common",
        "name": "myNode:80",
        "port": 80,
        "nodeReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/bcad3364-7481-3c1c-b4cf-093486816a48"
         }
    }

Upon a successful pool member creation, you can find a member under the
target pool. It looks like,

::

    GET https://ip/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1/members/43ef0c03-0630-379f-a652-0c2e4fbbdce0 

    Results:
    {
        "connectionLimit": 0,
        "port": 80,
        "priorityGroup": 0,
        "rateLimit": "disabled",
        "ratio": 1,
        "sessionConfig": "user-enabled",
        "stateConfig": "user-up",
        "nodeReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/bcad3364-7481-3c1c-b4cf-093486816a48"
        },
        "partition": "Common",
        "name": "myNode:80",
        "id": "43ef0c03-0630-379f-a652-0c2e4fbbdce0",
        "generation": 1,
        "lastUpdateMicros": 1481061178891481,
        "kind": "cm:adc-core:working-config:ltm:pool:members:adcpoolmemberstate",
        "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1/members/43ef0c03-0630-379f-a652-0c2e4fbbdce0"
    }

Create a virtual server
^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    POST https://ip/mgmt/cm/adc-core/working-config/ltm/virtual

    Request Body:
    {
          "partition": "Common",
          "name": "myVirtual",
          "destinationAddress": "10.10.10.10",
          "mask": "255.255.255.255",
          "destinationPort": 80,
          "sourceAddress": "0.0.0.0/0",
          "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/4fcf3469-f9ca-4a51-80d0-3336f779f949"
        }
    }

Upon a successful creation, a virtual server object is created and it
looks like

::

    GET  https://ip/mgmt/cm/adc-core/working-config/ltm/virtual/b4469b6f-f18f-3978-8372-4fbd562f31b8

    {
        "sourceAddress": "0.0.0.0/0",
        "sourceAddressTranslation": {
            "type": "none"
        },
        "destinationAddress": "10.10.10.10",
        "destinationPort": 80,
        "mask": "255.255.255.255",
        "state": "enabled",
        "mirror": "disabled",
        "ipProtocol": "any",
        "profilesCollectionReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual/b4469b6f-f18f-3978-8372-4fbd562f31b8/profiles",
            "isSubcollection": true
        },
        "vlansEnabled": "disabled",
        "addressStatus": "yes",
        "autoLasthop": "default",
        "connectionLimit": 0,
        "gtmScore": 0,
        "nat64": "disabled",
        "rateLimit": "disabled",
        "rateLimitMode": "object",
        "translateAddress": "enabled",
        "translatePort": "enabled",
        "sourcePort": "preserve",
        "partition": "Common",
        "deviceReference": {
            "id": "4fcf3469-f9ca-4a51-80d0-3336f779f949",
            "name": "bigip12-swu.f5.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "4fcf3469-f9ca-4a51-80d0-3336f779f949",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/4fcf3469-f9ca-4a51-80d0-3336f779f949"
        },
        "name": "myVirtual",
        "id": "b4469b6f-f18f-3978-8372-4fbd562f31b8",
        "generation": 1,
        "lastUpdateMicros": 1481062132296433,
        "kind": "cm:adc-core:working-config:ltm:virtual:adcvirtualstate",
        "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual/b4469b6f-f18f-3978-8372-4fbd562f31b8"
    }

If you want to create a virtual server with pool attached. You need to
include property "poolReference" into the POST request body. For
example,

::

    POST https://ip/mgmt/cm/adc-core/working-config/ltm/virtual

    Request Body:
    {
          "partition": "Common",
          "name": "myVirtual",
          "destinationAddress": "10.10.10.10",
          "mask": "255.255.255.255",
          "destinationPort": 80,
          "sourceAddress": "0.0.0.0/0",
          "poolReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1"
          },
          "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/4fcf3469-f9ca-4a51-80d0-3336f779f949"
           }
    }

Attach a pool to virtual server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Technically speaking, step 4 and step 5 can be combined into one step.
Since attach and detach a pool is a significant step, we call it out as
a separate step. If you like to combine step 5 with step 4, you just
need to add the property "poolReference" into the POST request body.

::

    PATCH https://ip/mgmt/cm/adc-core/working-config/ltm/virtual/b4469b6f-f18f-3978-8372-4fbd562f31b8

    Request Body:
    {
        "poolReference": {
            "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1"
        }
    }
        

API references:
~~~~~~~~~~~~~~~
:doc:`ApiReferences/application-server-node-management`
:doc:`ApiReferences/pool-member-management`
:doc:`ApiReferences/virtual-server-management`
