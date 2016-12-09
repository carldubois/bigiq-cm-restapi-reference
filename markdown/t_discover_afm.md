## Discover the Advanced Firewall service on a BIG-IP device using a BIG-IQ Centralized Management system

### Overview
You can use the REST API to discover the current configuration of the Advanced Firewall service on a BIG-IP device on a BIG-IQ Centralized Management system.

### Prerequisites
You should be sure the following prerequisites have been met.
- All BIG-IP devices are operational and have the services provisioned that will be managed by the BIG-IQ Centralized Management system.
- The BIG-IQ Centralized Management system is operational, has completed the setup wizard, and completed any other needed configuration.
- Trust has been established between the BIG-IP device and the BIG-IQ Centralized Management system and the current configuration of the BIG-IP device has been discovered on the BIG-IQ Centralized Management system for the Local Traffic service.
- When performing the tasks in this example, review the listed IP addresses and change them as appropriate for your environment. For example, if you are not running  the script directly on the BIG-IQ system, you should change localhost to be the IP address of the BIG-IQ Centralized Management system.

### Description
You use the following process to discover the Advanced Firewall service for a BIG-IP device on the BIG-IQ Centralized Management system.
1. Perform a GET method on the machineid-resolver URI to determine the current state of the BIG-IP device. 
2. Perform a GET method on the discovery URI using a filter of the machineId found in Step 1. The content of the response determines whether a PATCH or POST method will be used. You use either a POST method to create the discovery task or a PATCH method to update an existing task. In this case, a task will be found if the associated Local Traffic discovery task was not deleted.
3. Perform a PATCH method on the discovery URI to discover the current configuration of the BIG-IP device.
4. Monitor the task using GET methods until the status has reached a value of FINISHED, FAILED or CANCELLED. When the GET method status value is FINISHED and the currentStep value is DONE, the discovery has completed.

### Example for Advanced Firewall Device Discovery
In the following example:
- The BIG-IP device discovery address is 10.255.4.124.  you substitute your BIG-IP device’s discovery address for this address when you implement the example.  
-  The BIG-IP device is in a DSC cluster with another BIG-IP device which has a discovery address of 10.255.4.125. The trust relationship with the clustered BIG-IP device is established later and is not covered in this example.

#### 1. Determine the current status of the BIG-IP device on the BIG-IQ Centralized Management system.
Perform a GET method on the machineid-resolver URI to determine if the BIG-IP device already has trust established. You will want to use the filter option to narrow the returned JSON information to just this particular BIG-IP device. If the value of the items element is not an empty list [], then the trust has already been established. If the value of the items element is an empty list, you must establish trust before you can attempt to discover the device.

In the response to the GET method, trust is established since the following data is found in the list:

```
"properties": {
    "cm:gui:module": [
        "BigIPDevice",
        "adc"
    ]
```
If the sharedsecurity and networksecurity values are found in the list, the Advanced Firewall service has already been discovered; the adc value represents the Local Traffic service and this must be found in order to continue with the Advanced Firewall discovery workflow. Other possible values may also be shown in addition to adc, such as dns, asm, or access.

The machineId from the response JSON will be used in Step 2.

```
GET: https://<mgmtip>/mgmt/cm/system/machineid-resolver?$filter=('address'+eq+'10.255.4.124')
```

The following is the response JSON from the GET method:

```
{
    "generation": 0,
    "items": [
        {
            "address": "10.255.4.124",
            "build": "0.0.141",
            "deviceUri": "https://10.255.4.124:443",
            "edition": "Final",
            "generation": 8,
            "hostname": "bigip124.f5.com",
            "httpsPort": 443,
            "isClustered": false,
            "isLicenseExpired": false,
            "isVirtual": true,
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "lastUpdateMicros": 1478896179454035,
            "machineId": "9f320100-2177-42e0-8a46-2e33cd3366da",
            "managementAddress": "10.255.4.124",
            "mcpDeviceName": "/Common/bigip124.f5.com",
            "product": "BIG-IP",
            "properties": {
                "cm-adccore-allDevices": {
                    "cm:gui:module": [],
                    "modules": []
                },
                "cm-adccore-allbigipDevices": {
                    "cm:gui:module": [
                        "BigIPDevice",
                        "adc"
                    ],
                    "discovered": true,
                    "discoveryStatus": "FINISHED",
                    "importStatus": "FINISHED",
                    "imported": true,
                    "importedDateTime": "2016-11-11T20:29:39.452Z",
                    "lastDiscoveredDateTime": "2016-11-11T20:29:25.011Z",
                    "lastUserDiscoveredDateTime": "2016-11-11T20:29:25.011Z",
                    "modules": [],
                    "requiresDhcpProfileInDhcpVirtualServer": false,
                    "restrictsPortTranslationStatelessVirtual": false,
                    "supportsAlpineEnhs": false,
                    "supportsBadgerEnhs": false,
                    "supportsClassification": false,
                    "supportsRest": true
                },
                "cm-bigip-allBigIpDevices": {
                    "cm:gui:module": [
                        "BigIPDevice"
                    ],
                    "modules": [],
                    "shared:resolver:device-groups:discoverer": "0f556542-74fc-4936-898e-727be8793230"
                },
                "cm-bigip-allDevices": {
                    "cm:gui:module": [],
                    "modules": [],
                    "shared:resolver:device-groups:discoverer": "0f556542-74fc-4936-898e-727be8793230"
                },
                "cm:gui:module": [
                    "BigIPDevice",
                    "adc"
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
```

#### 2. Perform a GET method on the discovery URI using a filter of the machineId found in Step 1.
The content of the response determines whether a PATCH or POST method will be used. You use either a POST method to create the discovery task or a PATCH method to update an existing task. 
An existing task would be found if:
- A previous discovery of the device was performed (and you now want to perform a rediscovery of the device).
- A previous discovery task for this device was not deleted.
Finding existing discovery tasks should be rare.

```
GET: https://localhost/mgmt/cm/global/tasks/device-discovery?$filter=deviceReference/link+eq+'*9f320100-2177-42e0-8a46-2e33cd3366da'
```

The following is the response JSON from the GET method when an existing task is found, which is expected:

```
{
    "generation": 2274,
    "items": [
        {
            "allModuleStatus": [
                {
                    "endTime": "2016-11-11T20:29:25.965Z",
                    "module": "adc_core",
                    "startTime": "2016-11-11T20:29:14.893Z"
                }
            ],
            "currentConfigConsistencyCheckReference": {
                "link": "https://localhost/mgmt/cm/global/tasks/current-config-consistency-check/16010a74-fc57-4887-90b3-1a3a2f496e86"
            },
            "currentStep": "DONE",
            "deviceReference": {
                "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
            },
            "generation": 7.0,
            "id": "dfbf4d92-a057-4520-bc7d-37f0f0f6f5df",
            "identityReferences": [
                {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                }
            ],
            "kind": "cm:global:tasks:device-discovery:discoverysupertaskitemstate",
            "lastUpdateMicros": 1478896167042899.0,
            "moduleList": [
                {
                    "endTime": "2016-11-11T20:29:25.965Z",
                    "module": "adc_core",
                    "startTime": "2016-11-11T20:29:14.893Z",
                    "status": "FINISHED"
                }
            ],
            "name": "discovery_10.255.4.124",
            "ownerMachineId": "0f556542-74fc-4936-898e-727be8793230",
            "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery/dfbf4d92-a057-4520-bc7d-37f0f0f6f5df",
            "startDateTime": "2016-11-11T15:29:14.657-0500",
            "status": "STARTED",
            "taskWorkerGeneration": 1.0,
            "userReference": {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            },
            "username": "admin"
        }
    ],
    "kind": "cm:global:tasks:device-discovery:discoverysupertaskcollectionstate",
    "lastUpdateMicros": 1478896167106041,
    "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery",
    "totalItems": 1
}
```

#### 3. Perfom a PATCH method to the discovery task returned in Step 2 to start the discovery or rediscovery.
It is expected that the task will exist, since the Local Traffic service has been discovered. In the case of the Advanced Firewall service, two modules are required for the discovery: the firewall module and the shared security module. 
If the task is not found, proceed to Step 4 for the POST procedure.
The PATCH JSON data should include:
- moduleList: The modules to discover, firewall and security_shared.
- status: The status of the task, STARTED.

```
PATCH: https://localhost/mgmt/cm/global/tasks/device-discovery/dfbf4d92-a057-4520-bc7d-37f0f0f6f5df
{
    "moduleList": [
        {
            "module": "firewall"
        },
        {
            "module": "security_shared"
        }
    ],
    "status": "STARTED"
}
```
The following is the response JSON from the PATCH method:

```
{
    "allModuleStatus": [
        {
            "endTime": "2016-11-11T20:29:25.965Z",
            "module": "adc_core",
            "startTime": "2016-11-11T20:29:14.893Z"
        }
    ],
    "currentConfigConsistencyCheckReference": {
        "link": "https://localhost/mgmt/cm/global/tasks/current-config-consistency-check/16010a74-fc57-4887-90b3-1a3a2f496e86"
    },
    "currentStep": "DONE",
    "deviceReference": {
        "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
    },
    "generation": 8,
    "id": "dfbf4d92-a057-4520-bc7d-37f0f0f6f5df",
    "identityReferences": [
        {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    ],
    "kind": "cm:global:tasks:device-discovery:discoverysupertaskitemstate",
    "lastUpdateMicros": 1478896204780454,
    "moduleList": [
        {
            "module": "firewall"
        },
        {
            "module": "security_shared"
        }
    ],
    "name": "discovery_10.255.4.124",
    "ownerMachineId": "0f556542-74fc-4936-898e-727be8793230",
    "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery/dfbf4d92-a057-4520-bc7d-37f0f0f6f5df",
    "startDateTime": "2016-11-11T15:30:04.781-0500",
    "status": "STARTED",
    "taskWorkerGeneration": 1,
    "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
    },
    "username": "admin"
}
```

#### 4. Perfom a POST method to the discovery task returned in Step 2 to start the discovery. In most cases the PATCH will be used instead of the POST.
The POST JSON data should include:
- deviceReference: The BIG-IP device selfLink reference from Step 1.
- moduleList: The modules to discover, firewall and security_shared.
- status: The status of the task, STARTED.

```
PATCH: https://localhost/mgmt/cm/global/tasks/device-discovery
{
    "deviceReference": {
        "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
    },
    "moduleList": [
        {
            "module": "firewall"
        },
        {
            "module": "security_shared"
        }
    ],
    "status": "STARTED"
}
```

The following is the response JSON from the POST method:

```
{
    "deviceReference": {
        "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
    },
    "generation": 1,
    "id": "c8529d3a-aa33-4a5d-abf9-1feb048cea76",
    "identityReferences": [
        {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    ],
    "kind": "cm:global:tasks:device-discovery:discoverysupertaskitemstate",
    "lastUpdateMicros": 1478905274610051,
    "moduleList": [
        {
            "module": "firewall"
        },
        {
            "module": "security_shared"
        }
    ],
    "ownerMachineId": "0f556542-74fc-4936-898e-727be8793230",
    "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery/c8529d3a-aa33-4a5d-abf9-1feb048cea76",
    "status": "STARTED",
    "taskWorkerGeneration": 1,
    "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
    }
}
```

#### 5. Perform additional GET methods to the discovery task created in Step 3 or Step 4.
Perform additional GET methods on the selfLink returned from the Step 3 or Step 4 response JSON. Perform them in a loop until the status reaches one of the following: FINISHED, CANCELLED or FAILED. Use a select option to reduce the content of the returned JSON to a manageable amount. In addition to the status, currentStep should have the value of DONE.

```
GET: https://localhost/mgmt/cm/global/tasks/device-discovery/dfbf4d92-a057-4520-bc7d-37f0f0f6f5df?$select=status,currentStep
```

The following is the response JSON from the GET method:

```
{
    "currentStep": "DONE",
    "status": "FINISHED",
}
```

### Common Errors
When an error occurs, review the BIG-IQ Centralized Management user interface for device management to determine the details of the failure. In addition to using the user interface, some error information can be determined from the REST API response JSON as shown in the following errors.

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

#### Discovery failure for a device that is no longer available.

```
{
    "allModuleStatus": [
        {
            "endTime": "2016-11-11T20:29:25.965Z",
            "module": "adc_core",
            "startTime": "2016-11-11T20:29:14.893Z"
        },
        {
            "endTime": "2016-11-11T20:39:37.239Z",
            "errorMsg": "Error getting resource provisioning from /mgmt/tm/sys/provision on bigip124.f5.com (10.255.4.124); check if iControl REST service is running on the BIG-IP",
            "module": "security_shared",
            "startTime": "2016-11-11T20:39:36.218Z"
        },
        {
            "endTime": "2016-11-11T20:39:38.270Z",
            "errorMsg": "Error getting resource provisioning from /mgmt/tm/sys/provision on bigip124.f5.com (10.255.4.124); check if iControl REST service is running on the BIG-IP",
            "module": "firewall",
            "startTime": "2016-11-11T20:39:37.247Z"
        }
    ],
    "currentConfigConsistencyCheckReference": {
        "link": "https://localhost/mgmt/cm/global/tasks/current-config-consistency-check/078d566f-117f-46e5-aa79-ad736196d913"
    },
    "currentStep": "FAILED",
    "deviceReference": {
        "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
    },
    "endDateTime": "2016-11-11T15:39:39.360-0500",
    "errorMessage": "Failed to process module tasks : At least one module is failed",
    "generation": 21,
    "id": "dfbf4d92-a057-4520-bc7d-37f0f0f6f5df",
    "identityReferences": [
        {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    ],
    "kind": "cm:global:tasks:device-discovery:discoverysupertaskitemstate",
    "lastUpdateMicros": 1478896779412293,
    "moduleList": [
        {
            "endTime": "2016-11-11T20:39:38.270Z",
            "errorMsg": "Error getting resource provisioning from /mgmt/tm/sys/provision on bigip124.f5.com (10.255.4.124); check if iControl REST service is running on the BIG-IP",
            "module": "firewall",
            "startTime": "2016-11-11T20:39:37.247Z",
            "status": "FAILED"
        },
        {
            "endTime": "2016-11-11T20:39:37.239Z",
            "errorMsg": "Error getting resource provisioning from /mgmt/tm/sys/provision on bigip124.f5.com (10.255.4.124); check if iControl REST service is running on the BIG-IP",
            "module": "security_shared",
            "startTime": "2016-11-11T20:39:36.218Z",
            "status": "FAILED"
        }
    ],
    "name": "discovery_10.255.4.124",
    "ownerMachineId": "0f556542-74fc-4936-898e-727be8793230",
    "selfLink": "https://localhost/mgmt/cm/global/tasks/device-discovery/dfbf4d92-a057-4520-bc7d-37f0f0f6f5df",
    "startDateTime": "2016-11-11T15:39:35.954-0500",
    "status": "FAILED",
    "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
    },
    "username": "admin"
}
```