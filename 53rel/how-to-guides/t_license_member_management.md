# License Assign/Revoke API

## Overview
This task API simplifies assigning and revoking licenses to/from BIG-IP devices.  The API provides a simplified interface for the various pool license types supported by BIG-IQ.  The API does not require knowing the deviceReference of managed devices nor the reference of the license to be assigned/revoked.  All pool license types except Fraud Protection Service (FPS) licenses are supported.  This includes individual BIG-IP VE licenses managed in a RegKey Pool on BIG-IQ.

## Prerequisites
Make certain that the following prerequisites have been met.

- The BIG-IQ Centralized Management device is operational, has completed the setup wizard, and completed any other needed configuration.
- The BIG-IQ license allows licensing managed or unmanaged BIG-IP devices.
- You have one or more pool licenses activated and ready to be assigned to BIG-IP devices.  This can include standalone BIG-IP VE licenses in a RegKey Pool.
- You have one of the following roles: administrator, device manager, or license manager.

Note: When you perform these tasks using the example code provided, review the listed IP addresses and change them as appropriate for your environment. For example, if you are not running the script directly on the BIG-IQ device, change localhost to be the IP address of the BIG-IQ Centralized Management device.

### Assign a license
All assignment operations involve initiating a task, after which you should poll for task completion.  See the **Poll for task completion** section below for details about polling.

#### Assign a purchased pool license to a managed device
To assign a purchased pool license to a managed device, supply the name of the pool and the **discovery** address of the BIG-IP.  The discovery address is the address used to add the BIG-IP to BIG-IQ.  A successful response will indicate the assignment task has started.  You should subsequently poll the returned `selfLink` waiting for the task to complete.
```
POST https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management
```
Request
```
{
  "licensePoolName": "pool name",
  "command": "assign",
  "address": "192.0.2.1"
}
```

Response
```
{
    "licensePoolName": "pool name",
    "command": "assign",
    "address": "192.0.2.1",
    "id": "d717c6a1-f3bd-46cb-8410-c6fda58940b9",
    "status": "STARTED",
    "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/lm"
    },
    "identityReferences": [
        {
            "link": "https://localhost/mgmt/shared/authz/users/lm"
        }
    ],
    "ownerMachineId": "b814fef0-2e8b-460d-af43-0d100dc50352",
    "taskWorkerGeneration": 1,
    "generation": 1,
    "lastUpdateMicros": 1497509153046646,
    "kind": "cm:device:tasks:licensing:pool:member-management:devicelicensingassignmenttaskstate",
    "selfLink": "https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management/d717c6a1-f3bd-46cb-8410-c6fda58940b9"
}
```

#### Assign a pool license offering to a managed device
All supported licenses other than purchased pools will have one or more offerings under the top-level license.  An example utility license offering is `F5-BIG-MSP-BT-1G-LIC-DEV`.  The offering names generally include the feature (good/better/best -- the "BT" in the example) and throughput (the "1G" in the example).  For RegKey Pools, each registration key in the pool is an offering.  The API offers a couple of fields, `skuKeyword1` and `skuKeyword2` to allow you to specify the offering name you would like to assign.  The fields are optional -- you can supply zero, one or both of the fields.  The API will match the strings provided against the offering names in the specified pool.  If both search fields are provided, the first value must appear prior to the second in the offering name.  If multiple offerings match the provided search criteria, the API will assign the first available offering (licenses in a RegKey Pool that are already assigned will be bypassed).  In some cases, searching solely for the feature/throughput won't be specific enough.  The feature may be represented by "B", but that also matches against the "F5-BIG" prefix.  You can extend the search criteria, including dashes or other characters as needed to ensure the desired offering is selected.

Note, utility license assignments require one additional field, which is the unit of measure.

Example assignment of a utility license offering:
```
POST https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management
```
Request
```
{
  "licensePoolName": "u1",
  "command": "assign",
  "address": "192.0.2.1",
  "skuKeyword1": "BT",
  "skuKeyword2": "1G",
  "unitOfMeasure": "daily"
}
```

The response and need for polling for final status is similar to the purchased pool case shown above.

Example assignment of a license from a regkey pool:
```
POST https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management
```
Request
```
{
  "licensePoolName": "rgp1",
  "command": "assign",
  "address": "192.0.2.1",
  "skuKeyword1": "I3242"
}
```

#### Assigning a license to an unmanaged device
The above examples for managed devices also apply to unmanaged devices, the only difference being unmanaged devices require credentials also be provided.
```
POST https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management
```
Request:
```
{
  "licensePoolName": "pool name",
  "command": "assign",
  "address": "192.0.2.1",
  "user": "admin",
  "password": "password"
}
```

If you're using a BIG-IP that is configured with an ssl-port other than 443 that also supports licensing with this configuration, you can supply the relevant port via the `port` field:
```
POST https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management
```
Request:
```
{
  "licensePoolName": "pool name",
  "command": "assign",
  "address": "192.0.2.1",
  "user": "admin",
  "password": "password",
  "port": 8443
}
```

### Revoke a license
Similar to the assignment operations, revoking a license involves initiating a task, after which you should poll for task completion.

#### Revoke a license from a managed device
```
POST https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management
```
Request:
```
{
  "licensePoolName": "pool name",
  "command": "revoke",
  "address": "192.0.2.1"
}
```

#### Revoke a license from an unmanaged device
```
POST https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management
```
Request:
```
{
  "licensePoolName": "pool name",
  "command": "revoke",
  "address": "192.0.2.1",
  "user": "admin",
  "password": "password"
}
```
You can also supply the `port`, if needed.

### Poll for task completion
For any assign or revoke task, you will need to poll the task waiting for it to complete.  If successful, the final task `status` will be `FINISHED` and the `licenseAssignmentReference` will contain the reference to the resulting assignment.  If the task fails, the final task `status` will be `FAILED` and `errorMessage` will be populated with relevant details.  You can review restjavad logs for additional detail as needed.

Note that a finished task means BIG-IP accepted and installed the license, though subsequent MCP validation on BIG-IP may reject the license.  You may want to validate the BIG-IP is operational after the task completes.  This gap may be eliminated in a future release.

Tasks are retained for one week, though history also appears in the BIG-IQ Device audit log which has a longer default retention period.
```
GET https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management/d717c6a1-f3bd-46cb-8410-c6fda58940b9
```

Response
```
{
    "address": "192.0.2.1",
    "command": "assign",
    "currentStep": "POLL_ASSIGNMENT_STATUS",
    "endDateTime": "2017-06-14T23:46:04.532-0700",
    "generation": 7,
    "id": "d717c6a1-f3bd-46cb-8410-c6fda58940b9",
    "identityReferences": [
        {
            "link": "https://localhost/mgmt/shared/authz/users/lm"
        }
    ],
    "kind": "cm:device:tasks:licensing:pool:member-management:devicelicensingassignmenttaskstate",
    "lastUpdateMicros": 1497509164582382,
    "licenseAssignmentReference": {
        "link": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/9a79bcf5-906e-4418-83c2-190ea22b9ec8/member-management/9847bfb5-f0a4-474b-b978-04586fc6d17d"
    },
    "licensePoolName": "pool name",
    "ownerMachineId": "b814fef0-2e8b-460d-af43-0d100dc50352",
    "selfLink": "https://localhost/mgmt/cm/device/tasks/licensing/pool/member-management/d717c6a1-f3bd-46cb-8410-c6fda58940b9",
    "skuKeyword1": "",
    "skuKeyword2": "",
    "startDateTime": "2017-06-14T23:45:53.063-0700",
    "status": "FINISHED",
    "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/lm"
    },
    "username": "lm"
}
```

Example of a failed response:
```
{
    "address": "192.0.2.1",
    "command": "assign",
    "currentStep": "GET_LICENSE",
    "endDateTime": "2017-06-14T23:57:10.608-0700",
    "errorMessage": "License pool 'bad pool name' not found",
    "id": "dee9bd7a-7760-452e-ab61-93df87f5cf36",
    "licensePoolName": "bad pool name",
    "status": "FAILED",
	...
}
```
