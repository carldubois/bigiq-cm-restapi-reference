## Checking whether a policy is in use by a specific device.

### Overview
Describes how you use the REST API to determine if a policy is in use by a specific device.

### Prerequisites
None.
### Description
Describes how you use the REST API to determine if a policy is in use by a specific device.
A policy is in use if a virtual server of specific device has the policy attached to it.
A special virtual server called 'inactive' can be used to associate a policy to a device without actually using it to secure traffic.
Perform the REST API actions in the following order:
1. Perform a GET operation to determine the selfLink of a policy.
2. Perform a GET operation to determine the selfLink of a device.
3. Perform a GET operation to the virtual-servers collection with a filter to find if any virtual servers on that device are using that policy.

The following extended example shows each of these REST API actions.
### Example
#### 1. Perform a GET operation to determine the selfLink of a policy.
Perform a GET operation on the policies collection, filtering the results by a name and limiting the result to show specific fields that are defining the resource, together with a link to retrieve all the policy properties (selfLink). In this example the name being searched for is 'Policy_1'.
```
GET: https://<mgmtip>/mgmt/cm/asm/working-config/policies?$filter=name eq 'Policy_1'&$select=name,fullPath,selfLink
```
The following is the JSON response from the GET operation:
```
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
```
#### 2. Perform a GET operation to determine the selfLink of a device.
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
#### 3. Perform a GET operation to the virtual-servers collection with a filter to find if any virtual servers on that device are using that policy.
Perform a GET operation on the virtual-servers collection, filtering the results by the attachedPoliciesReferences field to retrieve virtual servers that are using the policy that was retrieved above in step #1 of the example, and by the deviceReference that was retrieved above in step #2 of the example.
```
GET https://mgmtip/mgmt/cm/asm/working-config/virtual-servers?$filter=attachedPoliciesReferences/link eq 'https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef' and deviceReference/link eq 'https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/c1444144-11e7-47e6-8e91-eaa913826a7f'
```
The following is the JSON response from the GET operation when one virtual server is using it:
```
{
    "selfLink": "https://localhost/mgmt/cm/asm/working-config/virtual-servers",
    "totalItems": 1,
    "items": [
        {
            "address": "1.1.1.1:80",
            "asmEnabled": true,
            "attachedPoliciesReferences": [
                {
                    "id": "1005831c-7e40-30ed-bd0d-f8068526d7ef",
                    "name": "Policy_1",
                    "kind": "cm:asm:working-config:policies:policystate",
                    "partition": "Common",
                    "link": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef"
                }
            ],
            "deviceReference": {
                "id": "c1444144-11e7-47e6-8e91-eaa913826a7f",
                "name": "device1.com",
                "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
                "machineId": "c1444144-11e7-47e6-8e91-eaa913826a7f",
                "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/c1444144-11e7-47e6-8e91-eaa913826a7f"
            },
            "generation": 3,
            "hasAttachedPolicies": true,
            "id": "fc4cb3cf-b2d8-378a-8a64-07a27e60316c",
            "isAdvanced": false,
            "isInactivePoliciesHolder": false,
            "kind": "cm:asm:working-config:virtual-servers:asmvirtualserverstate",
            "lastUpdateMicros": 1479388471920145,
            "mirror": "disabled",
            "name": "Virtual_1",
            "partition": "Common",
            "selfLink": "https://localhost/mgmt/cm/asm/working-config/virtual-servers/fc4cb3cf-b2d8-378a-8a64-07a27e60316c"
        }
    ],
    "generation": 8,
    "kind": "cm:asm:working-config:virtual-servers:asmvirtualservercollectionstate",
    "lastUpdateMicros": 1479388471928975
}
```
When no such virtual servers exist, the response would be:
```
{
    "selfLink": "https://localhost/mgmt/cm/asm/working-config/virtual-servers",
    "totalItems": 0,
    "items": [],
    "generation": 8,
    "kind": "cm:asm:working-config:virtual-servers:asmvirtualservercollectionstate",
    "lastUpdateMicros": 1479388471928975
}
```
Note - to determine the list of all policies that are in use, perform a GET operation to the policies collection and repeat the operations shown here for each policy.
