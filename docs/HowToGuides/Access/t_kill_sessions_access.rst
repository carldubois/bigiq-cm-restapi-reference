Kill active access sessions
---------------------------

Overview
~~~~~~~~

You can use the REST API to kill/terminate active access sessions on one
or more BIG-IP devices on a BIG-IQ Centralized Management system.

Prerequisites
~~~~~~~~~~~~~

You should be sure the following prerequisites have been met. - All
BIG-IP devices are operational and have the services provisioned that
will be managed by the BIG-IQ Centralized Management system. - The
BIG-IQ Centralized Management system is operational, has completed the
setup wizard, and completed any other needed configuration. - Trust has
been established between the BIG-IP device and the BIG-IQ Centralized
Management system. - APM Service is discovered for the BIG-IP device in
BIG-IQ Centralized Management system. - APM Configuration is imported,
if access group name needs to be used as input criteria. - To kill
sessions using device reference of an BIG-IP device that is part of
cluster, except for kill selected sessions action, it is recommended to
use cluster name instead of device references. If you have to use device
reference, then device reference of the ACTIVE device of cluster should
be used for the kill session API to work. If device reference of PASSIVE
device is passed as input, the task may finish, but API will not be able
to send additional warning or error in the response. ACTIVE device has
to only manually identified by the user, as currently there is no way to
determine this information through API. One way to find the ACTIVE
device for the session in BIG IQ UI, go to Monitoring tab and select
Dashboards & Reports->Access->Sessions. The hostname field corresponds
to the ACTIVE device. Then you can use the filter query to find the
corresponding deviceReference. - When performing the tasks in this
example, review the listed IP addresses and change them as appropriate
for your environment. For example, if you are not running the script
directly on the BIG-IQ system, you should change localhost to be the IP
address of the BIG-IQ Centralized Management system.

Description
~~~~~~~~~~~

You use the following process to Kill Sessions on BIG-IP devices on the
BIG-IQ Centralized Management system. 1. Perform a GET method on the
machineid-resolver URI to determine the current state of the BIG-IP
device and get other inputs parameters to kill sessions. 2. Perform a
POST method on the kill sessions task URI to kill active sessions. 3.
Monitor the task using GET methods until the status has reached a value
of FINISHED, FAILED or CANCELLED. When the GET method status value is
FINISHED and the currentStep value is DONE, the kill sessions is
completed.

Example for Kill Active Access Sessions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the following example: - The BIG-IP device address is 10.255.4.124.
You substitute your BIG-IP device’s address for this address when you
implement the example. If the device that you want to use is part of
cluster, refer to prerequisites section for more details. - The Access
Config Group name is TestGroup,TestGroup1,TestGroup2. You substitute
your access group name when you implement the example. - The BIG-IP
cluster name is BlueCluster,RedCluster. You substitute your cluster name
when you implement the example.

1. Determine the current status of the BIG-IP device and other input parameters on the BIG-IQ Centralized Management system.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a GET method on the machineid-resolver URI to determine if the
BIG-IP device already has trust established. You will want to use the
filter option to narrow the returned JSON information to just this
particular BIG-IP device. If the value of the items element is not an
empty list [], then the trust has already been established. If the value
of the items element is an empty list, you must establish trust before
you can attempt to discover the device.

::

    GET: https://<mgmtip>/mgmt/cm/system/machineid-resolver?$filter=('address'+eq+'10.255.4.124')

To filter more than one address, you can use below kind of filter with
multiple checks on the URI

::

    $filter=('address' eq '10.255.4.1' or 'address' eq '10.255.4.2' )

The following is the response JSON from the GET method:

::

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

1.1. Check if Trust is established.
'''''''''''''''''''''''''''''''''''

In the response to the GET method, you see trust is established since
the following data is found in the list:

::

    "properties": {
        "cm:gui:module": [
            "BigIPDevice"
        ]

1.2. Check if Access Discovery is done.
'''''''''''''''''''''''''''''''''''''''

In the response to the GET method, if the Access value is found in the
list, the Access Policy Manager service has already been discovered; the
adc value represents the Local Traffic service and this must be found in
order to continue with the Access Policy Manager discovery workflow.

::

    "properties": {
        "cm:gui:module": [
            "BigIPDevice",
            "adc",
            "Access"
        ]

1.3. Check if Access Configuration is Imported
''''''''''''''''''''''''''''''''''''''''''''''

In the response to the GET method, you see access import is done if
value of imported property is true in cm-access-allBigIpDevices:

::

    "properties": {
        "cm-access-allBigIpDevices": {
            "imported": true
        }
    }

1.4. Find Access Config Group Name of the device:
'''''''''''''''''''''''''''''''''''''''''''''''''

This is applicable only if the device is imported. In the response to
the GET method, value of cm:access:access-group-name property contains
the access group name. This property is present in
cm-access-allBigIpDevices, which is present inside properties field
value. In this example, access group name is TestGroup:

::

    "properties": {
        "cm-access-allBigIpDevices": {
            "cm:access:access-group-name": "TestGroup"
        }
    }

1.5. Find Cluster Name of an device that is part of Cluster:
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

This is applicable only if the device is discovered and part of cluster.
To kill session in an device which is part of cluster, it is recommended
to use cluster name instead of device reference.

In the response to the GET method, value of clusterName property
contains the cluster name. This property is present in
cm-access-allBigIpDevices, which is present inside properties field
value. In this example, cluster name is BlueCluster:

::

    "properties": {
        "cm-access-allBigIpDevices": {
            "clusterName": "BlueCluster"
        }
    }

1.6. Find device reference of an device:
''''''''''''''''''''''''''''''''''''''''

In the response to the GET method, value of selfLink is the device
reference of the device.

::

    {
        "selfLink": "https://localhost/mgmt/cm/system/machineid-resolver/98901455-6384-47cd-bc41-00a39dfe338f"
    }

1.7. List All Access Config Groups:
'''''''''''''''''''''''''''''''''''

To get list of all access config group name, perform following GET on
device groups resolver API with filter to retrieve only access config
group. In the response, groupName refers to access config group name.

::

    GET: https://<mgmtip>/mgmt/shared/resolver/device-groups/?$filter='properties/cm:access:access_group'+eq+'true'&$select=groupName,displayName

The following is the response JSON from the GET method:

::

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

Repeat steps in Section 1.1 to 1.6 for the all the devices you want to
use. The device reference, access group name and cluster name from the
response JSON in this step will be used in Step 2.

2. Perform a POST method on the kill sessions task URI to kill active sessions.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Different ways to Kill Active Sessions is listed below.

Use a POST method with the following JSON on the kill sessions task to
start the task.

+----------------------------------+-----------------------------------------+
| Parameter                        | Description                             |
+==================================+=========================================+
| action                           | action value has to be KILL\_BY\_USER,  |
|                                  | KILL\_ALL\_SESSIONS or                  |
|                                  | KILL\_BY\_LIST\_OF\_SESSIONS            |
+----------------------------------+-----------------------------------------+
| deviceReferences                 | list of device references               |
+----------------------------------+-----------------------------------------+
| accessGroupNames                 | list of access config group names       |
+----------------------------------+-----------------------------------------+
| clusterNames                     | list of cluster names                   |
+----------------------------------+-----------------------------------------+
| userName                         | Case sensitive field name. user name of |
|                                  | user whose active sessions needs to be  |
|                                  | killed.                                 |
+----------------------------------+-----------------------------------------+
| sessions                         | list of one or more session info        |
|                                  | object, with each object containing     |
|                                  | device reference and list of sesion ids |
+----------------------------------+-----------------------------------------+
| status                           | As part of response, status denotes the |
|                                  | status of the task. It can be STARTED,  |
|                                  | FINISHED, FAILED, CANCELLED or          |
|                                  | CANCEL\_REQUESTED                       |
+----------------------------------+-----------------------------------------+
| result                           | As part of response, result denotes     |
|                                  | whether kill sessions action was        |
|                                  | COMPLETE or FAILED                      |
+----------------------------------+-----------------------------------------+
| errorMessage                     | This can contain error message during   |
|                                  | failure                                 |
+----------------------------------+-----------------------------------------+

2.1 Kill All Active Sessions of an User
'''''''''''''''''''''''''''''''''''''''

You can kill an user's session (for a given username) on one or more
BIG-IP devices that matches one or more input criteria specified below.

2.1.1 Kill All Active Sessions of an User in BIG-IP devices matching one or more Device Reference
                                                                                                 

To use this action, you need to manually determine the username of the
user.

Note: To kill sessions in an device that is part of cluster, then it is
recommended to use cluster name instead of device references. Refer to
prerequisites section for more details.

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_BY_USER",
       "userName":"user2",
       "deviceReferences":[
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
          },
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
          }
       ]
    }

The following is the response JSON from the previous POST method:

::

    {
      "action": "KILL_BY_USER",
      "currentStep": "RESOLVE_DEVICES",
      "deviceReferences": [
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
          },
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
          }
      ],
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userName": "user2",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

2.1.2 Kill All Active Sessions of an User in BIG-IP devices matching one or more Access config groups
                                                                                                     

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_BY_USER",
       "userName":"user2",
       "accessGroupNames":[
          "TestGroup1",
          "TestGroup2",
       ]
    }

The following is the response JSON from the previous POST method:

::

    {
      "action": "KILL_BY_USER",
      "currentStep": "RESOLVE_DEVICES",
       "accessGroupNames":[
          "TestGroup1",
          "TestGroup2",
       ]
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userName": "user2",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

2.1.3 Kill All Active Sessions of an User in BIG-IP devices matching one or more BIG-IP clusters
                                                                                                

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_BY_USER",
       "userName":"user2",
       "clusterNames":[
          "BlueCluster",
          "RedCluster"
       ]
    }

The following is the response JSON from the previous POST method:

::

    {
      "action": "KILL_BY_USER",
      "currentStep": "RESOLVE_DEVICES",
       "clusterNames":[
          "BlueCluster",
          "RedCluster"
       ]
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userName": "user2",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

2.1.4 Kill All Active Sessions of an User in BIG-IP devices matching one or more BIG-IP clusters, one or more Access config groups and one or more device references
                                                                                                                                                                    

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_BY_USER",
       "userName":"user2",
       "accessGroupNames":[
          "TestGroup1",
          "TestGroup2",
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

The following is the response JSON from the previous POST method:

::

    {
      "action": "KILL_BY_USER",
      "currentStep": "RESOLVE_DEVICES",
       "accessGroupNames":[
          "TestGroup1",
          "TestGroup2",
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
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userName": "user2",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

2.2 Kill All Active Sessions
''''''''''''''''''''''''''''

You can kill all active sessions on one or more BIG-IP devices that
matches one or more input criteria specified below.

2.2.1 Kill All Active Sessions in BIG-IP devices matching one or more Device Reference
                                                                                      

Note: To kill sessions in an device that is part of cluster, then it is
recommended to use cluster name instead of device references. Refer to
example in next section. If that is not possible then device reference
of ACTIVE device of cluster should be used for the API to work. Refer to
prerequisites section for more details.

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_ALL_SESSIONS",
       "deviceReferences":[
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
          },
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
          }
       ]
    }

The following is the response JSON from the previous POST method:

::

    {
      "action": "KILL_ALL_SESSIONS",
      "currentStep": "RESOLVE_DEVICES",
      "deviceReferences": [
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
          },
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
          }
      ],
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

2.2.2 Kill All Active Sessions in BIG-IP devices matching one or more Access config groups
                                                                                          

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_ALL_SESSIONS",
       "accessGroupNames":[
          "TestGroup1",
          "TestGroup2",
       ]
    }

The following is the response JSON from the previous POST method:

::

    {
      "action": "KILL_ALL_SESSIONS",
      "currentStep": "RESOLVE_DEVICES",
       "accessGroupNames":[
          "TestGroup1",
          "TestGroup2",
       ]
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

2.2.3 Kill All Active Sessions in one or more BIG-IP clusters
                                                             

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_ALL_SESSIONS",
       "clusterNames":[
          "BlueCluster",
          "RedCluster"
       ]
    }

The following is the response JSON from the previous POST method:

::

    {
      "action": "KILL_ALL_SESSIONS",
      "currentStep": "RESOLVE_DEVICES",
       "clusterNames":[
          "BlueCluster",
          "RedCluster"
       ]
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

2.2.4 Kill All Active Sessions in BIG-IP devices matching one or more BIG-IP clusters, one or more Access config groups and one or more device references
                                                                                                                                                         

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_ALL_SESSIONS",
       "accessGroupNames":[
          "TestGroup1",
          "TestGroup2",
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

The following is the response JSON from the previous POST method:

::

    {
      "action": "KILL_ALL_SESSIONS",
      "currentStep": "RESOLVE_DEVICES",
       "accessGroupNames":[
          "TestGroup1",
          "TestGroup2",
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
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

2.3 Kill List of Active Sessions in BIG-IP devices matching one or more Device Reference
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Note: \* if the input device reference is part of cluster, then device
reference of ACTIVE device of cluster should be used in this action, for
the API to work. If device reference of PASSIVE device is passed as
input, the task may finish, but API will not be able to send additional
warning or error in the response. Refer to prerequisites section for
more details. \* Session id's that has to be killed, need to be manually
determined, currently there is no API support to list session
information. In BIG-IQ UI, active sessions information can be found in
Monitoring tab under Dashboards & Reports->Access->Sessions->Active.

::

    POST:  https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions
    {
       "action":"KILL_BY_LIST_OF_SESSIONS",
       "sessions":[
          {
             "deviceReference":{
                "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
             },
             "sessionIds":[
                "2a5d7604",
                "875f7fed"
             ]
          },
          {
             "deviceReference":{
                "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
             },
             "sessionIds":[
                "2hjj234",
                "9as3323"
             ]
          }
       ]
    }

The following is the response JSON from the previous POST method:

::

    {
         "action":"KILL_BY_LIST_OF_SESSIONS",
         "sessions":[
          {
             "deviceReference":{
                "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
             },
             "sessionIds":[
                "2a5d7604",
                "875f7fed"
             ]
          },
          {
             "deviceReference":{
                "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
             },
             "sessionIds":[
                "2hjj234",
                "9as3323"
             ]
          }
       ]
      "currentStep": "RESOLVE_DEVICES",
      "deviceReferences": [
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
          },
          {
             "link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"
          }
      ],
      "generation": 4,
      "id": "1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479242595185322,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf",
      "startDateTime": "2016-11-15T12:42:31.294-0800",
      "status": "STARTED",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

3. Perform additional GET methods to the kill sessions task created in Step 2.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform additional GET methods on the selfLink returned from the Step 2
response JSON. Perform them in a loop until the status reaches one of
the following: FINISHED, CANCELLED or FAILED. Use a select option to
reduce the content of the returned JSON to a manageable amount. In
addition to the status, result should have the value of COMPLETE.

For a task to be successful,response should have values of status as
FINISHED and result as COMPLETE.

Note: Replace below URI with selfLink from json response or replace
1834e57c-94a2-42eb-860a-1d5cf67ba9bf in below URI with id from json
response.

To get select fields in the response use below query

::

    GET: https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf?$select=status,result,resultDetails,errorMessage

To get complete response use below query

::

    GET: https://<mgmtip>/mgmt/cm/access/tasks/kill-sessions/1834e57c-94a2-42eb-860a-1d5cf67ba9bf

3.1 Sample of Successful Response
'''''''''''''''''''''''''''''''''

The following is an sample successful response JSON from the GET method:

::

     {
      "action": "KILL_BY_LIST_OF_SESSIONS",
      "result": "COMPLETE",
      "currentStep": "DONE",
      "endDateTime": "2016-11-15T12:25:35.764-0800",
      "generation": 4,
      "id": "1ab38f85-0178-4ce5-af08-ea5f5fd3ac5e",
      "identityReferences": [
        {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
      ],
      "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
      "lastUpdateMicros": 1479241535815782,
      "name": "kill-access-sessions",
      "ownerMachineId": "adf1e56b-bf8c-472a-9b2d-e2dd7199ffbd",
      "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/1ab38f85-0178-4ce5-af08-ea5f5fd3ac5e",
      "sessions": [
        {
          "sessionIds": [
            "2a5d7604",
            "875f7fed"
          ],
          "deviceReference": {
            "link": "https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
          }
        }
      ],
      "startDateTime": "2016-11-15T12:25:35.610-0800",
      "status": "FINISHED",
      "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
      },
      "username": "admin"
    }

3.2 Sample of Failed Response
'''''''''''''''''''''''''''''

The following is sample of failed task response JSON from the GET
method:

::

    {
        "items": [
            {
                "accessGroupNames": [
                    "TestGroup123"
                ],
                "action": "KILL_BY_USER",
                "currentStep": "KILL",
                "deviceReferences": [
                    {
                        "link": "https://localhost/mgmt/cm/system/machineid-resolver/217270dc-83bc-469d-9b84-36d7ebf2f6be"
                    }
                ],
                "endDateTime": "2016-11-30T14:32:23.395-0800",
                "errorMessage": "Internal Error occurred",
                "generation": 3,
                "id": "b3c02bb2-594e-44e1-bce7-eceb607111fb",
                "identityReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/authz/users/admin"
                    }
                ],
                "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
                "lastUpdateMicros": 1480545143445735,
                "name": "kill-access-sessions",
                "ownerMachineId": "da4a4ca7-19f9-4a31-a1c2-004d5557ff10",
                "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/b3c02bb2-594e-44e1-bce7-eceb607111fb",
                "startDateTime": "2016-11-30T14:32:23.295-0800",
                "status": "FAILED",
                "userName": "user2",
                "userReference": {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                },
                "username": "admin"
            }
        ],
        "generation": 4,
        "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskcollectionstate",
        "lastUpdateMicros": 1480545143451463,
        "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions"
    }

Common Errors
~~~~~~~~~~~~~

When an error occurs, review the BIG-IQ Centralized Management user
interface for device management to determine the details of the failure.
In addition to using the user interface, some error information can be
determined from the REST API response JSON as shown in the following
error.

Error generated when an incorrect URI is sent in the REST request.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

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

Task failure when action is not provided.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Task creation will not happen, when required data is missing in the
input JSON during POST. Due to this reason, you will not see id or
selfLink in the response for validation failures.

::

    {
        "code": 400,
        "message": "action is missing.",
        "originalRequestBody": "{\"clusterNames\":[\"ca-cluster\"],\"id\":\"2e4b7a58-0016-44bd-ad4b-fd5a72202ce8\",\"status\":\"CREATED\",\"name\":\"kill-access-sessions\",\"generation\":1,\"lastUpdateMicros\":1480543050548655,\"kind\":\"cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate\",\"selfLink\":\"https://localhost/mgmt/cm/access/tasks/kill-sessions/2e4b7a58-0016-44bd-ad4b-fd5a72202ce8\"}",
        "referer": "192.168.85.81",
        "restOperationId": 30692644,
        "kind": ":resterrorresponse"
    }

Task failure when required input is not available.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    {
        "code": 400,
        "message": "Request should have atleast one of these fields populated: accessGroupNames , clusterNames , deviceReferences",
        "originalRequestBody": "{\"action\":\"KILL_ALL_SESSIONS\",\"id\":\"d28291d1-3547-4843-8b44-2331e3e40f4e\",\"status\":\"CREATED\",\"name\":\"kill-access-sessions\",\"generation\":1,\"lastUpdateMicros\":1480542944805994,\"kind\":\"cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate\",\"selfLink\":\"https://localhost/mgmt/cm/access/tasks/kill-sessions/d28291d1-3547-4843-8b44-2331e3e40f4e\"}",
        "referer": "192.168.85.81",
        "restOperationId": 30687454,
        "kind": ":resterrorresponse"
    }

Task failure when non-existing or invalid device reference is provided
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    {
        "action": "KILL_BY_LIST_OF_SESSIONS",
        "currentStep": "RESOLVE_DEVICES",
        "endDateTime": "2016-11-30T13:58:42.866-0800",
        "errorMessage": "item not found at /cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642",
        "generation": 2,
        "id": "89645318-b29f-4a46-9cf8-6f844ebe72f3",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate",
        "lastUpdateMicros": 1480543122917061,
        "name": "kill-access-sessions",
        "ownerMachineId": "d5d58cdd-f5b5-4379-9d12-08e28253a16f",
        "result": "PENDING",
        "selfLink": "https://localhost/mgmt/cm/access/tasks/kill-sessions/89645318-b29f-4a46-9cf8-6f844ebe72f3",
        "sessions": [
            {
                "deviceReference": {
                    "link": "https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"
                }
            }
        ],
        "startDateTime": "2016-11-30T13:58:42.860-0800",
        "status": "FAILED",
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin"
    }

Task failure when session info is empty for KILL\_BY\_LIST\_OF\_SESSIONS action
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    {
        "code": 400,
        "message": "deviceReference is missing",
        "originalRequestBody": "{\"action\":\"KILL_BY_LIST_OF_SESSIONS\",\"sessions\":[{}],\"id\":\"66d1b009-4998-4f24-bb30-00f86c185652\",\"status\":\"CREATED\",\"name\":\"kill-access-sessions\",\"generation\":1,\"lastUpdateMicros\":1480543895438425,\"kind\":\"cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate\",\"selfLink\":\"https://localhost/mgmt/cm/access/tasks/kill-sessions/66d1b009-4998-4f24-bb30-00f86c185652\"}",
        "referer": "192.168.85.81",
        "restOperationId": 30713876,
        "kind": ":resterrorresponse"
    }

Task failure when session ids are missing for KILL\_BY\_LIST\_OF\_SESSIONS action
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    {
        "code": 400,
        "message": "sessionIds are missing for https://localhost/mgmt/cm/system/machineid-resolver/217270dc-83bc-469d-9b84-36d7ebf2f6be",
        "originalRequestBody": "{\"action\":\"KILL_BY_LIST_OF_SESSIONS\",\"sessions\":[{\"deviceReference\":{\"link\":\"https://localhost/mgmt/cm/system/machineid-resolver/217270dc-83bc-469d-9b84-36d7ebf2f6be\"}}],\"id\":\"b7f2a143-0440-4cfd-96c3-a17a107856d5\",\"status\":\"CREATED\",\"name\":\"kill-access-sessions\",\"generation\":1,\"lastUpdateMicros\":1480544881158043,\"kind\":\"cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate\",\"selfLink\":\"https://localhost/mgmt/cm/access/tasks/kill-sessions/b7f2a143-0440-4cfd-96c3-a17a107856d5\"}",
        "referer": "192.168.85.81",
        "restOperationId": 233634,
        "kind": ":resterrorresponse"
    }

API reference:
~~~~~~~~~~~~~

`Api reference - Access kill user
sessions <../html-reference/access-kill-user-sessions.html>`__
