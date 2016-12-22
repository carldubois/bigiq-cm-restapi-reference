License - purchased pools
^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ licensing - Purchased Pools.
   :name: big-iq-licensing---purchased-pools.

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

API used to license BIG-IP devices via a purchased licensed pool.

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

| *BasePath* : /mgmt/cm/device/licensing/pool/purchased-pool
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

.. rubric:: GET the BIG-IQ purchased license pools.
   :name: _pools_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /licenses

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

Returns a BIG-IQ purchaced license pools allowing an administrator to
license BIG-IP devices.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+----------------------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                 |
+=============+====================================================+========================================================+
| **200**     | GET BIG-IQ purchased license pools.                | `properties\_collection <#_properties_collection>`__   |
+-------------+----------------------------------------------------+--------------------------------------------------------+
| **400**     | Error response "Bad Request"                       | `400\_error\_collection <#_400_error_collection>`__    |
+-------------+----------------------------------------------------+--------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."   | `404\_error\_collection <#_404_error_collection>`__    |
+-------------+----------------------------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to GET a purchased license pool.
   :name: _pools_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /licenses/{objectId}

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

Returns a purchased licensed pool object identified by id for an
endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+------------------+---------------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                             | Schema         | Default   |
+============+==================+=========================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to purchased licensed pool object.   | string(UUID)   | None      |
|            | | *required*     |                                                         |                |           |
+------------+------------------+---------------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+----------------------------------------------------+-----------------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                          |
+=============+====================================================+=================================================================+
| **200**     | Purchased license pool object returned.            | `properties\_purchased\_pool <#_properties_purchased_pool>`__   |
+-------------+----------------------------------------------------+-----------------------------------------------------------------+
| **400**     | Server error response "Bad Request".               | `400\_error\_collection <#_400_error_collection>`__             |
+-------------+----------------------------------------------------+-----------------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."   | `404\_error\_collection <#_404_error_collection>`__             |
+-------------+----------------------------------------------------+-----------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: License a BIG-IP device and add to purchased license pool
   members.
   :name: _pools_objectid_members_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /licenses/{objectId}/members

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

Invoke a task to license a BIG-IP and add to this specific purchased
license pool as a member to the pool.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------+-----------+
| Type       | Name                              | Description                                                                                                            | Schema                                                         | Default   |
+============+===================================+========================================================================================================================+================================================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to license purchased pool object.                                                                   | string(UUID)                                                   | None      |
|            | | *required*                      |                                                                                                                        |                                                                |           |
+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. Ex. {"deviceAddress": "bigip\_address","username": "admin","password": "admin"}   | `post\_purchased\_pool\_body <#_post_purchased_pool_body>`__   | None      |
|            | | *required*                      |                                                                                                                        |                                                                |           |
+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+--------------------------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                                            | Schema                                                 |
+=============+========================================================+========================================================+
| **200**     | POST a device level task to license a BIG-IP device.   | `properties\_collection <#_properties_collection>`__   |
+-------------+--------------------------------------------------------+--------------------------------------------------------+
| **400**     | Error response "Bad Request"                           | `400\_error\_collection <#_400_error_collection>`__    |
+-------------+--------------------------------------------------------+--------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."       | `404\_error\_collection <#_404_error_collection>`__    |
+-------------+--------------------------------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to GET purchased license pool members.
   :name: _pools_objectid_members_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /pools/{objectId}/members

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_4

.. raw:: html

   <div class="paragraph">

Returns all members (BIG-IP) devices that are assingned to this
purchased license pool. Each are identified by id/members for an
endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_3

+------------+------------------+--------------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                            | Schema         | Default   |
+============+==================+========================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to purchased license pool object.   | string(UUID)   | None      |
|            | | *required*     |                                                        |                |           |
+------------+------------------+--------------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_4

+-------------+----------------------------------------------------+-----------------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                          |
+=============+====================================================+=================================================================+
| **200**     | Purchased license pool members object returned.    | `properties\_purchased\_pool <#_properties_purchased_pool>`__   |
+-------------+----------------------------------------------------+-----------------------------------------------------------------+
| **400**     | Server error response "Bad Request".               | `400\_error\_collection <#_400_error_collection>`__             |
+-------------+----------------------------------------------------+-----------------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."   | `404\_error\_collection <#_404_error_collection>`__             |
+-------------+----------------------------------------------------+-----------------------------------------------------------------+

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

+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                        | Schema             |
+============================+====================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                | string             |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of purchased license pool objects.                                                      | < object > array   |
| | *optional*               |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for purchased license pools - cm:shared:licensing:pools:licensepoolworkerstate.   | string             |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                | string             |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                           | string             |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                              | integer(int64)     |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: 404\_error\_collection
   :name: _404_error_collection

+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                        | Schema             |
+============================+====================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                | string             |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of purchased license pool objects.                                                      | < object > array   |
| | *optional*               |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for purchased license pools - cm:shared:licensing:pools:licensepoolworkerstate.   | string             |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                | string             |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                           | string             |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                              | integer(int64)     |
| | *optional*               |                                                                                                    |                    |
| | *read-only*              |                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_purchased\_pool\_body
   :name: _post_purchased_pool_body

+-----------------------+--------------------------------------------+----------+
| Name                  | Description                                | Schema   |
+=======================+============================================+==========+
| | **deviceAddress**   | IP Address of BIGIP you wish to license.   | string   |
| | *required*          |                                            |          |
+-----------------------+--------------------------------------------+----------+
| | **username**        | Username of BIGIP you wish to license.     | string   |
| | *required*          |                                            |          |
+-----------------------+--------------------------------------------+----------+
| | **password**        | Password of BIGIP you wish to license.     | string   |
| | *required*          |                                            |          |
+-----------------------+--------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_collection
   :name: _properties_collection

+--------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                        | Schema             |
+==========================+====================================================================================================+====================+
| | **generation**         | A integer that will track change made to a purchased license pool collection object. generation.   | integer(int64)     |
| | *optional*             |                                                                                                    |                    |
| | *read-only*            |                                                                                                    |                    |
+--------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Collection of purchased license pool objects.                                                      | < object > array   |
| | *optional*             |                                                                                                    |                    |
+--------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for a purchased license pool collection object.                                   | string             |
| | *optional*             |                                                                                                    |                    |
| | *read-only*            |                                                                                                    |                    |
+--------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an purchaced license pool collection object. time.    | integer(int64)     |
| | *optional*             |                                                                                                    |                    |
| | *read-only*            |                                                                                                    |                    |
+--------------------------+----------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to a purchased license pool collection object.                                | string             |
| | *optional*             |                                                                                                    |                    |
| | *read-only*            |                                                                                                    |                    |
+--------------------------+----------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_purchased\_pool
   :name: _properties_purchased_pool

+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| Name                        | Description                                                                                                                                    | Schema                                                        |
+=============================+================================================================================================================================================+===============================================================+
| | **baseRegKey**            | Based Registration Key used to (re) activate purchased license pool.                                                                           | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **freeDeviceLicenses**    | Total number of free device licenses for this purchased license pool.                                                                          | integer                                                       |
| | *read-only*               |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **generation**            | A integer that will track change made to a purchased license pool object. generation.                                                          | integer(int64)                                                |
| | *optional*                |                                                                                                                                                |                                                               |
| | *read-only*               |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **isInternal**            | Is this purchased licensed pool internal to BIG-IQ.                                                                                            | boolean                                                       |
| | *BIG-IQ use only*         |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **kind**                  | Type information for this purchased license pool object.                                                                                       | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
| | *read-only*               |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **lastUpdateMicros**      | Update time (micros) for last change made to an purchased license pool object. time.                                                           | integer(int64)                                                |
| | *optional*                |                                                                                                                                                |                                                               |
| | *read-only*               |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **licenseState**          | State representation of what is returned from the license server.                                                                              | `licenseState <#_properties_purchased_pool_licensestate>`__   |
| | *read-only*               |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **licenseText**           | Contents of licensed purchased pool. Spefices for purchased license pool such as Auth version, Tech support info, license tokens, keys etc..   | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
| | *read-only*               |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **method**                | Activation method used. (Example - MANUAL / AUTOMATIC)                                                                                         | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **name**                  | Name of purchased license pool object.                                                                                                         | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **privateKey**            | Private key cryptography keys which are known only to the owner.                                                                               | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **publicKey**             | Public key cryptography which may be disseminated widely.                                                                                      | < integer > array                                             |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **registeredKey**         | Registered key post cryptography response from server.                                                                                         | < integer > array                                             |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **selfLink**              | Reference link to ppurchased licensed pool.                                                                                                    | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
| | *read-only*               |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **sortName**              | Sort string based on BIG-IQ licensing type. (Purchased Pool)                                                                                   | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **state**                 | State of license for purchaced license pool. (Example - LICENSED)                                                                              | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **totalDeviceLicenses**   | Total number of device licenses for this purchased license pool.                                                                               | integer                                                       |
| | *optional*                |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **uuid**                  | Unique id assigned to a purchased license pool object.                                                                                         | string                                                        |
| | *optional*                |                                                                                                                                                |                                                               |
| | *read-only*               |                                                                                                                                                |                                                               |
+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+

.. raw:: html

   <div id="_properties_purchased_pool_licensestate" class="paragraph">

**licenseState**

.. raw:: html

   </div>

+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| Name                            | Description                                                                                                                                      | Schema                                                                  |
+=================================+==================================================================================================================================================+=========================================================================+
| | **activeModules**             | Modules activivated for purchased license pool. (Example - VEP1, LTM, 1G, 4 Instances\|V092327-5105381\|IPV6 Gateway\|Rate Shaping\|Ram Cache)   | < string > array                                                        |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **authVers**                  | Version of authentication used by BIG-IQ. (Example - 5b)                                                                                         | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **authorization**             | Authorization string used by purchased license pool. Response from license server.                                                               | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **dossier**                   | Dossier generated for this purchased license pool. Response from license server.                                                                 | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **evaluationEndDateTime**     | End date and time a license server evaluate took place (Format - 2016-10-26T00:00:00-04:00)                                                      | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **evaluationStartDateTime**   | Start date and time a license server evaluate took place (Format - 2016-10-26T00:00:00-04:00)                                                    | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **exclusivePlatform**         | Platfrom description response from server. (Example - BIG-IQ Pool, Z100, Z100H, Z100K, Z100x)                                                    | < string > array                                                        |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **featureFlags**              | Descritive flags avalible to purchased license pools.                                                                                            | < `featureFlags <#_properties_purchased_pool_featureflags>`__ > array   |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **licenseDateTime**           | Date and time license was generated. (Format - 2016-10-26T00:00:00-04:00)                                                                        | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **licenseEndDateTime**        | End date and time a license was instatiated on BIG-IQ (Format - 2016-10-26T00:00:00-04:00)                                                       | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **licenseStartDateTime**      | Start date and time a license was instatiated on BIG-IQ (Format - 2016-10-26T00:00:00-04:00)                                                     | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **licenseVersion**            | Version of BIG-IQ this license is generated for. (Example - 5.1.0)                                                                               | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **optionalModules**           | Modules that are optional for purchased license pool. (Example - VEP1, LTM, 1G, Add 25 Instances)                                                | < string > array                                                        |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **platformId**                | Type of BIG-IQ platform information. (Example - BIG-IQ Pool)                                                                                     | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **registrationKey**           | Registration Key used by this purchased license pool. Response from license server.                                                              | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **serviceCheckDateTime**      | Data and time the last service check status request / respose occur from server. (Format - 2016-10-26T00:00:00-04:00)                            | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **serviceStatus**             | Server response describing service status. (Example - As of 2016-10-26 this system has an active service contract.)                              | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **usage**                     | Organization usage data. Example - F5 Internal Product Development                                                                               | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
| | **vendor**                    | Company Name. Example F5 Networks, Inc.                                                                                                          | string                                                                  |
| | *optional*                    |                                                                                                                                                  |                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_purchased_pool_featureflags" class="paragraph">

**featureFlags**

.. raw:: html

   </div>

+----------------------+---------------------------------------------------------------------------------------------------------------------+----------+
| Name                 | Description                                                                                                         | Schema   |
+======================+=====================================================================================================================+==========+
| | **featureName**    | Name of feature. (Example - purchased\_license\_pool\_count, apm\_urlf\_limited\_session, apm\_web\_applications)   | string   |
| | *optional*         |                                                                                                                     |          |
+----------------------+---------------------------------------------------------------------------------------------------------------------+----------+
| | **featureValue**   | Weighted value for each feature. (Example - 10)                                                                     | string   |
| | *optional*         |                                                                                                                     |          |
+----------------------+---------------------------------------------------------------------------------------------------------------------+----------+

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

Last updated 2016-12-07 10:14:58 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
