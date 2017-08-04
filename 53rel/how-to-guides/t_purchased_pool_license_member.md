# API Purchased Pool License Members

## Overview

API to assign, refresh or revoke a purchased pool license seat for managed or unmanaged BIG-IP devices.  Note that administrator credentials are required for all operations involving unmanaged devices.

### Prerequisites
You should be sure the following prerequisites have been met.

- The BIG-IQ Centralized Management system is operational, has completed the setup wizard, and completed any other needed configuration.
- BIG-IQ is managing the BIG-IP device(s) to be licensed.  If dealing with unmanaged BIG-IP devices, you will need their IP addresses and administrator credentials.
- You have one of the following roles: administrator, device manager, or license manager.

### Assign
A purchased pool license can be assigned to a BIG-IP by sending a POST to the `/members` subcollection of the license.  Items 2 and 3 below show examples of assigning a license to managed and unmanaged devices respectively.

### Refresh
If a purchased pool license is reactivated within BIG-IQ, the updated license will not be reflected on any BIG-IP devices automatically.  The updated license can be pushed to BIG-IP devices that are already using the license.  Item 5 below shows an example of refreshing the license on a BIG-IP by sending a PATCH to a license assignment in the `/members` subcollection.

### Revoke
A license seat can be reclaimed by sending a DELETE to a license assignment in the `/members` subcollection.  Item 6 below shows an example of revoking the license from a BIG-IP.

#### 1. Query assignments for a purchased pool license
```
GET https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members
```

Response:
```
{
  "items": [
    {
      "auditRecordReference": {
        "link": "https://localhost/mgmt/cm/device/licensing/audit/6f14789b-c12f-4018-b086-d0b4b638beec"
      },
      "deviceAddress": "10.145.198.181",
      "deviceMachineId": "77d9d4a4-9255-4f46-907e-b2bbd717e819",
      "deviceName": "dsc-ip3.pdsea.f5net.com",
      "deviceReference": {
        "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/77d9d4a4-9255-4f46-907e-b2bbd717e819"
      },
      "generation": 4,
      "kind": "cm:device:licensing:pool:purchased-pool:licenses:licensepoolmemberstate",
      "lastUpdateMicros": 1488240514143425,
      "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/56c1b433-8cfa-485e-b1fb-0d964f994f90/members/e228a87d-3b89-4f42-951e-557e839a4d59",
      "state": "LICENSED",
      "uuid": "e228a87d-3b89-4f42-951e-557e839a4d59"
    },
    ...
```

#### 2. License a managed device
Assigning a license to a managed device only requires providing a `deviceReference`.  All managed BIG-IP devices will exist in the `cm-bigip-allBigIpDevices` device group.  If needed, you can query the device group to find a device reference.

After the POST to assign a license, you can poll the assignment to check the status, waiting for `state` to be `LICENSED` (see item 4).
```
POST https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members
```
Request:
```
{
  "deviceReference": {
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/77d9d4a4-9255-4f46-907e-b2bbd717e819"
  }
}
```

Response:
```
{
  "uuid": "20a5cf91-f9a3-400f-9325-b4fc2a2c464b",
  "deviceName": "dsc-ip3.pdsea.f5net.com",
  "deviceReference": {
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/77d9d4a4-9255-4f46-907e-b2bbd717e819"
  },
  "deviceMachineId": "77d9d4a4-9255-4f46-907e-b2bbd717e819",
  "deviceAddress": "10.145.198.181",
  "state": "INSTALL",
  "generation": 1,
  "lastUpdateMicros": 1488434123132956,
  "kind": "cm:device:licensing:pool:purchased-pool:licenses:licensepoolmemberstate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/56c1b433-8cfa-485e-b1fb-0d964f994f90/members/20a5cf91-f9a3-400f-9325-b4fc2a2c464b"
}
```

#### 3. License an unmanaged device
BIG-IQ also supports licensing devices that are not actively managed.  BIG-IQ has no interaction with such devices outside of licensing.  Because of the lower overhead, BIG-IQ supports this type of licensing at a larger scale (thousands).  Because BIG-IQ isn't managing such BIG-IP devices, they have no device reference.  Instead, the required inputs are an IP address, administrator username and password.

Similar to managed devices, you can poll the assignment after it's created to check the status, waiting for `state` to be `LICENSED` (see item 4).
```
POST https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members
```
Request:
```
{
  "deviceAddress": "10.145.193.61",
  "username": "admin",
  "password": "password"
}
```

Response:
```
{
  "uuid": "ab267880-c34a-418a-9e75-fb507f636120",
  "deviceName": "dsc-ip4.pdsea.f5net.com",
  "deviceMachineId": "fb4e7e62-f3ae-4a95-b1a4-e89d7ba6ead3",
  "deviceAddress": "10.145.193.61",
  "state": "INSTALL",
  "generation": 1,
  "lastUpdateMicros": 1488435208256456,
  "kind": "cm:device:licensing:pool:purchased-pool:licenses:licensepoolmemberstate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/56c1b433-8cfa-485e-b1fb-0d964f994f90/members/ab267880-c34a-418a-9e75-fb507f636120"
}
```

#### 4. Query license assignment status
After a license assignment is made, you can query the status of the assignment.  Successful assignments will reach a `state` of `LICENSED`.  This typically takes less than a minute.

For unmanaged device assignments, basic health checking occurs periodically because BIG-IQ isn't otherwise managing the device.  Fields related to the health checking will appear only for unmanaged device assignments as shown in the example here.  
```
GET https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members/{member_uuid}

```
Response:
```
{
  "auditRecordReference": {
    "link": "https://localhost/mgmt/cm/device/licensing/audit/7252695f-1531-4c1a-8775-18a872f22fc8"
  },
  "deviceAddress": "10.145.193.61",
  "deviceMachineId": "fb4e7e62-f3ae-4a95-b1a4-e89d7ba6ead3",
  "deviceName": "dsc-ip4.pdsea.f5net.com",
  "generation": 5,
  "healthCheckFailureCount": 0,
  "kind": "cm:device:licensing:pool:purchased-pool:licenses:licensepoolmemberstate",
  "lastGoodHealthCheckDateTime": "2017-03-02T06:15:57.846Z",
  "lastUpdateMicros": 1488435357850120,
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/56c1b433-8cfa-485e-b1fb-0d964f994f90/members/ab267880-c34a-418a-9e75-fb507f636120",
  "state": "LICENSED",
  "uuid": "ab267880-c34a-418a-9e75-fb507f636120"
}
```

#### 5. Refresh the license on a BIG-IP device
If a license is reactivated within BIG-IQ, the updated license can be pushed to a BIG-IP device that is using the license via a simple PATCH.  Similar to the initial license assignment, you can poll the assignment after the PATCH completes to check the status, waiting for `state` to be `LICENSED` (see item 4).

The PATCH body should also include administrator credentials (`username` and `password`) for unmanaged devices.
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members/{member_uuid}
```
Request:
```
{
  "state": "INSTALL"
}
```

Response:
```
{
  "uuid": "ec234bf5-80bb-41dc-96bc-4d5e15f6dcf5",
  "deviceName": "bigip11-41.f5net.com",
  "deviceReference": {
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/7141a063-7cf8-423f-9829-9d40599fa3e0"
  },
  "deviceMachineId": "7141a063-7cf8-423f-9829-9d40599fa3e0",
  "deviceAddress": "10.145.197.41",
  "state": "INSTALL",
  "auditRecordReference": {
    "link": "https://localhost/mgmt/cm/device/licensing/audit/ef7ce604-1c61-498e-a6df-32e13780ea14"
  },
  "generation": 8,
  "lastUpdateMicros": 1488436813066133,
  "kind": "cm:device:licensing:pool:purchased-pool:licenses:licensepoolmemberstate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/56c1b433-8cfa-485e-b1fb-0d964f994f90/members/ec234bf5-80bb-41dc-96bc-4d5e15f6dcf5"
}
```

#### 6. Revoke license from a device
To revoke a license from a BIG-IP device to reclaim a seat, send a DELETE to the assignment.  For managed devices, no request body is needed.  For unmanaged devices, the request body must include administrator credentials and the member_uuid for the assignment as shown in the example.
```
DELETE https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members/{member_uuid}
```
Request:
```
{
  "uuid": "1ecbb7fb-8f2a-421c-9450-d2d927181b47",
  "username": "admin",
  "password": "password"
}
```

