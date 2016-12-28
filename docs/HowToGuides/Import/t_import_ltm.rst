Import the LTM service into the working configuration.
------------------------------------------------------

Overview
~~~~~~~~

You can use the REST API to import the current configuration for the
Local Traffic service on a BIG-IP device into the working configuration
on the BIG-IQ Centralized Management system.

Prerequisites
~~~~~~~~~~~~~

You should be sure the following prerequisites have been met. - All
BIG-IP devices are operational and have the services provisioned that
will be managed by the BIG-IQ Centralized Management system. - The
BIG-IQ Centralized Management system is operational, has completed the
setup wizard, and completed any other needed configuration. - Trust has
been established between the BIG-IP device and the BIG-IQ Centralized
Management system and the current configuration of the BIG-IP device has
been discovered on the BIG-IQ Centralized Management system. - When
performing the tasks in this example, review the listed IP addresses and
change them as appropriate for your environment. For example, if you are
not running the script directly on the BIG-IQ system, you should change
localhost to be the IP address of the BIG-IQ Centralized Management
system.

Description
~~~~~~~~~~~

You use the following process to import the current configuration for
the Local Traffic service of a BIG-IP device into the BIG-IQ Centralized
Management system working configuration. 1. Determine the current state
of the BIG-IP device by performing a GET method on the
machineid-resolver URI. Using this information, the trust and discovery
status of the BIG-IP device can be determined. 2. Perform a POST method
to the declare management authority URI to import the current
configuration of the BIG-IP device. 3. Monitor the task in the previous
step using GET methods until the status reaches a value of FINISHED,
FAILED, or CANCELLED. 4. If pending conflicts are detected (when the
value of currentStep is PENDING\_CONFLICTS), perform a PATCH method on
the declare management authority URI, with the appropriate conflict
JSON. 5. Perform additional GET methods on the declare management
authority URI until the status value is FINISHED and the currentStep
value is DONE.

Example for Importing the Local Traffic service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

| In the following example: - The BIG-IP device discovery address is
  10.255.4.124. you can substitute your BIG-IP device’s discovery
  address for this address when you implement the example.
| - The BIG-IP device is in a DSC cluster with another BIG-IP device
  which has a discovery address of 10.255.4.125. The trust relationship
  with the clustered BIG-IP device is established later and is not
  covered in this example.

1. Determine the current status of the BIG-IP device on the BIG-IQ Centralized Management system.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a GET method on the machineid-resolver URI to determine if the
BIG-IP device already has trust established. You should use the filter
option to narrow the returned JSON information to just this particular
BIG-IP device. If the value of the items element is not an empty list
[], then the trust has already been established.

::

    GET: https://<mgmtip>/mgmt/cm/system/machineid-resolver?$filter=('address'+eq+'10.255.4.124')

In the following response JSON from the GET method, the adc value is
returned. Having the adc value returned indicates that the Local Traffic
service has been discovered, and that trust already exists between the
BIG-IP device and the BIG-IQ Centralized Management system.

::

    "properties": {
        "cm:gui:module": [
            "BigIPDevice"
            "adc"
        ]
    }

The Local Traffic service is discovered before any other service. If the
adc value is not found in the list, the Local Traffic service has not
been discovered and discovery must be performed. The machineId found in
the response JSON will be used in Step 2.

::

    GET: https://<mgmtip>/mgmt/cm/system/machineid-resolver?$filter=('address'+eq+'10.255.4.124')

The following is the response JSON from the GET method:

::

    {
        "generation": 0,
        "items": [
            {
                "address": "10.255.4.124",
                "build": "0.0.141",
                "deviceUri": "https://10.255.4.124:443",
                "edition": "Final",
                "generation": 3,
                "hostname": "bigip124.f5.com",
                "httpsPort": 443,
                "isClustered": false,
                "isVirtual": true,
                "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
                "lastUpdateMicros": 1478009254692241,
                "machineId": "9f320100-2177-42e0-8a46-2e33cd3366da",
                "managementAddress": "10.255.4.124",
                "mcpDeviceName": "/Common/bigip124.f5.com",
                "product": "BIG-IP",
                "properties": {
                    "cm-bigip-allBigIpDevices": {
                        "clusterName": "Cluster-124-125",
                        "cm:gui:module": [
                            "BigIPDevice"
                        ],
                        "modules": [],
                        "shared:resolver:device-groups:discoverer": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2"
                    },
                    "cm-bigip-allDevices": {
                        "clusterName": "Cluster-124-125",
                        "cm:gui:module": [],
                        "modules": [],
                        "shared:resolver:device-groups:discoverer": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2"
                    },
                    "cm-bigip-cluster_Cluster-124-125": {
                        "clusterName": "Cluster-124-125",
                        "cm:gui:module": [],
                        "modules": [],
                        "shared:resolver:device-groups:discoverer": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2"
                    },
                    "cm:gui:module": [
                        "BigIPDevice"
                    ],
                    "modules": []
                },
                "restFrameworkVersion": "12.0.0-0.0.4211",
                "selfLink": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da",
                "slots": [
                    {
                        "build": "0.0.141",
                        "isActive": false,
                        "product": "BIG-IP",
                        "version": "11.5.2",
                        "volume": "HD1.1"
                    },
                    {
                        "build": "0.0.141",
                        "isActive": true,
                        "product": "BIG-IP",
                        "version": "11.5.2",
                        "volume": "HD1.2"
                    }
                ],
                "state": "ACTIVE",
                "trustDomainGuid": "91bd712a-ad8f-4570-ab540050560145f3",
                "uuid": "9f320100-2177-42e0-8a46-2e33cd3366da",
                "version": "11.5.2"
            }
        ],
        "lastUpdateMicros": 0,
        "selfLink": "http://localhost:8100/cm/system/machineid-resolver?$filter=%28%27address%27+eq+%2710.255.4.124%27%29"
    }

Before you import the Local Traffic service, verify that it has not
already been imported. Perform a GET method on the
cm-adccore-allbigipDevices device group, using the machine-id from the
previous response to determine if the Local Traffic service on the
BIG-IP device is already imported. Use the select filter to reduce the
response JSON content. Review the indicated information in the response
JSON:

::

        "properties": {
            "discovered": true,
            "discoveryStatus": "FINISHED",
            "importStatus": "FINISHED",     <-- Should be missing
            "imported": true                <-- Should be false
         }

If the Local Traffic service is already imported, continuing with the
example will re-import the existing current configuration into the
working configuration.

::

    GET: https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da?$select=address,properties

The following is the response JSON from the GET method:

::

    {
        "address": "10.255.4.124",
        "properties": {
            "discovered": true,
            "discoveryStatus": "FINISHED",
            "imported": false,
            "lastDiscoveredDateTime": "2016-11-01T20:07:23.690Z",
            "lastUserDiscoveredDateTime": "2016-11-01T20:07:23.690Z",
            "requiresDhcpProfileInDhcpVirtualServer": false,
            "restrictsPortTranslationStatelessVirtual": false,
            "supportsAlpineEnhs": false,
            "supportsBadgerEnhs": false,
            "supportsClassification": false,
            "supportsRest": true
        }
    }

2. Perform a POST method to the declare management authority URI.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a POST method containing the following JSON to the declare
management authority discovery task URI. This POST starts the import.
The following are the items that must be sent in the POST JSON:

-  clusterName: Indicates the name of the cluster used when trust was
   established.
-  createChildTask: Indicates whether there is a child import associated
   with the main import task. Set to false for Local Traffic.
-  deviceReference: The BIG-IP device selfLink reference from Step 1.
-  skipDiscovery: Indicates whether discovery should be skipped. Set to
   true since discovery is performed in another example.
-  snapshotWorkingConfig: Indicates whether the working configuration on
   the BIG-IQ Centralized Management system should be captured in a
   snapshot prior to the import. Set to false for this example.
-  useBigiqSync: Indicates whether the BIG-IQ Centralized Management
   system should synchronize objects for the cluster or whether the
   BIG-IP device should handle the synchronization. Set to the value
   that was set during trust establishment, false in this example.

   ::

       POST: https://localhost/mgmt/cm/global/tasks/declare-mgmt-authority
       {
       "clusterName": "Cluster-124-125",
       "createChildTasks": false,
       "deviceReference": {
           "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
       },
       "skipDiscovery": true,
       "snapshotWorkingConfig": false,
       "useBigiqSync": false
       }

   The following is the response JSON from the POST method:

   ::

       {
       "clusterName": "Cluster-124-125",
       "createChildTasks": false,
       "deviceReference": {
           "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
       },
       "generation": 1,
       "id": "58dec475-b55d-40d9-a40c-64422d1a7374",
       "identityReferences": [
           {
               "link": "https://localhost/mgmt/shared/authz/users/admin"
           }
       ],
       "kind": "cm:adc-core:tasks:declare-mgmt-authority:dmataskitemstate",
       "lastUpdateMicros": 1478009277993664,
       "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
       "selfLink": "https://localhost/mgmt/cm/adc-core/tasks/declare-mgmt-authority/58dec475-b55d-40d9-a40c-64422d1a7374",
       "skipDiscovery": true,
       "snapshotWorkingConfig": false,
       "status": "STARTED",
       "taskWorkerGeneration": 1,
       "useBigiqSync": false,
       "userReference": {
           "link": "https://localhost/mgmt/shared/authz/users/admin"
       }
       }

3. Perform additional GET methods to the import task created in Step 2.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform additional GET methods on the selfLink that is returned from the
response JSON in Step 2. Perform them in a loop until the status reaches
one of the following: FINISHED, CANCELLED or FAILED. In addition to the
status, currentStep should have the value of DONE or PENDING\_CONFLICTS.
In the following example, the currentStep value is PENDING\_CONFLICTS,
indicating that a conflict was detected, and so you need to perform
Steps 4 and 5. If the currentStep value is DONE, then the import is
complete and Steps 4 and 5 would not be performed.

::

    GET: https://localhost/mgmt/cm/adc-core/tasks/declare-mgmt-authority/58dec475-b55d-40d9-a40c-64422d1a7374

The following is the response JSON from the GET method:

::

    {
        "clusterName": "Cluster-124-125",
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/persistence/source-addr/35d67560-c1f4-3c23-83e2-b3fdde826df4"
                },
                "resolution": "NONE",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/current-config/ltm/persistence/source-addr/f144e386-b746-3944-bd01-714246db83c6"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/profile/http/ad348aed-0309-36d5-b5cd-c5b9e00cbb26"
                },
                "resolution": "NONE",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/current-config/ltm/profile/http/712da21c-353e-31b3-94bc-751c09347c7c"
                }
            }
        ],
        "createChildTasks": false,
        "currentStep": "PENDING_CONFLICTS",
        "deviceIp": "10.255.4.124",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "differenceReference": {
            "link": "https://localhost/mgmt/cm/adc-core/reports/config-differences/93fccd5f-6c32-4004-8d40-77a7d1a3cea8"
        },
        "differencerTaskReference": {
            "link": "https://localhost/mgmt/cm/adc-core/tasks/difference-config/b7e4c971-d424-4b75-853a-3466865cee8b"
        },
        "endDateTime": "2016-11-01T10:07:59.663-0400",
        "generation": 13,
        "id": "58dec475-b55d-40d9-a40c-64422d1a7374",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:adc-core:tasks:declare-mgmt-authority:dmataskitemstate",
        "lastUpdateMicros": 1478009279713746,
        "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
        "reimport": false,
        "selfLink": "https://localhost/mgmt/cm/adc-core/tasks/declare-mgmt-authority/58dec475-b55d-40d9-a40c-64422d1a7374",
        "skipDiscovery": true,
        "snapshotWorkingConfig": false,
        "startDateTime": "2016-11-01T10:07:58.011-0400",
        "status": "FINISHED",
        "useBigiqSync": false,
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin",
        "validationBypassMode": "BYPASS_FINAL"
    }

4. Use a PATCH method to the import task returned in Step 2 to resolve the conflict and restart the import task.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You resolve conflicts by selecting one of following options: - Select
USE\_BIGIQ to indicate that the existing working configuration on the
BIG-IQ Centralized Management system will be maintained where any
conflict exists. - Select USE\_BIGIP to indicate that the current
configuration on the BIG-IP device will be used to update the working
configuration on the BIG-IQ Centralized Management system where any
conflict exists. In this example, USE\_BIGIQ is selected.

You perform conflict resolution by using the PATCH method and looping
through each of the listed conflicts and setting the resolution element
as shown in the following example. In addition, the status must be set
to STARTED.

::

    PATCH: https://localhost/mgmt/cm/adc-core/tasks/declare-mgmt-authority/58dec475-b55d-40d9-a40c-64422d1a7374
    {
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/persistence/source-addr/35d67560-c1f4-3c23-83e2-b3fdde826df4"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/current-config/ltm/persistence/source-addr/f144e386-b746-3944-bd01-714246db83c6"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/profile/http/ad348aed-0309-36d5-b5cd-c5b9e00cbb26"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/current-config/ltm/profile/http/712da21c-353e-31b3-94bc-751c09347c7c"
                }
            }
        ],
        "status": "STARTED"
    }

The following is the response JSON from the PATCH method:

::

    {
        "clusterName": "Cluster-124-125",
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/persistence/source-addr/35d67560-c1f4-3c23-83e2-b3fdde826df4"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/current-config/ltm/persistence/source-addr/f144e386-b746-3944-bd01-714246db83c6"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/working-config/ltm/profile/http/ad348aed-0309-36d5-b5cd-c5b9e00cbb26"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/adc-core/current-config/ltm/profile/http/712da21c-353e-31b3-94bc-751c09347c7c"
                }
            }
        ],
        "createChildTasks": false,
        "currentStep": "COPY_CONFIG",
        "deviceIp": "10.255.4.124",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-adccore-allbigipDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "differenceReference": {
            "link": "https://localhost/mgmt/cm/adc-core/reports/config-differences/93fccd5f-6c32-4004-8d40-77a7d1a3cea8"
        },
        "differencerTaskReference": {
            "link": "https://localhost/mgmt/cm/adc-core/tasks/difference-config/b7e4c971-d424-4b75-853a-3466865cee8b"
        },
        "generation": 23,
        "id": "58dec475-b55d-40d9-a40c-64422d1a7374",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:adc-core:tasks:declare-mgmt-authority:dmataskitemstate",
        "lastUpdateMicros": 1478009283751175,
        "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
        "reimport": false,
        "selfLink": "https://localhost/mgmt/cm/adc-core/tasks/declare-mgmt-authority/58dec475-b55d-40d9-a40c-64422d1a7374",
        "skipDiscovery": true,
        "snapshotWorkingConfig": false,
        "startDateTime": "2016-11-01T10:08:01.156-0400",
        "status": "STARTED",
        "useBigiqSync": false,
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin",
        "validationBypassMode": "BYPASS_FINAL"
    }

5. Perform additional GET methods on the import task created in Step 2.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform additional GET methods on the selfLink returned from either the
Step 3 or Step 4 response. Perform the methods in a loop until the
status reaches one of the following: FINISHED, CANCELLED or FAILED, and
currentStep has a value of DONE. Use a select option to reduce the
content of the returned JSON to a manageable amount.

::

    GET: https://localhost/mgmt/cm/adc-core/tasks/declare-mgmt-authority/58dec475-b55d-40d9-a40c-64422d1a7374?$select=deviceIp,status,currentStep

The following is the response JSON from the GET method:

::

    {
        "deviceIp": "10.255.4.124",
        "status": "FINISHED",
        "currentStep": "DONE"
    }

Common Errors
~~~~~~~~~~~~~

When an error occurs, use the BIG-IQ Centralized Management user
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
    
    API references
    ~~~~~~~~~~~~~~
