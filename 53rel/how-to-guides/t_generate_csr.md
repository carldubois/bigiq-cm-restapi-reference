## Generate CSR to create a CA signed certificate using a BIG-IQ Centralized Management system

### Overview
You can use the REST API to generate a CSR and send it to the CA for signing.

### Prerequisites

You should be sure the following prerequisites have been met.

- The BIG-IQ Centralized Management system is operational, has completed the setup wizard, and completed any other needed configuration.
- When performing the tasks in this example, review the listed IP addresses and change them as appropriate for your environment. For example, if you are not running the script directly on the BIG-IQ system, you should change localhost to be the IP address of the BIG-IQ Centralized Management system.

### Description

You use the following process to create a CSR on the BIG-IQ Centralized Management system.

1. Perform a POST method on the certificate-management URI to generate the CSR.
2. Monitor the task using GET methods until the status has reached a value of FINISHED, FAILED or CANCELLED. When the GET method status value is FINISHED, the CSR generation has completed.

### Example for generating a CSR

#### 1. Perform a POST method to the certificate-management task.

Use a POST method with the following JSON on the certificate-management task to start generating the CSR.
- __command__: To generate CSR use "GENERATE_CSR" command
- __itemName__: The name of the configuration item on BIG-IQ, must contain ".csr" suffix
- __itemPartition__: The partition of the configuration item
- __durationInDays__: The length of time that certificate will be valid before expiration (in days)
- __commonName__: The certificate Common Name or "CN" to identify the host name associated with the certificate.
- __country__: The certificate country field.
- __division__: The certificate division field.
- __organization__: The certificate organization field.
- __locality__: The certificate locality field.
- __state__: The certificate state field.
- __email__: The certificate email field.
- __subjectAlternativeName__: The Subject Alternative Name that is embedded in a certificate for X509 extension purposes. Supported names include email, DNS, URI, IP, and RID. For the Subject Alternative Name field, use the format of a comma-separated list of name:value pairs.
- __keyType__: The key type for the generated key. Supported types are RSA, DSA and ECDSA
- __keySize__: The key size for the generated key. Valid values are 1024, 2048 and 4096. Only required if keyType is RSA or DSA.
- __keyCurveName__: The key curve for the generated key. Valid values are prime256v1, secp384r1 and secp521r1 . Only required if keyType is ECDSA.
- __keyPassphrase__: The key password. Only required if securityType is password. For security, it is a good idea to encrypt your key. If you provide 'normal' value, the key will be stored as unencrypted, which can put your data at risk.
- __administratorEmail__: The optional administrator email.
- __challengePassword__: The CA challenge password for the CSR.
```
POST: https://localhost/mgmt/cm/adc-core/tasks/certificate-management
{
    "command": "GENERATE_CSR",
    "itemName": "MyCACert.csr",
    "itemPartition": "Common",
    "durationInDays": 365,
    "commonName": "example.com",
    "country": "US",
    "division": "div",
    "organization": "org",
    "locality": "local",
    "state": "state",
    "email": "john@example.com",
    "subjectAlternativeName": "DNS:login.example.com,IP:192.0.2.1",
    "securityType": "password",
    "keyType": "RSA",
    "keySize": 2048,
    "keyPassphrase": "password",
    "administratorEmail": "admin@example.com",
    "challengePassword": "challengePassword"
}
```
The following is the response JSON from the previous POST method:
```
{
    "command": "GENERATE_CSR",
    "itemName": "MyCACert.csr",
    "itemPartition": "Common",
    "keyType": "RSA",
    "keySize": 2048,
    "commonName": "example.com",
    "division": "div",
    "organization": "org",
    "locality": "local",
    "state": "state",
    "country": "US",
    "subjectAlternativeName": "DNS:login.example.com,IP:172.16.1.2",
    "email": "john@example.com",
    "durationInDays": 365,
    "administratorEmail": "admin@example.com",
    "id": "6845991e-8b66-4391-a71c-1f7416473e23",
    "status": "STARTED",
    "userReference": {
        "link": "https://localhost/mgmt/shared/authz/users/admin"
    },
    "identityReferences": [{
        "link": "https://localhost/mgmt/shared/authz/users/admin"
    }],
    "ownerMachineId": "f714c000-f5f8-45bd-9e06-2a475f3f342e",
    "taskWorkerGeneration": 1,
    "generation": 1,
    "lastUpdateMicros": 1501622193221888,
    "kind": "cm:adc-core:tasks:certificate-management:certmgmttaskstate",
    "selfLink": "https://localhost/mgmt/cm/adc-core/tasks/certificate-management/6845991e-8b66-4391-a71c-1f7416473e23"
}
```

#### 2. Perform additional GET methods to the discovery task created in Step 1.

Perform additional GET methods on the selfLink returned from the Step 1. Perform them in a loop until the status reaches one of the following: FINISHED, CANCELLED or FAILED. You may use a select option to reduce the content of the returned JSON to a manageable amount.
```
GET: https://localhost/mgmt/cm/adc-core/tasks/certificate-management/6845991e-8b66-4391-a71c-1f7416473e23
```
Additional fields received on success
- __csrReference__: Reference to the CSR configuration item
- __csrText__: The CSR in text format. New lines in the text are represented by \n.
- __keyReference__: Reference to the generated key configuration item
The following is the response JSON from the GET method:
```
{
    "command": "GENERATE_CSR",
    "itemName": "MyCACert.csr",
    "itemPartition": "Common",
    "keyType": "RSA",
    "keySize": 2048,
    "commonName": "example.com",
    "division": "div",
    "organization": "org",
    "locality": "local",
    "state": "state",
    "country": "US",
    "subjectAlternativeName": "DNS:login.example.com,IP:172.16.1.2",
    "email": "john@example.com",
    "durationInDays": 365,
    "administratorEmail": "admin@example.com",
    "csrReference": {
        "id": "aa680548-26b1-3493-bca1-42040cad1518",
        "name": "aaa.csr",
        "kind": "cm:adc-core:working-config:sys:file:ssl-csr:adcsslcsrstate",
        "partition": "Common",
        "link": "https://localhost/mgmt/cm/adc-core/working-config/sys/file/ssl-csr/aa680548-26b1-3493-bca1-42040cad1518"
    },
    "csrText": "-----BEGIN CERTIFICATE REQUEST-----\nMIIC9TCCAd0CAQAwYTELMAkGA1UEBhMCVVMxCjAIBgNVBAgTAWUxCjAIBgNVBAcT\nAWQxCjAIBgNVBAoTAWMxCjAIBgNVBAsTAWIxCjAIBgNVBAMTAWExFjAUBgkqhkiG\n9w0BCQEWB2ZAZy5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCg\nTWYYdZ16hKfE6ZCwbvUxSXAOi04X8g6x4OL177HK0gXPZglxsWMWnNsFMfePj1hL\n9XzG/XsX5kJnoxK1iKARF4xxDm3uRU0WhiQl88yV63oaW51Gh8Lzeax9ZPwEpucV\niviTW5CQcfgUY7biQju4PqffMsXAM91VRM6xB0XJsrKTE9z8zgw+Au1AmNeAx/Dq\nSv5BrzJ5/Zu08dUyslC772wZtYDACuV1QnAoOfYKBX57CfV2kK7VUPivwqOHJecc\nE4bDND5uYO03dTyh0VLuCINdnE5QBHJwFhX3SgZmc70l4CB5bOtfEeZN5bHWj8ny\nj/R49KNdYX6WHopSlASVAgMBAAGgTzAQBgkqhkiG9w0BCQcxAxMBbjAWBgkqhkiG\n9w0BCQExCRYHbEBtLmNvbTAjBgkqhkiG9w0BCQ4xFjAUMBIGA1UdEQQLMAmBB2ZA\nZy5jb20wDQYJKoZIhvcNAQENBQADggEBAAk7rB+Z0i1b6c+E8n8lABxSlONc5ktc\nHz8Cyb0VnQlHEnlVNuh8ih/wkohSjEUGTXe389JAs/nmu9EH8XNWIhxKydfizez+\n2/rn8E0fi7n7TPH5NelV7wRCJ4Irg1VwoBl3VH+GPJHcRSMIm/RVUc7HHWLra2Fy\nIvKL1YoYwjgbxmXctWq4aDpIu2mrZ4NsT0Rb5Lfz/2ExfYToMOvn5I7GKVORqLuo\nCJT1XnRocr2L0dw+aSU7ZhxiRcolPO6wYFTZhdZvSA0+jct+VGoxYG7Oweureb17\nnYtQysbfGRfVqqY3Ecd+XB3ZWsNVBsVZ8z7g4vvoKsXDfz33wsQAoLc=\n-----END CERTIFICATE REQUEST-----\n",
    "endDateTime": "2017-08-01T12:50:24.696-0700",
    "filePath": "/tmp/cert-mgmt-5394076854566655482/MyCACert.key",
    "generation": 10,
    "id": "1aa670e5-dbb8-4306-a8e7-6ae054daae7c",
    "identityReferences": [
        {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
        }
    ],
    "keyReference": {
        "id": "46f012a2-3218-3062-8524-c8658c711665",
        "name": "aaa.key",
        "kind": "cm:adc-core:working-config:sys:file:ssl-key:adcsslkeystate",
        "partition": "Common",
        "link": "https://localhost/mgmt/cm/adc-core/working-config/sys/file/ssl-key/46f012a2-3218-3062-8524-c8658c711665"
    },
    "kind": "cm:adc-core:tasks:certificate-management:certmgmttaskstate",
    "lastUpdateMicros": 1501622193224853,
    "ownerMachineId": "f714c000-f5f8-45bd-9e06-2a475f3f342e",
    "progress": "Finished",
    "selfLink": "https://localhost/mgmt/cm/adc-core/tasks/certificate-management/1aa670e5-dbb8-4306-a8e7-6ae054daae7c",
    "startDateTime": "2017-08-01T12:50:22.987-0700",
    "status": "FINISHED",
    "subjectAlternativeName": "",
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

### API Reference