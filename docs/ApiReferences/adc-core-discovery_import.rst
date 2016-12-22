.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ Device Discovery for ADC Core Management.
   :name: big-iq-device-discovery-for-adc-core-management.

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

API used for discovery task management of BIGIP for the ADC namespace by
BIGIQ. This task will be used for import as well.

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

| *BasePath* : /mgmt/cm/adc-core/tasks
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

.. rubric:: Create a device discovery declare-mgmt-authority task
   managed by BIGIQ module (LTM/ADC).
   :name: _declare-mgmt-authority_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /declare-mgmt-authority

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

Create a device discovery declare-mgmt-authority task and add to
collection.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+-----------------------------------+-------------------------------------------------------+-----------------------------------------------------+-----------+
| Type       | Name                              | Description                                           | Schema                                              | Default   |
+============+===================================+=======================================================+=====================================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to device discovery task object.   | string(UUID)                                        | None      |
|            | | *required*                      |                                                       |                                                     |           |
+------------+-----------------------------------+-------------------------------------------------------+-----------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. Ex. {}           | `post\_discovery\_body <#_post_discovery_body>`__   | None      |
|            | | *required*                      |                                                       |                                                     |           |
+------------+-----------------------------------+-------------------------------------------------------+-----------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+--------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                            | Schema                                                                                                  |
+=============+========================================================+=========================================================================================================+
| **200**     | POST a device discovery declare-mgmt-authority task.   | `properties\_declare\_mgmt\_authority\_collection <#_properties_declare_mgmt_authority_collection>`__   |
+-------------+--------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                           | `error\_collection <#_error_collection>`__                                                              |
+-------------+--------------------------------------------------------+---------------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List of device declare-mgmt-authority collection tasks
   managed by BIGIQ module (LTM/ADC).
   :name: _declare-mgmt-authority_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /declare-mgmt-authority

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

Returns the collection of device discover declare-mgmt-authority tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+-------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                                             | Schema                                                                                                  |
+=============+=========================================================================+=========================================================================================================+
| **200**     | Returns a collection of device discover declare-mgmt-authority tasks.   | `properties\_declare\_mgmt\_authority\_collection <#_properties_declare_mgmt_authority_collection>`__   |
+-------------+-------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                                            | `error\_collection <#_error_collection>`__                                                              |
+-------------+-------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single device discovery declare-mgmt-authority
   task (LTM/ADC).
   :name: _declare-mgmt-authority_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /declare-mgmt-authority/{objectId}

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

Returns the device discovery declare-mgmt-authority task identified by a
endpoint URI (LTM/ADC).

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+------------------+------------------------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                                      | Schema         | Default   |
+============+==================+==================================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to this declare-mgmt-authority task object.   | string(UUID)   | None      |
|            | | *required*     |                                                                  |                |           |
+------------+------------------+------------------------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+------------------------------------------------------------------+--------------------------------------------------------------------------------+
| HTTP Code   | Description                                                      | Schema                                                                         |
+=============+==================================================================+================================================================================+
| **200**     | Device discovery declare-mgmt-authority task object. (LTM/ADC)   | `properties\_declare-mgmt-authority <#_properties_declare-mgmt-authority>`__   |
+-------------+------------------------------------------------------------------+--------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                                     | `error\_collection <#_error_collection>`__                                     |
+-------------+------------------------------------------------------------------+--------------------------------------------------------------------------------+

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

+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                                                 | Schema             |
+============================+=============================================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                                         | string             |
| | *optional*               |                                                                                                                                                             |                    |
| | *read-only*              |                                                                                                                                                             |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of device discovery declare-mgmt-authority task objects.                                                                                         | < object > array   |
| | *optional*               |                                                                                                                                                             |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for this device discovery declare-mgmt-authority task collection object. cm:adc-core:tasks:declare-mgmt-authority:dmataskcollectionstate   | string             |
| | *optional*               |                                                                                                                                                             |                    |
| | *read-only*              |                                                                                                                                                             |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                                         | string             |
| | *optional*               |                                                                                                                                                             |                    |
| | *read-only*              |                                                                                                                                                             |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                                                    | string             |
| | *optional*               |                                                                                                                                                             |                    |
| | *read-only*              |                                                                                                                                                             |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                                                       | integer(int64)     |
| | *optional*               |                                                                                                                                                             |                    |
| | *read-only*              |                                                                                                                                                             |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_declare-mgmt-authority
   :name: _properties_declare-mgmt-authority

+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| Name                             | Description                                                                                                                                                                                         | Schema                                                                                        |
+==================================+=====================================================================================================================================================================================================+===============================================================================================+
| | **copyTaskReference**          | Enable / Disable declare-mgmt-authority copy difference between working-configuration (BIGIQ) and current-configuration (BIGIP).                                                                    | `copyTaskReference <#_properties_declare-mgmt-authority_copytaskreference>`__                 |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **currentStep**                | The current step of device declare-mgmt-authority task as predicated by state.                                                                                                                      | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **deviceReference**            | Reference link to resolver for device declare-mgmt-authority to be managed by BIGIQ. (LTM / ADC)                                                                                                    | `deviceReference <#_properties_declare-mgmt-authority_devicereference>`__                     |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **differenceReference**        | Reference link to differences object containing differences between working-configuration (BIGIQ) and current-configuration (BIGIP)                                                                 | `differenceReference <#_properties_declare-mgmt-authority_differencereference>`__             |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **differencerTaskReference**   | Reference link to differencer task. Used to manage difference between working-configuration (BIGIQ) and current-configuration (BIGIP)                                                               | `differencerTaskReference <#_properties_declare-mgmt-authority_differencertaskreference>`__   |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **endDateTime**                | Date/Time when device discovery task declare-mgmt-authority ended. 2016-10-11T10:30:17.834-0400                                                                                                     | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **generation**                 | A integer that will track change made to a device discovery declare-mgmt-authority task object. generation.                                                                                         | integer(int64)                                                                                |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **id**                         | Unique id assigned to a device discovery declare-mgmt-authority task object.                                                                                                                        | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **identityReference**          | Array of reference links to user used to discover device declare-mgmt-authority. mgmt/shared/authz/users/admin                                                                                      | < `identityReference <#_properties_declare-mgmt-authority_identityreference>`__ > array       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **kind**                       | Type information for this device discovery declare-mgmt-authority task object. cm:adc-core:tasks:declare-mgmt-authority:dmataskitemstate                                                            | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **lastUpdateMicros**           | Update time (micros) for last change made to an device discovery task object. time (1476742109026835).                                                                                              | integer(int64)                                                                                |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **ownerMachineId**             | A unique id string for the BIGIQ acting as a device owner for declare-mgmt-authority. (LTM / ADC)                                                                                                   | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **reImport**                   | Flag to enable / disable re import configuration.                                                                                                                                                   | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **selfLink**                   | A reference link URI to the device discovery declare-mgmt-authority task object.                                                                                                                    | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **startDateTime**              | Date/Time when device discovery declare-mgmt-authority task began. 2016-10-11T10:30:17.834-0400                                                                                                     | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **status**                     | Status of device discovery declare-mgmt-authority task during state transistion. (LTM / ADC)                                                                                                        | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **userReference**              | Reference link to user used to discover device declare-mgmt-authority. mgmt/shared/authz/users/admin                                                                                                | `userReference <#_properties_declare-mgmt-authority_userreference>`__                         |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **username**                   | User name of device declare-mgmt-authority object to be managed. (LTM / ADC)                                                                                                                        | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **validationBypassMode**       | Enable / Disable validation check when importing configuration device. BYPASS\_NONE - no bypass (default), BYPASS\_FINAL - skip final validation phase, BYPASS\_ALL - skip all validation phases.   | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_copytaskreference"
   class="paragraph">

**copyTaskReference**

.. raw:: html

   </div>

+----------------+----------------------------------------------------------------+----------+
| Name           | Description                                                    | Schema   |
+================+================================================================+==========+
| | **link**     | Reference link to a declare-mgmt-authority copy task object.   | string   |
| | *optional*   |                                                                |          |
+----------------+----------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_devicereference"
   class="paragraph">

**deviceReference**

.. raw:: html

   </div>

+----------------+-------------------------------------------------------------+----------+
| Name           | Description                                                 | Schema   |
+================+=============================================================+==========+
| | **link**     | Reference link to declare-mgmt-authority adc task device.   | string   |
| | *optional*   |                                                             |          |
+----------------+-------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_differencereference"
   class="paragraph">

**differenceReference**

.. raw:: html

   </div>

+----------------+-----------------------------------------------------------------------------------+----------+
| Name           | Description                                                                       | Schema   |
+================+===================================================================================+==========+
| | **link**     | Reference link to shared security configuration difference report for adc-core.   | string   |
| | *optional*   |                                                                                   |          |
+----------------+-----------------------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_differencertaskreference"
   class="paragraph">

**differencerTaskReference**

.. raw:: html

   </div>

+----------------+------------------------------------------------------------------------------------+----------+
| Name           | Description                                                                        | Schema   |
+================+====================================================================================+==========+
| | **link**     | Reference link to shared security configuration difference adc-core task object.   | string   |
| | *optional*   |                                                                                    |          |
+----------------+------------------------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_identityreference"
   class="paragraph">

**identityReference**

.. raw:: html

   </div>

+----------------+-----------------------------------------------------------+----------+
| Name           | Description                                               | Schema   |
+================+===========================================================+==========+
| | **link**     | Reference link to users. /mgmt/shared/authz/users/admin   | string   |
| | *optional*   |                                                           |          |
+----------------+-----------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_userreference"
   class="paragraph">

**userReference**

.. raw:: html

   </div>

+----------------+-----------------------------------------------------------+----------+
| Name           | Description                                               | Schema   |
+================+===========================================================+==========+
| | **link**     | Reference link to users. /mgmt/shared/authz/users/admin   | string   |
| | *optional*   |                                                           |          |
+----------------+-----------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_declare\_mgmt\_authority\_collection
   :name: _properties_declare_mgmt_authority_collection

+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                                                                 | Schema             |
+==========================+=============================================================================================================================================================+====================+
| | **generation**         | A integer that will track change made to a device discovery declare-mgmt-authority task collection object. generation.                                      | integer(int64)     |
| | *optional*             |                                                                                                                                                             |                    |
| | *read-only*            |                                                                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Array of device discovery task object.                                                                                                                      | < object > array   |
| | *optional*             |                                                                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this device discovery declare-mgmt-authority task collection object. cm:adc-core:tasks:declare-mgmt-authority:dmataskcollectionstate   | string             |
| | *optional*             |                                                                                                                                                             |                    |
| | *read-only*            |                                                                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an device discovery declare-mgmt-authority task collection object. time.                                       | integer(int64)     |
| | *optional*             |                                                                                                                                                             |                    |
| | *read-only*            |                                                                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the device discovery declare-mgmt-authority task collection object.                                                                 | string             |
| | *optional*             |                                                                                                                                                             |                    |
| | *read-only*            |                                                                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_discovery\_body
   :name: _post_discovery_body

+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| Name                                 | Description                                                                             | Schema    |
+======================================+=========================================================================================+===========+
| | **deviceReference**                | Reference link to device in resolver group.                                             | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **moduleList**                     | List of modules to discover. ex. adc\_core, asm, shared\_security, firewall             | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **userName**                       | Username of device.                                                                     | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **password**                       | Password of device.                                                                     | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **rootUser**                       | Root user of device.                                                                    | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **rootPassword**                   | Root password of device.                                                                | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **automaticallyUpdateFramework**   | To update rest framework automatically. It is recommended to do so if using REST API.   | boolean   |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+

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

Last updated 2016-11-21 16:07:22 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
