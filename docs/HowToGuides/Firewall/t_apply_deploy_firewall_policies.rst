.. raw:: html

   <div id="header">

.. raw:: html

   </div>

.. raw:: html

   <div id="content">

.. raw:: html

   <div class="sect1">

.. rubric:: Applying firewall policies to contexts and deploying them to
   BIG-IP devices
   :name: _applying_firewall_policies_to_contexts_and_deploying_them_to_big_ip_devices

.. raw:: html

   <div class="sectionbody">

.. raw:: html

   <div class="sect2">

.. rubric:: Overview
   :name: _overview

.. raw:: html

   <div class="paragraph">

Describes how you use the REST API to apply one or more firewall
policies to one or more firewall contexts and then deploy those changes
to associated BIG-IP devices.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Prerequisites
   :name: _prerequisites

.. raw:: html

   <div class="ulist">

-  All BIG-IP devices to be used have been imported for the Local
   Traffic and Network Security services.

-  All firewall policies to be deployed have been configured on the
   BIG-IQ Centralized Management system.

-  All firewall contexts that will have firewall policies assigned to
   them have been created in the Local Traffic service and deployed to
   the BIG-IP device.

-  When performing the tasks in this example, review the listed IP
   addresses and change them as appropriate for your environment. For
   example, if you are not running the script directly on the BIG-IQ
   system, you should change localhost to be the IP address of the
   BIG-IQ Centralized Management system.

-  The odata query will differ between rest clients POSTMAN and curl.
   Please note the filter='contents should be encapsulated in single
   quotes'

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Description
   :name: _description

.. raw:: html

   <div class="paragraph">

Describes the steps you perform to apply one or more firewall policies
to one or more firewall contexts and deploy the firewall changes to
associated BIG-IP devices. Perform the REST API actions in the following
order: 1. GET the firewall policies to use. 2. GET the firewall contexts
to use. 3. PATCH each firewall context with the appropriate firewall
policy. 4. Select the BIG-IP devices to which you want to deploy these
changes. 5. POST the deployment task JSON to the deployment task URI. If
needed, PATCH the deployment task as well. 6. GET the deployment task
status to determine if the deployment completed successfully.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

The following extended example show each of these REST API actions.
Example

## 1. Retrieve the firewall policy to be applied to the firewall
contexts.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

Perform a GET operation on the policies collection. In the steps in this
example, the context used is a virtual server. Use the filter and select
options to narrow the returned JSON information to just the policy in
which you are interested.

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    GET: https://<mgmtip>/mgmt/cm/firewall/working-config/policies?$filter=('name'+eq+'Policy_1')&$select=name,selfLink

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

The following is the JSON response from the GET operation:

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
      "selfLink": "https://localhost/mgmt/cm/firewall/working-config/policies",
      "totalItems": 1,
      "items": [
        {
          "name": "Policy_1",
          "selfLink": "https://localhost/mgmt/cm/firewall/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef"
        }
      ],
      "generation": 401,
      "kind": "cm:firewall:working-config:policies:policycollectionstate",
      "lastUpdateMicros": 1474559397713741
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: 2. Retrieve the firewall contexts by type, name, or both.
   :name: _2_retrieve_the_firewall_contexts_by_type_name_or_both

.. raw:: html

   <div class="paragraph">

Perform a GET operation on the firewall collection to retrieve the
contexts. In this example, a single virtual server is returned. Use the
filter and select options to narrow the returned JSON information to
just the firewall context in which you are interested. In addition if a
specific BIG-IP device is required, that could be used by appending the
following: ``and('deviceReference/name'eq'<name>')``

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    GET: https://<mgmtip>/mgmt/cm/firewall/working-config/firewalls?$filter=('name'+eq+'VirtualServer_1')+and+(firewallType+eq+'vip') &$select=name,firewallType,selfLink,deviceReference

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

The following is the JSON response from the GET:

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
      "selfLink": "https://localhost/mgmt/cm/firewall/working-config/firewalls",
      "totalItems": 1,
      "items": [
        {
          "deviceReference": {
            "id": "6e932e01-7b5e-431d-b1d3-8ca5e3eb891d",
            "name": "bigip25.f5.com",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "machineId": "6e932e01-7b5e-431d-b1d3-8ca5e3eb891d",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"
          },
          "firewallType": "vip",
          "name": "VirtualServer_1",
          "selfLink": "https://localhost/mgmt/cm/firewall/working-config/firewalls/970b7b0b-8f21-3a88-909a-29df7e73fd5d"
        }
      ],
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: 3. Apply the firewall policy to the virtual server firewall
   context (staged or enforced).
   :name: _3_apply_the_firewall_policy_to_the_virtual_server_firewall_context_staged_or_enforced

.. raw:: html

   <div class="paragraph">

Perform a PATCH operation on the virtual server firewall context. The
virtual server is identified by a URI containing its selfLink. Set
either ``stagedPolicyReference`` or ``enforcedPolicyReference`` to the
firewall policy selfLink.

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    PATCH: https://<mgmtip>/mgmt/cm/firewall/working-config/firewalls/970b7b0b-8f21-3a88-909a-29df7e73fd5d
    {
      "enforcedPolicyReference":{
        "link":https://localhost/mgmt/cm/firewall/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef
      },
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

The following is the JSON response from the PATCH operation. The
response to any successful PATCH is the complete patched object with the
patch applied:

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
        "description": "Virtual Server for VirtualServer_1",
        "deviceReference": {
            "id": "6e932e01-7b5e-431d-b1d3-8ca5e3eb891d",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d",
            "machineId": "6e932e01-7b5e-431d-b1d3-8ca5e3eb891d",
            "name": "bigip25.f5.com"
        },
        "enforcedPolicyReference": {
            "link": "https://localhost/mgmt/cm/firewall/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef"
        },
        "firewallIpAddress": "1.241.136.63:29763",
        "firewallType": "vip",
        "generation": 2,
        "id": "970b7b0b-8f21-3a88-909a-29df7e73fd5d",
        "kind": "cm:firewall:working-config:firewalls:firewallstate",
        "lastUpdateMicros": 1474559398139114,
        "name": "VirtualServer_1",
        "partition": "Common",
        "rulesCollectionReference": {
            "isSubcollection": true,
            "link": "https://localhost/mgmt/cm/firewall/working-config/firewalls/970b7b0b-8f21-3a88-909a-29df7e73fd5d/rules"
        },
        "selfLink": "https://localhost/mgmt/cm/firewall/working-config/firewalls/970b7b0b-8f21-3a88-909a-29df7e73fd5d"
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: 4. Determine which BIG-IP devices need changes deployed to
   them based on which firewalls were modified.
   :name: _4_determine_which_big_ip_devices_need_changes_deployed_to_them_based_on_which_firewalls_were_modified

.. raw:: html

   <div class="paragraph">

The device references needed for the deployment are found in the
firewall context JSON for each modified context. This example shows the
deviceReference for the virtual server returned in the previous example:

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

        "deviceReference": {
            "id": "6e932e01-7b5e-431d-b1d3-8ca5e3eb891d",
            "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d",
            "machineId": "6e932e01-7b5e-431d-b1d3-8ca5e3eb891d",
            "name": "bigip25.f5.com"
        }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: 5. Evaluate the configuration changes created by the
   firewall configuration modifications to determine if there are
   errors.
   :name: _5_evaluate_the_configuration_changes_created_by_the_firewall_configuration_modifications_to_determine_if_there_are_errors

.. raw:: html

   <div class="paragraph">

A deployment task must be created that includes each BIG-IP device that
had an associated firewall context updated.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

Perform a POST operation to the following URL to create the deployment
task:

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    POST: https://<mgmtip>/mgmt/cm/firewall/tasks/deploy-configuration

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

The deployment can also be created in the deploy-immediately mode (where
``skipDistribution`` is set to false) as follows. This type of
deployment is only recommended if no warnings or errors are expected.

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
        "createChildTasks": true,
        "description": "Policy Deploy",
        "deviceReferences": [
            {
                "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"
            }
        ],
        "name": "Policy Deploy",
        "skipDistribution": false
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

After creating the deployment task in either of these ways, continue to
the next step to determine when the deployment completes and its final
status. The ``deviceReferences`` will be a list of device references
determined from the previous step. The name and description fields
should be modified to allow unique tracking of each deployment.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

If there is a concern that there may be issues with the configuration,
the deployment can be done in stages. The first stage is the evaluation
stage. If no errors or warnings are detected during evaluation, the
configuration can then be deployed to the BIG-IP device in the second
stage.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

The deployment evaluation is created by performing a POST of the
following to the deployment task URI defined above. Once again, the name
and description fields should be modified to allow unique tracking of
each deployment.

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
        "createChildTasks": true,
        "description": "Policy Deploy",
        "deviceReferences": [
            {
                "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"
            }
        ],
        "name": "Policy Deploy",
        "skipDistribution": true
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

In either deployment case, the response JSON for the POST is as follows:

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
        "childDeployTasks": [
            {
                "description": "Policy Deploy",
                "deviceReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-security-shared-allSharedDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"
                    }
                ],
                "generation": 1,
                "id": "4cf1f614-704c-466b-9ed9-558d28fd1644",
                "identityReferences": [
                    {
                        "link": "https://localhost/mgmt/shared/authz/users/admin"
                    }
                ],
                "isChildTask": true,
                "kind": "cm:security-shared:tasks:deploy-configuration:deployconfigtaskstate",
                "lastUpdateMicros": 1474579219691578,
                "name": "Policy Deploy",
                "ownerMachineId": "ece40a9a-c62d-4ee0-b9ea-a42ef379515b",
                "parentTaskReference": {
                    "link": "https://localhost/mgmt/cm/firewall/tasks/deploy-configuration/70e8c87d-cec6-4ed5-8de4-88682ff3bd63"
                },
                "selfLink": "https://localhost/mgmt/cm/security-shared/tasks/deploy-configuration/4cf1f614-704c-466b-9ed9-558d28fd1644",
                "skipDistribution": true,
                "snapshotReference": {
                    "link": "https://localhost/mgmt/cm/security-shared/working-config/snapshots/9619b966-390d-457e-abe2-044eadc74571"
                },
                "status": "STARTED",
                "taskWorkerGeneration": 1,
                "userReference": {
                    "link": "https://localhost/mgmt/shared/authz/users/admin"
                }
            }
        ],
        "childSnapshotReference": {
            "link": "https://localhost/mgmt/cm/security-shared/working-config/snapshots/9619b966-390d-457e-abe2-044eadc74571"
        },
        "childTaskReferences": [
            {
                "link": "https://localhost/mgmt/cm/security-shared/tasks/deploy-configuration/4cf1f614-704c-466b-9ed9-558d28fd1644"
            }
        ],
        "createChildTasks": true,
        "currentStep": "WAIT_FOR_CHILD_DEPLOY",
        "description": "Policy Deploy",
        "deviceDetails": [
            {
                "deviceReference": {
                    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"
                },
                "differenceCount": 4,
                "hostname": "bigip25.f5.com",
                "postDeploymentErrorCount": 0,
                "verificationCriticalErrorCount": 0,
                "verificationErrorCount": 1
            }
        ],
        "deviceReferences": [
            {
                "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"
            }
        ],
        "differenceReference": {
            "link": "https://localhost/mgmt/cm/firewall/reports/config-differences/3717d94d-41ac-46cc-8a2d-30dede717a28"
        },
        "differenceTaskReference": {
            "link": "https://localhost/mgmt/cm/firewall/tasks/difference-config/1a2fa07f-bc4a-4190-ae30-c92e1e8f6db1"
        },
        "discoveryTaskReferences": [
            {
                "link": "https://localhost/mgmt/cm/firewall/tasks/discover-config/de08c2a3-a5a4-4f30-bff0-20484f585080"
            }
        ],
        "generation": 12,
        "id": "70e8c87d-cec6-4ed5-8de4-88682ff3bd63",
        "identityReferences": [
            {
                "link": "https://localhost/mgmt/shared/authz/users/admin"
            }
        ],
        "kind": "cm:firewall:tasks:deploy-configuration:deployconfigtaskstate",
        "lastUpdateMicros": 1474579219766431,
        "name": "Policy Deploy",
        "ownerMachineId": "ece40a9a-c62d-4ee0-b9ea-a42ef379515b",
        "selfLink": "https://localhost/mgmt/cm/firewall/tasks/deploy-configuration/70e8c87d-cec6-4ed5-8de4-88682ff3bd63",
        "skipDistribution": true,
        "snapshotReference": {
            "link": "https://localhost/mgmt/cm/firewall/working-config/snapshots/f2dcf02f-b334-4616-a025-d2c2137bccf0"
        },
        "snapshotTaskReference": {
            "link": "https://localhost/mgmt/cm/firewall/tasks/snapshot-config/7389e9e2-f4e5-4d1c-a39d-c7fdc5f98bf9"
        },
        "startDateTime": "2016-09-22T17:20:11.926-0400",
        "status": "STARTED",
        "userReference": {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "username": "admin",
        "verifyConfigReference": {
            "link": "https://localhost/mgmt/cm/firewall/reports/config-verifications/4efd2db4-e049-4039-b13b-2d18e5becaaf"
        },
        "verifyConfigTaskReference": {
            "link": "https://localhost/mgmt/cm/firewall/tasks/verify-config/3d35d99e-b1f1-4329-a6e8-0ea482529fd0"
        }
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

If the deploy-immediately option was not used, the following URL should
be queried approximately every 10 seconds, waiting for the status value
to be FINISHED, FAILED or CANCELED:

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    GET: https://<mgmtip>/mgmt/cm/firewall/tasks/deploy-configuration/70e8c87d-cec6-4ed5-8de4-88682ff3bd63

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

If the task reaches the FINISHED status, the ``deviceDetails`` for the
main task and ``childDeployTasks`` should be checked for the
``verificationCriticalErrorCount`` and ``verificationErrorCount`` as
shown in the following.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

If however, the status does not reach FINISHED or either count is not 0,
consult the BIG-IQ Centralized Management Network Security Deployment
page to determine the issue encountered with the deployment evaluation
task.

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

        “childDeployTasks”: [
            .
            .
            "deviceDetails": [
                {
                    "deviceReference": {
                        "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-shared-allSharedDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"
                    },
                    "differenceCount": 4,
                    "hostname": "bigip25.f5.com",
                    "postDeploymentErrorCount": 0,
                    "verificationCriticalErrorCount": 0,
                    "verificationErrorCount": 1
                }
            ],
            .
            .
        ],
        .
        .
        "deviceDetails": [
            {
                "deviceReference": {
                    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"
                },
                "differenceCount": 4,
                "hostname": "bigip25.f5.com",
                "postDeploymentErrorCount": 0,
                "verificationCriticalErrorCount": 0,
                "verificationErrorCount": 1
            }
        ],

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

If the verification counts are all 0, then the deployment evaluation
phase did not find any issues and the deployment can continue.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

Perform a PATCH operation on the existing deployment task as follows and
then continue to the next step.

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    PATCH:  https://<mgmtip>/mgmt/cm/firewall/tasks/deploy-configuration/70e8c87d-cec6-4ed5-8de4-88682ff3bd63

    {
        "skipDistribution": false,
        "status": "STARTED"
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: 6. Check the status of the deployment of the firewall
   configuration changes to the network.
   :name: _6_check_the_status_of_the_deployment_of_the_firewall_configuration_changes_to_the_network

.. raw:: html

   <div class="paragraph">

Check that the deployment task has completed without errors. Poll the
deployment task as outlined previously, looking for the status of
FINISHED, FAILED or CANCELED. The optional select is used to limit the
return JSON content to the elements interested.

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    GET: https://<mgmtip>/mgmt/cm/firewall/tasks/deploy-configuration/70e8c87d-cec6-4ed5-8de4-88682ff3bd63?$select=name,status

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

The final task response JSON should look similar to the following:

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
        "name": "Policy Deploy",
        "status": "FINISHED",
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

If the status does not reach FINISHED, consult the Network Security
Deployment page in the BIG-IQ Centralized Management user interface to
determine the issue encountered with the deployment task.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

###Common Errors

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

##Error generated when an incorrect URI is sent in the REST request

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

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

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

#GET response when no objects are found based on the filter criteria

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
      "selfLink": "https://localhost/mgmt/cm/firewall/working-config/policies",
      "totalItems": 0,
      "items": [],
      "generation": 14,
      "kind": "cm:firewall:working-config:policies:policycollectionstate",
      "lastUpdateMicros": 1474033768399515
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

#PATCH response to a deleted evaluation task

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

    {
        "code": 404,
        "kind": ":resterrorresponse",
        "message": "cm/firewall/tasks/deploy-configuration/3d702bd0-5963-4949-a1b5-279191054fa8",
        "originalRequestBody": "{\"skipDistribution\":false,\"status\":\"STARTED\",\"generation\":0,\"lastUpdateMicros\":0}",
        "referer": "10.145.192.11",
        "restOperationId": 4644482
    }

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: API references used to support this workflow:
   :name: _api_references_used_to_support_this_workflow

.. raw:: html

   <div class="paragraph">

`Api reference - firewall
policies <../html-reference/firewall-policies.html>`__

`Api reference - firewall contexts <../html-reference/firewalls.html>`__

`Api reference -
deploy-configuration <../html-reference/deploy-configuration.html>`__

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div id="footer">

.. raw:: html

   <div id="footer-text">

Last updated 2016-12-14 10:18:57 EST

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>
