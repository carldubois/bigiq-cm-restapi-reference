.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ LTM/ADC Self-Service Task. (enable/disable pool
   member)
   :name: big-iq-ltmadc-self-service-task.-enabledisable-pool-member

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

API used create a self-service task to perform functions such as
enable/disable pool member.

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

.. rubric:: Create a adc self-service task managed by BIGIQ module.
   :name: _self-service_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /self-service

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

Create a adc self-service task and add to collection.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+-----------+
| Type       | Name                              | Description                                                                                                                                                                                                                                   | Schema                                                              | Default   |
+============+===================================+===============================================================================================================================================================================================================================================+=====================================================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to a self-service task.                                                                                                                                                                                                    | string(UUID)                                                        | None      |
|            | | *required*                      |                                                                                                                                                                                                                                               |                                                                     |           |
+------------+-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. Ex. {"resourceReference":{"link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/3a3361a8-64fa-33d7-bc1a-d6658f31e687/members/a0fd9118-b58c-339f-8085-e92f1f75ec1e"},"operation":"enable"}   | `post\_adc\_self\_service\_body <#_post_adc_self_service_body>`__   | None      |
|            | | *required*                      |                                                                                                                                                                                                                                               |                                                                     |           |
+------------+-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+--------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                    | Schema                                                 |
+=============+================================+========================================================+
| **200**     | POST a self-service task.      | `properties\_collection <#_properties_collection>`__   |
+-------------+--------------------------------+--------------------------------------------------------+
| **400**     | Error response "Bad Request"   | `error\_collection <#_error_collection>`__             |
+-------------+--------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all collections of self-service tasks.
   :name: _self-service_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /self-service

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

Returns the collection of self-service tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+-----------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                             | Schema                                                 |
+=============+=========================================+========================================================+
| **200**     | GET collection of self-service tasks.   | `properties\_collection <#_properties_collection>`__   |
+-------------+-----------------------------------------+--------------------------------------------------------+
| **400**     | Error response "Bad Request"            | `error\_collection <#_error_collection>`__             |
+-------------+-----------------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single instance of a self-service task object.
   :name: _self-service_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /self-service/{objectId}

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

Returns a self-service task object identified by id for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+------------------+----------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                  | Schema         | Default   |
+============+==================+==============================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to a self-service task.   | string(UUID)   | None      |
|            | | *required*     |                                              |                |           |
+------------+------------------+----------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+----------------------------------------+-------------------------------------------------------------+
| HTTP Code   | Description                            | Schema                                                      |
+=============+========================================+=============================================================+
| **200**     | Self-service task object.              | `properties\_self\_service <#_properties_self_service>`__   |
+-------------+----------------------------------------+-------------------------------------------------------------+
| **400**     | Server error response "Bad Request".   | `error\_collection <#_error_collection>`__                  |
+-------------+----------------------------------------+-------------------------------------------------------------+

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

+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                       | Schema             |
+============================+===================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                               | string             |
| | *optional*               |                                                                                                   |                    |
| | *read-only*              |                                                                                                   |                    |
+----------------------------+---------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of self-service task errors.                                                           | < object > array   |
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

+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                              | Schema             |
+==========================+==========================================================================================+====================+
| | **generation**         | A integer that will track change made to a self-service collection object. generation.   | integer(int64)     |
| | *optional*             |                                                                                          |                    |
| | *read-only*            |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Self-serivce task properties associated with the collection.                             | < object > array   |
| | *optional*             |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this self-service task collection object.                           | string             |
| | *optional*             |                                                                                          |                    |
| | *read-only*            |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an self-service collection object. time.    | integer(int64)     |
| | *optional*             |                                                                                          |                    |
| | *read-only*            |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the self-service task collection object.                         | string             |
| | *optional*             |                                                                                          |                    |
| | *read-only*            |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_self\_service
   :name: _properties_self_service

+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Name                      | Description                                                                                        | Schema                                                                          |
+===========================+====================================================================================================+=================================================================================+
| | **deviceReference**     | Reference link to device object in resolver.                                                       | `deviceReference <#_properties_self_service_devicereference>`__                 |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **endDateTime**         | Date/Time when self-service task end. 2016-10-11T10:30:17.834-0400                                 | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **generation**          | A integer that will track change made to a self-service task object. generation.                   | integer(int64)                                                                  |
| | *optional*              |                                                                                                    |                                                                                 |
| | *read-only*             |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **id**                  | Unique id assigned to a self-service task object.                                                  | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
| | *read-only*             |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **identityReference**   | Array of reference links to user used to create self-service task. mgmt/shared/authz/users/admin   | < `identityReference <#_properties_self_service_identityreference>`__ > array   |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **kind**                | Type information for this self-service task object.                                                | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
| | *read-only*             |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **lastUpdateMicros**    | Update time (micros) for last change made to an self-service task object. time.                    | integer(int64)                                                                  |
| | *optional*              |                                                                                                    |                                                                                 |
| | *read-only*             |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **name**                | Name of self-service task object. example. 'Self-Service\_10.55.2.20:80'                           | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **operation**           | Description of operation type. example. (enable/disable/force offline).                            | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **ownerMachineId**      | A unique id string for the BIGIQ acting as a device owner.                                         | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
| | *read-only*             |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **resourceReference**   | Reference link to resource used. example. pool member enable/disable                               | `resourceReference <#_properties_self_service_resourcereference>`__             |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **selfLink**            | A reference link URI to the self-service task object.                                              | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
| | *read-only*             |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **stateDateTime**       | Date/Time when self-service task began. 2016-10-11T10:30:17.834-0400                               | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **status**              | Status if self-service task based on state. STARTED; FINSIHED etc..                                | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **userReference**       | Reference link to user used to create self-service task. mgmt/shared/authz/users/admin             | `userReference <#_properties_self_service_userreference>`__                     |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **username**            | Username of user whom iniated the task.                                                            | string                                                                          |
| | *optional*              |                                                                                                    |                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_self_service_devicereference" class="paragraph">

**deviceReference**

.. raw:: html

   </div>

+----------------+------------------------------------------------------------------------------------------+----------+
| Name           | Description                                                                              | Schema   |
+================+==========================================================================================+==========+
| | **link**     | Reference link to device assocated with this self-service task in the device resolver.   | string   |
| | *optional*   |                                                                                          |          |
+----------------+------------------------------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_self_service_identityreference"
   class="paragraph">

**identityReference**

.. raw:: html

   </div>

+----------------+----------------------------------------+----------+
| Name           | Description                            | Schema   |
+================+========================================+==========+
| | **link**     | Reference link table to authz users.   | string   |
| | *optional*   |                                        |          |
+----------------+----------------------------------------+----------+

.. raw:: html

   <div id="_properties_self_service_resourcereference"
   class="paragraph">

**resourceReference**

.. raw:: html

   </div>

+----------------+------------------------------------------------------------------+----------+
| Name           | Description                                                      | Schema   |
+================+==================================================================+==========+
| | **link**     | Reference link to the resource in which the task is mananging.   | string   |
| | *optional*   |                                                                  |          |
+----------------+------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_self_service_userreference" class="paragraph">

**userReference**

.. raw:: html

   </div>

+----------------+---------------------------------------+----------+
| Name           | Description                           | Schema   |
+================+=======================================+==========+
| | **link**     | Reference link table to authz user.   | string   |
| | *optional*   |                                       |          |
+----------------+---------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_adc\_self\_service\_body
   :name: _post_adc_self_service_body

+---------------------------+----------------------------------------------------------------+----------+
| Name                      | Description                                                    | Schema   |
+===========================+================================================================+==========+
| | **resourceReference**   | Reference link to the pool member resource for self service.   | string   |
| | *required*              |                                                                |          |
+---------------------------+----------------------------------------------------------------+----------+
| | **operation**           | Enable, Disable or Force Offline.                              | string   |
| | *required*              |                                                                |          |
+---------------------------+----------------------------------------------------------------+----------+

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

Last updated 2016-11-22 17:22:20 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
