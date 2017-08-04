# RegKey Pool Licenses API

## Overview
This API supports managing individual BIG-IP VE licenses within BIG-IQ.  The API provides methods to create a RegKey Pool, add/remove registration keys to or from a pool, and assign/revoke a key to or from a BIG-IP device.

## Prerequisites
Make certain that the following prerequisites have been met.

- The BIG-IQ Centralized Management device is operational, has completed the setup wizard, and completed any other needed configuration.
- The BIG-IQ has an internet connection to the F5 licensing server if you plan to use automatic activation.
- You have a set of BIG-IP VE license keys to be managed.
- You have one of the following roles: administrator, device manager, or license manager.

Note: When you perform these tasks using the example code provided, review the listed IP addresses and change them as appropriate for your environment. For example, if you are not running the script directly on the BIG-IQ device, change localhost to be the IP address of the BIG-IQ Centralized Management device.

### Manage a RegKey Pool
This API provides methods to manage the RegKey Pool collection by creating, updating, or deleting a RegKey Pool.

#### 1. Query existing RegKey Pools
```
GET https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses
```

Response
```
{
  "items": [
    {
      "id": "cc010b7d-9c9e-40a9-9668-321f4ebc26f6",
      "name": "RegKey Pool #1",
      "sortName": "Registration Key Pool",
      "generation": 1,
      "lastUpdateMicros": 1488535202069037,
      "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensestate",
      "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/cc010b7d-9c9e-40a9-9668-321f4ebc26f6"
    }
  ],
  "generation": 6,
  "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensecollectionstate",
  "lastUpdateMicros": 1488535202076692,
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses"
}
```

#### 2. Create a RegKey Pool
```
POST https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses
```
Request
```
{
  "name": "RegKey Pool #2",
  "description": "Custom description"
}
```

Response
```
{
  "id": "150102a0-66ec-411f-8776-221019f430f3",
  "name": "RegKey Pool #2",
  "description": "Custom description",
  "sortName": "Registration Key Pool",
  "generation": 1,
  "lastUpdateMicros": 1488535345324793,
  "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensestate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/150102a0-66ec-411f-8776-221019f430f3"
}
```

#### 3. Update a RegKey Pool to change name and/or description
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}
```
Request
```
{
  "name": "RegKey Pool #2 - updated",
  "description" : "Updated description"
}
```

Response
```
{
  "id": "150102a0-66ec-411f-8776-221019f430f3",
  "name": "RegKey Pool #2 - updated",
  "description": "Updated description",
  "sortName": "Registration Key Pool",
  "generation": 2,
  "lastUpdateMicros": 1488535758312642,
  "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensestate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/150102a0-66ec-411f-8776-221019f430f3"
}
```

#### 4. Remove a RegKey Pool
Note: You cannot delete a RegKey Pool if it includes one or more registration keys assigned to a BIG-IP device.
```
DELETE https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}
```

### Managing registration keys in a RegKey Pool

Each RegKey Pool can contain an arbitrary number of BIG-IP registration keys.

#### 1. Query existing license keys for a RegKey Pool
```
GET https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings
```

Response:
```
{
  "items": [],
  "generation": 0,
  "kind": "cm:device:licensing:pool:regkey:licenses:item:offerings:regkeypoollicenseofferingcollectionstate",
  "lastUpdateMicros": 0,
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/150102a0-66ec-411f-8776-221019f430f3/offerings"
}
```

#### 2. Add a license key with automatic activation
Replace MY-REGISTRATION-KEY in this example with your actual BIG-IP VE registration key (optionally including any add-on keys, similar to what's shown in the section about reactivation further below).
```
POST https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings
```
Request:
```
{
  "regKey": "MY-REGISTRATION-KEY",
  "status": "ACTIVATING_AUTOMATIC",
  "description": "my freeform description"
}
```

Response:
```
{
  "regKey": "MY-REGISTRATION-KEY",
  "sortName": "Registration Key Pool Item",
  "publicKey": [
    16,
    96,
    61,
    ...
  ],
  "internalPrivateKey": "hXIOe4RROD...",
  "encryptedPrivateKey": [
    15,
    104,
    19,
    ...
  ],
  "name": "License for MY-REGISTRATION-KEY",
  "description": "my freeform description",
  "message": "Automatic activation in progress",
  "dossier": "4a133ec092...",
  "status": "ACTIVATING_AUTOMATIC",
  "generation": 1,
  "lastUpdateMicros": 1488538151253316,
  "kind": "cm:device:licensing:pool:regkey:licenses:item:offerings:regkeypoollicenseofferingstate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/150102a0-66ec-411f-8776-221019f430f3/offerings/Q0223-28107-64761-06159-4281213"
}
```

#### 3. Poll to get status
After adding a registration key, you should poll to check the activation status.
```
GET https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```

Response:
```
{
  "eulaText": "END USER LICENSE AGREEMENT\r\nDOC-0355-08\r\n\r\nIMPORTANT - READ BEFORE..."
  "message": "Accept EULA to continue",
  "status": "ACTIVATING_AUTOMATIC_NEED_EULA_ACCEPT",
  ...
}
```

#### 4. Complete automatic activation by accepting the EULA
Echo the EULA text back to the license endpoint to agree to the EULA and complete the automatic activation workflow.

After doing so, again poll to get the final activation status (either `READY` or `ACTIVATION_FAILED`).
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Request:
```
{
  "status": "ACTIVATING_AUTOMATIC_EULA_ACCEPTED",
  "eulaText": "END USER LICENSE AGREEMENT\r\nDOC-0355-08\r\n\r\nIMPORTANT - READ BEFORE..."
}
```

Response:
```
{
  "message": "Finishing activation",
  "status": "ACTIVATING_AUTOMATIC_EULA_ACCEPTED",
  ...
}
```

#### 5. Complete manual activation by providing license text
If manual activation is used instead of automatic activation (in the POST to add a registration key, `status` is `ACTIVATING_MANUAL` instead of `ACTIVATING_AUTOMATIC`), then the PATCH to complete activation will include the license text received from the F5 licensing web portal.

The response will include the final activation status (either `READY` or `ACTIVATION_FAILED`).
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Request:
```
{
  "status": "ACTIVATING_MANUAL_LICENSE_TEXT_PROVIDED",
  "licenseText": "..."
}
```

Response:
```
{
  "licenseState": {
    "vendor": "F5 Networks, Inc.",
    "licensedDateTime": "2017-03-03T00:00:00-08:00",
    "licensedVersion": "5.2.0",
    ...
  },
  "message": "Activated",
  "status": "READY",
  ...
}
```

#### 6. Retry a failed activation or reactivate an existing license
The process to retry an activation that failed or to reactivate an existing license is the same.  Note, if an activation fails, check error messages returned from the API or the restjavad logs for details.

Similar to the prior steps, you will need to poll to get the final activation status.
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Request:
```
{
  "status": "ACTIVATING_AUTOMATIC"
}
```

Response:
```
{
  "message": "Automatic activation in progress",
  "status": "ACTIVATING_AUTOMATIC",
  ...
}
```

#### 7. Reactivate a license with add-on key(s)
Replace MY-ADD-ON-KEY in this example with your actual add-on key(s).

Similar to the prior steps, you will need to poll to get the final activation status.
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Request:
```
{
  "status": "ACTIVATING_AUTOMATIC",
  "addOnKeys": ["MY-ADD-ON-KEY"]
}
```

Response:
```
{
  "message": "Automatic activation in progress",
  "status": "ACTIVATING_AUTOMATIC",
  ...
}
```

#### 8. Delete
Note, you cannot delete a registration key if it is assigned to a BIG-IP device.
```
DELETE https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```

### Manage license assignment to a BIG-IP device
Each registration key in a RegKey Pool can be assigned to only one BIG-IP.  Assignments can be managed via the `/members` subcollection under each registration key.

Note, assigning a new license to a BIG-IP device can cause a temporary interruption of operation.

#### 1. Get the assignment for a registration key in a RegKey Pool
```
GET https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members
```

Response:
```
{
  "items": [
    {
      "auditRecordReference": {
        "link": "https://localhost/mgmt/cm/device/licensing/audit/04236435-986c-44fc-94cc-97a072b4b747"
      },
      "deviceAddress": "10.145.197.41",
      "deviceMachineId": "7141a063-7cf8-423f-9829-9d40599fa3e0",
      "deviceName": "bigip11-41.f5net.com",
      "deviceReference": {
        "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/7141a063-7cf8-423f-9829-9d40599fa3e0"
      },
      "generation": 4,
      "id": "73854946-2e75-41e0-9ffb-7ebc06abd87d",
      "kind": "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensememberstate",
      "lastUpdateMicros": 1488785701966707,
      "message": "Device licensed",
      "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/17be603d-3978-4c82-ac86-0d0b4cce8ce3/offerings/H4537-72099-57885-27527-0188153/members/73854946-2e75-41e0-9ffb-7ebc06abd87d",
      "status": "LICENSED"
    }
  ],
  "generation": 5,
  "kind": "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensemembercollectionstate",
  "lastUpdateMicros": 1488785701969074,
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/17be603d-3978-4c82-ac86-0d0b4cce8ce3/offerings/H4537-72099-57885-27527-0188153/members"
}
```

#### 2. Assign a license to a managed device
Below is an example of assigning a registration key to a managed device. Afterwards, you should poll to check the assignment status.
```
POST https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members
```
Request:
```
{
  "deviceReference": {
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/7141a063-7cf8-423f-9829-9d40599fa3e0"
  }
}
```

Response:
```
{
  "id": "6dabfc7c-9bfc-4666-b0cf-e6fc076ac0ad",
  "deviceMachineId": "7141a063-7cf8-423f-9829-9d40599fa3e0",
  "deviceReference": {
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/7141a063-7cf8-423f-9829-9d40599fa3e0"
  },
  "deviceAddress": "10.145.197.41",
  "deviceName": "bigip11-41.f5net.com",
  "status": "INSTALLING",
  "generation": 1,
  "lastUpdateMicros": 1488786814492210,
  "kind": "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensememberstate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/17be603d-3978-4c82-ac86-0d0b4cce8ce3/offerings/H4537-72099-57885-27527-0188153/members/6dabfc7c-9bfc-4666-b0cf-e6fc076ac0ad"
}
```

#### 3. Assign a license to an unmanaged device
Below is an example of assigning a registration key to an unmanaged device. Afterwards, you should poll to check the assignment status.
```
POST https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members
```
Request:
```
{
  "deviceAddress": "10.145.198.181",
  "username": "admin",
  "password": "password"
}
```

Response:
```
{
  "id": "c90b62f0-65ee-48aa-ad57-c4ce8d1dc933",
  "deviceMachineId": "77d9d4a4-9255-4f46-907e-b2bbd717e819",
  "deviceAddress": "10.145.198.181",
  "deviceName": "dsc-ip3.pdsea.f5net.com",
  "status": "INSTALLING",
  "generation": 1,
  "lastUpdateMicros": 1488787037718076,
  "kind": "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensememberstate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/17be603d-3978-4c82-ac86-0d0b4cce8ce3/offerings/H4537-72099-57885-27527-0188153/members/c90b62f0-65ee-48aa-ad57-c4ce8d1dc933"
}
```

#### 4. Get the status of an assignment
After initiating an assignment of a registration key to a device, you can query the status of the assignment to confirm the device is licensed successfully.
```
GET https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members/{member_uuid}
```

Response:
```
{
  "message": "Device licensed",
  "status": "LICENSED",
  ...
}
```

#### 5. Revoke license from a managed device
```
DELETE https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members/{member_uuid}
```

#### 6. Revoke license from an unmanaged device
For unmanaged devices, the request body must include administrator credentials and the member_uuid for the assignment as shown in the example.
```
DELETE https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members/{member_uuid}
```
Request:
```
{
  "id": "c90b62f0-65ee-48aa-ad57-c4ce8d1dc933",
  "username": "admin",
  "password": "password"
}
```

### API Reference
