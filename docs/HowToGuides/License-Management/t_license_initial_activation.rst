.. raw:: html

   <div id="header">

.. raw:: html

   </div>

.. raw:: html

   <div id="content">

.. raw:: html

   <div class="sect1">

.. rubric:: Initial Activation of license
   :name: _initial_activation_of_license

.. raw:: html

   <div class="sectionbody">

.. raw:: html

   <div class="sect2">

.. rubric:: Overview
   :name: _overview

.. raw:: html

   <div class="paragraph">

Using the BIG-IQ REST API, you can activate a BIG-IP license of various
types. This endpoint is the common starting point for activating a
Pool-style regkey (e.g.: Utility License, Volume License, etc.). Clients
use this endpoint to perform the initial activation of the top-level
regkey, then they perform all other license actions in the relevant
collection.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

For automatic activation, the system will obtain license text from the
F5 server without user intervention. For manual activation, the client
will be provided with a dossier, which they must then activate at the F5
licensing web portal. The client obtains license text there, and inputs
it back in this collection in order to complete this manual activation
step. Note: Automatic activation would typically involve requiring the
user to accept EULA text before proceeding. For manual activation, this
happens on the web portal.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

Once license text is obtained, this worker will determine what kind of
license it represents. Using that information, it will create an entry
in the appropriate specific license collection. For instance, a
purchased pool License regkey would result in an entry being created in
/cm/device/licensing/pool/purchased-pool/licenses.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

A Reference to the item in that collection will be stored, and made
available to the client.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

For the case of automatic activation, this worker will wait for the
activation process to finish in the specific collection. This would
typically be a multi-step process, as each offering will need to be
activated. Eventually, either success or failure will be encountered,
and that information will be propagated to the user. In this way, for
automatic activation, the client need not perform any additional action
other than the initial POST, and then wait for the result.

.. raw:: html

   </div>

.. raw:: html

   <div class="paragraph">

For manual activation, the process is necessarily more involved. As
before, an item will be created in the relevant license collection based
on the initial license text. However, for manual activation, this worker
will be done at that point. The client must go visit that collection
(through the provided Reference) and complete manual activation there.
The client will need to use that license collection’s specific API to
finish manual activation

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Prerequisities
   :name: _prerequisities

.. raw:: html

   <div class="paragraph">

You should be sure the following prerequisites have been met.

.. raw:: html

   </div>

.. raw:: html

   <div class="ulist">

-  The BIG-IQ Centralized Management system is operational, has
   completed the setup wizard, and completed any other needed
   configuration.

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: 1. Start initial activation of a license.
   :name: _1_start_initial_activation_of_a_license

.. raw:: html

   <div class="paragraph">

POST https://ip/mgmt/cm/device/licensing/pool/initial-activation

.. raw:: html

   </div>

.. raw:: html

   <div class="listingblock">

.. raw:: html

   <div class="content">

.. code:: highlight

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

    #### 2. Poll to get status.
    After posting the license, user should poll to check the activation status

    GET https://ip/mgmt/cm/device/licensing/pool/initial-activation/{uuid}

    Response:
    {
        "regKey" : "MY-REGISTRATION-KEY",
        "name" : "my own freeform name",
        "status" : "ACTIVATING_AUTOMATIC_NEED_EULA_ACCEPT",
        "message" : "Need EULA acceptance in order to continue",
        "eulaText" : "The exact EULA text goes here..."
    }

    #### 3. Patch to accept EULA.
    After user accepts the EULA, subsequent poll shows status of the activation process.  Eventually the activation should have a status of either ACTIVATION_FAILED or READY

    PATCH https://ip/mgmt/cm/device/licensing/pool/initial-activation/{uuid}

    Request:
    {
        "status" : "ACTIVATING_AUTOMATIC_EULA_ACCEPTED",
        "eulaText" : "The exact EULA text goes here..."
    }

    Response:
    {
        "regKey" : "MY-REGISTRATION-KEY",
        "name" : "my own freeform name",
        "status" : "ACTIVATING_AUTOMATIC_EULA_ACCEPTED",
        "eulaText" : "The exact EULA text goes here..."
    }

    #### 4. Patch to provide license text for manual activation
    For manually activation, the license text is submitted to finish the activation process

    PATCH https://ip/mgmt/cm/device/licensing/pool/initial-activation/{uuid}

    Request:
    {
        "status" : "ACTIVATING_MANUAL_LICENSE_TEXT_PROVIDED",
        "licenseText" : "The exact license text goes here..."
    }
    Response:
    {
        "regKey" : "MY-REGISTRATION-KEY",
        "name" : "my own freeform name",
        "status" : "ACTIVATING_MANUAL_LICENSE_TEXT_PROVIDED",
        "licenseText" : "The exact license text goes here..."
    }

    #### 5. Patch to re-try a failed activation
    Before re-try activation, user should check the log and error message to find the root cause of the failure.  Some of the reasons are, wrong registration key, connection error to licensing server, etc.

    PATCH https://ip/mgmt/cm/device/licensing/pool/initial-activation/{uuid}

    Request:
    {
        "status" : "ACTIVATING_AUTOMATIC",
    }

    Response:
    {
        "regKey" : "MY-REGISTRATION-KEY",
        "name" : "my own freeform name",
        "status" : "ACTIVATING_AUTOMATIC"
    }

    #### 6. Remove a failed activation

    DELETE https://ip/mgmt/cm/device/licensing/pool/initial-activation/{uuid}

.. raw:: html

   </div>

.. raw:: html

   </div>

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

`Api reference - initial license
activation <../html-reference/license-initial-activation.html>`__

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

Last updated 2016-12-14 10:26:25 EST

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>
