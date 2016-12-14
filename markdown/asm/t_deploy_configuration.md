## Deploying a Web Application Security configuration.

### Overview
The document describes how to use the REST API to deploy Web Application Security configuration changes as saved on BIG-IQ to BIG-IP devices.

### Prerequisites
Device configuration discovered and imported to Web Application Security.
 
### Description
The document describes how to use the REST API to deploy Web Application Security configuration changes as saved on BIG-IQ to BIG-IP devices.
Perform the REST API actions in the following order:
1. Perform a GET operation to determine the selfLink of a device.
2. Evaluate the configuration changes created by the Web Application Security configuration modifications to determine if there are errors.
3. Check the status of the deployment of the Web Application Security configuration changes to the network.

The following extended example shows each of these REST API actions.
### Example
#### 1. Perform a GET operation to determine the selfLink of a device.
Perform a GET operation on the Web Application Security devices collection, filtering the results by a name and limiting the result to show the device name and the device selfLink that will be used later for searches. In this example the name being searched for is 'device1.com'.
```
GET: https://<mgmtip>/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices?$filter=hostname eq 'device1.com'&$select=hostname,selfLink
```
The following is the JSON response from the GET operation:
```
{
    "selfLink": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices",
    "totalItems": 1,
    "items": [
        {
            "hostname": "device1.com",
            "selfLink": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/c1444144-11e7-47e6-8e91-eaa913826a7f"
        }
    ],
    "generation": 18,
    "kind": "shared:resolver:device-groups:devicegroupdevicecollectionstate",
    "lastUpdateMicros": 1479388471935401
}
```
#### 2. Evaluate the configuration changes created by the Web Application Security configuration modifications to determine if there are errors.

A deployment task must be created that includes the required BIG-IP devices.

Perform a POST operation to the following URL to create the deployment task:
```
POST: https://<mgmtip>/mgmt/cm/asm/tasks/deploy-configuration
```
The deployment can also be created in the deploy-immediately mode (where `skipDistribution` is set to false) as follows.  This type of deployment is only recommended if no warnings or errors are expected. 
```
{
    "createChildTasks": true,
    "description": "Deploy and distribute",
    "deviceReferences": [
        {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/d22358b7-2124-48f6-8fc0-3cf69fb4728b"
        }
    ],
    "name": "Deploy_1",
    "skipDistribution": false
}
```
After creating the deployment task in either of these ways, continue to the next step to determine when the deployment completes and its final status. The `deviceReferences` will be a list of device references determined from the previous step. The name and description fields should be modified to allow unique tracking of each deployment.

If there is a concern that there may be issues with the configuration, the deployment can be done in stages. The first stage is the evaluation stage. If no errors or warnings are detected during evaluation, the configuration can then be deployed to the BIG-IP device in the second stage.

The deployment evaluation is created by performing a POST of the following to the deployment task URI defined above. Once again, the name and description fields should be modified to allow unique tracking of each deployment.
```
{
    "createChildTasks": true,
    "description": "Deploy without distribution to BIG-IP",
    "deviceReferences": [
        {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/c1444144-11e7-47e6-8e91-eaa913826a7f"
        }
    ],
    "name": "Deploy_2"
    "skipDistribution": true
}
```
In either deployment case, the response JSON for the POST is as follows:
```
{
    "skipDistribution": false,
    "deviceReferences": [
        {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/d22358b7-2124-48f6-8fc0-3cf69fb4728b"
        }
    ],
    "createChildTasks": true,
    "id": "e58bb493-3fb4-4661-bee3-5e6c1cbec531",
    "status": "STARTED",
    "name": "Deploy_1",
    "description": "Deploy and distribute",
    "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
    },
    "identityReferences": [
        {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    ],
    "ownerMachineId": "415334a7-c1d7-44d4-af1a-b11fad4d9d85",
    "taskWorkerGeneration": 1,
    "generation": 1,
    "lastUpdateMicros": 1480338832043019,
    "kind": "cm:asm:tasks:deploy-configuration:deployconfigtaskstate",
    "selfLink": "https://localhost/mgmt/cm/asm/tasks/deploy-configuration/e58bb493-3fb4-4661-bee3-5e6c1cbec531"
}
```
If the deploy-immediately option was not used, the following URL should be queried approximately every 10 seconds, waiting for the status value to be FINISHED, FAILED or CANCELED:
```
GET: https://<mgmtip>/mgmt/cm/asm/tasks/deploy-configuration/e58bb493-3fb4-4661-bee3-5e6c1cbec531
```
If the task reaches the FINISHED status, the `deviceDetails` for the main task and `childDeployTasks` should be checked for the `verificationCriticalErrorCount` and `verificationErrorCount` as shown in the following.

If however, the status does not reach FINISHED or either count is not 0, consult the BIG-IQ Centralized Management Web Application Security Deployment page to determine the issue encountered with the deployment evaluation task.
```
    “childDeployTasks”: [
        .
        .
        "deviceDetails": [
            {
                "deviceReference": {
                    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-security-shared-allSharedDevices/devices/d22358b7-2124-48f6-8fc0-3cf69fb4728b"
                },
                "differenceCount": 4,
                "hostname": "device1.com",
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
            "status": "SUCCESS",
            "deviceReference": {
                "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-asm-allAsmDevices/devices/d22358b7-2124-48f6-8fc0-3cf69fb4728b"
            },
            "differenceCount": 4,
            "verificationErrorCount": 0,
            "verificationCriticalErrorCount": 0,
            "postDeploymentErrorCount": 0,
            "hostname": "device1.com"
        }
    ],
```
If the verification counts are all 0, then the deployment evaluation phase did not find any issues and the deployment can continue. 

Perform a PATCH operation on the existing deployment task as follows and then continue to the next step.
```
PATCH:  https://<mgmtip>//mgmt/cm/asm/tasks/deploy-configuration/e58bb493-3fb4-4661-bee3-5e6c1cbec531
{
    "skipDistribution": false,
    "status": "STARTED"
}
```
#### 3. Check the status of the deployment of the Web Application Security configuration changes to the network.

Check that the deployment task has completed without errors. 
Poll the deployment task as outlined previously, looking for the status of FINISHED, FAILED or CANCELED. The optional select is used to limit the return JSON content to the elements interested.
```
GET:  https://<mgmtip>//mgmt/cm/asm/tasks/deploy-configuration/e58bb493-3fb4-4661-bee3-5e6c1cbec531?$select=name,status
```
The final task response JSON should look similar to the following:
```
{
    "name": "Deploy_1",
    "status": "FINISHED",
}
```
If the status does not reach FINISHED, consult the Web Application Security Deployment page in the BIG-IQ Centralized Management user interface to determine the issue encountered with the deployment task.

### API reference used to support this workflow
[Api reference - ASM deploy configuration](../html-reference/deploy-configuration.html)