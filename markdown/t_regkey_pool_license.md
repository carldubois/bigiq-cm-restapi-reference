# RegKey Pool Licence

## Overview
This set of API provides a way to manage standalone registration key.  The API provides methods to create a RegKey Pool, add/remove registration keys to/from the pool, assign a key to a BIG-IP device and generate a usage report.

## Prerequisites
The user should be sure the following prerequisites have been met.

- The BIG-IQ Centralized Management system is operational, has completed the setup wizard, and completed any other needed configuration.
- The BIG-IQ has an internet connection to F5 licensing server if the user plans to use automatic activation
- A set of BIG-IP VE license keys to be managed

### Manage RegKey Pool
The API provides methods to manage the RegKey Pool collection to create, update, or delete an item.

#### 1. Create a RegKey Pool

POST https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses
```
Request
    {
        "name" : "Primary RegKey Pool",
        "description" : "This is the main pool to use"
    }

Response
    {
        "id": "cae1479c-39da-4cc3-989f-cabee61a630d",
        "name": "Primary RegKey Pool",
        "description": "This is the main pool to use",
        "sortName": "Registration Key Pool",
        "generation": 1,
        "lastUpdateMicros": 1469047687414241,
        "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensestate",
        "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/cae1479c-39da-4cc3-989f-cabee61a630d"
    }
```
#### 2. View RegKey Pool data

GET https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses
```
Response
    {
        "items": [
        {
          "id": "01b6b9db-4e8a-4dd0-90c7-69f61aa33869",
          "name": "Pool A",
          "description": "My first RegKey Pool",
          "sortName": "Registration Key Pool",
          "generation": 3,
          "lastUpdateMicros": 1469047312780414,
          "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensestate",
          "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/01b6b9db-4e8a-4dd0-90c7-69f61aa33869"
        },
        {
          "id": "996c7d63-78af-44be-969f-e50c67bb34f0",
          "name": "Pool B",
          "description": "My second RegKey Pool",
          "sortName": "Registration Key Pool",
          "generation": 1,
          "lastUpdateMicros": 1469047340095990,
          "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensestate",
          "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/996c7d63-78af-44be-969f-e50c67bb34f0"
        }
        ],
        "generation": 4,
        "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensecollectionstate",
        "lastUpdateMicros": 1469047340099287,
        "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses"
    }
```
#### 3. Update individual RegKey Pool to change name and/or description

PATCH https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses/{id}
```
Request
    {
        "name" : "new name",
        "description" : "new description"
    }

Response
    {
        "id": "cae1479c-39da-4cc3-989f-cabee61a630d",
        "name": "new name",
        "description": "new description",
        "sortName": "Registration Key Pool",
        "generation": 1,
        "lastUpdateMicros": 1469047687414241,
        "kind": "cm:device:licensing:pool:regkey:licenses:regkeypoollicensestate",
        "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/cae1479c-39da-4cc3-989f-cabee61a630d"
    }
```
#### 4. Remove a RegKey Pool
Note: a regkey may not be deleted if it is assigned to a BIG-IP device.

DELETE https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses/{id}

### Managing registration keys for a RegKey Pool.

A collection is automatically created beneath a top-level Regkey Pool. Unlike a typical Offerings Collection employed
by other pool license types, user needs to interact directly with this collection to activate regkeys in it.

The activation process exposed by this collection's API is very similar to that of the top-level
collections for other pool license types.

#### 1. Add a license key with automatic activation.
POST https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings
```
Request:

{
    "regKey": "AAAAA-BBBBB-CCCCC-DDDDD-EEEEEEE",
    "status": "ACTIVATING_AUTOMATIC",
    "name" : "my own freeform name",
}

Response:
{
    "regKey" : "MY-REGISTRATION-KEY",
    "name" : "my own freeform name",
    "status" : "ACTIVATING_AUTOMATIC",
    "message" : "Activation in progress",
}
```
#### 2. Poll to get status.
After posting the license, user should poll to check the activation status

GET https://ip/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Response:
{
    "regKey" : "MY-REGISTRATION-KEY",
    "name" : "my own freeform name",
    "status" : "ACTIVATING_AUTOMATIC_NEED_EULA_ACCEPT",
    "message" : "Need EULA acceptance in order to continue",
    "eulaText" : "The exact EULA text goes here..."
}
```
#### 3. Patch to accept EULA.
After user accepts the EULA, subsequent poll shows status of the activation process.  Eventually, the activation should have a status of either ACTIVATION_FAILED or READY.

PATCH https://ip/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Request:
{
    "status" : "ACTIVATING_AUTOMATIC_EULA_ACCEPTED",
    "eulaText" : "The exact EULA text goes here..."
}

Response:
{
	"regKey" : "MY-REGISTRATION-KEY",
	"name" : "my own freeform name",
	"status" : "ACTIVATING_AUTOMATIC_EULA_ACCEPTED",
	"eulaText" : "The exact EULA text goes here..."
}
```
#### 4. For manual activation, patch to provide license text to activate the license.
For manual activation, the license text is submitted to finish the activation process.

PATCH https://ip/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Request:
{
	"status" : "ACTIVATING_MANUAL_LICENSE_TEXT_PROVIDED",
	"licenseText" : "The exact license text goes here..."
}
Response:
{
	"regKey" : "MY-REGISTRATION-KEY",
	"name" : "my own freeform name",
	"status" : "ACTIVATING_MANUAL_LICENSE_TEXT_PROVIDED",
	"licenseText" : "The exact license text goes here..."
}
```
#### 5. Patch to retry a failed activation or reactivate an existing license.
Before retrying activation, user should check the logs and error messages to find the root cause of the failure.  Possible causes might be an incorrect registration key or a connection error to licensing server, etc.

PATCH https://ip/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Request:
{
	"status" : "ACTIVATING_AUTOMATIC",
}

Response:
{
	"regKey" : "MY-REGISTRATION-KEY",
	"name" : "my own freeform name",
	"status" : "ACTIVATING_AUTOMATIC"
}
```
#### 6 Reactivate a license with add-on keys.
For automatic activation, there is no need to accept the EULA again.

PATCH https://ip/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}
```
Request:
{
	"status" : "ACTIVATING_AUTOMATIC",
	"addOnKeys": ["adfasdfasdfasdf"]
}

Response:
{
	"regKey" : "MY-REGISTRATION-KEY",
	"addOnKeys": ["adfasdfasdfasdf"]
	"name" : "my own freeform name",
	"status" : "ACTIVATING_AUTOMATIC"
}
```
#### 7 DELETE
Note: a regkey may not be deleted if it is assigned to a BIG-IP device.
DELETE https://ip/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}

### Manage license assignment to a BIG-IP device
A collection is automatically created beneath each Offering Collection. Each entry in this collection represents a license granted to a device.
Note that for RegKey Pools, each offering can only have one grant, maximum. This is in contrast to other pool-style licenses, where multiple devices can be licensed under a given offering.
POSTing a new entry to this collection will push a new license to the device. Granting a new license to a BIG-IP device may cause a temporary interruption of operation.

#### 1. Get the assignment for a regkey in a regkey pool.

GET https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members
```
Response
{
    "items" : [ {
        "id" : "fb5090c9-6214-4874-a55b-2524fa38e48d",
        "status" : "LICENSED",
        "generation" : 9,
        "message" : "Device is licensed",
        "deviceReference" : {
            "link" : "https://localhost/mgmt/shared/resolver/device-groups/cmallDevices/devices/a8a813db-922a-49fd-ba6b-6c3c66420831"
        },
        "lastUpdateMicros" : 1694552994873217,
        "kind" : "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensememberstate",
        "selfLink" : "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/xxxx1479c-39da-4cc3-989f-cabee61a630d/offerings/W3227-46114-50761-84901-0566329/members/fb5090c9-6214-4874-a55b-2524fa38e48d"
    }],
    "generation" : 6,
    "kind" : "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensemembercollectionstate",
    "lastUpdateMicros" : 1694552994873217,
    "selfLink" : "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/cae1479c-39da-4cc3-989f-cabee61a630d/offerings/W3227-46114-50761-84901-0566329/members"
}
```
#### 2. Assign a license to a managed device.

POST https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members
```
Request
{
    "deviceReference" : {
        "link" : "https://localhost/mgmt/shared/resolver/device-groups/cmallDevices/devices/a8a813db-922a-49fd-ba6b-6c3c66420831"
    }
}

Response
{
    "id": "56f2d346-67e5-4000-af0d-5ff6cdf596c9",
    "deviceMachineId": "a8a813db-922a-49fd-ba6b-6c3c66420831",
    "deviceReference": {
      "link": "https://localhost/mgmt/shared/resolver/device-groups/cmallDevices/devices/a8a813db-922a-49fd-ba6b-6c3c66420831"
    },
    "deviceAddress": "10.0.2.100",
    "deviceName": "my.device.hostname",
    "status": "INSTALLING",
    "generation": 1,
    "lastUpdateMicros": 1469127986668382,
    "kind": "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensememberstate",
    "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/563076fa-1fe8-4203-96ae-4cb943382153/offerings/Z6527-79773-64853-38712-6298060/members/56f2d346-67e5-4000-af0d-5ff6cdf596c9"
}
```
#### 3. Grant a license to an unmanaged device

POST https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members
```
Request
{
    "deviceAddress" : "11.22.33.44",
    "username" : "my_admin_username",
    "password" : "my password"
}

Response
{
    "id": "56f2d346-67e5-4000-af0d-5ff6cdf596c9",
    "deviceMachineId": "a8a813db-922a-49fd-ba6b-6c3c66420831",
    "deviceReference": {
      "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allDevices/devices/a8a813db-922a-49fd-ba6b-6c3c66420831"
    },
    "deviceAddress": "10.0.2.100",
    "deviceName": "my.device.hostname",
    "status": "INSTALLING",
    "generation": 1,
    "lastUpdateMicros": 1469127986668382,
    "kind": "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensememberstate",
    "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/563076fa-1fe8-4203-96ae-4cb943382153/offerings/Z6527-79773-64853-38712-6298060/members/56f2d346-67e5-4000-af0d-5ff6cdf596c9"
}
```
#### 4. Get status for individual assignment.  Use this query to check the licensing progress

GET https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members/{uuid}
```
Response
{
    "id" : "fb5090c9-6214-4874-a55b-2524fa38e48d",
    "status" : "LICENSED",
    "deviceName": "my.device.hostname",
    "generation" : 9,
    "message" : "Device is licensed",
    "deviceReference" : {
        "link" : "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allDevices/devices/a8a813db-922a-49fd-ba6b-6c3c66420831"
    },
    "deviceAddress" : "11.22.33.44",
    "deviceName": "my.device.hostname",
    "lastUpdateMicros" : 1694552994873217,
    "kind" : "cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensememberstate",
    "selfLink" : "https://localhost/mgmt/cm/device/licensing/pool/regkey/licenses/cae1479c-39da-4cc3-989f-cabee61a630d/offerings/W3227-46114-50761-84901-0566329/members/fb5090c9-6214-4874-a55b-2524fa38e48d"
}
```
#### 5. Revoke a license

DELETE https://{ip}/mgmt/cm/device/licensing/pool/regkey/licenses/{id}/offerings/{regkey}/members/{uuid}
```
For managed devices:
Request
{
    For managed devices, no request body is required.
}

For unmanaged devices:
Request
{
    "id" : "fb5090c9-6214-4874-a55b-2524fa38e48d",
    "username" : "my_admin_username",
    "password" : "my password"
}
```