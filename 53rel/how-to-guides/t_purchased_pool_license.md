# Purchased Pool Licenses API

## Overview

This API supports activating, reactivating, and removing a purchased pool license.  

1. A pool license is different from the traditional device-based license.  
2. When you use BIG-IQ to push a pool license to a managed device, the action is called "granting" the license. 
3. By doing this you "create a grant," and the BIG-IP that you pushed the license to is counted as "occupying a seat" for the license. 
4. This is also known as a license "assignment," and is typically done through the "/members" subcollection for the pool license.  
5. There are two fields: totalDeviceLicenses, which tracks the seats a purchased pool license has, and freeDeviceLicenses, that tracks how many seats are still available.

### Prerequisites

Make certain that the following prerequisites have been met.

- The BIG-IQ Centralized Management device is operational, has completed the setup wizard, and completed any other needed configuration.
- The BIG-IQ has an internet connection to the F5 licensing server if you plan to use automatic activation.
- You have one of the following roles: administrator, device manager, or license manager.

Note: When you perform these tasks using the example code provided, review the listed IP addresses and change them as appropriate for your environment. For example, if you are not running the script directly on the BIG-IQ device, change localhost to be the IP address of the BIG-IQ Centralized Management device.


### Activate
You can choose to activate a purchased pool license with the API directly instead of through the initial activation API.  The steps are almost identical. For automatic activation, the steps are:
 * POST with regkey and activation method.
 * Poll the endpoint for this license to check for status.
 * PATCH to accept EULA.
 * Poll the endpoint for the license to check the final status.

For manual action, the steps are:
 * POST with regkey and activation method.
 * Using the dossier from POST response, go to the F5 licensing web portal to accept the EULA and get the generated license.
 * PATCH the endpoint for the license with the license text.

### Reactivate
This is the process to reactivate a purchased pool license.  The steps to reactivate automatically are:
 * PATCH with state = RELICENSE (step 4)
 * Poll the endpoint for this license to get the status (step 3).  Because this is a reactivation, you do not need to accept EULA.

The steps to reactivate manually are:
 * PATCH with state = RELICENSE (step 4).
 * Get the generated license from the F5 licensing web portal and PATCH it to the license endpoint (step 6).

### Remove
 * To remove a purchased pool license, send a DELETE on the endpoint (step 7).

#### 1. Query existing purchased pool licenses
```
GET https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses
```

Response:
```
{
  "items": [],
  "generation": 7,
  "kind": "cm:device:licensing:pool:purchased-pool:licenses:licensepoolworkercollectionstate",
  "lastUpdateMicros": 1487328656734798,
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses"
}
```

#### 2. Start activation of a new purchased pool license
There are a few activation methods.  Automatic is the default and requires connectivity to the F5 licensing server.  For manual activation, the POST body should set the method to MANUAL.
```
POST https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses
```
Request:
```
{
  "baseRegKey": "R8573-25996-57909-24167-3331348",
  "name": "my license",
  "method": "AUTOMATIC"
}
```

Response:
```
{
  "uuid": "ae74294e-f3f2-4ad3-86bc-ab3fdb5dfe4c",
  "baseRegKey": "R8573-25996-57909-24167-3331348",
  "method": "AUTOMATIC",
  "name": "my license",
  "dossier": "82b215e883...",
  "sortName": "Purchased Pool",
  "state": "GETTING_EULA",
  "publicKey": [
    48,
    -126,
    1,
    ...
  ],
  "privateKey": "HC57Vph6Ke...",
  "registeredKey": [
    -116,
    -30,
    50,
    ...
  ],
  "generation": 1,
  "lastUpdateMicros": 1487329927179822,
  "kind": "cm:device:licensing:pool:purchased-pool:licenses:licensepoolworkerstate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/ae74294e-f3f2-4ad3-86bc-ab3fdb5dfe4c"
}
```

#### 3. Poll to get purchased pool license status
The desired state of a purchased pool license is that the status is LICENSED.  After the initial POST, the license eventually transitions to WAITING_FOR_EULA_ACCEPTANCE.
```
GET https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/ae74294e-f3f2-4ad3-86bc-ab3fdb5dfe4c
```

Response:
```
{
  "eulaText": "END USER LICENSE AGREEMENT\r\nDOC-0355-08\r\n\r\nIMPORTANT - READ BEFORE...",
  "state": "WAITING_FOR_EULA_ACCEPTANCE",
  ...
}
```

#### 4. Reactivate a purchased pool license
After a purchased pool license is activated, it can be reactivated if needed (e.g. to add an add-on key).
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/ae74294e-f3f2-4ad3-86bc-ab3fdb5dfe4c
```
Request:
```
{
  "state": "RELICENSE",
  "method": "AUTOMATIC"
}
```

After the PATCH completes, poll the license (step 3) until it reaches the LICENSED state.

Response:
```
{
  "state": "LICENSED",
  "totalDeviceLicenses": 25,
  "freeDeviceLicenses": 25,
  "licenseText": "#\nAuth vers :...",
  "licenseState": {
    "vendor": "F5 Networks, Inc.",
    "licensedDateTime": "2017-02-17T00:00:00-08:00",
    "licensedVersion": "5.2.0",
    "evaluationStartDateTime": "2017-02-16T00:00:00-08:00",
    "evaluationEndDateTime": "2017-03-20T00:00:00-07:00",
    "licenseEndDateTime": "2017-03-20T00:00:00-07:00",
    "licenseStartDateTime": "2017-02-16T00:00:00-08:00",
    "registrationKey": "R8573-25996-57909-24167-3331348",
    "platformId": "BIG-IQ Pool",
    "authVers": "5b",
    "serviceCheckDateTime": "2017-02-17T00:00:00-08:00",
    "exclusivePlatform": [
      "BIG-IQ Pool"
    ],
    "featureFlags": [
      {
        "featureName": "gtm_rate_fallback",
        "featureValue": "1000"
      },
      ...
  },
  ...
}
```

#### 5. Complete automatic activation by accepting the EULA
Echo the EULA text back to the license endpoint to agree to the EULA and complete the automatic activation workflow.

```
PATCH https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/ae74294e-f3f2-4ad3-86bc-ab3fdb5dfe4c
```
Request:
```
{
  "eulaText": "END USER LICENSE AGREEMENT\r\nDOC-0355-08\r\n\r\nIMPORTANT - READ BEFORE...",
  "state":"ACCEPTED_EULA"
}
```

After the PATCH completes, poll the license (step 3) until it reaches the LICENSED state.

Response:
```
{
  "state": "LICENSED",
  "totalDeviceLicenses": 25,
  "freeDeviceLicenses": 25,
  "licenseText": "#\nAuth vers :...",
  "licenseState": {
    "vendor": "F5 Networks, Inc.",
    "licensedDateTime": "2017-02-17T00:00:00-08:00",
    "licensedVersion": "5.2.0",
    "evaluationStartDateTime": "2017-02-16T00:00:00-08:00",
    "evaluationEndDateTime": "2017-03-20T00:00:00-07:00",
    "licenseEndDateTime": "2017-03-20T00:00:00-07:00",
    "licenseStartDateTime": "2017-02-16T00:00:00-08:00",
    "registrationKey": "R8573-25996-57909-24167-3331348",
    "platformId": "BIG-IQ Pool",
    "authVers": "5b",
    "serviceCheckDateTime": "2017-02-17T00:00:00-08:00",
    "exclusivePlatform": [
      "BIG-IQ Pool"
    ],
    "featureFlags": [
      {
        "featureName": "gtm_rate_fallback",
        "featureValue": "1000"
      },
      ...
  },
  ...
}
```

#### 6. Complete manual activation by providing license text
If manual activation was used in step 2, then using license text received from the F5 licensing web portal, submit the following request to complete the manual activation workflow.

```
PATCH https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/ae74294e-f3f2-4ad3-86bc-ab3fdb5dfe4c
```
Request:
```
{
  "licenseText": "..."
}
```

Response:
```
{
  "state": "LICENSED",
  "totalDeviceLicenses": 25,
  "freeDeviceLicenses": 25,
  "licenseText": "#\nAuth vers :...",
  "licenseState": {
    "vendor": "F5 Networks, Inc.",
    "licensedDateTime": "2017-02-17T00:00:00-08:00",
    "licensedVersion": "5.2.0",
    "evaluationStartDateTime": "2017-02-16T00:00:00-08:00",
    "evaluationEndDateTime": "2017-03-20T00:00:00-07:00",
    "licenseEndDateTime": "2017-03-20T00:00:00-07:00",
    "licenseStartDateTime": "2017-02-16T00:00:00-08:00",
    "registrationKey": "R8573-25996-57909-24167-3331348",
    "platformId": "BIG-IQ Pool",
    "authVers": "5b",
    "serviceCheckDateTime": "2017-02-17T00:00:00-08:00",
    "exclusivePlatform": [
      "BIG-IQ Pool"
    ],
    "featureFlags": [
      {
        "featureName": "gtm_rate_fallback",
        "featureValue": "1000"
      },
      ...
  },
  ...
}
```

#### 7. Delete a purchased pool license
```
DELETE https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/ae74294e-f3f2-4ad3-86bc-ab3fdb5dfe4c
```

### API Reference
