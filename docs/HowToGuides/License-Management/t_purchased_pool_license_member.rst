Purchased Pool License Members
==============================

Overview
~~~~~~~~

API to license a BIG-IP device with a seat of the purchased pool
license, refresh the the license or revoking the license.

Grant
~~~~~

User grants a license to a BIG-IP by POSTing a new item to the
``/members`` subcollection to grant a license to a device For a
Purchased pool license, there is only one such collection. Item 2 and
item 3 are examples for granting a seat to managed and unmanaged device
respectively.

Refresh
~~~~~~~

User could refresh a license granted to a device by PATCHing the end
point in the member subcollection(item 5). Admin credential is required
for an unmanaged device.

Revoke
~~~~~~

User could revoke a license granted to a devive by removing the end
point from the member subcollection(item 6).

1. Get all the members of a purchased pool license [GET]
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

GET
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members

    Response:
    {
        items: {
            individual member
        }
    }

2. License a managed device by adding it to the purchased pool license.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is the typical case, where a managed device is granted a seat. It
is a relatively simple process, since trust is already established with
the device. User should poll the individual member to check licensing
status

::

POST
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members

    Request:
    {
        "deviceReference": {
                "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/267a2427-daa7-4e33-963f-300dbbe1a9f6"
        }
    }

    Response:
    {
        "uuid": "1c353141-3738-4bd1-9daa-48450e88cf63",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/267a2427-daa7-4e33-963f-300dbbe1a9f6"
        },
        "state": "LICENSED",
        "generation": 2,
        "lastUpdateMicros": 1392154597441615,
        "kind": "cm:shared:licensing:pools:licensepoolmemberstate",
        "selfLink": "https://localhost/mgmt/cm/shared/licensing/pools/858ecc73-ddb8-45d5-893b-c4f1b9b9fcbf/members/1c353141-3738-4bd1-9daa-48450e88cf63"
    }

3. License an unmanaged device by adding it to the purchased pool license.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Since managing a device can be a somewhat expensive operation, BIG-IQ
has the ability to grant licenses to unmanaged devices. This allows
supporting thousands of grants. However, licensing operations for
unmanaged grants require different inputs — instead of a
deviceReference, expected fields are an IP address, username and
password. User should poll the individual member to check licensing
status

::

POST
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members

    Request:
    {
        deviceAddress: "172.27.92.241",
        username: "username",
        password: "password"
    }

    Response:
    {
        uuid:"d3b1a0d5-e63d-43b0-a959-0ae80d7e1dad",
        deviceName:"mgmtadc2.olympus.f5net.com",
        deviceMachineId:"7db419f9-2c31-45fb-9fa5-3285fd613a06",
        deviceAddress:"172.27.92.241",
        state:"INSTALL",
        generation:1,
        lastUpdateMicros:1480540947173394,
        kind:"cm:device:licensing:pool:purchased-pool:licenses:licensepoolmemberstate",
        selfLink:"https://localhost/mgmt/cm/device/licensing/pool/purchased-pool/licenses/87a7e757-7dc8-4af3-9404-63d1c83bbf53/members/d3b1a0d5-e63d-43b0-a959-0ae80d7e1dad"
    }

4. Poll purchased pool license memeber status
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

GET
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members/{member\_uuid}

    Response:
    {
        "uuid": "1c353141-3738-4bd1-9daa-48450e88cf63",
        "deviceReference": {
            "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/267a2427-daa7-4e33-963f-300dbbe1a9f6"
        },
        "state": "LICENSED",
        "generation": 2,
        "lastUpdateMicros": 1392154597441615,
        "kind": "cm:shared:licensing:pools:licensepoolmemberstate",
        "selfLink": "https://localhost/mgmt/cm/shared/licensing/pools/858ecc73-ddb8-45d5-893b-c4f1b9b9fcbf/members/1c353141-3738-4bd1-9daa-48450e88cf63"
    }

5. Refresh a device with a purchased pool license
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

User should poll the individual member to check licensing status. Status
will become LICENSED if the process is successful.

::

PATCH
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members/{member\_uuid}

    Request:
    {
        "state":"INSTALL"
    }

    For unmanaged device, admin credential is required
    {
        username: "admin",
        password: "password",
        state: "INSTALL"
    }

    Response:
    {
        "uuid": "1c353141-3738-4bd1-9daa-48450e88cf63",
        "deviceReference": {
        "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-bigip-allBigIpDevices/devices/267a2427-daa7-4e33-963f-300dbbe1a9f6"
        },
        "state": "INSTALL",
        "generation": 2,
        "lastUpdateMicros": 1392154597441615,
        "kind": "cm:shared:licensing:pools:licensepoolmemberstate",
        "selfLink": "https://localhost/mgmt/cm/shared/licensing/pools/858ecc73-ddb8-45d5-893b-c4f1b9b9fcbf/members/1c353141-3738-4bd1-9daa-48450e88cf63"
    }

6. Revoke license from a device with a purchased pool license
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

DELETE
https://ip/mgmt/cm/device/licensing/pool/purchased-pool/licenses/{uuid}/members/{member\_uuid}

    Request:
    {
        username: "username",
        password: "password",
        uuid: "d3b1a0d5-e63d-43b0-a959-0ae80d7e1dad"
    }

API references
~~~~~~~~~~~~~~
:doc:`../../ApiReferences/license-purchased-pools`
