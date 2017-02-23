## Create simple application

### Overview

Using the BIG-IQ REST API, you can create a simple application and then deploy that application to BIG-IP devices. A typical simple application includes the following four LTM objects: virtual server, pool, pool member, and node. To create a simple application, all four LTM objects are required. 

Virtual server is an entry point to a simple application. A virtual server references a pool. A pool includes a list of pool member objects. A pool member is dependent on a node object. 

Use the following steps to create a simple application:

- step 1: Create a node. 
- step 2: Create a pool. 
- step 3: Add a pool member to a pool. 
- step 4: Create a virtual server.
- step 5: Attach the pool to a virtual server.


### Prerequisites
Make certain that the following prerequisites have been met.

- All BIG-IP devices are operational and have the services provisioned that will be managed by the BIG-IQ Centralized Management device.
- The BIG-IQ Centralized Management device is operational, has completed the setup wizard, and completed any other needed configuration.
- Trust has been established between the BIG-IP device and the BIG-IQ Centralized Management device, and the current configuration of the BIG-IP device has been discovered on the BIG-IQ Centralized Management device.

Note: When you perform these tasks using the example code provided, review the listed IP addresses and change them as appropriate for your environment. For example, if you are not running the script directly on the BIG-IQ device, change localhost to be the IP address of the BIG-IQ Centralized Management device.

### Examples for creating a simple application
Below are a few examples showing how to create a simple application. 

#### 1. Create a node
```
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
```

When the POST command completes successfully, it creates a node in working config. The response is the selfLink of the object. Here is an example POST response:
```
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
```

Take note of the selfLink. Posting a GET to the selfLink creates the object in working config. A successful response looks like this:

```
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
```


#### 2. Create a pool
```
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
```
After a successful creation, a new pool is created. A successful response looks like this:

```
GET  https://ip/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1

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

```

#### 3. Create a pool member
To create a pool member, you must create a pool and a node first. Here is an example that shows how to create a pool member using the node created in the Create a node task and the pool created in the Create a pool task. 

```
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
```

When a pool member is successfully created, you can find a member under the target pool. A successful response looks like this:

```
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
```

#### 4. Create a virtual server

```
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
```

When a virtual server object is successfully created, the response looks like this:
```
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
```

To create a virtual server with a pool attached, include the property "poolReference" in the POST request body.
For example:
```
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

```

#### 5. Attach a pool to a virtual server
In practice, this task and the last one (Create a virtual server) can be combined into a single step. Because attaching and detaching a pool is a significant step, we document it as a separate step. If you want to combine these two tasks, you just need to add the property "poolReference" into the POST request body. 

```
PATCH https://ip/mgmt/cm/adc-core/working-config/ltm/virtual/b4469b6f-f18f-3978-8372-4fbd562f31b8

Request Body:
{
    "poolReference": {
        "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/db935eaf-69b8-34b1-8c0c-d61d665698c1"
    }
}
    
```

### API Reference

