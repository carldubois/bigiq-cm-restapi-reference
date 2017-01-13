.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ Discovery for Web Application Security (ASM)
   Management.
   :name: big-iq-discovery-for-web-application-security-asm-management.

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

API used for discovery task management of BIGIP for the ASM (Web
Application Security) namespace by BIGIQ. Re-import will use this task
as well.

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

| *BasePath* : /mgmt/cm/asm/tasks
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
   managed by BIGIQ module (ASM).
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
collection. (ASM)

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                                  | Schema                                                                                                  |
+=============+==============================================================+=========================================================================================================+
| **200**     | POST a device discovery declare-mgmt-authority task. (ASM)   | `properties\_declare\_mgmt\_authority\_collection <#_properties_declare_mgmt_authority_collection>`__   |
+-------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                                 | `error\_collection <#_error_collection>`__                                                              |
+-------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List of device declare-mgmt-authority collection tasks
   managed by BIGIQ module (ASM).
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
(ASM)

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+-------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                                                   | Schema                                                                                                  |
+=============+===============================================================================+=========================================================================================================+
| **200**     | Returns a collection of device discover declare-mgmt-authority tasks. (ASM)   | `properties\_declare\_mgmt\_authority\_collection <#_properties_declare_mgmt_authority_collection>`__   |
+-------------+-------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                                                  | `error\_collection <#_error_collection>`__                                                              |
+-------------+-------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single device discovery declare-mgmt-authority
   task (ASM).
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
endpoint URI (ASM).

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+------------------+-----------------------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                                     | Schema         | Default   |
+============+==================+=================================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assinged to declare-mgmt-authority ASM task object.   | string(UUID)   | None      |
|            | | *required*     |                                                                 |                |           |
+------------+------------------+-----------------------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+--------------------------------------------------------------+--------------------------------------------------------------------------------+
| HTTP Code   | Description                                                  | Schema                                                                         |
+=============+==============================================================+================================================================================+
| **200**     | Device discovery declare-mgmt-authority task object. (ASM)   | `properties\_declare-mgmt-authority <#_properties_declare-mgmt-authority>`__   |
+-------------+--------------------------------------------------------------+--------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                                 | `error\_collection <#_error_collection>`__                                     |
+-------------+--------------------------------------------------------------+--------------------------------------------------------------------------------+

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

+----------------------------+-------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                   | Schema             |
+============================+===============================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                           | string             |
| | *optional*               |                                                                                                                               |                    |
| | *read-only*              |                                                                                                                               |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of device discovery ASM task objects.                                                                              | < object > array   |
| | *optional*               |                                                                                                                               |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for this device discovery ASM task collection object. cm:ASM:tasks:declare-mgmt-authority:dmataskitemstate   | string             |
| | *optional*               |                                                                                                                               |                    |
| | *read-only*              |                                                                                                                               |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                           | string             |
| | *optional*               |                                                                                                                               |                    |
| | *read-only*              |                                                                                                                               |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                      | string             |
| | *optional*               |                                                                                                                               |                    |
| | *read-only*              |                                                                                                                               |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                         | integer(int64)     |
| | *optional*               |                                                                                                                               |                    |
| | *read-only*              |                                                                                                                               |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_declare-mgmt-authority
   :name: _properties_declare-mgmt-authority

+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| Name                             | Description                                                                                                                                                                                         | Schema                                                                                        |
+==================================+=====================================================================================================================================================================================================+===============================================================================================+
| | **childTaskReference**         | Reference link to child task. shared-object security discovery.                                                                                                                                     | < `childTaskReference <#_properties_declare-mgmt-authority_childtaskreference>`__ > array     |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **childTaskStates**            | Description of child task state properties used by declare-mgmt-authority task object.                                                                                                              | < `childTaskStates <#_properties_declare-mgmt-authority_childtaskstates>`__ > array           |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **copyTaskReference**          | Enable / Disable declare-mgmt-authority ASM copy difference between working-configuration (BIGIQ) and current-configuration (BIGIP).                                                                | `copyTaskReference <#_properties_declare-mgmt-authority_copytaskreference>`__                 |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **createChildTasks**           | To create a child task as part of this declare-mgmt-authority for ASM.                                                                                                                              | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **currentStep**                | The current step of device declare-mgmt-authority ASM task as predicated by state.                                                                                                                  | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **deviceReference**            | Reference link to resolver for device to be managed by BIGIQ. (ASM)                                                                                                                                 | `deviceReference <#_properties_declare-mgmt-authority_devicereference>`__                     |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **differenceReference**        | Reference link to differences object containing differences between working-configuration (BIGIQ) and current-configuration (BIGIP)                                                                 | `differenceReference <#_properties_declare-mgmt-authority_differencereference>`__             |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **differencerTaskReference**   | Reference link to differencer task. Used to manage difference between working-configuration (BIGIQ) and current-configuration (BIGIP)                                                               | `differencerTaskReference <#_properties_declare-mgmt-authority_differencertaskreference>`__   |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **endDateTime**                | Date/Time when device discovery task declare-mgmt-authority ASM ended. 2016-10-11T10:30:17.834-0400                                                                                                 | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **generation**                 | An integer that will track change made to a device discovery declare-mgmt-authority task object. (ASM) generation.                                                                                  | integer(int64)                                                                                |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **id**                         | Unique id assigned to a device declare-mgmt-authority ASM task object.                                                                                                                              | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **identityReference**          | Array of reference links to user used to discover device declare-mgmt-authority ASM. mgmt/shared/authz/users/admin                                                                                  | < `identityReference <#_properties_declare-mgmt-authority_identityreference>`__ > array       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **kind**                       | Type information for this device discovery declare-mgmt-authority ASM task object. cm:ASM:tasks:declare-mgmt-authority:dmataskitemstate                                                             | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **lastUpdateMicros**           | Update time (micros) for last change made to a device discovery ASM task object. time (1476742109026835).                                                                                           | integer(int64)                                                                                |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **name**                       | Name of device declare-mgmt-authority task.                                                                                                                                                         | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **ownerMachineId**             | A unique id string for the BIGIQ acting as a device owner for declare-mgmt-authority. (ASM)                                                                                                         | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **reImport**                   | Flag to enable / disable re-import configuration.                                                                                                                                                   | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **selfLink**                   | A reference link URI to the device discovery declare-mgmt-authority task object. (ASM)                                                                                                              | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **snapshotWorkingConfig**      | To snapshot the working-configuration (BIGIQ) during ASM module discovery.                                                                                                                          | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **startDateTime**              | Date/Time when device discovery declare-mgmt-authority ASM task began. 2016-10-11T10:30:17.834-0400                                                                                                 | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **status**                     | Status of device declare-mgmt-authority task predicated on state.                                                                                                                                   | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **userReference**              | Reference link to user used to discover device declare-mgmt-authority ASM. mgmt/shared/authz/users/admin                                                                                            | `userReference <#_properties_declare-mgmt-authority_userreference>`__                         |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **username**                   | User name of device ASM object to be managed. (ASM)                                                                                                                                                 | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **validationBypassMode**       | Enable / Disable validation check when importing configuration device. BYPASS\_NONE - no bypass (default), BYPASS\_FINAL - skip final validation phase, BYPASS\_ALL - skip all validation phases.   | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_childtaskreference"
   class="paragraph">

**childTaskReference**

.. raw:: html

   </div>

+----------------+----------------------------------------+----------+
| Name           | Description                            | Schema   |
+================+========================================+==========+
| | **link**     | Reference link to child task object.   | string   |
| | *optional*   |                                        |          |
+----------------+----------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_childtaskstates"
   class="paragraph">

**childTaskStates**

.. raw:: html

   </div>

+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| Name                             | Description                                                                                                                                                                                         | Schema                                                                                        |
+==================================+=====================================================================================================================================================================================================+===============================================================================================+
| | **copyTaskReference**          | Enable / Disable declare-mgmt-authority ASM copy difference between working-configuration (BIGIQ) and current-configuration (BIGIP).                                                                | `copyTaskReference <#_properties_declare-mgmt-authority_copytaskreference>`__                 |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **createChildTasks**           | To create a child task as part of this declare-mgmt-authority for ASM module.                                                                                                                       | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **currentStep**                | The current step of device declare-mgmt-authority ASM task as predicated by state.                                                                                                                  | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **deviceIp**                   | Device ip address this task is running on.                                                                                                                                                          | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **deviceReference**            | Reference link to the device in the shared allAsmDevices resolver device group.                                                                                                                     | `deviceReference <#_properties_declare-mgmt-authority_devicereference>`__                     |
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
| | **generation**                 | An integer that will track change made to a device discovery declare-mgmt-authority task object. (ASM) generation.                                                                                  | integer(int64)                                                                                |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **id**                         | Unique id for child task.                                                                                                                                                                           | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **identityReference**          | Array of reference links to user used to discover device declare-mgmt-authority. mgmt/shared/authz/users/admin                                                                                      | < `identityReference <#_properties_declare-mgmt-authority_identityreference>`__ > array       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **isChildTask**                | Identify if task is a child of this declare-mgmt-authority for ASM module.                                                                                                                          | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **kind**                       | Type information for this device discovery declare-mgmt-authority ASM task object. cm:asm:tasks:declare-mgmt-authority:dmataskitemstate                                                             | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **lastUpdateMicros**           | Update time (micros) for last change made to a device discovery ASM task object. time (1476742109026835).                                                                                           | integer(int64)                                                                                |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **ownerMachineId**             | A unique id string for the BIGIQ acting as a device owner for declare-mgmt-authority. (ASM)                                                                                                         | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **parentTaskReference**        | Reference link to parent process.                                                                                                                                                                   | `parentTaskReference <#_properties_declare-mgmt-authority_parenttaskreference>`__             |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **reImport**                   | Flag to enable / disable re-import configuration.                                                                                                                                                   | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **selfLink**                   | A reference link URI to the device discovery declare-mgmt-authority task object. (ASM)                                                                                                              | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
| | *read-only*                    |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **skipDiscovery**              | Skip discovery for re-import configuration.                                                                                                                                                         | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **startDateTime**              | Date/Time when device discovery declare-mgmt-authority task began. 2016-10-11T10:30:17.834-0400                                                                                                     | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **status**                     | Status of device discovery declare-mgmt-authority task during state transistion. (ASM)                                                                                                              | string                                                                                        |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **useBigiqSync**               | Flag to sync BIGIP cluster management (True / False)                                                                                                                                                | boolean                                                                                       |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **userReference**              | Reference link to user used to discover device declare-mgmt-authority. mgmt/shared/authz/users/admin                                                                                                | `userReference <#_properties_declare-mgmt-authority_userreference>`__                         |
| | *optional*                     |                                                                                                                                                                                                     |                                                                                               |
+----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| | **username**                   | User name of device ASM object to be managed. (ASM)                                                                                                                                                 | string                                                                                        |
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

+----------------+--------------------------------------------------------------+----------+
| Name           | Description                                                  | Schema   |
+================+==============================================================+==========+
| | **link**     | Reference link to declare-mgmt-authority copy task object.   | string   |
| | *optional*   |                                                              |          |
+----------------+--------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_devicereference"
   class="paragraph">

**deviceReference**

.. raw:: html

   </div>

+----------------+-----------------------------------------------------------------------------------+----------+
| Name           | Description                                                                       | Schema   |
+================+===================================================================================+==========+
| | **link**     | Reference link to the device in the shared allAsmDevices resolver device group.   | string   |
| | *optional*   |                                                                                   |          |
+----------------+-----------------------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_differencereference"
   class="paragraph">

**differenceReference**

.. raw:: html

   </div>

+----------------+-------------------------------------------------------------------------------------------------------------------------------+----------+
| Name           | Description                                                                                                                   | Schema   |
+================+===============================================================================================================================+==========+
| | **link**     | Reference link to delcare-mgmt-authority differences found (current-config (BIGIP) and working-config (BIGIQ)) during task.   | string   |
| | *optional*   |                                                                                                                               |          |
+----------------+-------------------------------------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_differencertaskreference"
   class="paragraph">

**differencerTaskReference**

.. raw:: html

   </div>

+----------------+---------------------------------------------------------------------+----------+
| Name           | Description                                                         | Schema   |
+================+=====================================================================+==========+
| | **link**     | Reference link to delcare-mgmt-authority differences task object.   | string   |
| | *optional*   |                                                                     |          |
+----------------+---------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_identityreference"
   class="paragraph">

**identityReference**

.. raw:: html

   </div>

+----------------+--------------------------------------------------------------------+----------+
| Name           | Description                                                        | Schema   |
+================+====================================================================+==========+
| | **link**     | Array of reference links to users. mgmt/shared/authz/users/admin   | string   |
| | *optional*   |                                                                    |          |
+----------------+--------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_parenttaskreference"
   class="paragraph">

**parentTaskReference**

.. raw:: html

   </div>

+----------------+---------------------------------------------------------------------------+----------+
| Name           | Description                                                               | Schema   |
+================+===========================================================================+==========+
| | **link**     | Reference link to parent task. This declare-mgmt-authority task object.   | string   |
| | *optional*   |                                                                           |          |
+----------------+---------------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_userreference"
   class="paragraph">

**userReference**

.. raw:: html

   </div>

+----------------+---------------------------------------------------+----------+
| Name           | Description                                       | Schema   |
+================+===================================================+==========+
| | **link**     | Reference links to user. mgmt/shared/authz/user   | string   |
| | *optional*   |                                                   |          |
+----------------+---------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_copytaskreference"
   class="paragraph">

**copyTaskReference**

.. raw:: html

   </div>

+----------------+------------------------------------------------------------------+----------+
| Name           | Description                                                      | Schema   |
+================+==================================================================+==========+
| | **link**     | Reference link to declare-mgmt-authority difference copy task.   | string   |
| | *optional*   |                                                                  |          |
+----------------+------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_devicereference"
   class="paragraph">

**deviceReference**

.. raw:: html

   </div>

+----------------+---------------------------------------------------------+----------+
| Name           | Description                                             | Schema   |
+================+=========================================================+==========+
| | **link**     | Reference link to declare-mgmt-authority task device.   | string   |
| | *optional*   |                                                         |          |
+----------------+---------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_differencereference"
   class="paragraph">

**differenceReference**

.. raw:: html

   </div>

+----------------+----------------------------------------------------------------------+----------+
| Name           | Description                                                          | Schema   |
+================+======================================================================+==========+
| | **link**     | Reference link to shared security configuration difference report.   | string   |
| | *optional*   |                                                                      |          |
+----------------+----------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_declare-mgmt-authority_differencertaskreference"
   class="paragraph">

**differencerTaskReference**

.. raw:: html

   </div>

+----------------+---------------------------------------------------------------------------+----------+
| Name           | Description                                                               | Schema   |
+================+===========================================================================+==========+
| | **link**     | Reference link to shared security configuration difference task object.   | string   |
| | *optional*   |                                                                           |          |
+----------------+---------------------------------------------------------------------------+----------+

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

+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                                  | Schema             |
+==========================+==============================================================================================================================+====================+
| | **generation**         | An integer that will track change made to a device discovery ASM task collection object. generation.                         | integer(int64)     |
| | *optional*             |                                                                                                                              |                    |
| | *read-only*            |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Array of device discovery ASM task objects.                                                                                  | < object > array   |
| | *optional*             |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this device discover ASM task collection object. cm:asm:tasks:declare-mgmt-authority:dmataskitemstate   | string             |
| | *optional*             |                                                                                                                              |                    |
| | *read-only*            |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to a device discovery ASM task collection object. time.                            | integer(int64)     |
| | *optional*             |                                                                                                                              |                    |
| | *read-only*            |                                                                                                                              |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the device discovery ASM task collection object.                                                     | string             |
| | *optional*             |                                                                                                                              |                    |
| | *read-only*            |                                                                                                                              |                    |
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

Last updated 2017-01-13 13:13:45 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
