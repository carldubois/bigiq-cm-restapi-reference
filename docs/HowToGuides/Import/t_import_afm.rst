Import the firewall service into the working configuration.
-----------------------------------------------------------

Overview
~~~~~~~~

You can use the REST API to import the current configuration for the
Advanced Firewall service on a BIG-IP device into the working
configuration on the BIG-IQ Centralized Management system.

Prerequisites
~~~~~~~~~~~~~

You should be sure the following prerequisites have been met. 

- All BIG-IP devices are operational and have the services provisioned that will be managed by the BIG-IQ Centralized Management system. 

- The BIG-IQ Centralized Management system is operational, has completed the setup wizard, and completed any other needed configuration. 

- Trust has been established between the BIG-IP device and the BIG-IQ Centralized Management system and the Local Traffic service of the BIG-IP has been
  discovered and imported on the BIG-IQ Centralized Management system. In addition, the Advanced Firewall service of the BIG-IP has been
  discovered on the BIG-IQ Centralized Management system. 

- When performing the tasks in this example, review the listed IP addresses and change them as appropriate for your environment. For example, if you are
  not running the script directly on the BIG-IQ system, you should change localhost to be the IP address of the BIG-IQ Centralized Management
  system.

Description
~~~~~~~~~~~

You use the following process to import the current configuration for
the Advanced Firewall service of a BIG-IP device into the BIG-IQ
Centralized Management system working configuration. 

1. Determine the current state of the BIG-IP device by performing a GET method on the machineid-resolver URI. Using this information, the trust and discovery status of the BIG-IP device can be determined. 

2. Perform a POST method to the declare management authority URI to import the current configuration of the BIG-IP device. 

3. Monitor the task in the previous step using GET methods until the status reaches a value of FINISHED, FAILED, or CANCELLED. 

4. If pending conflicts are detected (when the value of currentStep is PENDING\_CONFLICTS or PENDING\_CHILD\_CONFLICTS), perform a PATCH method on the declare management authority URI, with the appropriate conflict JSON. 

5. Perform additional GET methods on the declare management authority URI until the status value is FINISHED and the currentStep value is DONE.

Example for Importing the Advanced Firewall service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the following example: 

- The BIG-IP device discovery address is 10.255.4.124. you can substitute your BIG-IP device's discovery address for this address when you implement the example.
- The BIG-IP device is in a DSC cluster with another BIG-IP device which has a discovery address of 10.255.4.125. The trust relationship with the clustered BIG-IP device is established later and is not
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

In the following response JSON from the GET method, the adc,
sharedsecurity and networksecurity values are returned. Having these
values returned indicates that the Local Traffic and Advanced Firewall
services have been discovered, and that trust already exists between the
BIG-IP device and the BIG-IQ Centralized Management system.

::

    "properties": {
        "cm:gui:module": [
            "sharedsecurity",
            "networksecurity",
            "BigIPDevice",
            "adc"
        ]
    }

The Local Traffic service is discovered and imported before any other
service. If the adc value is not found in the list, the Local Traffic
service has not been discovered and discovery and import must be
performed. If sharedsecurity and networksecurity values are not found in
the list, the Advanced Firewall service has not been discovered and
discovery must be performed. The machineId found in the response JSON
will be used in Step 2.

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
                "generation": 1,
                "hostname": "bigip124.f5.com",
                "httpsPort": 443,
                "isClustered": false,
                "isVirtual": true,
                "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
                "lastUpdateMicros": 1480692512743700,
                "machineId": "9f320100-2177-42e0-8a46-2e33cd3366da",
                "managementAddress": "10.255.4.124",
                "mcpDeviceName": "/Common/bigip124.f5.com",
                "product": "BIG-IP",
                "properties": {
                    "cm-adccore-adccluster_CLUSTER-124-125": {
                        "clusterName": "CLUSTER-124-125",
                        "cm:gui:module": [
                            "adc"
                        ],
                        "modules": [],
                        "requiresDhcpProfileInDhcpVirtualServer": false,
                        "restrictsPortTranslationStatelessVirtual": false,
                        "supportsAlpineEnhs": false,
                        "supportsBadgerEnhs": false,
                        "supportsClassification": false,
                        "supportsRest": true,
                        "supports_13_0_Enhs": false
                    },
                    "cm-adccore-allDevices": {
                        "cm:gui:module": [],
                        "modules": []
                    },
                    "cm-adccore-allbigipDevices": {
                        "clusterName": "CLUSTER-124-125",
                        "cm:gui:module": [
                            "adc"
                        ],
                        "discovered": true,
                        "discoveryStatus": "FINISHED",
                        "importStatus": "FINISHED",
                        "imported": true,
                        "importedDateTime": "2016-12-02T15:28:54.676Z",
                        "lastDiscoveredDateTime": "2016-12-02T15:28:21.816Z",
                        "lastUserDiscoveredDateTime": "2016-12-02T15:28:21.816Z",
                        "modules": [],
                        "requiresDhcpProfileInDhcpVirtualServer": false,
                        "restrictsPortTranslationStatelessVirtual": false,
                        "supportsAlpineEnhs": false,
                        "supportsBadgerEnhs": false,
                        "supportsClassification": false,
                        "supportsRest": true,
                        "supports_13_0_Enhs": false
                    },
                    "cm-bigip-allBigIpDevices": {
                        "clusterName": "CLUSTER-124-125",
                        "cm:gui:module": [
                            "BigIPDevice"
                        ],
                        "modules": [],
                        "shared:resolver:device-groups:discoverer": "93c853d1-0527-489d-ba7b-72c4f6870a4c"
                    },
                    "cm-bigip-allDevices": {
                        "clusterName": "CLUSTER-124-125",
                        "cm:gui:module": [],
                        "modules": [],
                        "shared:resolver:device-groups:discoverer": "93c853d1-0527-489d-ba7b-72c4f6870a4c"
                    },
                    "cm-bigip-cluster_CLUSTER-124-125": {
                        "clusterName": "CLUSTER-124-125",
                        "cm:gui:module": [],
                        "modules": [],
                        "shared:resolver:device-groups:discoverer": "93c853d1-0527-489d-ba7b-72c4f6870a4c"
                    },
                    "cm-firewall-allDevices": {
                        "cm:gui:module": [
                            "sharedsecurity",
                            "networksecurity",
                            "BigIPDevice",
                            "adc"
                        ],
                        "modules": [
                            "Security"
                        ]
                    },
                    "cm-firewall-allFirewallDevices": {
                        "clusterName": "CLUSTER-124-125",
                        "cm:gui:module": [
                            "networksecurity"
                        ],
                        "discovered": true,
                        "discoveryStatus": "FINISHED",
                        "imported": false,
                        "lastDiscoveredDateTime": "2016-12-02T15:28:37.998Z",
                        "lastUserDiscoveredDateTime": "2016-12-02T15:28:37.998Z",
                        "modules": [
                            "Security"
                        ],
                        "restrictsFirewallInlineRules": true,
                        "supportsAddressRange": true,
                        "supportsAfm": true,
                        "supportsAlpineDosProfileEnhs": false,
                        "supportsFlowIdleTimers": false,
                        "supportsFqdn": false,
                        "supportsFwPolicy": true,
                        "supportsGeoLocation": true,
                        "supportsIruleAction": true,
                        "supportsIruleSampleRate": false,
                        "supportsNatPolicy": false,
                        "supportsNestedAddressLists": true,
                        "supportsNestedPortLists": true,
                        "supportsPortMisusePolicy": false,
                        "supportsRest": true,
                        "supportsRuleLogging": true,
                        "supportsServicePolicy": false,
                        "supportsUserIdentity": false
                    },
                    "cm-security-shared-allDevices": {
                        "cm:gui:module": [],
                        "modules": []
                    },
                    "cm-security-shared-allSharedDevices": {
                        "clusterName": "CLUSTER-124-125",
                        "cm:gui:module": [
                            "sharedsecurity"
                        ],
                        "discovered": true,
                        "discoveryStatus": "FINISHED",
                        "imported": false,
                        "lastDiscoveredDateTime": "2016-12-02T15:28:35.280Z",
                        "lastUserDiscoveredDateTime": "2016-12-02T15:28:35.280Z",
                        "modules": [
                            "Security"
                        ],
                        "requiresDhcpProfileInDhcpVirtualServer": false,
                        "supportUdpPortList": false,
                        "supportsAlpineDosDeviceConfig": false,
                        "supportsAlpineDosDeviceWhitelistIpProcotol": false,
                        "supportsAlpineDosProfileEnhs": false,
                        "supportsAlpineEnhs": false,
                        "supportsAlpineLogProfileEnhs": false,
                        "supportsBadgerEnhs": false,
                        "supportsCascadeEnhs": false,
                        "supportsPortMisusePolicy": false,
                        "supportsRest": true,
                        "supportsSshProfile": false,
                        "supports_13_0_Enhs": false
                    },
                    "cm:gui:module": [
                        "sharedsecurity",
                        "networksecurity",
                        "BigIPDevice",
                        "adc"
                    ],
                    "modules": [
                        "Security"
                    ]
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

Before you import the Advanced Firewall service, verify that it has not
already been imported. Perform a GET method on the
cm-adccore-allbigipDevices device group, using the machine-id from the
previous response to determine if the Advanced Firewall service on the
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

If the Advanced Firewall service is already imported, continuing with
the example will re-import the existing current configuration into the
working configuration.

::

    GET: https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da?$select=address,properties

The following is the response JSON from the GET method:

::

    {
        "address": "10.255.4.124",
        "properties": {
            "clusterName": "CLUSTER-124-125",
            "discovered": true,
            "discoveryStatus": "FINISHED",
            "imported": false,
            "importedDateTime": "2016-12-02T15:29:21.278Z",
            "lastDiscoveredDateTime": "2016-12-02T15:28:37.998Z",
            "lastUserDiscoveredDateTime": "2016-12-02T15:28:37.998Z",
            "restrictsFirewallInlineRules": true,
            "supportsAddressRange": true,
            "supportsAfm": true,
            "supportsAlpineDosProfileEnhs": false,
            "supportsFlowIdleTimers": false,
            "supportsFqdn": false,
            "supportsFwPolicy": true,
            "supportsGeoLocation": true,
            "supportsIruleAction": true,
            "supportsIruleSampleRate": false,
            "supportsNatPolicy": false,
            "supportsNestedAddressLists": true,
            "supportsNestedPortLists": true,
            "supportsPortMisusePolicy": false,
            "supportsRest": true,
            "supportsRuleLogging": true,
            "supportsServicePolicy": false,
            "supportsUserIdentity": false
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
   with the main import task. Set to true for Advanced Firewall, this
   imports the Shared Security configuration.
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

    POST: https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority

    {
        "clusterName": "CLUSTER-124-125",
        "createChildTasks": true,
        "deviceReference": {
            "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "skipDiscovery": true,
        "snapshotWorkingConfig": false,
        "useBigiqSync": true
    }

The following is the response JSON from the POST method:

::

    {
        "clusterName": "CLUSTER-124-125",
        "createChildTasks": true,
        "deviceReference": {
            "link": "https://localhost/mgmt/cm/system/machineid-resolver/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "generation": 1,
        "id": "9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:firewall:tasks:declare-mgmt-authority:dmataskitemstate",
        "lastUpdateMicros": 1480692537248416,
        "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
        "selfLink": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "skipDiscovery": true,
        "snapshotWorkingConfig": false,
        "status": "STARTED",
        "taskWorkerGeneration": 1,
        "useBigiqSync": true,
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    }

3. Perform additional GET methods to the import task created in Step 2.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform additional GET methods on the selfLink that is returned from the
response JSON in Step 2. Perform them in a loop until the status reaches
one of the following: FINISHED, CANCELLED or FAILED. In addition to the
status, currentStep should have the value of DONE, PENDING\_CONFLICTS or
PENDING\_CHILD\_CONFLICTS. In the following example, the currentStep
value is PENDING\_CHILD\_CONFLICTS, indicating that a conflict was
detected in the child task, and so you need to perform Steps 4 and 5. If
the currentStep value is DONE, then the import is complete.

::

    GET: https://10.145.192.10/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad

The following is the response JSON from the GET method:

::

    {
        "childTaskReferences": [
            {
                "link": "https://localhost/mgmt/cm/security-shared/tasks/declare-mgmt-authority/f10eca99-1a80-4342-a98a-e25f69b2eda0"
            }
        ],
        "childTaskStates": [
            {
                "clusterName": "CLUSTER-124-125",
                "conflicts": [
                    {
                        "fromReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/6a6abd6d-daab-3e28-ab1e-ae7ac605be4b"
                        },
                        "resolution": "NONE",
                        "toReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/aba61f43-371d-3768-bbf1-184bbb4a8357"
                        }
                    },
                    {
                        "fromReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/673eb7de-6480-3e59-94e2-d97b46d3d99e"
                        },
                        "resolution": "NONE",
                        "toReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/bb7cf4bd-3259-3ff4-b06d-df2c0ebde3dd"
                        }
                    },
                    {
                        "fromReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/working-config/log-profiles/362ebb6a-f899-3e24-af39-4f57b1f798e8"
                        },
                        "resolution": "NONE",
                        "toReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/current-config/log-profiles/dc4bd777-b34d-3761-85bf-0d55da08e7bb"
                        }
                    }
                ],
                "createChildTasks": false,
                "currentStep": "PENDING_CONFLICTS",
                "deviceIp": "10.255.4.124",
                "deviceReference": {
                    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-security-shared-allSharedDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
                },
                "differenceReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/reports/config-differences/740b35d2-4ac0-4fe9-9770-f1fb439d7b3d"
                },
                "differencerTaskReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/tasks/difference-config/bc9b9b13-d25b-4390-bbc1-4207e03e4962"
                },
                "endDateTime": "2016-12-02T10:28:59.495-0500",
                "generation": 13,
                "id": "f10eca99-1a80-4342-a98a-e25f69b2eda0",
                "identityReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/authz/users/admin"
                    }
                ],
                "isChildTask": true,
                "kind": "cm:security-shared:tasks:declare-mgmt-authority:dmataskitemstate",
                "lastUpdateMicros": 1480692539546736,
                "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
                "parentTaskReference": {
                    "link": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad"
                },
                "reimport": false,
                "selfLink": "https://localhost/mgmt/cm/security-shared/tasks/declare-mgmt-authority/f10eca99-1a80-4342-a98a-e25f69b2eda0",
                "skipDiscovery": true,
                "startDateTime": "2016-12-02T10:28:57.740-0500",
                "status": "FINISHED",
                "useBigiqSync": true,
                "userReference": {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                },
                "username": "admin",
                "validationBypassMode": "BYPASS_FINAL"
            }
        ],
        "clusterName": "CLUSTER-124-125",
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/6a6abd6d-daab-3e28-ab1e-ae7ac605be4b"
                },
                "resolution": "NONE",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/aba61f43-371d-3768-bbf1-184bbb4a8357"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/673eb7de-6480-3e59-94e2-d97b46d3d99e"
                },
                "resolution": "NONE",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/bb7cf4bd-3259-3ff4-b06d-df2c0ebde3dd"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/log-profiles/362ebb6a-f899-3e24-af39-4f57b1f798e8"
                },
                "resolution": "NONE",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/log-profiles/dc4bd777-b34d-3761-85bf-0d55da08e7bb"
                }
            }
        ],
        "createChildTasks": true,
        "currentStep": "PENDING_CHILD_CONFLICTS",
        "deviceIp": "10.255.4.124",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "endDateTime": "2016-12-02T10:28:59.876-0500",
        "generation": 11,
        "id": "9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:firewall:tasks:declare-mgmt-authority:dmataskitemstate",
        "lastUpdateMicros": 1480692539928364,
        "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
        "reimport": false,
        "selfLink": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "skipDiscovery": true,
        "snapshotWorkingConfig": false,
        "startDateTime": "2016-12-02T10:28:57.267-0500",
        "status": "FINISHED",
        "useBigiqSync": true,
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin",
        "validationBypassMode": "BYPASS_FINAL"
    }

4. Use a PATCH method to the import task returned in Step 2 to resolve the conflicts and restart the import task.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

    PATCH: https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad

    {
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/6a6abd6d-daab-3e28-ab1e-ae7ac605be4b"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/aba61f43-371d-3768-bbf1-184bbb4a8357"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/673eb7de-6480-3e59-94e2-d97b46d3d99e"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/bb7cf4bd-3259-3ff4-b06d-df2c0ebde3dd"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/log-profiles/362ebb6a-f899-3e24-af39-4f57b1f798e8"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/log-profiles/dc4bd777-b34d-3761-85bf-0d55da08e7bb"
                }
            }
        ],
        "status": "STARTED"
    }

The following is the response JSON from the PATCH method:

::

    {
        "childTaskReferences": [
            {
                "link": "https://localhost/mgmt/cm/security-shared/tasks/declare-mgmt-authority/f10eca99-1a80-4342-a98a-e25f69b2eda0"
            }
        ],
        "childTaskStates": [
            {
                "clusterName": "CLUSTER-124-125",
                "conflicts": [
                    {
                        "fromReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/6a6abd6d-daab-3e28-ab1e-ae7ac605be4b"
                        },
                        "resolution": "NONE",
                        "toReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/aba61f43-371d-3768-bbf1-184bbb4a8357"
                        }
                    },
                    {
                        "fromReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/673eb7de-6480-3e59-94e2-d97b46d3d99e"
                        },
                        "resolution": "NONE",
                        "toReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/bb7cf4bd-3259-3ff4-b06d-df2c0ebde3dd"
                        }
                    },
                    {
                        "fromReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/working-config/log-profiles/362ebb6a-f899-3e24-af39-4f57b1f798e8"
                        },
                        "resolution": "NONE",
                        "toReference": {
                            "link": "https://localhost/mgmt/cm/security-shared/current-config/log-profiles/dc4bd777-b34d-3761-85bf-0d55da08e7bb"
                        }
                    }
                ],
                "createChildTasks": false,
                "currentStep": "PENDING_CONFLICTS",
                "deviceIp": "10.255.4.124",
                "deviceReference": {
                    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-security-shared-allSharedDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
                },
                "differenceReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/reports/config-differences/740b35d2-4ac0-4fe9-9770-f1fb439d7b3d"
                },
                "differencerTaskReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/tasks/difference-config/bc9b9b13-d25b-4390-bbc1-4207e03e4962"
                },
                "endDateTime": "2016-12-02T10:28:59.495-0500",
                "generation": 13,
                "id": "f10eca99-1a80-4342-a98a-e25f69b2eda0",
                "identityReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/authz/users/admin"
                    }
                ],
                "isChildTask": true,
                "kind": "cm:security-shared:tasks:declare-mgmt-authority:dmataskitemstate",
                "lastUpdateMicros": 1480692539546736,
                "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
                "parentTaskReference": {
                    "link": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad"
                },
                "reimport": false,
                "selfLink": "https://localhost/mgmt/cm/security-shared/tasks/declare-mgmt-authority/f10eca99-1a80-4342-a98a-e25f69b2eda0",
                "skipDiscovery": true,
                "startDateTime": "2016-12-02T10:28:57.740-0500",
                "status": "FINISHED",
                "useBigiqSync": true,
                "userReference": {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                },
                "username": "admin",
                "validationBypassMode": "BYPASS_FINAL"
            }
        ],
        "clusterName": "CLUSTER-124-125",
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/6a6abd6d-daab-3e28-ab1e-ae7ac605be4b"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/aba61f43-371d-3768-bbf1-184bbb4a8357"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/ip-intelligence/blacklist-categories/673eb7de-6480-3e59-94e2-d97b46d3d99e"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/ip-intelligence/blacklist-categories/bb7cf4bd-3259-3ff4-b06d-df2c0ebde3dd"
                }
            },
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/log-profiles/362ebb6a-f899-3e24-af39-4f57b1f798e8"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/current-config/log-profiles/dc4bd777-b34d-3761-85bf-0d55da08e7bb"
                }
            }
        ],
        "createChildTasks": true,
        "currentStep": "PENDING_CHILD_CONFLICTS",
        "deviceIp": "10.255.4.124",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "generation": 12,
        "id": "9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:firewall:tasks:declare-mgmt-authority:dmataskitemstate",
        "lastUpdateMicros": 1480692540524857,
        "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
        "reimport": false,
        "selfLink": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "skipDiscovery": true,
        "snapshotWorkingConfig": false,
        "startDateTime": "2016-12-02T10:29:00.528-0500",
        "status": "STARTED",
        "taskWorkerGeneration": 1,
        "useBigiqSync": true,
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
currentStep has a value of DONE or PENDING\_CONFLICTS. In the following
example, the currentStep value is PENDING\_CONFLICTS, indicating that a
conflict was detected in the main task, and so you need to perform Steps
6 and 7. If the currentStep value is DONE, then the import is complete.

::

    GET: https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad

The following is the response JSON from the GET method:

::

    {
        "childTaskReferences": [
            {
                "link": "https://localhost/mgmt/cm/security-shared/tasks/declare-mgmt-authority/f10eca99-1a80-4342-a98a-e25f69b2eda0"
            }
        ],
        "childTaskStates": [
            {
                "clusterName": "CLUSTER-124-125",
                "createChildTasks": false,
                "currentStep": "DONE",
                "deviceIp": "10.255.4.124",
                "deviceReference": {
                    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-security-shared-allSharedDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
                },
                "differenceReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/reports/config-differences/740b35d2-4ac0-4fe9-9770-f1fb439d7b3d"
                },
                "differencerTaskReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/tasks/difference-config/bc9b9b13-d25b-4390-bbc1-4207e03e4962"
                },
                "endDateTime": "2016-12-02T10:28:59.495-0500",
                "generation": 13,
                "id": "f10eca99-1a80-4342-a98a-e25f69b2eda0",
                "identityReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/authz/users/admin"
                    }
                ],
                "isChildTask": true,
                "kind": "cm:security-shared:tasks:declare-mgmt-authority:dmataskitemstate",
                "lastUpdateMicros": 1480692539546736,
                "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
                "parentTaskReference": {
                    "link": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad"
                },
                "reimport": false,
                "selfLink": "https://localhost/mgmt/cm/security-shared/tasks/declare-mgmt-authority/f10eca99-1a80-4342-a98a-e25f69b2eda0",
                "skipDiscovery": true,
                "startDateTime": "2016-12-02T10:28:57.740-0500",
                "status": "FINISHED",
                "useBigiqSync": true,
                "userReference": {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                },
                "username": "admin",
                "validationBypassMode": "BYPASS_FINAL"
            }
        ],
        "clusterName": "CLUSTER-124-125",
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/firewall/working-config/address-lists/5b6128e7-574a-3034-8e62-941d8e42c3f3"
                },
                "resolution": "NONE",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/firewall/current-config/address-lists/7c310612-e1e2-32ae-8816-c6ea0bcbbe0c"
                }
            }
        ],
        "createChildTasks": true,
        "currentStep": "PENDING_CONFLICTS",
        "deviceIp": "10.255.4.124",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "differenceReference": {
            "link": "https://localhost/mgmt/cm/firewall/reports/config-differences/04cf7ee7-0183-4f09-a213-94f358c244af"
        },
        "differencerTaskReference": {
            "link": "https://localhost/mgmt/cm/firewall/tasks/difference-config/2d09a094-c80d-4d71-a186-f2a625bacc87"
        },
        "endDateTime": "2016-12-02T10:29:10.814-0500",
        "generation": 18,
        "id": "9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:firewall:tasks:declare-mgmt-authority:dmataskitemstate",
        "lastUpdateMicros": 1480692550865936,
        "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
        "reimport": false,
        "selfLink": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "skipDiscovery": true,
        "snapshotWorkingConfig": false,
        "startDateTime": "2016-12-02T10:29:00.528-0500",
        "status": "FINISHED",
        "useBigiqSync": true,
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin",
        "validationBypassMode": "BYPASS_FINAL"
    }

6. Use a PATCH method to the import task returned in Step 3 or 4 to resolve the conflicts and restart the import task.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

    PATCH: https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad

    {
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/firewall/working-config/address-lists/5b6128e7-574a-3034-8e62-941d8e42c3f3"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/firewall/current-config/address-lists/7c310612-e1e2-32ae-8816-c6ea0bcbbe0c"
                }
            }
        ],
        "status": "STARTED"
    }

The following is the response JSON from the PATCH method:

::

    {
        "childTaskReferences": [
            {
                "link": "https://localhost/mgmt/cm/security-shared/tasks/declare-mgmt-authority/f10eca99-1a80-4342-a98a-e25f69b2eda0"
            }
        ],
        "childTaskStates": [
            {
                "clusterName": "CLUSTER-124-125",
                "createChildTasks": false,
                "currentStep": "DONE",
                "deviceIp": "10.255.4.124",
                "deviceReference": {
                    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-security-shared-allSharedDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
                },
                "differenceReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/reports/config-differences/740b35d2-4ac0-4fe9-9770-f1fb439d7b3d"
                },
                "differencerTaskReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/tasks/difference-config/bc9b9b13-d25b-4390-bbc1-4207e03e4962"
                },
                "endDateTime": "2016-12-02T10:28:59.495-0500",
                "generation": 13,
                "id": "f10eca99-1a80-4342-a98a-e25f69b2eda0",
                "identityReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/authz/users/admin"
                    }
                ],
                "isChildTask": true,
                "kind": "cm:security-shared:tasks:declare-mgmt-authority:dmataskitemstate",
                "lastUpdateMicros": 1480692539546736,
                "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
                "parentTaskReference": {
                    "link": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad"
                },
                "reimport": false,
                "selfLink": "https://localhost/mgmt/cm/security-shared/tasks/declare-mgmt-authority/f10eca99-1a80-4342-a98a-e25f69b2eda0",
                "skipDiscovery": true,
                "startDateTime": "2016-12-02T10:28:57.740-0500",
                "status": "FINISHED",
                "useBigiqSync": true,
                "userReference": {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                },
                "username": "admin",
                "validationBypassMode": "BYPASS_FINAL"
            }
        ],
        "clusterName": "CLUSTER-124-125",
        "conflicts": [
            {
                "fromReference": {
                    "link": "https://localhost/mgmt/cm/firewall/working-config/address-lists/5b6128e7-574a-3034-8e62-941d8e42c3f3"
                },
                "resolution": "USE_BIGIQ",
                "toReference": {
                    "link": "https://localhost/mgmt/cm/firewall/current-config/address-lists/7c310612-e1e2-32ae-8816-c6ea0bcbbe0c"
                }
            }
        ],
        "createChildTasks": true,
        "currentStep": "PENDING_CONFLICTS",
        "deviceIp": "10.255.4.124",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/9f320100-2177-42e0-8a46-2e33cd3366da"
        },
        "differenceReference": {
            "link": "https://localhost/mgmt/cm/firewall/reports/config-differences/04cf7ee7-0183-4f09-a213-94f358c244af"
        },
        "differencerTaskReference": {
            "link": "https://localhost/mgmt/cm/firewall/tasks/difference-config/2d09a094-c80d-4d71-a186-f2a625bacc87"
        },
        "generation": 19,
        "id": "9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:firewall:tasks:declare-mgmt-authority:dmataskitemstate",
        "lastUpdateMicros": 1480692553727578,
        "ownerMachineId": "93c853d1-0527-489d-ba7b-72c4f6870a4c",
        "reimport": false,
        "selfLink": "https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad",
        "skipDiscovery": true,
        "snapshotWorkingConfig": false,
        "startDateTime": "2016-12-02T10:29:13.731-0500",
        "status": "STARTED",
        "taskWorkerGeneration": 1,
        "useBigiqSync": true,
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin",
        "validationBypassMode": "BYPASS_FINAL"
    }

7. Perform additional GET methods on the import task created in Step 2.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform additional GET methods on the selfLink returned from either the
Step 3 or Step 4 response. Perform the methods in a loop until the
status reaches one of the following: FINISHED, CANCELLED or FAILED, and
currentStep has a value of DONE. Use a select option to reduce the
content of the returned JSON to a manageable amount.

::

    GET: https://localhost/mgmt/cm/firewall/tasks/declare-mgmt-authority/9c1daed3-0e68-4e0a-bed3-8c37242b2cad?$select=deviceIp,status,currentStep

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
:doc:`../../ApiReferences/firewall-discovery_import`
