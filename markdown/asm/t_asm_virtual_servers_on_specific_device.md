## Getting the active policy of a specific virtual server on a specific device.

### Overview
Describes how you use the REST API to get the active policy of a specific virtual server on a specific device.

### Prerequisites
1. Device configuration discovered and imported to Web Application Security.
2. The name and partition of the virtual server should be known.

### Description
Describes how you use the REST API to get the active policy of a specific virtual server on a specific device.
Perform the REST API actions in the following order:
1. Perform a GET operation to determine the selfLink of a device.
2. Perform a GET operation to determine the active policy of the virtual server.

The following extended example shows each of these REST API actions.

### Example

#### 1. Perform a GET operation to determine the selfLink of a device.
Perform a GET operation on the Web Application Security devices collection, filtering the results by a name and limiting the result to show the device name and the device selfLink that will be used later for searches. In this example the name being searched for is 'device1.com'.
```
GET: https://<mgmtip>/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices?$filter=hostname eq 'device1.com'&$select=hostname,selfLink
```
The following is the JSON response from the GET operation:
```
{
    "selfLink": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices",
    "totalItems": 1,
    "items": [
        {
            "hostname": "device1.com",
            "selfLink": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/c1444144-11e7-47e6-8e91-eaa913826a7f"
        }
    ],
    "generation": 18,
    "kind": "shared:resolver:device-groups:devicegroupdevicecollectionstate",
    "lastUpdateMicros": 1479388471935401
}
```

#### 2. Perform a GET operation to determine the active policy of the virtual server.
Perform a GET operation to determine the active policy of the virtual server, filtering the results using the deviceReference that was retrieved in step #1 and by the virtual server properties.
```
GET: https://<mgmtip>/mgmt/cm/asm/working-config/virtual-servers?$select=selfLink,name,fullPath&$filter=deviceReference/link eq 'https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/c1444144-11e7-47e6-8e91-eaa913826a7f' and name eq 'Virtual_1' and partition eq 'Common'
```
The following is the JSON response from the GET operation:
```
{
    "selfLink": "https://localhost/mgmt/cm/asm/working-config/virtual-servers",
    "totalItems": 1,
    "items": [
        {
            "name": "Virtual_1",
            "selfLink": "https://localhost/mgmt/cm/asm/working-config/virtual-servers/fc4cb3cf-b2d8-378a-8a64-07a27e60316c"
        }
    ],
    "generation": 8,
    "kind": "cm:asm:working-config:virtual-servers:asmvirtualservercollectionstate",
    "lastUpdateMicros": 1479388471928975
}
```

### API references:
[Api reference - virtual server management](../html-reference/virtual-server-management.html)