Discover the LTM service on a BIG-IP device.
--------------------------------------------

Overview
~~~~~~~~

You can use the REST API to discover the current configuration of the
Local Traffic service on a BIG-IP device on a BIG-IQ Centralized
Management system.

Prerequisites
~~~~~~~~~~~~~

You should be sure the following prerequisites have been met. - All
BIG-IP devices are operational and have the services provisioned that
will be managed by the BIG-IQ Centralized Management system. - The
BIG-IQ Centralized Management system is operational, has completed the
setup wizard, and completed any other needed configuration. - Trust has
been established between the BIG-IP device and the BIG-IQ Centralized
Management system. - When performing the tasks in this example, review
the listed IP addresses and change them as appropriate for your
environment. For example, if you are not running the script directly on
the BIG-IQ system, you should change localhost to be the IP address of
the BIG-IQ Centralized Management system.

Description
~~~~~~~~~~~

You use the following process to discover the Local Traffic service for
a BIG-IP device on the BIG-IQ Centralized Management system. 1. Perform
a GET method on the machineid-resolver URI to determine the current
state of the BIG-IP device. 2. Perform a GET method on the discovery URI
using a filter of the machineId found in Step 1. The content of the
response determines whether a PATCH or POST method will be used. You use
either a POST method to create the discovery task or a PATCH method to
update an existing task. 3. Perform a POST method (or PATCH method) on
the discovery URI to discover the current configuration of the BIG-IP
device. 4. Monitor the task using GET methods until the status has
reached a value of FINISHED, FAILED or CANCELLED. When the GET method
status value is FINISHED and the currentStep value is DONE, the
discovery has completed.

Example for Device Discovery
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

| In the following example: - The BIG-IP device discovery address is
  10.255.4.124. you substitute your BIG-IP device’s discovery address
  for this address when you implement the example.
| - The BIG-IP device is in a DSC cluster with another BIG-IP device
  which has a discovery address of 10.255.4.125. The trust relationship
  with the clustered BIG-IP device is established later and is not
  covered in this example.

1. Determine the current status of the BIG-IP device on the BIG-IQ Centralized Management system.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a GET method on the machineid-resolver URI to determine if the
BIG-IP device already has trust established. You will want to use the
filter option to narrow the returned JSON information to just this
particular BIG-IP device. If the value of the items element is not an
empty list [], then the trust has already been established. If the value
of the items element is an empty list, you must establish trust before
you can attempt to discover the device.

In the response to the GET method, you see trust is established since
the following data is found in the list:

::

    "properties": {
        "cm:gui:module": [
            "BigIPDevice"
        ]

If the adc value is found in the list, the Local Traffic service has
already been discovered; the adc value represents the Local Traffic
service.

The machineId from the response JSON will be used in Step 2.

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
                "generation": 4,
                "hostname": "bigip124.f5.com",
                "httpsPort": 443,
                "isClustered": false,
                "isLicenseExpired": false,
                "isVirtual": true,
                "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
                "lastUpdateMicros": 1477676742276559,
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

2. Perform a GET method on the discovery URI using a filter of the machineId found in Step 1.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The content of the response determines whether a PATCH or POST method
will be used. You use either a POST method to create the discovery task
or a PATCH method to update an existing task. An existing task would be
found if: - A previous discovery of the device was performed (and you
may now want to perform a rediscovery of the device). - A previous
discovery task for this device was not deleted. Finding existing
discovery tasks should be rare.

::

    GET: https://localhost/mgmt/cm/global/tasks/device-discovery?$filter=deviceReference/link+eq+'*9f320100-2177-42e0-8a46-2e33cd3366da'

The following is the response JSON from the GET method when no existing
task is found:

::

    {
        "generation": 791,
        "items": [],
        "kind": "cm:global:tasks:device-discovery:discoverysupertaskcollectionstate",
        "lastUpdateMicros": 1477678379537052,
        "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery",
        "totalItems": 0
    }

3. Perform a POST method to the discovery task if one was not returned in Step 2, or continue to Step 4 and perform the PATCH method to an existing task for the device.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use a POST method with the following JSON on the discovery task to start
the discovery. - deviceReference: The BIG-IP device selfLink reference
from Step 1 - moduleList: The module to discover, adc\_core - status:
The status of the task, STARTED

::

    POST: https://localhost/mgmt/cm/global/tasks/device-discovery
    {
        "deviceReference": {
            "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "moduleList": [
            {
                "module": "adc_core"
            }
        ],
        "status": "STARTED"
    }

The following is the response JSON from the previous POST method:

::

    {
        "deviceReference": {
            "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "generation": 1,
        "id": "d435934f-c615-4873-85f9-ddb4ac4e6c3e",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:global:tasks:device-discovery:discoverysupertaskitemstate",
        "lastUpdateMicros": 1477678409190342,
        "moduleList": [
            {
                "module": "adc_core"
            }
        ],
        "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
        "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery/d435934f-c615-4873-85f9-ddb4ac4e6c3e",
        "status": "STARTED",
        "taskWorkerGeneration": 1,
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    }

4. If a task already exists, perform a PATCH method to the discovery task returned in Step 2 to start the discovery or rediscovery.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This operation reuses a task for the same device that exists either
because the device is already discovered or the device was removed and
the task was never deleted. The PATCH JSON data should include: -
moduleList: The module to discover, adc\_core - status: The status of
the task, STARTED

::

    PATCH: https://localhost/mgmt/cm/global/tasks/device-trust/a27f6fd7-d0cc-4f2a-892b-cb859b182cdb
    {
        "moduleList": [
            {
                "module": "adc_core"
            }
        ],
        "status": "STARTED"
    }

Response JSON from the PATCH:

::

    {
        "allModuleStatus": [
            {
                "endTime": "2016-10-28T18:42:11.187Z",
                "module": "adc_core",
                "startTime": "2016-10-28T18:42:02.062Z"
            }
        ],
        "currentConfigConsistencyCheckReference": {
            "link": "https://localhost/mgmt/cm/global/tasks/current-config-consistency-check/7c2df895-16f8-42a6-b38a-96ed519fbda4"
        },
        "currentStep": "DONE",
        "deviceReference": {
            "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "generation": 8,
        "id": "4d3dd0f7-4a1e-424c-8b02-ad9e952189fc",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:global:tasks:device-discovery:discoverysupertaskitemstate",
        "lastUpdateMicros": 1477680292504922,
        "moduleList": [
            {
                "module": "adc_core"
            }
        ],
        "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
        "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery/4d3dd0f7-4a1e-424c-8b02-ad9e952189fc",
        "startDateTime": "2016-10-28T14:44:52.506-0400",
        "status": "STARTED",
        "taskWorkerGeneration": 1,
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin"
    }

5. Perform additional GET methods to the discovery task created in Step 3 or Step 4.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform additional GET methods on the selfLink returned from the Step 3
or Step 4 response JSON. Perform them in a loop until the status reaches
one of the following: FINISHED, CANCELLED or FAILED. Use a select option
to reduce the content of the returned JSON to a manageable amount. In
addition to the status, currentStep should have the value of DONE.

::

    GET: https://localhost/mgmt/cm/global/tasks/device-discovery/d435934f-c615-4873-85f9-ddb4ac4e6c3e?$select=status,currentStep

The following is the response JSON from the GET method:

::

    {
      "currentStep": "DONE",
      "status": "FINISHED"
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

Discovery failure for a device that is no longer available.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    {
        "allModuleStatus": [
            {
                "endTime": "2016-10-28T18:54:24.915Z",
                "errorMsg": "Error getting resource provisioning from /mgmt/tm/sys/provision on bigip124.f5.com (10.145.192.3); check if iControl REST service is running on the BIG-IP",
                "module": "adc_core",
                "startTime": "2016-10-28T18:54:23.891Z"
            }
        ],
        "currentConfigConsistencyCheckReference": {
            "link": "https://localhost/mgmt/cm/global/tasks/current-config-consistency-check/44e46a83-b6a1-4760-b643-ed2ea310fb0c"
        },
        "currentStep": "FAILED",
        "deviceReference": {
            "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "endDateTime": "2016-10-28T14:54:26.033-0400",
        "errorMessage": "Failed to process module tasks : At least one module is failed",
        "generation": 7,
        "id": "e4a23fed-570c-4607-afd5-ee2c96ba6b06",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:global:tasks:device-discovery:discoverysupertaskitemstate",
        "lastUpdateMicros": 1477680866084285,
        "moduleList": [
            {
                "endTime": "2016-10-28T18:54:24.915Z",
                "errorMsg": "Error getting resource provisioning from /mgmt/tm/sys/provision on bigip124.f5.com (10.145.192.3); check if iControl REST service is running on the BIG-IP",
                "module": "adc_core",
                "startTime": "2016-10-28T18:54:23.891Z",
                "status": "FAILED"
            }
        ],
        "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
        "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery/e4a23fed-570c-4607-afd5-ee2c96ba6b06",
        "startDateTime": "2016-10-28T14:54:23.659-0400",
        "status": "FAILED",
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin"
    }      

API references
~~~~~~~~~~~~~~
:doc:`../../ApiReferences/device-discovery`
