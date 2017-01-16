Device trust
^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ Device Trust
   :name: big-iq-device-trust

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

API used to create a device trust certificate between BIG-IQ and BIG-IP.

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

| *BasePath* : /mgmt/cm/global/tasks
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

.. rubric:: List all device-trust task items.
   :name: _device-trust_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /device-trust

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

Returns the collection of device-trust tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------+-----------+
| Type       | Name                              | Description                                                                                                                                     | Schema                                                     | Default   |
+============+===================================+=================================================================================================================================================+============================================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to device trust task.                                                                                                        | string(UUID)                                               | None      |
|            | | *required*                      |                                                                                                                                                 |                                                            |           |
+------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. Ex. {"address":"10.90.2.22","userName":"admin","password":"admin","clusterName":"","useBigiqSync":false}   | `post\_device\_trust\_body <#_post_device_trust_body>`__   | None      |
|            | | *required*                      |                                                                                                                                                 |                                                            |           |
+------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+-------------------------------------+------------------------------------------------------------------------+
| HTTP Code   | Description                         | Schema                                                                 |
+=============+=====================================+========================================================================+
| **200**     | Collection of device-trust tasks.   | `properties\_device\_trust\_post <#_properties_device_trust_post>`__   |
+-------------+-------------------------------------+------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"        | `400\_error\_collection <#_400_error_collection>`__                    |
+-------------+-------------------------------------+------------------------------------------------------------------------+
| **404**     | Public URI path not registered.     | `404\_error\_collection <#_404_error_collection>`__                    |
+-------------+-------------------------------------+------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all device-trust task items.
   :name: _device-trust_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /device-trust

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

Returns the collection of device-trust tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+-------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                         | Schema                                                 |
+=============+=====================================+========================================================+
| **200**     | Collection of device-trust tasks.   | `properties\_collection <#_properties_collection>`__   |
+-------------+-------------------------------------+--------------------------------------------------------+
| **400**     | Error response "Bad Request"        | `400\_error\_collection <#_400_error_collection>`__    |
+-------------+-------------------------------------+--------------------------------------------------------+
| **404**     | Public URI path not registered.     | `404\_error\_collection <#_404_error_collection>`__    |
+-------------+-------------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single device-trust task.
   :name: _device-trust_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /device-trust/{objectId}

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

Returns the device-trust identified by id for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+------------------+--------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                | Schema         | Default   |
+============+==================+============================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to device trust task.   | string(UUID)   | None      |
|            | | *required*     |                                            |                |           |
+------------+------------------+--------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+----------------------------------------+------------------------------------------------------------+
| HTTP Code   | Description                            | Schema                                                     |
+=============+========================================+============================================================+
| **200**     | Device-trust object.                   | `properties\_device-trust <#_properties_device-trust>`__   |
+-------------+----------------------------------------+------------------------------------------------------------+
| **400**     | Server error response "Bad Request".   | `400\_error\_collection <#_400_error_collection>`__        |
+-------------+----------------------------------------+------------------------------------------------------------+
| **404**     | Public URI path not registered.        | `404\_error\_collection <#_404_error_collection>`__        |
+-------------+----------------------------------------+------------------------------------------------------------+

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

+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                       | Schema             |
+============================+===================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                               | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of device-trust task objects.                                                          | < object > array   |
| | *optional*               |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for device-trust collections-cm:global:tasks:device-trust:bigiptrusttaskstate.   | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                               | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                          | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                             | integer(int64)     |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: 404\_error\_collection
   :name: _404_error_collection

+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                       | Schema             |
+============================+===================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                               | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of device-trust task objects.                                                          | < object > array   |
| | *optional*               |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for device-trust collections-cm:global:tasks:device-trust:bigiptrusttaskstate.   | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                               | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                          | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                             | integer(int64)     |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_collection
   :name: _properties_collection

+--------------------------+-------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                               | Schema             |
+==========================+===========================================================================================+====================+
| | **generation**         | An integer that will track change made to a device trust collection object. generation.   | integer(int64)     |
| | *optional*             |                                                                                           |                    |
| | *read-only*            |                                                                                           |                    |
+--------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Collection of device-trust task objects.                                                  | < object > array   |
| | *optional*             |                                                                                           |                    |
+--------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this device trust collection object.                                 | string             |
| | *optional*             |                                                                                           |                    |
| | *read-only*            |                                                                                           |                    |
+--------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to a device trust collection object. time.      | integer(int64)     |
| | *optional*             |                                                                                           |                    |
| | *read-only*            |                                                                                           |                    |
+--------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the device trust collection object.                               | string             |
| | *optional*             |                                                                                           |                    |
| | *read-only*            |                                                                                           |                    |
+--------------------------+-------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_device-trust
   :name: _properties_device-trust

+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Name                      | Description                                                                                                                                                 | Schema                                                                          |
+===========================+=============================================================================================================================================================+=================================================================================+
| | **address**             | IP address of device object.                                                                                                                                | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **clusterName**         | DSC cluster name of device object to be managed. None if not part of a cluster group.                                                                       | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **currentStep**         | State machine current step for device trust task.                                                                                                           | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **endDateTime**         | Date/Time when device trust task end. 2016-10-11T10:30:17.834-0400                                                                                          | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **generation**          | An integer that will track change made to a device-trust object. generation.                                                                                | integer(int64)                                                                  |
| | *optional*              |                                                                                                                                                             |                                                                                 |
| | *read-only*             |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **id**                  | Unique id assigned to a device trust task object.                                                                                                           | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
| | *read-only*             |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **identityReference**   | Array of reference links to user used to estabish trust. mgmt/shared/authz/users/admin                                                                      | < `identityReference <#_properties_device-trust_identityreference>`__ > array   |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **isChassisDevice**     | Is this device virtual or appliance. (True / False)                                                                                                         | boolean                                                                         |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **kind**                | Type information for this device trust object.                                                                                                              | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
| | *read-only*             |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **lastUpdateMicros**    | Update time (micros) for last change made to a policy object. time.                                                                                         | integer(int64)                                                                  |
| | *optional*              |                                                                                                                                                             |                                                                                 |
| | *read-only*             |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **machineId**           | A unique id string for the BIGIP device.                                                                                                                    | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **ownerMachineId**      | A unique id string for the BIGIQ acting as a device owner.                                                                                                  | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
| | *read-only*             |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **password**            | Password of device object to be managed.                                                                                                                    | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **selfLink**            | A reference link URI to the device trust object.                                                                                                            | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
| | *read-only*             |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **stateDateTime**       | Date/Time when device trust task began. 2016-10-11T10:30:17.834-0400                                                                                        | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **status**              | Status of device trust during state transistion.                                                                                                            | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **useBigiqSync**        | To enable DSC configuration sync. True / False. When enabled, the BIG-IQ will manually synchronize configurations changes between members in a DSC group.   | boolean                                                                         |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **userName**            | Username of BIGIQ device object.                                                                                                                            | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **userReference**       | Reference link to user used to estabish trust. mgmt/shared/authz/users/admin                                                                                | `userReference <#_properties_device-trust_userreference>`__                     |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **username**            | User name of device object to be managed.                                                                                                                   | string                                                                          |
| | *optional*              |                                                                                                                                                             |                                                                                 |
+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_device-trust_identityreference"
   class="paragraph">

**identityReference**

.. raw:: html

   </div>

+----------------+------------------------------------------------------------+----------+
| Name           | Description                                                | Schema   |
+================+============================================================+==========+
| | **link**     | Array of user reference links used to discovery devices.   | string   |
| | *optional*   |                                                            |          |
+----------------+------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_device-trust_userreference" class="paragraph">

**userReference**

.. raw:: html

   </div>

+----------------+------------------------------------------------------+----------+
| Name           | Description                                          | Schema   |
+================+======================================================+==========+
| | **link**     | Reference link to a user used to discover devices.   | string   |
| | *optional*   |                                                      |          |
+----------------+------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_device\_trust\_body
   :name: _post_device_trust_body

+----------------------+-----------------------------------------------------------------------------------------+-----------+
| Name                 | Description                                                                             | Schema    |
+======================+=========================================================================================+===========+
| | **address**        | IP address of device object.                                                            | string    |
| | *required*         |                                                                                         |           |
+----------------------+-----------------------------------------------------------------------------------------+-----------+
| | **userName**       | Username of device object.                                                              | string    |
| | *required*         |                                                                                         |           |
+----------------------+-----------------------------------------------------------------------------------------+-----------+
| | **password**       | Password of device object to be managed.                                                | string    |
| | *required*         |                                                                                         |           |
+----------------------+-----------------------------------------------------------------------------------------+-----------+
| | **clusterName**    | DSC cluster name of device object to be managed. None if not part of a cluster group.   | string    |
| | *required*         |                                                                                         |           |
+----------------------+-----------------------------------------------------------------------------------------+-----------+
| | **useBigiqSync**   | To enable DSC configuration sync. True / False                                          | boolean   |
| | *required*         |                                                                                         |           |
+----------------------+-----------------------------------------------------------------------------------------+-----------+

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

Last updated 2017-01-13 13:13:45 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
