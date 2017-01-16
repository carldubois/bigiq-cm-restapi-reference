Device discovery
^^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ Device Discovery
   :name: big-iq-device-discovery

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

API used for discovery task management of BIGIP by BIGIQ.

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

.. rubric:: Create a device discovery task managed by BIGIQ module (LTM,
   AFM, ASM).
   :name: _device-discovery_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /device-discovery

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

Create a device discovery task and add to collection.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+-----------+
| Type       | Name                              | Description                                                                                                                                                                                              | Schema                                                             | Default   |
+============+===================================+==========================================================================================================================================================================================================+====================================================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to device discovery task.                                                                                                                                                             | string(UUID)                                                       | None      |
|            | | *required*                      |                                                                                                                                                                                                          |                                                                    |           |
+------------+-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. Ex. {"moduleList":[{"module":"adc\_core"}],"deviceReference":{"link":"https://localhost/mgmt/cm/system/machineid-resolver/2a2baaf0-b22f-49dc-81c6-4711fa189820"}}   | `post\_device\_discovery\_body <#_post_device_discovery_body>`__   | None      |
|            | | *required*                      |                                                                                                                                                                                                          |                                                                    |           |
+------------+-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+---------------------------------+--------------------------------------------------------------------------------------------+
| HTTP Code   | Description                     | Schema                                                                                     |
+=============+=================================+============================================================================================+
| **200**     | POST a device discovery task.   | `properties\_device\_discovery\_collection <#_properties_device_discovery_collection>`__   |
+-------------+---------------------------------+--------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"    | `error\_collection <#_error_collection>`__                                                 |
+-------------+---------------------------------+--------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List of device discovery collections managed by BIGIQ module
   (LTM, AFM, ASM).
   :name: _device-discovery_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /device-discovery

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

Returns the collection of device discovery tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+---------------------------------------------------+--------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                       | Schema                                                                                     |
+=============+===================================================+============================================================================================+
| **200**     | Returns a collection of device discovery tasks.   | `properties\_device\_discovery\_collection <#_properties_device_discovery_collection>`__   |
+-------------+---------------------------------------------------+--------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                      | `error\_collection <#_error_collection>`__                                                 |
+-------------+---------------------------------------------------+--------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single device discovery task.
   :name: _device-discovery_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /device-discovery/{objectId}

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

Returns the device discovery task identified by a endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+------------------+------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                    | Schema         | Default   |
+============+==================+================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to device discovery task.   | string(UUID)   | None      |
|            | | *required*     |                                                |                |           |
+------------+------------------+------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+--------------------------------+---------------------------------------------------------------------+
| HTTP Code   | Description                    | Schema                                                              |
+=============+================================+=====================================================================+
| **200**     | Device discovery task object   | `properties\_device\_discovery <#_properties_device_discovery>`__   |
+-------------+--------------------------------+---------------------------------------------------------------------+
| **400**     | Error response "Bad Request"   | `error\_collection <#_error_collection>`__                          |
+-------------+--------------------------------+---------------------------------------------------------------------+

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

.. rubric:: error\_collection
   :name: _error_collection

+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                             | Schema             |
+============================+=========================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                     | string             |
| | *optional*               |                                                                                                                                         |                    |
| | *read-only*              |                                                                                                                                         |                    |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of device-discovery task objects.                                                                                            | < object > array   |
| | *optional*               |                                                                                                                                         |                    |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for this device discovery task collection object. cm:global:tasks:device-discovery:discoverysupertaskcollectionstate   | string             |
| | *optional*               |                                                                                                                                         |                    |
| | *read-only*              |                                                                                                                                         |                    |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                     | string             |
| | *optional*               |                                                                                                                                         |                    |
| | *read-only*              |                                                                                                                                         |                    |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                                | string             |
| | *optional*               |                                                                                                                                         |                    |
| | *read-only*              |                                                                                                                                         |                    |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                                   | integer(int64)     |
| | *optional*               |                                                                                                                                         |                    |
| | *read-only*              |                                                                                                                                         |                    |
+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_device\_discovery
   :name: _properties_device_discovery

+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| Name                      | Description                                                                                                          | Schema                                                                              |
+===========================+======================================================================================================================+=====================================================================================+
| | **allModuleStatus**     | Discovery module status and information. (module type, discovery start time and end time 2016-10-17T22:07:31.633Z)   | < `allModuleStatus <#_properties_device_discovery_allmodulestatus>`__ > array       |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **deviceReference**     | Reference link to resolver for device to be managed by BIGIQ.                                                        | `deviceReference <#_properties_device_discovery_devicereference>`__                 |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **endDateTime**         | Date/Time when device discovery task ended. 2016-10-11T10:30:17.834-0400                                             | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **generation**          | An integer that will track change made to a device discovery task object. generation.                                | integer(int64)                                                                      |
| | *optional*              |                                                                                                                      |                                                                                     |
| | *read-only*             |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **id**                  | Unique id assigned to a device discovery task object.                                                                | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
| | *read-only*             |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **identityReference**   | Array of reference links to user used to discover device. mgmt/shared/authz/users/admin                              | < `identityReference <#_properties_device_discovery_identityreference>`__ > array   |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **kind**                | Type information for this device discovery task object.                                                              | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
| | *read-only*             |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **lastUpdateMicros**    | Update time (micros) for last change made to a device discovery task object. time (1476742109026835).                | integer(int64)                                                                      |
| | *optional*              |                                                                                                                      |                                                                                     |
| | *read-only*             |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **name**                | Name of device discovery task.                                                                                       | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **ownerMachineId**      | A unique id string for the BIGIQ acting as a device owner.                                                           | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **selfLink**            | A reference link URI to the device discovery task object.                                                            | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
| | *read-only*             |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **startDateTime**       | Date/Time when device discovery task began. 2016-10-11T10:30:17.834-0400                                             | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **status**              | Status of device discovery task during state transistion.                                                            | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **userReference**       | Reference link to user used to discover device. mgmt/shared/authz/users/admin                                        | `userReference <#_properties_device_discovery_userreference>`__                     |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
| | **username**            | User name of device object to be managed.                                                                            | string                                                                              |
| | *optional*              |                                                                                                                      |                                                                                     |
+---------------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_device_discovery_allmodulestatus"
   class="paragraph">

**allModuleStatus**

.. raw:: html

   </div>

+-------------------+---------------------------------------------------------------------------------------------------------------+----------+
| Name              | Description                                                                                                   | Schema   |
+===================+===============================================================================================================+==========+
| | **endTime**     | End time of device discovery task, per module.                                                                | string   |
| | *optional*      |                                                                                                               |          |
+-------------------+---------------------------------------------------------------------------------------------------------------+----------+
| | **module**      | Module type of device discovery task, (Module List- access, adc-core, firewall, asm, security\_shared, dns)   | string   |
| | *optional*      |                                                                                                               |          |
+-------------------+---------------------------------------------------------------------------------------------------------------+----------+
| | **startTime**   | Start time of device discovery task, per module                                                               | string   |
| | *optional*      |                                                                                                               |          |
+-------------------+---------------------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_device_discovery_devicereference"
   class="paragraph">

**deviceReference**

.. raw:: html

   </div>

+----------------+---------------------------------------------+----------+
| Name           | Description                                 | Schema   |
+================+=============================================+==========+
| | **link**     | Device reference link to device resolver.   | string   |
| | *optional*   |                                             |          |
+----------------+---------------------------------------------+----------+

.. raw:: html

   <div id="_properties_device_discovery_identityreference"
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

   <div id="_properties_device_discovery_userreference"
   class="paragraph">

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

.. rubric:: properties\_device\_discovery\_collection
   :name: _properties_device_discovery_collection

+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                                             | Schema             |
+==========================+=========================================================================================================================================+====================+
| | **generation**         | An integer that will track change made to a device discovery task collection object. generation.                                        | integer(int64)     |
| | *optional*             |                                                                                                                                         |                    |
| | *read-only*            |                                                                                                                                         |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Array of device discovery task object.                                                                                                  | < object > array   |
| | *optional*             |                                                                                                                                         |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this device discovery task collection object. cm:global:tasks:device-discovery:discoverysupertaskcollectionstate   | string             |
| | *optional*             |                                                                                                                                         |                    |
| | *read-only*            |                                                                                                                                         |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to a device discovery task collection object. time.                                           | integer(int64)     |
| | *optional*             |                                                                                                                                         |                    |
| | *read-only*            |                                                                                                                                         |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the device discovery task collection object.                                                                    | string             |
| | *optional*             |                                                                                                                                         |                    |
| | *read-only*            |                                                                                                                                         |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_device\_discovery\_body
   :name: _post_device_discovery_body

+-------------------------+-------------------------------------------------------------------------------------------------+----------+
| Name                    | Description                                                                                     | Schema   |
+=========================+=================================================================================================+==========+
| | **moduleList**        | A list of all modules to discover. ex. access, adc-core, firewall, asm, security\_shared, dns   | array    |
| | *required*            |                                                                                                 |          |
+-------------------------+-------------------------------------------------------------------------------------------------+----------+
| | **deviceReference**   | Reference link to device in resolver.                                                           | string   |
| | *required*            |                                                                                                 |          |
+-------------------------+-------------------------------------------------------------------------------------------------+----------+

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
