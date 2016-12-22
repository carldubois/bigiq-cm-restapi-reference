License initiate
^^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ Licensing inital activation.
   :name: big-iq-licensing-inital-activation.

.. raw:: html

   </div>

.. raw:: html

   <div id="content">

.. raw:: html

   <div class="sect1">

.. rubric:: Overview
   :name: _overview

.. raw:: html

   <div class="sectionbody">

.. raw:: html

   <div class="paragraph">

API used activate a BIG-IP license of varying types.

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Version information
   :name: _version_information

.. raw:: html

   <div class="paragraph">

*Version* : 5.2

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: URI scheme
   :name: _uri_scheme

.. raw:: html

   <div class="paragraph">

| *BasePath* : /mgmt/cm/device/licensing/pool/
| *Schemes* : HTTPS

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Consumes
   :name: _consumes

.. raw:: html

   <div class="ulist">

-  ``application/json``

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Produces
   :name: _produces

.. raw:: html

   <div class="ulist">

-  ``application/json``

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect1">

.. rubric:: Paths
   :name: _paths

.. raw:: html

   <div class="sectionbody">

.. raw:: html

   <div class="sect2">

.. rubric:: BIG-IQ initial activation using API.
   :name: _initial-activation_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /initial-activation

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description

.. raw:: html

   <div class="paragraph">

Using this BIG-IQ API you can activate a BIG-IP license of varying
types. This endpoint is a common starting point for activating a
pool-style regkey (utility, volume, purchased, etc..)

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                              | Schema                                                                 | Default   |
+============+=======================================+==========================================================================================================================================+========================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {"regkey": "MY-REGISTRATION-KEY", "name": "freeform name", "status": "ACTIVATING\_AUTOMATIC"}   | `post\_initial\_activation\_body <#_post_initial_activation_body>`__   |           |
|            | | *required*                          |                                                                                                                                          |                                                                        |           |
+------------+---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+--------------------------------------------------+-------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                  |
+=============+==================================================+=========================================================================+
| **200**     | POST to create license activation task.          | `properties\_initial\_activation <#_properties_initial_activation>`__   |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------+
| **400**     | Error response Bad Request                       | `400\_error\_collection <#_400_error_collection>`__                     |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                     |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: BIG-IQ initial activation using API.
   :name: _initial-activation_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /initial-activation

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_2

.. raw:: html

   <div class="paragraph">

Using this BIG-IQ API you can activate a BIG-IP license of varying
types. This endpoint is a common starting point for activating a
pool-style regkey (utility, volume, purchased, etc..)

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+--------------------------------------------------+------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                         |
+=============+==================================================+================================================================================================+
| **200**     | POST to create license activation task.          | `properties\_initial\_activation\_collection <#_properties_initial_activation_collection>`__   |
+-------------+--------------------------------------------------+------------------------------------------------------------------------------------------------+
| **400**     | Error response Bad Request                       | `400\_error\_collection <#_400_error_collection>`__                                            |
+-------------+--------------------------------------------------+------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                            |
+-------------+--------------------------------------------------+------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: BIG-IQ returns the activation task using for licensing.
   :name: _initial-activation_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /initial-activation/{objectId}

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_3

.. raw:: html

   <div class="paragraph">

Returns the activation task allowing the user to poll for status.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+------------------+------------------------------------------+----------------+-----------+
| Type       | Name             | Description                              | Schema         | Default   |
+============+==================+==========================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to activation task.   | string(UUID)   | None      |
|            | | *required*     |                                          |                |           |
+------------+------------------+------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+--------------------------------------------------+-------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                  |
+=============+==================================================+=========================================================================+
| **200**     | BIG-IQ activation task.                          | `properties\_initial\_activation <#_properties_initial_activation>`__   |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------+
| **400**     | Server error response Bad Request.               | `400\_error\_collection <#_400_error_collection>`__                     |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                     |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect1">

.. rubric:: Definitions
   :name: _definitions

.. raw:: html

   <div class="sectionbody">

.. raw:: html

   <div class="sect2">

.. rubric:: 400\_error\_collection
   :name: _400_error_collection

+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                         | Schema             |
+============================+=====================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                 | string             |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of activation task objects                                                                                               | < object > array   |
| | *optional*               |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for initial activation task - cm:device:licensing:pool:initial-activation:initialactivationworkercollectionstate   | string             |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                 | string             |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                            | string             |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                               | integer(int64)     |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: 404\_error\_collection
   :name: _404_error_collection

+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                         | Schema             |
+============================+=====================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                 | string             |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of activation task objects.                                                                                              | < object > array   |
| | *optional*               |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for initial activation task - cm:device:licensing:pool:initial-activation:initialactivationworkercollectionstate   | string             |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                 | string             |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                            | string             |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                               | integer(int64)     |
| | *optional*               |                                                                                                                                     |                    |
| | *read-only*              |                                                                                                                                     |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_initial\_activation\_body
   :name: _post_initial_activation_body

+----------------+------------------------------------------------------------------------------+----------+
| Name           | Description                                                                  | Schema   |
+================+==============================================================================+==========+
| | **name**     | Name of activation process.                                                  | string   |
| | *optional*   |                                                                              |          |
+----------------+------------------------------------------------------------------------------+----------+
| | **regKey**   | Base registration key.                                                       | string   |
| | *optional*   |                                                                              |          |
+----------------+------------------------------------------------------------------------------+----------+
| | **status**   | The state or type of activation process to use. ex. ACTIVATING\_AUTOMATIC.   | string   |
| | *optional*   |                                                                              |          |
+----------------+------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_initial\_activation
   :name: _properties_initial_activation

+----------------+-------------------------------+---------------------------------------------------------------+
| Name           | Description                   | Schema                                                        |
+================+===============================+===============================================================+
| | **items**    | Activation task properties.   | < `items <#_properties_initial_activation_items>`__ > array   |
| | *optional*   |                               |                                                               |
+----------------+-------------------------------+---------------------------------------------------------------+

.. raw:: html

   <div id="_properties_initial_activation_items" class="paragraph">

**items**

.. raw:: html

   </div>

+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| Name                        | Description                                                                                                              | Schema                                                                    |
+=============================+==========================================================================================================================+===========================================================================+
| | **dossier**               | Auto-generated passphrase used for activation.                                                                           | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **encryptedPrivateKey**   | Encrypted private key used during calculation.                                                                           | < integer > array                                                         |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **generation**            | A integer that will track change made.                                                                                   | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **internalPrivateKey**    | Internal encrypted key used during calculation.                                                                          | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **kind**                  | Type information for initial activation. cm:device:licensing:pool:initial-activation:initialactivationworkeritemstate.   | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **lastUpdateMicros**      | Update time (micros) for last change made to a activation task.                                                          | integer                                                                   |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **licenseReference**      | Reference link to pool license used for activation.                                                                      | `licenseReference <#_properties_initial_activation_licensereference>`__   |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **licenseText**           | Contents of license file.                                                                                                | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **message**               | Status message to user. ex. License BASE-REG-KEY ready.                                                                  | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **name**                  | Name of initial activation task license type. ex. Purchased-Pools                                                        | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **publicKey**             | Public key used during calculation.                                                                                      | < integer > array                                                         |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **regKey**                | Base registration key.                                                                                                   | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **selfLink**              | Reference link to activation task.                                                                                       | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **sortName**              | Name used to intentify sorting status. ex. Pending                                                                       | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| | **status**                | Status of license key activation. ex. READY                                                                              | string                                                                    |
| | *optional*                |                                                                                                                          |                                                                           |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_initial_activation_licensereference"
   class="paragraph">

**licenseReference**

.. raw:: html

   </div>

+----------------+-----------------------------------+----------+
| Name           | Description                       | Schema   |
+================+===================================+==========+
| | **link**     | Reference link to license data.   | string   |
| | *optional*   |                                   |          |
+----------------+-----------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_initial\_activation\_collection
   :name: _properties_initial_activation_collection

+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                                  | Schema             |
+==========================+==============================================================================================================================+====================+
| | **generation**         | A integer that will track change made.                                                                                       | string             |
| | *optional*             |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Array of initial activation task properties.                                                                                 | < object > array   |
| | *optional*             |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for initial activation task. cm:device:licensing:pool:initial-activation:initialactivationworkeritemstate   | string             |
| | *optional*             |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to a initial activation task object. time.                                         | string             |
| | *optional*             |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | Reference link to initial activation task object.                                                                            | string             |
| | *optional*             |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+

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

Last updated 2016-12-07 16:37:03 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
