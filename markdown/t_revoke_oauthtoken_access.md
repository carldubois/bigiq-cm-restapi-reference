## OAuth Token Revocation on BIG-IP devices using a BIG-IQ Centralized Management system

### Overview
You can use the REST API to revoke OAuth Tokens on one or more BIG-IP devices on a BIG-IQ Centralized Management system.

### Prerequisites
You should be sure the following prerequisites have been met.
- All BIG-IP devices are operational and have the services provisioned that will be managed by the BIG-IQ Centralized Management system.
- The BIG-IQ Centralized Management system is operational, has completed the setup wizard, and completed any other needed configuration.
- Trust has been established between the BIG-IP device and the BIG-IQ Centralized Management system.
- APM Service is discovered for the BIG-IP device in BIG-IQ Centralized Management system.
- APM Configuration is imported, if access group name needs to be used as input criteria.
- To revoke oauth tokens using device reference of an BIG-IP device that is part of cluster, except for revoke list of tokens action, it is recommended to use cluster name instead of device references. If you have to use device reference, then  device reference of the ACTIVE device of cluster should be used for the token revocation API to work. If device reference of PASSIVE device is passed as input, the task may finish, but API will not be able to send additional warning or error in the response. ACTIVE device has to only manually identified by the user, as currently there is no way to determine this information through API and BIG-IQ UI.
- When performing the tasks in this example, review the listed IP addresses and change them as appropriate for your environment. For example, if you are not running  the script directly on the BIG-IQ system, you should change localhost to be the IP address of the BIG-IQ Centralized Management system.

### Description
You use the following process to Revoke OAuth Tokens on BIG-IP devices on the BIG-IQ Centralized Management system.
1. Perform a GET method on the machineid-resolver URI to determine the current state of the BIG-IP device and get other inputs parameters to revoke oauth tokens.
2. Perform a POST method on the revoke oauth tokens task URI to revoke oauth tokens.
3. Monitor the task using GET methods until the status has reached a value of FINISHED, FAILED or CANCELLED. When the GET method status value is FINISHED and the currentStep value is DONE, the revoke oauth tokens is completed.

### Example for OAuth Token Revocation
In the following example:
- The BIG-IP device address is 10.255.4.124. You substitute your BIG-IP device’s address for this address when you implement the example. If the device that you want to use is part of cluster, refer to prerequisites section for more details.
- The Access Config Group names are TestGroup,TestGroup1,TestGroup2. You substitute your access group name when you implement the example.
- The BIG-IP cluster name is BlueCluster,RedCluster. You substitute your cluster name when you implement the example.

#### 1. Determine the current status of the BIG-IP device and other input parameters on the BIG-IQ Centralized Management system.
Perform a GET method on the machineid-resolver URI to determine if the BIG-IP device already has trust established. You will want to use the filter option to narrow the returned JSON information to just this particular BIG-IP device. If the value of the items element is not an empty list [], then the trust has already been established. If the value of the items element is an empty list, you must establish trust before you can attempt to discover the device.

```
GET: https://<mgmtip>/mgmt/cm/system/machineid-resolver?$filter=('address'+eq+'10.255.4.124')
```

To filter more than one address, you can use below kind of filter with multiple checks on the URI
```
$filter=('address' eq '10.255.4.1' or 'address' eq '10.255.4.2' )
```

The following is the response JSON from the GET method:
```
{
    "uuid": "98901455-6384-47cd-bc41-00a39dfe338f",
    "deviceUri": "https://10.192.123.69:443",
    "machineId": "98901455-6384-47cd-bc41-00a39dfe338f",
    "state": "ACTIVE",
	"address": "10.255.4.124",
	"httpsPort": 443,
	"hostname": "bluebigipveha1.labf.com",
    "version": "12.1.0",
    "product": "BIG-IP",
    "edition": "Final",
    "build": "0.0.1354",
    "restFrameworkVersion": "12.1.0-0.0.1354",
    "managementAddress": "10.192.123.69",
    "mcpDeviceName": "/Common/bluebigipveha1",
    "trustDomainGuid": "5189f81c-96be-4449-b4110050560102e7",
    "properties": {
        "cm:gui:module": [
            "Access",
            "BigIPDevice",
            "adc"
        ],
        "modules": [
            "All Access managed BIG-IP devices"
        ],
        "cm-adccore-allbigipDevices": {
            "supportsBadgerEnhs": true,
            "supportsRest": true,
            "supportsAlpineEnhs": true,
            "lastDiscoveredDateTime": "2016-11-10T19:06:14.804Z",
            "imported": true,
            "clusterName": "BlueCluster",
            "restrictsPortTranslationStatelessVirtual": true,
            "requiresDhcpProfileInDhcpVirtualServer": true,
            "importStatus": "FINISHED",
            "discoveryStatus": "FINISHED",
            "importedDateTime": "2016-11-10T19:14:39.003Z",
            "lastUserDiscoveredDateTime": "2016-11-10T19:06:14.804Z",
            "modules": [
                "All Access managed BIG-IP devices"
            ],
            "cm:gui:module": [
                "Access",
                "BigIPDevice",
                "adc"
            ],
            "discovered": true,
            "supportsClassification": true
        },
        "cm-bigip-allBigIpDevices": {
            "shared:resolver:device-groups:discoverer": "d5d58cdd-f5b5-4379-9d12-08e28253a16f",
            "cm:gui:module": [
                "BigIPDevice"
            ],
            "modules": []
        },
        "cm-bigip-allDevices": {
            "shared:resolver:device-groups:discoverer": "d5d58cdd-f5b5-4379-9d12-08e28253a16f",
            "cm:gui:module": [],
            "modules": []
        },
        "cm-access-allBigIpDevices": {
            "discovered": true,
            "imported": true,
            "clusterName": "BlueCluster",
            "supportsRest": true,
            "supports_13_0_Enhs": false,
            "supportsCascadeEnhs": true,
            "lastDiscoveredDateTime": "2016-11-10T19:15:18.963Z",
            "lastUserDiscoveredDateTime": "2016-11-10T19:15:18.963Z",
            "cm:access:access-group-name": "TestGroup",
            "cm:access:source-device": true,
            "cm:access:access-group-device-link": "https://localhost/mgmt/shared/resolver/device-groups/CA/devices/98901455-6384-47cd-bc41-00a39dfe338f",
            "cm:access:import-version": "12.1.0",
            "cm:access:access-group-link": "https://localhost/mgmt/shared/resolver/device-groups/TestGroup",
            "importedDateTime": "2016-11-10T19:17:04.459Z",
            "discoveryStatus": "FINISHED",
            "importStatus": "FINISHED",
            "cm:gui:module": [
                "Access"
            ],
            "modules": [
                "All Access managed BIG-IP devices"
            ]
        },
        "cm-bigip-cluster_BlueCluster": {
            "clusterName": "BlueCluster",
            "shared:resolver:device-groups:discoverer": "da4a4ca7-19f9-4a31-a1c2-004d5557ff10",
            "cm:gui:module": [],
            "modules": []
        },
        "cm-access-allDevices": {
    		"clusterName": "BlueCluster",
            "cm:gui:module": [
                "Access"
            ],
            "modules": [
                "All Access managed BIG-IP devices"
            ]
        },
        "TestGroup": {
            "discovered": true,
            "imported": false,
            "supportsRest": true,
            "supports_13_0_Enhs": false,
            "supportsCascadeEnhs": true,
            "discoveryStatus": "FINISHED",
            "lastDiscoveredDateTime": "2016-10-26T04:15:56.356Z",
            "lastUserDiscoveredDateTime": "2016-10-26T04:15:56.356Z",
            "cm:access:all-bigip-device-link": "https://localhost/mgmt/shared/resolver/device-groups/cm-access-allBigIpDevices/devices/98901455-6384-47cd-bc41-00a39dfe338f",
            "cm:access:import-version": "12.1.0",
            "cm:access:source-device": true,
            "cm:gui:module": [
                "Access"
            ],
            "modules": [
                "All Access managed BIG-IP devices"
            ]
        },
        "cm-adccore-allDevices": {
            "cm:gui:module": [],
            "modules": []
        }
    },
    "isClustered": false,
    "isVirtual": true,
    "isLicenseExpired": false,
    "slots": [
        {
            "volume": "HD1.1",
            "product": "BIG-IP",
            "version": "12.1.0",
            "build": "0.0.1354",
            "isActive": true
        },
        {
            "volume": "HD1.3",
            "product": "BIG-IP",
            "version": "12.0.0",
            "build": "0.0.606",
            "isActive": false
        }
    ],
    "generation": 67,
    "lastUpdateMicros": 1479332833705505,
    "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
    "selfLink": "https://localhost/mgmt/cm/system/machineid-resolver/98901455-6384-47cd-bc41-00a39dfe338f"
}
```

##### 1.1. Check if Trust is established.
In the response to the GET method, you see trust is established since the following data is found in the list:
```
"properties": {
    "cm:gui:module": [
        "BigIPDevice"
    ]
```

##### 1.2. Check if Access Discovery is done.
In the response to the GET method, if the Access value is found in the list, the Access Policy Manager service has already been discovered; the adc value represents the Local Traffic service and this must be found in order to continue with the Access Policy Manager discovery workflow.

```
"properties": {
    "cm:gui:module": [
        "BigIPDevice",
        "adc",
        "Access"
    ]
```

##### 1.3. Check if Access Configuration is Imported
In the response to the GET method, you see access import is done if value of imported property is true in cm-access-allBigIpDevices:

```
"properties": {
    "cm-access-allBigIpDevices": {
        "imported": true
    }
}
```

##### 1.4. Find Access Config Group Name of the device:
This is applicable only if the device is imported. In the response to the GET method, value of cm:access:access-group-name property contains the access group name. This property is present in cm-access-allBigIpDevices, which is present inside properties field value. In this example, access group name is TestGroup:

```
"properties": {
    "cm-access-allBigIpDevices": {
        "cm:access:access-group-name": "TestGroup"
    }
}
```


##### 1.5. Find Cluster Name of an device that is part of Cluster:
This is applicable only if the device is discovered and part of cluster. To token revocation in an device which is part of cluster, it is recommended to use cluster name instead of device reference.

In the response to the GET method, value of clusterName property contains the cluster name. This property is present in cm-access-allBigIpDevices, which is present inside properties field value. In this example, cluster name is BlueCluster:

```
"properties": {
    "cm-access-allBigIpDevices": {
        "clusterName": "BlueCluster"
    }
}
```

##### 1.6. Find machine id and device reference of an device:
In the response to the GET method, value of machineId and selfLink is the machine id and device reference of the device.

```
{
	"selfLink": "https://localhost/mgmt/cm/system/machineid-resolver/98901455-6384-47cd-bc41-00a39dfe338f"
}
```

##### 1.7. List All Client Id's of OAuth Client App for given machine id:
To get list of all oauth client app info containing client id, perform following GET on oauth client app API with filter to retrieve only client apps for the machine id of the given device (refer to section 1.6 to get machine id of an device). In the response, clientId refers to client id of the oauth client app.

When using below URI, replace 26a65814-a2f4-4e91-9853-13e2e14d921a with your machine id value. $select query could be modified to add/remove required fields in the response.

```
GET: https://<mgmtip>/mgmt/cm/access/working-config/apm/oauth/oauth-client-app?$filter='lsoDeviceReference/machineId' eq '26a65814-a2f4-4e91-9853-13e2e14d921a'&$select=appName,name,clientId
```

The following is the response JSON containing list of client apps from the GET method:
```
{
    "selfLink": "https://localhost/mgmt/cm/access/working-config/apm/oauth/oauth-client-app",
    "totalItems": 2,
    "items": [
        {
            "appName": "Shutterfly",
            "clientId": "89923892aed8eb142a8871058da9005056b09ae221df6a57",
            "name": "shutterfly-client"
        },
        {
            "appName": "Maps",
            "clientId": "5b3e8851b1d872feed3086484141005056b09ae2d5277c57",
            "name": "maps-client"
        }
    ],
    "generation": 7,
    "kind": "cm:access:working-config:apm:oauth:oauth-client-app:oauthclientappcollectionstate",
    "lastUpdateMicros": 1478208069057233
}
```

##### 1.8. List All Access Config Groups:
To get list of all access config group name, perform following GET on device groups resolver API with filter to retrieve only access config group. In the response, groupName refers to access config group name.

```
GET: https://<mgmtip>/mgmt/shared/resolver/device-groups/?$filter='properties/cm:access:access_group'+eq+'true'&$select=groupName,displayName
```

The following is the response JSON from the GET method:
```
{
    "selfLink": "https://localhost/mgmt/shared/resolver/device-groups",
    "totalItems": 1,
    "items": [
        {
            "displayName": "TestGroup",
            "groupName": "TestGroup"
        },
        {
            "displayName": "TestGroup2",
            "groupName": "TestGroup2"
        }
    ],
    "generation": 23,
    "kind": "shared:resolver:device-groups:devicegroupcollectionstate",
    "lastUpdateMicros": 1479942921954266
}
```

Repeat steps in Section 1.1 to 1.7 for the all the devices you want to use. The device reference, access group name and cluster name from the response JSON in this step will be used in Step 2.

#### 2. Perform a POST method on the revoke oauth tokens task URI to revoke oauth tokens.
Different ways to revoke oauth tokens is listed below.

Use a POST method with the following JSON on the revoke oauth tokens task to start the task.

Parameter | Description | Required
----------------------------------------| --------------------------------------------------
action | action value has to be REVOKE_TOKEN_FOR_USER, REVOKE_TOKEN_FOR_CLIENT_ID or REVOKE_LIST_OF_TOKENS | Yes
deviceReferences | list of device references |
accessGroupNames | list of access config group names |
clusterNames | list of cluster names |
userName | Case sensitive field name. user name of user whose tokens needs to be revoked.| Only if action is REVOKE_TOKEN_FOR_USER
perDeviceOauthIds | list of one or more oauth id info object, with each object containing device reference and list of pair of id(oauth id) and clientId| Only if action is REVOKE_LIST_OF_TOKENS
status | As part of response, status denotes the status of the task. It can be STARTED, FINISHED, FAILED, CANCELLED or CANCEL_REQUESTED |
result | As part of response, result denotes whether oauth tokens revocation action was COMPLETE or FAILED |
resultDetails | As part of response, on some cases during failure, this is populated with list of device level failure info containing oauth id info |
errorMessage | This can contain error message during failure |

##### 2.1 Revoke All OAuth Tokens for a User
You can revoke all oauth tokens of a user on one or more BIG-IP devices that matches one or more input criteria specified below.

###### 2.1.1 Revoke All OAuth Tokens for a User in BIG-IP devices matching one or more Device Reference
To use this action, you need to manually determine the username of the user.

Note: To revoke oauth tokens in an device that is part of cluster, then it is recommended to use cluster name instead of device references. Refer to prerequisites section for more details.

```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_TOKEN_FOR_USER",
   "userName":"user1",
   "deviceReferences":[
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      }
   ]
}
```
The following is the response JSON from the previous POST method:
```
{
  "action": "REVOKE_TOKEN_FOR_USER",
  "currentStep": "RESOLVE_DEVICES",
  "deviceReferences": [
    {
      "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
    }
  ],
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "status": "STARTED",
  "userName": "user1",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

###### 2.1.2 Revoke All OAuth Tokens for a User in BIG-IP devices matching one or more Access config groups

```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_TOKEN_FOR_USER",
   "userName":"user1",
   "accessGroupNames":[
      "TestGroup1",
      "TestGroup2"
   ]
}
```
The following is the response JSON from the previous POST method:
```
{
  "action": "REVOKE_TOKEN_FOR_USER",
  "currentStep": "RESOLVE_DEVICES",
   "accessGroupNames":[
      "TestGroup1",
      "TestGroup2"
   ],
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "status": "STARTED",
  "userName": "user1",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

###### 2.1.3 Revoke All OAuth Tokens for a User in BIG-IP devices matching one or more BIG-IP clusters

```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_TOKEN_FOR_USER",
   "userName":"user1",
   "clusterNames":[
      "BlueCluster",
      "RedCluster"
   ]
}
```
The following is the response JSON from the previous POST method:
```
{
  "action": "REVOKE_TOKEN_FOR_USER",
  "currentStep": "RESOLVE_DEVICES",
   "clusterNames":[
      "BlueCluster",
      "RedCluster"
   ],
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "status": "STARTED",
  "userName": "user1",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

###### 2.1.4 Revoke All OAuth Tokens for a User in BIG-IP devices matching one or more BIG-IP clusters, one or more Access config groups and  one or more device references

```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_TOKEN_FOR_USER",
   "userName":"user1",
   "accessGroupNames":[
      "TestGroup1",
      "TestGroup2"
   ],
   "clusterNames":[
      "BlueCluster",
      "RedCluster"
   ],
   "deviceReferences": [
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      },
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
      }
  ]
}
```
The following is the response JSON from the previous POST method:
```
{
  "action": "REVOKE_TOKEN_FOR_USER",
  "currentStep": "RESOLVE_DEVICES",
   "accessGroupNames":[
      "TestGroup1",
      "TestGroup2"
   ],
   "clusterNames":[
      "BlueCluster",
      "RedCluster"
   ],
   "deviceReferences": [
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      },
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
      }
  ],
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "userName": "user1",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

##### 2.2 Revoke All OAuth Tokens for given Client Id
You can revoke all oauth tokens for given client id in one or more BIG-IP devices that matches one or more input criteria specified below.

###### 2.2.1 Revoke All OAuth Tokens for given Client Id in BIG-IP devices matching one or more Device Reference

Mostly it suffices to provide one device reference as input, as Client id is unique per device for an oauth client app, so its not common to have same client id in more than one device.

Note: To revoke oauth tokens in an device that is part of cluster, then it is recommended to use cluster name instead of device reference. Refer to example in next section. If that is not possible then device reference of ACTIVE device of cluster should be used for the API to work. Refer to prerequisites section for more details.

```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_TOKEN_FOR_CLIENT_ID",
   "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
   "deviceReferences":[
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      }
   ]
}
```
The following is the response JSON from the previous POST method:
```
{
   "action":"REVOKE_TOKEN_FOR_CLIENT_ID",
   "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
  "currentStep": "RESOLVE_DEVICES",
  "deviceReferences": [
    {
      "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
    }
  ],
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "status": "STARTED",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

###### 2.2.2 Revoke All OAuth Tokens for given Client Id in BIG-IP devices matching one or more Access config groups
```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_TOKEN_FOR_CLIENT_ID",
   "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
   "accessGroupNames":[
      "TestGroup1",
      "TestGroup2"
   ]
}
```

The following is the response JSON from the previous POST method:
```
{
   "action":"REVOKE_TOKEN_FOR_CLIENT_ID",
   "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
   "accessGroupNames":[
      "TestGroup1",
      "TestGroup2"
   ],
  "currentStep": "RESOLVE_DEVICES",
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "status": "STARTED",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

###### 2.2.3 Revoke All OAuth Tokens for given Client Id in one or more BIG-IP clusters
```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_TOKEN_FOR_CLIENT_ID",
   "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
   "clusterNames":[
      "BlueCluster",
      "RedCluster"
   ]
}
```

The following is the response JSON from the previous POST method:
```
{
   "action":"REVOKE_TOKEN_FOR_CLIENT_ID",
   "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
   "clusterNames":[
      "BlueCluster",
      "RedCluster"
   ],
  "currentStep": "RESOLVE_DEVICES",
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "status": "STARTED",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

###### 2.2.4 Revoke All OAuth Tokens for given Client Id in BIG-IP devices matching one or more BIG-IP clusters, one or more Access config groups and  one or more device references
```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_TOKEN_FOR_CLIENT_ID",
   "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
   "accessGroupNames":[
      "TestGroup1",
      "TestGroup2"
   ],
   "clusterNames":[
      "BlueCluster",
      "RedCluster"
   ],
   "deviceReferences": [
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      },
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
      }
  ]
}
```

The following is the response JSON from the previous POST method:
```
{
   "action":"REVOKE_TOKEN_FOR_CLIENT_ID",
   "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
   "accessGroupNames":[
      "TestGroup1",
      "TestGroup2"
   ],
   "clusterNames":[
      "BlueCluster",
      "RedCluster"
   ],
   "deviceReferences": [
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      },
      {
         "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
      }
  ],
  "currentStep": "RESOLVE_DEVICES",
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "status": "STARTED",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

##### 2.3 Revoke List of OAuth Tokens in BIG-IP devices for one or more Device Reference

Note:
* If the input device reference is part of cluster, then device reference of ACTIVE device of cluster should be used in this action, for the API to work. If device reference of PASSIVE device is passed as input, the task may finish, but API will not be able to send additional warning or error in the response. Refer to prerequisites section for more details.
* OAuth id's that has to be revoked, need to be manually determined, currently there is no API support to list session information. In BIG-IQ UI, token information can be found in Monitoring tab under Dashboards & Reports->Access->OAuth->Tokens. If OAuth Id column is not visible, it needs to be selected in Grid Settings on top left most corner of the tokens table.

```
POST:  https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens
{
   "action":"REVOKE_LIST_OF_TOKENS",
   "perDeviceOauthIds": [
    {
      "oauthIds": [
        {
          "id": "da6d57ffab9decbe9d75b7fdd4440ad43bedc7a475f3105b",
          "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
        },
        {
          "id": "0df998ae62ace6fb6a82bb745b8586e7306afb94e3ca146a",
          "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
        }
      ],
      "deviceReference": {
        "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      }
    },
    {
      "oauthIds": [
        {
          "id": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
          "clientId": "bb745b8586e7306afb94"
        },
        {
          "id": "8586e7306afb8586e7306afb8586e7306afb",
          "clientId": "8ad92cbb970dd500"
        }
      ],
      "deviceReference": {
        "link":"https://localhost/mgmt/cm/system/machineid-resolver/23h4jkhk324-f405-489f-kj3434-98234"
      }
    }
  ]
}
```

The following is the response JSON from the previous POST method:
```
{
   "action":"REVOKE_LIST_OF_TOKENS",
   "perDeviceOauthIds": [
    {
      "oauthIds": [
        {
          "id": "da6d57ffab9decbe9d75b7fdd4440ad43bedc7a475f3105b",
          "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
        },
        {
          "id": "0df998ae62ace6fb6a82bb745b8586e7306afb94e3ca146a",
          "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
        }
      ],
      "deviceReference": {
        "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      }
    },
    {
      "oauthIds": [
        {
          "id": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
          "clientId": "bb745b8586e7306afb94"
        },
        {
          "id": "8586e7306afb8586e7306afb8586e7306afb",
          "clientId": "8ad92cbb970dd500"
        }
      ],
      "deviceReference": {
        "link":"https://localhost/mgmt/cm/system/machineid-resolver/23h4jkhk324-f405-489f-kj3434-98234"
      }
    }
  ],
  "currentStep": "RESOLVE_DEVICES",
  "generation": 7,
  "id": "5b688828-2279-40b0-9dc1-eccdebb6837f",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733104269292,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f",
  "startDateTime": "2016-09-12T19:18:23.451-0700",
  "status": "STARTED",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

#### 3. Perform additional GET methods to the revoke oauth tokens task created in Step 2.
Perform additional GET methods on the selfLink returned from the Step 2 response JSON. Perform them in a loop until the status reaches one of the following: FINISHED, CANCELLED or FAILED. Use a select option to reduce the content of the returned JSON to a manageable amount. In addition to the status, result should have the value of COMPLETE.

For a task to be successful,response should have values of status as FINISHED and result as COMPLETE.

Note: Replace below URI with selfLink from json response or replace 5b688828-2279-40b0-9dc1-eccdebb6837f in below URI with id from json response.

To get select fields in the response use below query
```
GET: https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f?$select=status,result,errorMessage
```

To get complete response use below query
```
GET: https://<mgmtip>/mgmt/cm/access/tasks/revoke-tokens/5b688828-2279-40b0-9dc1-eccdebb6837f
```

##### 3.1 Sample of Successful Response
The following is an sample successful response JSON from the GET method:
```
{
  "action": "REVOKE_TOKEN_FOR_CLIENT_ID",
  "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
  "currentStep": "DONE",
  "deviceReferences": [
    {
      "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
    }
  ],
  "endDateTime": "2016-09-12T19:18:56.027-0700",
  "generation": 7,
  "id": "9ae2bf8a-a53b-4f4e-b012-8b7c5df56a73",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733136078468,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "result": "COMPLETE",
  "resultDetails": [],
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/9ae2bf8a-a53b-4f4e-b012-8b7c5df56a73",
  "startDateTime": "2016-09-12T19:18:54.861-0700",
  "status": "FINISHED",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

##### 3.2 Sample of Failed Response
The following is sample of failed task response JSON from the GET method:
```
{
  "action": "REVOKE_LIST_OF_TOKENS",
  "currentStep": "REVOKE_TOKENS_FOR_STANDALONE",
  "endDateTime": "2016-09-12T19:19:26.794-0700",
  "errorMessage": "Tokens not found in index. Possibly already revoked tokens.",
  "generation": 6,
  "id": "56a6994d-06b7-4085-b93d-29c489c805c5",
  "identityReferences": [
    {
      "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
  ],
  "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
  "lastUpdateMicros": 1473733166845546,
  "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
  "perDeviceOauthIds": [
    {
      "oauthIds": [
        {
          "id": "da6d57ffab9decbe9d75b7fdd4440ad43bedc7a475f3105b",
          "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
        },
        {
          "id": "0df998ae62ace6fb6a82bb745b8586e7306afb94e3ca146a",
          "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
        }
      ],
      "deviceReference": {
        "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      }
    }
  ],
  "result": "FAILED",
  "resultDetails": [
    {
      "failedIds": [
        {
          "id": "0df998ae62ace6fb6a82bb745b8586e7306afb94e3ca146a",
          "dbInstance": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
          "clientId": ""
        },
        {
          "id": "da6d57ffab9decbe9d75b7fdd4440ad43bedc7a475f3105b",
          "dbInstance": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
          "clientId": ""
        }
      ],
      "deviceReference": {
        "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
      }
    }
  ],
  "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/56a6994d-06b7-4085-b93d-29c489c805c5",
  "startDateTime": "2016-09-12T19:19:26.509-0700",
  "status": "FAILED",
  "userReference": {
    "link": "https://localhost/mgmt/shared/authz/users/admin"
  },
  "username": "admin"
}
```

### Common Errors
When an error occurs, review the BIG-IQ Centralized Management user interface for device management to determine the details of the failure. In addition to using the user interface, some error information can be determined from the REST API response JSON as shown in the following error.

#### Error generated when an incorrect URI is sent in the REST request.
```
{
  "code": 404,
  "message": "Public URI path not registered",
  "referer": "192.168.101.130",
  "restOperationId": 19541801,
  "errorStack": [
    "com.f5.rest.common.RestWorkerUriNotFoundException: Public URI path not registered",
    "at com.f5.rest.workers.ForwarderPassThroughWorker.cloneAndForwardRequest(ForwarderPassThroughWorker.java:250)",
    "at com.f5.rest.workers.ForwarderPassThroughWorker.onForward(ForwarderPassThroughWorker.java:106)",
    "at com.f5.rest.workers.ForwarderPassThroughWorker.onQuery(ForwarderPassThroughWorker.java:409)",
    "at com.f5.rest.common.RestWorker.callDerivedRestMethod(RestWorker.java:1071)",
    "at com.f5.rest.common.RestWorker.callRestMethodHandler(RestWorker.java:1040)",
    "at com.f5.rest.common.RestServer.processQueuedRequests(RestServer.java:1467)",
    "at com.f5.rest.common.RestServer.access$000(RestServer.java:53)",
    "at com.f5.rest.common.RestServer$1.run(RestServer.java:333)",
    "at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)",
    "at java.util.concurrent.FutureTask.run(FutureTask.java:262)",
    "at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.access$201(ScheduledThreadPoolExecutor.java:178)",
    "at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(ScheduledThreadPoolExecutor.java:292)",
    "at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)",
    "at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)",
    "at java.lang.Thread.run(Thread.java:745)\n"
  ],
  "kind": ":resterrorresponse"
}
```

#### Task failure when action is not provided.
Task creation will not happen, when required data is missing in the input JSON during POST. Due to this reason, you will not see id or selfLink in the response for validation failures.

```
{
    "code": 400,
    "message": "action is missing",
    "originalRequestBody": "{\"id\":\"e8f92ff2-0367-4393-b79f-ea91147c71ac\",\"status\":\"CREATED\",\"name\":\"revoke-oauth-tokens\",\"generation\":1,\"lastUpdateMicros\":1480715155144821,\"kind\":\"cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate\",\"selfLink\":\"https://localhost/mgmt/cm/access/tasks/revoke-tokens/e8f92ff2-0367-4393-b79f-ea91147c71ac\"}",
    "referer": "192.168.85.74",
    "restOperationId": 5541817,
    "kind": ":resterrorresponse"
}
```

#### Task failure when required input is not available.
```
{
    "code": 400,
    "message": "Request should have atleast one of these fields populated: accessGroupNames , clusterNames , machineIds ",
    "originalRequestBody": "{\"action\":\"REVOKE_TOKEN_FOR_CLIENT_ID\",\"perDeviceOauthIds\":[{\"deviceReference\":{\"link\":\"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642\"}}],\"id\":\"0bd7f801-2b83-46ec-a953-2464b9a5aada\",\"status\":\"CREATED\",\"name\":\"revoke-oauth-tokens\",\"generation\":1,\"lastUpdateMicros\":1480723471881889,\"kind\":\"cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate\",\"selfLink\":\"https://localhost/mgmt/cm/access/tasks/revoke-tokens/0bd7f801-2b83-46ec-a953-2464b9a5aada\"}",
    "referer": "192.168.85.74",
    "restOperationId": 5898985,
    "kind": ":resterrorresponse"
}
```

#### Task failure when for given input, there is no matching devices for non-existing or invalid (device reference or access group or cluster names)
```
{
    "accessGroupNames": [
        "TestGroup1",
        "TestGroup2",
        null
    ],
    "action": "REVOKE_TOKEN_FOR_CLIENT_ID",
    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
    "clusterNames": [
        "BlueCluster",
        "RedCluster"
    ],
    "currentStep": "RESOLVE_DEVICES",
    "deviceReferences": [
        {
            "link": "https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
        }
    ],
    "endDateTime": "2016-12-02T13:57:54.644-0800",
    "errorMessage": "No matching device(s) found for given accessGroup or cluster or deviceReference list.",
    "failureDetails": [],
    "generation": 2,
    "id": "8cb892a9-98a1-4433-ab09-e1d3ceafd3e6",
    "identityReferences": [
        {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    ],
    "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
    "lastUpdateMicros": 1480715874695778,
    "name": "revoke-oauth-tokens",
    "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
    "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/8cb892a9-98a1-4433-ab09-e1d3ceafd3e6",
    "startDateTime": "2016-12-02T13:57:54.640-0800",
    "status": "FAILED",
    "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
    },
    "username": "admin"
}
```

#### Task failure when when input is valid, but the matching tokens doesn't exist anymore on BIG-IP for REVOKE_TOKEN_FOR_USER or REVOKE_TOKEN_FOR_CLIENT_ID action
Even for valid request, you can sometimes see failures, because currently API will try to revoke EXPIRED tokens also.

```
{
    "action": "REVOKE_TOKEN_FOR_CLIENT_ID",
    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
    "currentStep": "REVOKE_TOKENS_FOR_STANDALONE",
    "deviceReferences": [
	{
	    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-access-allBigIpDevices/devices/b795b3da-b703-4b7c-9f9b-ec3d32a7668d"
	}
    ],
    "endDateTime": "2016-12-02T14:47:25.215-0800",
    "errorMessage": "Tokens not found in index. Possibly already revoked tokens.",
    "failureDetails": [
	{
	    "failedIds": [
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "21548559d296d726b12747ab45f5aed0d249436e652f1ff5",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		},
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "b189aa46265af31c6f240d1789374dd985d6baea546217e7",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		},
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "6c784d41f24baefa363834be139e66dd0ba61f045227fb87",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		},
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "b3913c61dad4e65aa2cd1c3fb5f3e3d74adf2b01f851e687",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		},
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "08f38dc356b4d5ad6e5f856c0f2792aa98ae993b2305469b",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		}
	    ],
	    "deviceReference": {
		"link": "https://localhost/mgmt/shared/resolver/device-groups/cm-access-allBigIpDevices/devices/b795b3da-b703-4b7c-9f9b-ec3d32a7668d"
	    }
	}
    ],
    "generation": 6,
    "id": "92be2f5d-2d88-4810-be1f-72443a4e87d0",
    "identityReferences": [
	{
	    "link": "https://localhost/mgmt/shared/authz/users/admin"
	}
    ],
    "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
    "lastUpdateMicros": 1480718845268487,
    "name": "revoke-oauth-tokens",
    "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
    "result": "FAILED",
    "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/92be2f5d-2d88-4810-be1f-72443a4e87d0",
    "startDateTime": "2016-12-02T14:47:09.095-0800",
    "status": "FAILED",
    "userReference": {
	"link": "https://localhost/mgmt/shared/authz/users/admin"
    },
    "username": "admin"
}
```

#### Task failure when when input is valid, but the matching tokens doesn't exist anymore on BIG-IP for REVOKE_TOKEN_FOR_USER action
Even for valid request, you can sometimes see failures, because currently API will try to revoke EXPIRED tokens also.

```
{
    "action": "REVOKE_TOKEN_FOR_USER",
    "currentStep": "REVOKE_TOKENS_FOR_STANDALONE",
    "deviceReferences": [
	{
	    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-access-allBigIpDevices/devices/b795b3da-b703-4b7c-9f9b-ec3d32a7668d"
	}
    ],
    "endDateTime": "2016-12-02T15:01:22.144-0800",
    "errorMessage": "Tokens not found in index. Possibly already revoked tokens.",
    "failureDetails": [
	{
	    "failedIds": [
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "7578a282db6c6e37a396421cb0a6511c58ee7d64e2dd1050",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		},
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "8a9fc4951123ac5f8c0014331aa0d58dfe6c7436d26a503c",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		},
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "e376b1c025577121a883d9dfc13ccbf93dcc201ac617225b",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		},
		{
		    "errorCode": 400,
		    "error": "status:400, body:{\"code\":400,\"message\":\"Token revoke failed. The OAuth ID is not found\",\"errorStack\":[],\"apiError\":26214401}",
		    "id": "3b7e0e581400df4786708e0447f9c3b285cee9533616e686",
		    "dbInstance": "/Common/oauthdb",
		    "clientId": "e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"
		}
	    ],
	    "deviceReference": {
		"link": "https://localhost/mgmt/shared/resolver/device-groups/cm-access-allBigIpDevices/devices/b795b3da-b703-4b7c-9f9b-ec3d32a7668d"
	    }
	}
    ],
    "generation": 6,
    "id": "5c717dcf-fa6a-4ae1-b5fd-3b20be6f2ba7",
    "identityReferences": [
	{
	    "link": "https://localhost/mgmt/shared/authz/users/admin"
	}
    ],
    "kind": "cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate",
    "lastUpdateMicros": 1480719682195917,
    "name": "revoke-oauth-tokens",
    "ownerMachineId": "fd870e82-842d-4194-a882-71cb92e2a5c3",
    "result": "FAILED",
    "selfLink": "https://localhost/mgmt/cm/access/tasks/revoke-tokens/5c717dcf-fa6a-4ae1-b5fd-3b20be6f2ba7",
    "startDateTime": "2016-12-02T15:00:45.580-0800",
    "status": "FAILED",
    "userName": "jack",
    "userReference": {
	"link": "https://localhost/mgmt/shared/authz/users/admin"
    },
    "username": "admin"
}
```

#### Task failure when deviceReference is missing for REVOKE_LIST_OF_TOKENS action
```
{
    "code": 400,
    "message": "Expected deviceReference per list of perDeviceOauthIds",
    "originalRequestBody": "{\"action\":\"REVOKE_LIST_OF_TOKENS\",\"perDeviceOauthIds\":[{}],\"id\":\"9707fa05-eb02-4827-aff1-b1059673ef1f\",\"status\":\"CREATED\",\"name\":\"revoke-oauth-tokens\",\"generation\":1,\"lastUpdateMicros\":1480723333609721,\"kind\":\"cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate\",\"selfLink\":\"https://localhost/mgmt/cm/access/tasks/revoke-tokens/9707fa05-eb02-4827-aff1-b1059673ef1f\"}",
    "referer": "192.168.85.74",
    "restOperationId": 5895882,
    "kind": ":resterrorresponse"
}
```

#### Task failure when oauthIds are missing for REVOKE_LIST_OF_TOKENS action
```
{
    "code": 400,
    "message": "Expected oauthIds per list of perDeviceOauthIds",
    "originalRequestBody": "{\"action\":\"REVOKE_LIST_OF_TOKENS\",\"perDeviceOauthIds\":[{\"deviceReference\":{\"link\":\"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642\"}}],\"id\":\"691e86a6-4adb-48c7-8e45-3c9a43d3d8a4\",\"status\":\"CREATED\",\"name\":\"revoke-oauth-tokens\",\"generation\":1,\"lastUpdateMicros\":1480723393766436,\"kind\":\"cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate\",\"selfLink\":\"https://localhost/mgmt/cm/access/tasks/revoke-tokens/691e86a6-4adb-48c7-8e45-3c9a43d3d8a4\"}",
    "referer": "192.168.85.74",
    "restOperationId": 5897207,
    "kind": ":resterrorresponse"
}
```

#### API reference:
[Api reference - revoke oauth authentication token](../html-reference/access-revoke-oauth-token-sessions.html)