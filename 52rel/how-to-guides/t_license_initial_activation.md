## Licensing Initial Activation API

### Overview
The Initial Activation API provides a common starting point for activating all pool-style licenses (Purchased Pool, Utility, Volume, and FPS licenses).  You can use the API to perform the initial activation of the top-level pool and any offerings it may include.  The API helps to avoid having know the type of particular registration key and which API should be used to activate it.

1. For automatic activation, the system gets the license text from the F5 license server. For manual activation, the API provides a dossier, which you can use to acquire license text from the F5 licensing web portal.
2. The API uses the license text to determine the type of license and with that, it creates an entry in the appropriate license collection. For instance, a purchased pool license registration key will result in an entry in `cm/device/licensing/pool/purchased-pool/licenses`.
3. For automatic activation, the API waits for the activation process to finish in the specific collection. This is typically a multi-step process, as each offering needs to be activated.
4. For manual activation, the process is more involved. As with automatic activation, an item will be created in the relevant license collection, but activation of any offerings must be completed via that license collection's API.

### Prerequisites
Make certain that the following prerequisites have been met.

- The BIG-IQ Centralized Management device is operational, has completed the setup wizard, and completed any other needed configuration.
- The BIG-IQ has an internet connection to the F5 licensing server if you plan to use automatic activation.
- You have either the administrator or device manager role.

Note: When you perform these tasks using the example code provided, review the listed IP addresses and change them as appropriate for your environment. For example, if you are not running the script directly on the BIG-IQ device, change localhost to be the IP address of the BIG-IQ Centralized Management device.


#### 1. Start activation of a license
There are three methods to activate a license: automatic, manual and closed-circuit network (CCN).  An example of an starting an automatic activation is shown here.  For manual activation, set `status` to `ACTIVATING_MANUAL`.  CCN activation requires opening a support case with F5.

Replace MY-REGISTRATION-KEY in this example with your actual registration key.
```
POST https://localhost/mgmt/cm/device/licensing/pool/initial-activation
```
Request:
```
{
  "regKey": "MY-REGISTRATION-KEY",
  "name": "my own freeform name",
  "status": "ACTIVATING_AUTOMATIC"
}
```

Response:
```
{
  "regKey": "MY-REGISTRATION-KEY",
  "sortName": "Pending",
  "publicKey": [
    -84,
    1,
    -48,
    ...
  ],
  "internalPrivateKey": "UAYLtswdQo...",
  "encryptedPrivateKey": [
    -125,
    -3,
    103,
    ...
  ],
  "name": "my own freeform name",
  "message": "Automatic activation in progress",
  "dossier": "60b0eaaa7q...",
  "status": "ACTIVATING_AUTOMATIC",
  "generation": 1,
  "lastUpdateMicros": 1488929240559574,
  "kind": "cm:device:licensing:pool:initial-activation:initialactivationworkeritemstate",
  "selfLink": "https://localhost/mgmt/cm/device/licensing/pool/initial-activation/MY-REGISTRATION-KEY"
}
```

#### 2. Poll to get status
After initiating an activation, you should poll to check the activation status.
```
GET https://localhost/mgmt/cm/device/licensing/pool/initial-activation/MY-REGISTRATION-KEY
```

Response:
```
{
  "eulaText": "END USER LICENSE AGREEMENT\r\nDOC-0355-08\r\n\r\nIMPORTANT - READ BEFORE...",
  "message": "Accept EULA to continue",
  "status": "ACTIVATING_AUTOMATIC_NEED_EULA_ACCEPT",
  ...
}
```

#### 3. Complete automatic activation by accepting the EULA
Echo the EULA text back to the license endpoint to agree to the EULA and complete the automatic activation workflow.

After doing so, again poll to get the final activation status (either `READY` or `ACTIVATION_FAILED`).
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/initial-activation/MY-REGISTRATION-KEY
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

#### 4. Complete manual activation by providing license text
If manual activation is used instead of automatic activation, then the PATCH to complete activation will include the license text received from the F5 licensing web portal.

Similar to automatic activation, you will need to poll to get the final activation status.
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/initial-activation/MY-REGISTRATION-KEY
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
  "message": "Regkey MY-REGISTRATION-KEY activated - populating collection",
  "status": "ACTIVATING_MANUAL_LICENSE_TEXT_PROVIDED",
  ...
}
```

#### 5. Retry a failed activation
If an activation fails, check error messages returned from the API or the restjavad logs for details.

Similar to the prior steps, you will need to poll to get the final activation status.
```
PATCH https://localhost/mgmt/cm/device/licensing/pool/initial-activation/MY-REGISTRATION-KEY
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

#### 6. Remove a failed activation
If desired, you can remove a failed activation attempt.
```
DELETE https://localhost/mgmt/cm/device/licensing/pool/initial-activation/MY-REGISTRATION-KEY
```

#### 7. Confirm license is ready
After completing the initial activation process, the `status` will be `READY` and the API will provide a reference to the created license.  Depending on the license type, activation of any offerings will still be required when using manual activation.  Those activations will occur via the API endpoint noted in the reference.  Purchased pool licenses do not require this additional step.
```
GET https://localhost/mgmt/cm/device/licensing/pool/initial-activation/MY-REGISTRATION-KEY
```

Response:
```
{
  "licenseReference": {
    "link": "https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}"
  },
  "status": "READY",
  ...
}
```

Following the reference to the new license:
```
GET {endpoint noted in licenseReference}
```

Response:
```
{
  "state": "LICENSED",
  "totalDeviceLicenses": 25,
}
```

### API Reference