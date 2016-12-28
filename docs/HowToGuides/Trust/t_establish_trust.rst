Establish trust between BIG-IQ and BIG-IP.
------------------------------------------

Overview
~~~~~~~~

You can use the REST API to establish trust between the BIG-IQ
Centralized Management system and BIG-IP devices so that the BIG-IQ
Centralized Management system can manage, and communicate with, the
BIG-IP device. This trust establishment example also shows how to
upgrade the REST framework for a BIG-IP device version 12.0.0 or lower.

Prerequisites
~~~~~~~~~~~~~

This example assumes the following about the configuration: - All BIG-IP
devices are operational and have the services provisioned that will be
managed by the BIG-IQ Centralized Management system. - The BIG-IQ
Centralized Management system is operational, has completed the setup
wizard and has all system-level configuration in place. - When
performing the tasks in this example, review the listed IP addresses and
change them as appropriate for your environment. For example, if you are
not running the script directly on the BIG-IQ system, you should change
localhost to be the IP address of the BIG-IQ Centralized Management
system.

Description
~~~~~~~~~~~

You establish the trust between the BIG-IQ Centralized Management system
and the BIG-IP device as follows: 1. Perform a GET method on the
machineid-resolver URI to determine the current state of the BIG-IP
device. Using this information, you can determine the management status
of the BIG-IP device. 2. Perform a POST method on the trust URI to
create the trust between the BIG-IQ Centralized Management system and
the BIG-IP device. 3. Monitor the task via GET methods until the status
has a value of FINISHED, FAILED or CANCELLED. 4. If needed, perform a
PATCH method to the task with the necessary root credentials to support
a framework upgrade. You perform the patch when the status has a value
of FINISHED and the currentStep value indicates a framework upgrade is
required. 5. Perform GET methods to monitor the trust task until the
status has a value of FINISHED, FAILED or CANCELLED.

The following extended example show each of these REST API methods.

Extended example for establishing device trust
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| In the following example: - The BIG-IP device discovery address is
  10.255.4.124. you can substitute your BIG-IP device’s discovery
  address for this address when you implement the example.
| - The BIG-IP device is in a DSC cluster with another BIG-IP device
  which has a discovery address of 10.255.4.125. The trust relationship
  with the clustered BIG-IP device is established later and is not
  covered in this example.

1. Determine the current status of the BIG-IP device on the BIG-IQ Centralized Management system.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a GET method on the machineid-resolver to determine if the
BIG-IP device already has trust established. You will want to use the
filter option to narrow the returned JSON information to just this
particular BIG-IP device. If the value of items is not an empty list [],
then the trust has already been established.

::

    GET: https://<mgmtip>/mgmt/cm/system/machineid-resolver?$filter=('address'+eq+'10.255.4.124')

The following is the response JSON from the GET method:

::

    {
      "items": [],
      "generation": 0,
      "lastUpdateMicros": 0,
      "selfLink": "http://localhost:8100/cm/system/machineid-resolver?$filter=%28%27address%27+eq+%2710.255.4.124%27%29"
    }

2. Perform a POST method to the trust URI to establish trust between the BIG-IQ Centralized Management system and the BIG-IP device.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a POST method to the trust task URI. The following options must
be included in the POST JSON data: - address - The discovery address for
the BIG-IP device. - clusterName - The name to be used to label the DSC
cluster if this BIG-IP device is part of a DSC cluster. - useBigiqSync -
The mode to be used for synchronizing the DSC cluster. It is highly
recommended that this be included and set to false so that the BIG-IP
devices will perform the necessary syncing of the cluster. - userName -
The user name for the account that has admin privileges on the BIG-IP
device. - password - The password associated with the userName on the
BIG-IP device.

::

    POST: https://<mgmtip>/mgmt/cm/gloal/tasks/device-trust

    {
        "address": "10.255.4.124",
        "clusterName": "Cluster-124-125",
        "password": "admin",
        "useBigiqSync": false,
        "userName": "admin"
    }

The following is the response JSON from the POST method:

::

        "address": "10.255.4.124",
        "clusterName": "Cluster-124-125",
        "generation": 1,
        "id": "a27f6fd7-d0cc-4f2a-892b-cb859b182cdb",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:global:tasks:device-trust:bigiptrusttaskstate",
        "lastUpdateMicros": 1476994540596918,
        "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
        "password": "Gyw7sPg5BFC1vu23i5pKEDbQUw+WL3ZCGIxN/yg1IEQ=",
        "selfLink": "https://localhost/mgmt/cm/global/tasks/device-trust/a27f6fd7-d0cc-4f2a-892b-cb859b182cdb",
        "status": "STARTED",
        "taskWorkerGeneration": 1,
        "useBigiqSync": false,
        "userName": "admin",
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    }

3. Perform GET methods to the trust task returned in Step 2.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform GET methods to the 'selfLink' that is returned from the response
JSON in Step 2. These methods should be performed in a loop until the
status reaches one of the following: FINISHED, CANCELLED or FAILED. Use
a select option to reduce the content of the returned JSON to a
manageable amount.

::

    GET: https://localhost/mgmt/cm/global/tasks/device-trust/a27f6fd7-d0cc-4f2a-892b-cb859b182cdb?$select=address,status,currentStep

The following is the response JSON from the GET method:

::

    {
      "address": "10.255.4.124",
      "currentStep": "PENDING_FRAMEWORK_UPGRADE_CONFIRMATION",
      "status": "FINISHED"
    }

4. Perform a PATCH method on the trust task to start the framework upgrade, if needed.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This step is only needed for BIG-IP devices lower than version 12.0.0
that require a framework upgrade. BIG-IP devices that do not require the
framework upgrade would have a currentStep value of DONE.

Perform a PATCH method on the task selfLink as follows when the value of
currentStep in the task JSON is
PENDING\_FRAMEWORK\_UPGRADE\_CONFIRMATION and the status is FINISHED.

The following options must be included in the PATCH JSON data: -
confirmFrameworkUpgrade - The boolean element that indicates that the
upgrade should be performed, should be set to true. - rootPassword - The
password associated with the rootUser on the BIG-IP. - rootUser - The
user name that has root privileges on the BIG-IP. - status - The status
of the task, this must be set to the STARTED state for the task to
continue.

::

    PATCH: https://localhost/mgmt/cm/global/tasks/device-trust/a27f6fd7-d0cc-4f2a-892b-cb859b182cdb

    {
        "confirmFrameworkUpgrade": true,
        "rootPassword": "default",
        "rootUser": "root",
        "status": "STARTED"
    }

The following is the response JSON from the PATCH method:

::

    {
        "address": "10.255.4.124",
        "clusterName": "Cluster-124-125",
        "confirmFrameworkUpgrade": true,
        "currentStep": "PENDING_FRAMEWORK_UPGRADE_CONFIRMATION",
        "generation": 10,
        "id": "a27f6fd7-d0cc-4f2a-892b-cb859b182cdb",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "isChassisDevice": false,
        "kind": "cm:global:tasks:device-trust:bigiptrusttaskstate",
        "lastUpdateMicros": 1476994543714131,
        "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
        "password": "Gyw7sPg5BFC1vu23i5pKEDbQUw+WL3ZCGIxN/yg1IEQ=",
        "requireFrameworkUpgrade": true,
        "rootPassword": "QBPviVmuHPdmzHZRPQt4TAUJHlklLNp0aKnU6OkffRQ=",
        "rootUser": "root",
        "selfLink": "https://localhost/mgmt/cm/global/tasks/device-trust/a27f6fd7-d0cc-4f2a-892b-cb859b182cdb",
        "startDateTime": "2016-10-20T16:15:43.715-0400",
        "status": "STARTED",
        "taskWorkerGeneration": 1,
        "useBigiqSync": false,
        "userName": "admin",
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin"
    }

5. Perform additional GET methods to the trust task.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform additional GET methods on the 'selfLink' that is returned from
the Step 2 response JSON. Perform them in a loop until the status
reaches one of the following: FINISHED, CANCELLED or FAILED. Use a
select option to reduce the content of the returned JSON to a manageable
amount. In addition to the status, the currentStep should have the value
of DONE.

::

    GET: https://localhost/mgmt/cm/global/tasks/device-trust/a27f6fd7-d0cc-4f2a-892b-cb859b182cdb?$select=address,status,currentStep

The following is the response JSON from the GET method:

::

    {
      "address": "10.255.4.124",
      "currentStep": "DONE",
      "status": "FINISHED"
    }

Common Errors
~~~~~~~~~~~~~

On a failure condition, review the BIG-IQ Centralized Management Devices
user interface to determine the details of the failure. However, some
error information can be determined from the REST API response JSON as
shown in the following errors.

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

POST response to the trust URI with bad authentication for admin user credentials.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

           {
                "address": "10.145.192.4",
                "clusterName": "Cluster-124-125",
                "currentStep": "CHECK_BIGIP_AVAILABLE",
                "endDateTime": "2016-10-21T12:30:47.867-0400",
                "errorMessage": "Failed to connect to 10.145.192.4, check credentials: Unauthorized(401)",
                "generation": 7.0,
                "id": "225dfd23-f6a3-476a-aa20-a022e3104f9d",
                "identityReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/authz/users/admin"
                    }
                ],
                "kind": "cm:global:tasks:device-trust:bigiptrusttaskstate",
                "lastUpdateMicros": 1477067447917160.0,
                "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
                "password": "fxbJ6VMgFG+zmvc3sHNrOtP8S63zO/cV82Umoa10BXk=",
                "selfLink": "https://localhost/mgmt/cm/global/tasks/device-trust/225dfd23-f6a3-476a-aa20-a022e3104f9d",
                "startDateTime": "2016-10-21T12:30:46.147-0400",
                "status": "FAILED",
                "useBigiqSync": false,
                "userName": "admin",
                "userReference": {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                },
                "username": "admin"
            }

PATCH response to the trust URI with bad authentication for root user credentials used by framework upgrade.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

            {
                "address": "10.145.192.3",
                "clusterName": "Cluster-124-125",
                "confirmFrameworkUpgrade": true,
                "currentStep": "FAILED",
                "endDateTime": "2016-10-21T12:49:24.234-0400",
                "errorMessage": "could not upgrade REST framework: Authentication failed",
                "generation": 13.0,
                "id": "e9e28cb8-b79e-4a61-945a-a6a169b2069b",
                "identityReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/authz/users/admin"
                    }
                ],
                "isChassisDevice": false,
                "kind": "cm:global:tasks:device-trust:bigiptrusttaskstate",
                "lastUpdateMicros": 1477068564284693.0,
                "machineId": "9f320100-2177-42e0-8a46-2e33cd3366da",
                "ownerMachineId": "87611fbb-fb85-4c41-a9c0-ee7a5ba388d2",
                "password": "S6UaoDf+sOjWxCx78p4IHwxd3/Ro+45FkZ4R47XwK/I=",
                "requireFrameworkUpgrade": true,
                "requireRootCredential": true,
                "rootPassword": "P6toc0D6WpqESiOYbDqAZAlVn98n9ekoMN//DGIxukI=",
                "rootUser": "root",
                "selfLink": "https://localhost/mgmt/cm/global/tasks/device-trust/e9e28cb8-b79e-4a61-945a-a6a169b2069b",
                "startDateTime": "2016-10-21T12:49:03.071-0400",
                "status": "FAILED",
                "useBigiqSync": false,
                "userName": "admin",
                "userReference": {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                },
                "username": "admin"
            }

API references that support this workflow:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Api reference - device trust
task <../html-reference/device-trust.html>`__
