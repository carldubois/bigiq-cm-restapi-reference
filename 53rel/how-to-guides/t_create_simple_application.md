## Create simple application

### Overview

Using the BIG-IQ REST API, you can create a simple application and then deploy that application to BIG-IP devices. A typical simple application includes the following four LTM objects: virtual server, pool, pool member, and node. To create a simple application, all four LTM objects are required.

Virtual server is an entry point to a simple application. A virtual server references a pool. A pool includes a list of pool member objects. A pool member is dependent on a node object.  Typically, one or more profiles will also need to be attached to the virtual server.

Use the following steps to create a simple application:

1. Create a node.
2. Create a pool.
3. Add a pool member to a pool.
4. Create a virtual server.
5. Attach a pool to a virtual server.
6. Attach profiles to a virtual server.

### Prerequisites
Make certain that the following prerequisites have been met.

- All BIG-IP devices are operational and have the services provisioned that will be managed by the BIG-IQ Centralized Management device.
- The BIG-IQ Centralized Management device is operational, has completed the setup wizard, and completed any other needed configuration.
- Trust has been established between the BIG-IP device and the BIG-IQ Centralized Management device, and the current configuration of the BIG-IP device has been discovered on the BIG-IQ Centralized Management device.

Note: When you perform these tasks using the example code provided, review the listed IP addresses and device/object IDs and change them as appropriate for your environment. For example, if you are not running the script directly on the BIG-IQ device, change localhost to be the IP address of the BIG-IQ Centralized Management device.

### Examples for creating a simple application
Below are a few examples showing how to create a simple application.

#### 1. Create a node
When the POST command completes successfully, it creates a node in working config. The response is the state of the created object. The response contains a `selfLink`, which is used to reference the created object.

Nodes are device-specific objects, hence the `deviceReference` is required.  All devices eligible for use with LTM objects can be found by issuing a GET to `shared/resolver/device-groups/cm-adccore-allbigipDevices/devices` (the `selfLink` for the relevant device should be used as the `deviceReference`).
```
POST https://localhost/mgmt/cm/adc-core/working-config/ltm/node
```
Request:
```
{
  "partition": "Common",
  "name": "myNode",
  "address": "20.20.20.20",
  "deviceReference": {
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/6c094b2e-af44-40d3-9ca8-7af2e0d51b0f"
  }
}
```

Response:
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
    "id": "6c094b2e-af44-40d3-9ca8-7af2e0d51b0f",
    "name": "bigip13-234.f5net.com",
    "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
    "machineId": "6c094b2e-af44-40d3-9ca8-7af2e0d51b0f",
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/6c094b2e-af44-40d3-9ca8-7af2e0d51b0f"
  },
  "name": "myNode",
  "id": "f5bd1bf0-a49c-39eb-b1b0-4469aa165804",
  "generation": 1,
  "lastUpdateMicros": 1488955362239673,
  "kind": "cm:adc-core:working-config:ltm:node:adcnodestate",
  "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/f5bd1bf0-a49c-39eb-b1b0-4469aa165804"
}
```

#### 2. Create a pool
```
POST https://localhost/mgmt/cm/adc-core/working-config/ltm/pool
```
Request:
```
{
  "partition": "Common",
  "name": "myPool",
  "loadBalancingMode": "round-robin",
  "deviceReference": {
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/6c094b2e-af44-40d3-9ca8-7af2e0d51b0f"
  }
}
```

Response:
```
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
    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/186c7d78-a6bf-395a-9505-d0d49280d0a2/members",
    "isSubcollection": true
  },
  "partition": "Common",
  "deviceReference": {
    "id": "6c094b2e-af44-40d3-9ca8-7af2e0d51b0f",
    "name": "bigip13-234.f5net.com",
    "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
    "machineId": "6c094b2e-af44-40d3-9ca8-7af2e0d51b0f",
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/6c094b2e-af44-40d3-9ca8-7af2e0d51b0f"
  },
  "name": "myPool",
  "id": "186c7d78-a6bf-395a-9505-d0d49280d0a2",
  "generation": 1,
  "lastUpdateMicros": 1488956037638261,
  "kind": "cm:adc-core:working-config:ltm:pool:adcpoolstate",
  "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/186c7d78-a6bf-395a-9505-d0d49280d0a2"
}
```

#### 3. Add a pool member to a pool
Below is an example showing how to create a pool member using the node and pool created in the previous steps.

Note, pool member names must be of the format "{nodeName}:{port}".
```
POST https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/186c7d78-a6bf-395a-9505-d0d49280d0a2/members
```
Request:
```
{
  "partition": "Common",
  "name": "myNode:80",
  "port": 80,
  "nodeReference": {
    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/f5bd1bf0-a49c-39eb-b1b0-4469aa165804"
   }
}
```

Response:
```
{
  "connectionLimit": 0,
  "port": 80,
  "priorityGroup": 0,
  "rateLimit": "disabled",
  "sessionConfig": "user-enabled",
  "stateConfig": "user-up",
  "nodeReference": {
    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/node/f5bd1bf0-a49c-39eb-b1b0-4469aa165804"
  },
  "partition": "Common",
  "name": "myNode:80",
  "id": "43ef0c03-0630-379f-a652-0c2e4fbbdce0",
  "generation": 1,
  "lastUpdateMicros": 1488960207572659,
  "kind": "cm:adc-core:working-config:ltm:pool:members:adcpoolmemberstate",
  "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/186c7d78-a6bf-395a-9505-d0d49280d0a2/members/43ef0c03-0630-379f-a652-0c2e4fbbdce0"
}
```

#### 4. Create a virtual server
```
POST https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual
```
Request:
```
{
  "partition": "Common",
  "name": "myVirtual",
  "destinationAddress": "10.10.10.10",
  "mask": "255.255.255.255",
  "destinationPort": 80,
  "sourceAddress": "0.0.0.0/0",
  "deviceReference": {
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/6c094b2e-af44-40d3-9ca8-7af2e0d51b0f"
  }
}
```

Response:
```
{
  "sourceAddress": "0.0.0.0/0",
  "sourceAddressTranslation": {
    "type": "none"
  },
  "destinationAddress": "10.10.10.10",
  "destinationPort": "80",
  "mask": "255.255.255.255",
  "state": "enabled",
  "mirror": "disabled",
  "ipProtocol": "any",
  "profilesCollectionReference": {
    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual/9a269865-55c4-3a42-82db-5c099899dbc0/profiles",
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
    "id": "6c094b2e-af44-40d3-9ca8-7af2e0d51b0f",
    "name": "bigip13-234.f5net.com",
    "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
    "machineId": "6c094b2e-af44-40d3-9ca8-7af2e0d51b0f",
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/6c094b2e-af44-40d3-9ca8-7af2e0d51b0f"
  },
  "name": "myVirtual",
  "id": "9a269865-55c4-3a42-82db-5c099899dbc0",
  "generation": 1,
  "lastUpdateMicros": 1488963686800110,
  "kind": "cm:adc-core:working-config:ltm:virtual:adcvirtualstate",
  "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual/9a269865-55c4-3a42-82db-5c099899dbc0"
}
```

#### 5. Attach a pool to a virtual server
The below example shows how to attach a pool to an existing virtual server.  Note, it's also possible to include the `poolReference` directly when creating the virtual server.
```
PATCH https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual/9a269865-55c4-3a42-82db-5c099899dbc0
```
Request:
```
{
  "poolReference": {
    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/186c7d78-a6bf-395a-9505-d0d49280d0a2"
  }
}
```

To detach a pool from a virtual server:
```
PATCH https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual/9a269865-55c4-3a42-82db-5c099899dbc0
```
Request:
```
{
  "poolReference": null
}
```

#### 6. Attach profiles to a virtual server
Virtual servers generally need one or more profiles to be attached.  The below shows an example of finding and attaching an Any IP profile to our example virtual server.
```
GET https://localhost/mgmt/cm/adc-core/working-config/ltm/profile/ipother/
```

Response:
```
{
  "items": [
    {
      "partition": "Common",
      "name": "ipother",
      "id": "2220c38c-e8aa-33fe-8e82-5c269c8c5c64",
      "generation": 1,
      "lastUpdateMicros": 1488704404109159,
      "kind": "cm:adc-core:working-config:ltm:profile:ipother:adcprofileipotherstate",
      "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/profile/ipother/2220c38c-e8aa-33fe-8e82-5c269c8c5c64"
    }
  ],
  "generation": 1,
  "kind": "cm:adc-core:working-config:ltm:profile:ipother:adcprofileipothercollectionstate",
  "lastUpdateMicros": 1488704216186713,
  "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/profile/ipother"
}
```

```
POST https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual/9a269865-55c4-3a42-82db-5c099899dbc0/profiles
```
Request:
```
{
  "name": "ipother",
  "partition": "Common",
  "profileIpotherReference": {
    "link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/profile/ipother/2220c38c-e8aa-33fe-8e82-5c269c8c5c64"
  },
  "context": "all"
}
```

Response:
```
{
  "profileIpotherReference": {
    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/profile/ipother/2220c38c-e8aa-33fe-8e82-5c269c8c5c64"
  },
  "context": "all",
  "partition": "Common",
  "name": "ipother",
  "id": "2220c38c-e8aa-33fe-8e82-5c269c8c5c64",
  "generation": 1,
  "lastUpdateMicros": 1488967129854978,
  "kind": "cm:adc-core:working-config:ltm:virtual:profiles:adcvirtualprofilestate",
  "selfLink": "https://localhost/mgmt/cm/adc-core/working-config/ltm/virtual/9a269865-55c4-3a42-82db-5c099899dbc0/profiles/2220c38c-e8aa-33fe-8e82-5c269c8c5c64"
}
```

### API Reference
