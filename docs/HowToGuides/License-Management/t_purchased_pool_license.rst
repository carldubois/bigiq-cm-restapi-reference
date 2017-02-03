Purchased Pool Licenses
-----------------------

Overview
~~~~~~~~

The API supports activating, polling, reactivating and removing a
purchased pool license. Pool license is different from the traditional
device based license. When you use BIG-IQ to push a Pool license to a
managed device, this action is called "granting" the license. By doing
this you have "created a grant," and the BIG-IP is said to have
"occupied a seat" for the license. This is also known as a license
"assignment," and is typically done through the "/members" subcollection
for the pool license. There are two fields totalDeviceLicenses and
freeDeviceLicenses that tract the seats a purchased pool license has and
how many have been granted respectively

Activate
~~~~~~~~

User could choose to activate a purchased pool license with the API
directly instead of through the initial activation API. The steps are
almost identical. For automatic activation, the steps are \* Do a post
with regkey and activation method \* Pool the endpoint for this license
to check for status \* Patch to accept EULA \* Pool the endpoint for the
license to check the final status For manual action, steps are \* Do a
post with regkey and activation method \* Generate dossier for the
BIG-IQ \* Go to the F5 license website to accept EULA and get the
generated license \* Patch the endpoint for the license with the license
text

Reactivate
~~~~~~~~~~

This are the process to reactivate a purchased license. The steps to
reactivate automatically are as follow \* Do a patch with state=
RELICENSE and method = AUTOMATIC(item 4) \* Poll the endpoint for this
license to get the status(item 3). Since this is a reactivate, there is
not need to accept EULA. The status will end up being either failed or
licensed.

The steps to reactivate manually are as follow \* Do a patch with state=
RELICENSE and method = MANUAL(item 4) \* Get the license text from F5
licensing website and patch it to the license end point(item 7).

Remove
~~~~~~

-  To remove a purchase pool license, do a DELETE on the endpoint(item 8)

1. Poll to get purchased pool license collection
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

GET https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses

::

    Response:
    {
        items:{
            individual license
        }
    }

2. Start activation of a license.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

POST https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses

::

    Request:

    {
        "regKey" : "MY-REGISTRATION-KEY",
        "name" : "my own freeform name",
        "status" : "ACTIVATING_AUTOMATIC",
    }

    Response:
    {
        "regKey" : "MY-REGISTRATION-KEY",
        "name" : "my own freeform name",
        "status" : "ACTIVATING_AUTOMATIC",
        "message" : "Activation in progress",
    }

3. Poll to get purchased pool license status
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The desired state of a license should have a status equals to LICENSED

GET
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}

::

    Response:
    {
        "uuid": "858ecc73-ddb8-45d5-893b-c4f1b9b9fcbf",
        "baseRegKey": "AAA",
        "method": "AUTOMATIC",
        "name": "1",
        "dossier": "...",
        "eulaText": "...",
        "licenseText": "...",
        "licenseState": {
            "vendor": "F5 Networks, Inc.",
            "licensedDateTime": "2014-02-11T00:00:00-08:00",
            "licensedVersion": "4.3.0",
            "evaluationStartDateTime": "2014-02-10T00:00:00-08:00",
            "evaluationEndDateTime": "2014-03-14T00:00:00-07:00",
            "licenseEndDateTime": "2014-03-14T00:00:00-07:00",
            "licenseStartDateTime": "2014-02-10T00:00:00-08:00",
            "registrationKey": "L4792-90141-88537-01059-8877048",
            "dossier": "1a94fe2f89a443a5c52ca70f984fb3cffa1b8f1459cbe0a8ab1c00afd7e8c740d7a2",
            "authorization": "b1681f7255495fba773e7b2f286025f083908b0c9d02fb57e821b843b2ce7717255a85bd8b42759b03dd257762648e34f655a3b307b9854d4f9ef945edd3cf09c3d157cb36dbed51c916a9a7eaabb8de289201c8097a304deba34b7a81c7a697c9b83a12124758503a4ac3cbd656453f31efa957fccd0ec3d4a8532f9edf3424dd12be540f1a7addb08207bed103d9766ba08bc662c0495712f01eaf46659e39812503540121db15fa8465f243b243e162947e94ea8c404e34e3748d25101d2f48058b36963779a2d2944a4c9aa79479f258c1e75fb16f3245729756c5b97ed77a72a9c215d8905a7278cb7d205bed648f341462c1eeb0ab6d659ee909bab295",
            "usage": "F5 Internal Product Development",
            "platformId": "BIG-IQ Pool",
            "authVers": "5b",
            "serviceCheckDateTime": "2014-02-11T00:00:00-08:00",
            "serviceStatus": "As of 2014-02-11 there is no active service contract. This may inhibit your ability to upgrade your software.",
            "exclusivePlatform": [
                "BIG-IQ Pool"
            ],
            "activeModules": [
                "Purchased Pool License, 3 Instances|D921727-0228555|Recycle, VE"
            ],
            "optionalModules": [
                "1 Gbps - 3 Gbps Upgrade, plus 4 Cores",
                "Acceleration Manager, VE",
                "Advanced LTM Protocols, VE",
                "AFM, VE",
                "APM, Base, VE",
                "APM, Max CCU, VE",
                "App Mode (TMSH Only, No Root/Bash)",
                "ASM, VE",
                "Best Bundle, 1Gbps",
                "Better Bundle, 1Gbps",
                "Client Authentication",
                "DNS and GTM (1K QPS), VE",
                "DNS and GTM (250 QPS), VE",
                "DNS Services",
                "External Interface and Network HSM, VE",
                "GTM, VE",
                "IPI Subscription, 1Yr, VE",
                "IPI Subscription, 3Yr, VE",
                "LTM, 1 Gbps - 3 Gbps Upgrade, VE",
                "MSM",
                "PEM, VE",
                "PSM, VE",
                "Recycle, VE",
                "Routing Bundle, VE",
                "SDN Services, VE",
                "SSL, Forward Proxy",
                "SWG Subscription, 1Yr, VE",
                "SWG Subscription, 3Yr, VE",
                "URL Filtering Subscription, 1Yr, VE",
                "URL Filtering Subscription, 3Yr, VE",
                "WBA",
                "WBA, VE",
                "WOM, VE"
            ],
            "featureFlags": [
                {
                "featureName": "purchased_license_pool_count",
                "featureValue": "3"
                },
                {
                "featureName": "rlt_mysql",
                "featureValue": "enable"
                },
                {
                "featureName": "rlt_geoip",
                "featureValue": "enable"
                },
                {
                "featureName": "rlt_extremesql",
                "featureValue": "enable"
                },
                {
                "featureName": "rlt_extremedb",
                "featureValue": "enable"
                },
                {
                "featureName": "purchased_license_pool_grace_period",
                "featureValue": "1"
                },
                {
                "featureName": "purchased_license_pool",
                "featureValue": "enabled"
                },
                {
                "featureName": "license_recycle",
                "featureValue": "enabled"
                },
                {
                "featureName": "license_manager_key",
                "featureValue": "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQklqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FROEFNSUlCQ2dLQ0FRRUF3b1piQU0yWmsyY1U2S1Zia2xyWWdUaThCU3lhK3NaVgpYZjRoc292anEwd0RkczJrZlk2NWhYVVYxeXU0SWdITzdaZkFYVnlpV2orYkM5TU1jSVlpMUx6S3ZzZnI0MDA4NHFtNW5ob1Q3aG0xCit4cys1RVpTYk5adFpIZThWalBUVVZxWUdRMTE3MHYwNHNRWEoxNURxWVpncjN5Rktrc0NaSjVzblIxaFFWcGR3OC9wUmZsUWVmZUMKemNpSGtLM1RKMGVKT3doQyswVTJRUUU1QXdxeG1lQnFZb0dQZmZITk1qaXZCRWxJcEthU2l4U1lFYWtOdUgzdGVROVJxa3lVZXlrNgpGUUdTMVRqMEt3enArTEFmK1QwTVFYcG82a3E3ZE5wTXFCNGdMOHFYN2tQS01FQWdYeGdORm0vRVY0bUlzMDdQeUlJcDcvZU4wQTJnCk5MYnhmd0lEQVFBQgotLS0tLUVORCBQVUJMSUMgS0VZLS0tLS0K"
                }
            ],
            "generation": 0,
            "lastUpdateMicros": 0
        },
        "totalDeviceLicenses": 3,
        "freeDeviceLicenses": 3,
        "state": "LICENSED",
        "publicKey": [],
        "privateKey": "...",
        "registeredKey": [],
        "generation": 4,
        "lastUpdateMicros": 1392147649399191,
        "kind": "cm:shared:licensing:pools:licensepoolworkerstate",
        "selfLink": "https://localhost/mgmt/cm/shared/licensing/pools/858ecc73-ddb8-45d5-893b-c4f1b9b9fcbf"
        },
    }

4. Reactivate a purchased pool license:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

During the process, user could poll the license to check for status of
reactivation process

PATCH
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}

::

    Request:
    {
        state: "RELICENSE",
        method: "AUTOMATIC"
    }

    Response:
    {
        "uuid": "858ecc73-ddb8-45d5-893b-c4f1b9b9fcbf",
        "baseRegKey": "AAA",
        "method": "AUTOMATIC",
        "name": "1",
        "dossier": "...",
        "eulaText": "...",
        "licenseText": "...",
        "licenseState": {
            "vendor": "F5 Networks, Inc.",
            "licensedDateTime": "2014-02-11T00:00:00-08:00",
            "licensedVersion": "4.3.0",
            "evaluationStartDateTime": "2014-02-10T00:00:00-08:00",
            "evaluationEndDateTime": "2014-03-14T00:00:00-07:00",
            "licenseEndDateTime": "2014-03-14T00:00:00-07:00",
            "licenseStartDateTime": "2014-02-10T00:00:00-08:00",
            "registrationKey": "L4792-90141-88537-01059-8877048",
            "dossier": "1a94fe2f89a443a5c52ca70f984fb3cffa1b8f1459cbe0a8ab1c00afd7e8c740d7a2",
            "authorization": "b1681f7255495fba773e7b2f286025f083908b0c9d02fb57e821b843b2ce7717255a85bd8b42759b03dd257762648e34f655a3b307b9854d4f9ef945edd3cf09c3d157cb36dbed51c916a9a7eaabb8de289201c8097a304deba34b7a81c7a697c9b83a12124758503a4ac3cbd656453f31efa957fccd0ec3d4a8532f9edf3424dd12be540f1a7addb08207bed103d9766ba08bc662c0495712f01eaf46659e39812503540121db15fa8465f243b243e162947e94ea8c404e34e3748d25101d2f48058b36963779a2d2944a4c9aa79479f258c1e75fb16f3245729756c5b97ed77a72a9c215d8905a7278cb7d205bed648f341462c1eeb0ab6d659ee909bab295",
            "usage": "F5 Internal Product Development",
            "platformId": "BIG-IQ Pool",
            "authVers": "5b",
            "serviceCheckDateTime": "2014-02-11T00:00:00-08:00",
            "serviceStatus": "As of 2014-02-11 there is no active service contract. This may inhibit your ability to upgrade your software.",
            "exclusivePlatform": [
                "BIG-IQ Pool"
            ],
            "activeModules": [
                "Purchased Pool License, 3 Instances|D921727-0228555|Recycle, VE"
            ],
            "optionalModules": [
                "1 Gbps - 3 Gbps Upgrade, plus 4 Cores",
                "Acceleration Manager, VE",
                "Advanced LTM Protocols, VE",
                "AFM, VE",
                "APM, Base, VE",
                "APM, Max CCU, VE",
                "App Mode (TMSH Only, No Root/Bash)",
                "ASM, VE",
                "Best Bundle, 1Gbps",
                "Better Bundle, 1Gbps",
                "Client Authentication",
                "DNS and GTM (1K QPS), VE",
                "DNS and GTM (250 QPS), VE",
                "DNS Services",
                "External Interface and Network HSM, VE",
                "GTM, VE",
                "IPI Subscription, 1Yr, VE",
                "IPI Subscription, 3Yr, VE",
                "LTM, 1 Gbps - 3 Gbps Upgrade, VE",
                "MSM",
                "PEM, VE",
                "PSM, VE",
                "Recycle, VE",
                "Routing Bundle, VE",
                "SDN Services, VE",
                "SSL, Forward Proxy",
                "SWG Subscription, 1Yr, VE",
                "SWG Subscription, 3Yr, VE",
                "URL Filtering Subscription, 1Yr, VE",
                "URL Filtering Subscription, 3Yr, VE",
                "WBA",
                "WBA, VE",
                "WOM, VE"
            ],
            "featureFlags": [
                {
                "featureName": "purchased_license_pool_count",
                "featureValue": "3"
                },
                {
                "featureName": "rlt_mysql",
                "featureValue": "enable"
                },
                {
                "featureName": "rlt_geoip",
                "featureValue": "enable"
                },
                {
                "featureName": "rlt_extremesql",
                "featureValue": "enable"
                },
                {
                "featureName": "rlt_extremedb",
                "featureValue": "enable"
                },
                {
                "featureName": "purchased_license_pool_grace_period",
                "featureValue": "1"
                },
                {
                "featureName": "purchased_license_pool",
                "featureValue": "enabled"
                },
                {
                "featureName": "license_recycle",
                "featureValue": "enabled"
                },
                {
                "featureName": "license_manager_key",
                "featureValue": "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQklqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FROEFNSUlCQ2dLQ0FRRUF3b1piQU0yWmsyY1U2S1Zia2xyWWdUaThCU3lhK3NaVgpYZjRoc292anEwd0RkczJrZlk2NWhYVVYxeXU0SWdITzdaZkFYVnlpV2orYkM5TU1jSVlpMUx6S3ZzZnI0MDA4NHFtNW5ob1Q3aG0xCit4cys1RVpTYk5adFpIZThWalBUVVZxWUdRMTE3MHYwNHNRWEoxNURxWVpncjN5Rktrc0NaSjVzblIxaFFWcGR3OC9wUmZsUWVmZUMKemNpSGtLM1RKMGVKT3doQyswVTJRUUU1QXdxeG1lQnFZb0dQZmZITk1qaXZCRWxJcEthU2l4U1lFYWtOdUgzdGVROVJxa3lVZXlrNgpGUUdTMVRqMEt3enArTEFmK1QwTVFYcG82a3E3ZE5wTXFCNGdMOHFYN2tQS01FQWdYeGdORm0vRVY0bUlzMDdQeUlJcDcvZU4wQTJnCk5MYnhmd0lEQVFBQgotLS0tLUVORCBQVUJMSUMgS0VZLS0tLS0K"
                }
            ],
            "generation": 0,
            "lastUpdateMicros": 0
        },
        "totalDeviceLicenses": 3,
        "freeDeviceLicenses": 3,
        "state": "LICENSED",
        "publicKey": [],
        "privateKey": "...",
        "registeredKey": [],
        "generation": 4,
        "lastUpdateMicros": 1392147649399191,
        "kind": "cm:shared:licensing:pools:licensepoolworkerstate",
        "selfLink": "https://localhost/mgmt/cm/shared/licensing/pools/858ecc73-ddb8-45d5-893b-c4f1b9b9fcbf"
        },
    }

6 Patch to accept EULA
^^^^^^^^^^^^^^^^^^^^^^

PATCH
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}

::

    Request: Automatic Activation Step 3 - Agree to the EULA and proceed with the licensing activation
    {
        "eulaText": "...",
        "state":"ACCEPTED_EULA"
    }

    Response:
    {
        "name": "user1",
        "displayName": "user1 nowHasALastName",
        "encryptedPassword": "$6$qwNF89JH$dDjqS7rSc8GziaQo.XQ.ypW/QGtJOGXTiBcSIxf33YRbsI4pSbAx.DlG.hEDrhgLYG8o5fspE5Cmlvv6npZ/p/",
        "generation": 2,
        "lastUpdateMicros": 1389732048843260,
        "kind": "shared:authz:users:usersworkerstate",
        "selfLink": "https://localhost/mgmt/shared/authz/users/user1"
    }

7 Patch to provide license text
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

PATCH
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}

::

    Request: Manual Activation Step 3 - Copy the license text from activate.f5.com and submit it
    {
        "licenseText": "..."
    }

    Response:
    {
        "uuid":"123",
        "name" : "pool name"
        "baseRegKey" : "ABC-XYZ",
        "addOnKeys":["DEF-UVW"],
        "method":"MANUAL",
        "dossier":"...",
        "licenseText":"...",
        "selfLink":"https://localhost/mgmt/cm/shared/licensing/pools/123"
    }

8. Delete a purchased pool license
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

DELETE
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}

API references:
~~~~~~~~~~~~~~~

:doc:`../../ApiReferences/license-purchased-pools`
