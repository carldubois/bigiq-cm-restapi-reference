.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ licensing - Registration Key Pools.
   :name: big-iq-licensing---registration-key-pools.

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

API used to license BIGIP devices referencing a registration licensed
key.

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

| *BasePath* : /mgmt/cm/device/licensing/pool/regkey
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

.. rubric:: GET the BIG-IQ licensing registration key pool collection of
   license registration keys.
   :name: _licenses_get

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

Returns a BIGIQ licensed registration key allowing an administrator to
license BIGIP managned / unmanaged devices.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+------------------------------------------------------------------------------+-----------------------------------------------------------------------+
| HTTP Code   | Description                                                                  | Schema                                                                |
+=============+==============================================================================+=======================================================================+
| **200**     | GET BIGIQ licensed registration keys that make up a registration key pool.   | `properties\_regkey\_collection <#_properties_regkey_collection>`__   |
+-------------+------------------------------------------------------------------------------+-----------------------------------------------------------------------+
| **400**     | Error response Bad Request                                                   | `400\_error\_collection <#_400_error_collection>`__                   |
+-------------+------------------------------------------------------------------------------+-----------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.                               | `404\_error\_collection <#_404_error_collection>`__                   |
+-------------+------------------------------------------------------------------------------+-----------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to GET a license pool.
   :name: _licenses_objectid_get

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

Returns a licensed pool object identified by id for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+------------------+----------------------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                                    | Schema         | Default   |
+============+==================+================================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to licensed registration key pool object.   | string(UUID)   | None      |
|            | | *required*     |                                                                |                |           |
+------------+------------------+----------------------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+--------------------------------------------------+-------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                |
+=============+==================================================+=======================================================+
| **200**     | License pool object returned.                    | `properties\_regkey <#_properties_regkey>`__          |
+-------------+--------------------------------------------------+-------------------------------------------------------+
| **400**     | Server error response Bad Request.               | `400\_error\_collection <#_400_error_collection>`__   |
+-------------+--------------------------------------------------+-------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__   |
+-------------+--------------------------------------------------+-------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Create a new registration license key.
   :name: _licenses_objectid_offerings_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /licenses/{objectId}/offerings

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

Add a new registration license key adding to BIGIQ licese regkey pool.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------+-----------+
| Type       | Name                              | Description                                                                                                                        | Schema                                        | Default   |
+============+===================================+====================================================================================================================================+===============================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to licensed registration key pool object.                                                                       | string(UUID)                                  | None      |
|            | | *required*                      |                                                                                                                                    |                                               |           |
+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. ex. {regKey: U0151-71761-41002-45076-9552496, status: ACTIVATING\_AUTOMATIC, name: RegKey1}   | `post\_regkey\_body <#_post_regkey_body>`__   | None      |
|            | | *required*                      |                                                                                                                                    |                                               |           |
+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                           | Schema                                                                                     |
+=============+=======================================================+============================================================================================+
| **200**     | POST a device level task to license a BIGIP device.   | `properties\_regkey\_offerings\_collection <#_properties_regkey_offerings_collection>`__   |
+-------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------+
| **400**     | Error response Bad Request                            | `400\_error\_collection <#_400_error_collection>`__                                        |
+-------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.        | `404\_error\_collection <#_404_error_collection>`__                                        |
+-------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to GET license pool members.
   :name: _licenses_objectid_offerings_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /licenses/{objectId}/offerings

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

Returns all members (BIGIP) devices that make up the license pool
identified by id/members for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_3

+------------+------------------+----------------------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                                    | Schema         | Default   |
+============+==================+================================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to licensed registration key pool object.   | string(UUID)   | None      |
|            | | *required*     |                                                                |                |           |
+------------+------------------+----------------------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_4

+-------------+--------------------------------------------------+--------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                     |
+=============+==================================================+============================================================================================+
| **200**     | License pool members object returned.            | `properties\_regkey\_offerings\_collection <#_properties_regkey_offerings_collection>`__   |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------------------------+
| **400**     | Server error response Bad Request.               | `400\_error\_collection <#_400_error_collection>`__                                        |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                        |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to GET a specific license registration key.
   :name: _licenses_objectid_offerings_registrationkey_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /licenses/{objectId}/offerings/{registrationKey}

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_5

.. raw:: html

   <div class="paragraph">

Returns a registration key license identified by id for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_4

+------------+-------------------------+----------------------------------------------------------------+------------------+-----------+
| Type       | Name                    | Description                                                    | Schema           | Default   |
+============+=========================+================================================================+==================+===========+
| **Path**   | | **objectId**          | Unique id assigned to licensed registration key pool object.   | string(UUID)     | None      |
|            | | *required*            |                                                                |                  |           |
+------------+-------------------------+----------------------------------------------------------------+------------------+-----------+
| **Path**   | | **registrationKey**   | Generated registration key used when licensing BIGIP.          | string(string)   | None      |
|            | | *required*            |                                                                |                  |           |
+------------+-------------------------+----------------------------------------------------------------+------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_5

+-------------+----------------------------------------------------+-------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                |
+=============+====================================================+=======================================================+
| **200**     | License registration key object returned.          | `properties\_offering <#_properties_offering>`__      |
+-------------+----------------------------------------------------+-------------------------------------------------------+
| **400**     | Server error response Bad Request.                 | `400\_error\_collection <#_400_error_collection>`__   |
+-------------+----------------------------------------------------+-------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."   | `404\_error\_collection <#_404_error_collection>`__   |
+-------------+----------------------------------------------------+-------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Add, or license, a device as a member of a BIGIQ license
   registration key pool.
   :name: _licenses_objectid_offerings_registrationkey_members_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /licenses/{objectId}/offerings/{registrationKey}/members

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_6

.. raw:: html

   <div class="paragraph">

Will license a device and add as a member of a BIGIQ license
registration key pool.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_5

+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------+-----------+
| Type       | Name                              | Description                                                                                                | Schema                                                         | Default   |
+============+===================================+============================================================================================================+================================================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to licensed registration key pool object.                                               | string(UUID)                                                   | None      |
|            | | *required*                      |                                                                                                            |                                                                |           |
+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------+-----------+
| **Path**   | | **registrationKey**             | Generated registration key used when licensing BIGIP.                                                      | string(string)                                                 | None      |
|            | | *required*                      |                                                                                                            |                                                                |           |
+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. ex. {deviceAddress: 10.44.100.25, username: admin, password: admin}   | `post\_regkey\_members\_body <#_post_regkey_members_body>`__   | None      |
|            | | *required*                      |                                                                                                            |                                                                |           |
+------------+-----------------------------------+------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_6

+-------------+-------------------------------------------------------+----------------------------------------------------------------------------------------+
| HTTP Code   | Description                                           | Schema                                                                                 |
+=============+=======================================================+========================================================================================+
| **200**     | POST a device level task to license a BIGIP device.   | `properties\_regkey\_members\_collection <#_properties_regkey_members_collection>`__   |
+-------------+-------------------------------------------------------+----------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                          | `400\_error\_collection <#_400_error_collection>`__                                    |
+-------------+-------------------------------------------------------+----------------------------------------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."      | `404\_error\_collection <#_404_error_collection>`__                                    |
+-------------+-------------------------------------------------------+----------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to GET a collection of device licenses that make up
   registration key pool members.
   :name: _licenses_objectid_offerings_registrationkey_members_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /licenses/{objectId}/offerings/{registrationKey}/members

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_7

.. raw:: html

   <div class="paragraph">

Returns all members (BIGIP) devices that make up the registration key
license pool identified by key for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_6

+------------+-------------------------+----------------------------------------------------------------+------------------+-----------+
| Type       | Name                    | Description                                                    | Schema           | Default   |
+============+=========================+================================================================+==================+===========+
| **Path**   | | **objectId**          | Unique id assigned to licensed registration key pool object.   | string(UUID)     | None      |
|            | | *required*            |                                                                |                  |           |
+------------+-------------------------+----------------------------------------------------------------+------------------+-----------+
| **Path**   | | **registrationKey**   | Generated registration key used when licensing BIGIP.          | string(string)   | None      |
|            | | *required*            |                                                                |                  |           |
+------------+-------------------------+----------------------------------------------------------------+------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_7

+-------------+--------------------------------------------------+----------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                 |
+=============+==================================================+========================================================================================+
| **200**     | License pool members object returned.            | `properties\_regkey\_members\_collection <#_properties_regkey_members_collection>`__   |
+-------------+--------------------------------------------------+----------------------------------------------------------------------------------------+
| **400**     | Server error response Bad Request.               | `400\_error\_collection <#_400_error_collection>`__                                    |
+-------------+--------------------------------------------------+----------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                    |
+-------------+--------------------------------------------------+----------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to GET license pool members.
   :name: _licenses_objectid_offerings_registrationkey_members_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /licenses/{objectId}/offerings/{registrationKey}/members/{memberObjectId}

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_8

.. raw:: html

   <div class="paragraph">

Returns all members (BIGIP) devices that make up the license pool
identified by id/members for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_7

+------------+-------------------------+------------------------------------------------------------------------------+------------------+-----------+
| Type       | Name                    | Description                                                                  | Schema           | Default   |
+============+=========================+==============================================================================+==================+===========+
| **Path**   | | **objectId**          | Unique id assigned to licensed registration key pool object.                 | string(UUID)     | None      |
|            | | *required*            |                                                                              |                  |           |
+------------+-------------------------+------------------------------------------------------------------------------+------------------+-----------+
| **Path**   | | **registrationKey**   | Generated registration key used when licensing BIGIP.                        | string(string)   | None      |
|            | | *required*            |                                                                              |                  |           |
+------------+-------------------------+------------------------------------------------------------------------------+------------------+-----------+
| **Path**   | | **memberObjectId**    | Unique id assigned to a member device licensed to a registration key pool.   | string(string)   | None      |
|            | | *required*            |                                                                              |                  |           |
+------------+-------------------------+------------------------------------------------------------------------------+------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_8

+-------------+----------------------------------------------------+---------------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                        |
+=============+====================================================+===============================================================+
| **200**     | License pool members object returned.              | `properties\_regkey\_member <#_properties_regkey_member>`__   |
+-------------+----------------------------------------------------+---------------------------------------------------------------+
| **400**     | Server error response "Bad Request".               | `400\_error\_collection <#_400_error_collection>`__           |
+-------------+----------------------------------------------------+---------------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."   | `404\_error\_collection <#_404_error_collection>`__           |
+-------------+----------------------------------------------------+---------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to DEL license pool members.
   :name: _licenses_objectid_offerings_registrationkey_members_objectid_del

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    DEL /licenses/{objectId}/offerings/{registrationKey}/members/{memberObjectId}

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_9

.. raw:: html

   <div class="paragraph">

DELETES a member (BIGIP) device that is part of a license pool
identified by id/members/memberObjectId for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_8

+------------+-------------------------+------------------------------------------------------------------------------+------------------+-----------+
| Type       | Name                    | Description                                                                  | Schema           | Default   |
+============+=========================+==============================================================================+==================+===========+
| **Path**   | | **objectId**          | Unique id assigned to licensed registration key pool object.                 | string(UUID)     | None      |
|            | | *required*            |                                                                              |                  |           |
+------------+-------------------------+------------------------------------------------------------------------------+------------------+-----------+
| **Path**   | | **registrationKey**   | Generated registration key used when licensing BIGIP.                        | string(string)   | None      |
|            | | *required*            |                                                                              |                  |           |
+------------+-------------------------+------------------------------------------------------------------------------+------------------+-----------+
| **Path**   | | **memberObjectId**    | Unique id assigned to a member device licensed to a registration key pool.   | string(string)   | None      |
|            | | *required*            |                                                                              |                  |           |
+------------+-------------------------+------------------------------------------------------------------------------+------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_9

+-------------+----------------------------------------------------+---------------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                        |
+=============+====================================================+===============================================================+
| **200**     | License pool member object deleted returned.       | `properties\_regkey\_member <#_properties_regkey_member>`__   |
+-------------+----------------------------------------------------+---------------------------------------------------------------+
| **400**     | Server error response "Bad Request".               | `400\_error\_collection <#_400_error_collection>`__           |
+-------------+----------------------------------------------------+---------------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."   | `404\_error\_collection <#_404_error_collection>`__           |
+-------------+----------------------------------------------------+---------------------------------------------------------------+

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

+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                                        | Schema             |
+============================+====================================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                                | string             |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of license registration key pool objects. Error 400                                                                                     | < object > array   |
| | *optional*               |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for license purchased pools - cm:device:licensing:pool:regkey:licenses:item:offerings:regkeypoollicenseofferingcollectionstate.   | string             |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                                | string             |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                                           | string             |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                                              | integer(int64)     |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: 404\_error\_collection
   :name: _404_error_collection

+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                                        | Schema             |
+============================+====================================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                                | string             |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of license registration key pool objects. Error 404                                                                                     | < object > array   |
| | *optional*               |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for license purchased pools - cm:device:licensing:pool:regkey:licenses:item:offerings:regkeypoollicenseofferingcollectionstate.   | string             |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                                | string             |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                                           | string             |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                                              | integer(int64)     |
| | *optional*               |                                                                                                                                                    |                    |
| | *read-only*              |                                                                                                                                                    |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_regkey\_body
   :name: _post_regkey_body

+----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| Name           | Description                                                                                                                                                                                                        | Schema   |
+================+====================================================================================================================================================================================================================+==========+
| | **name**     | Name of license registration key.                                                                                                                                                                                  | string   |
| | *optional*   |                                                                                                                                                                                                                    |          |
+----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| | **regKey**   | Registration Key                                                                                                                                                                                                   | string   |
| | *optional*   |                                                                                                                                                                                                                    |          |
+----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| | **status**   | ACTIVATING\_AUTOMATIC, ACTIVATING\_MANUAL\_LICENSE\_TEXT\_PROVIDED. Please consult SA for activating manually, additional steps may be requested for generating dossier and retriving license txt file for POST.   | string   |
| | *optional*   |                                                                                                                                                                                                                    |          |
+----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_regkey\_members\_body
   :name: _post_regkey_members_body

+-----------------------+----------------------------------------+----------+
| Name                  | Description                            | Schema   |
+=======================+========================================+==========+
| | **deviceAddress**   | IP address of device to be licensed.   | string   |
| | *optional*          |                                        |          |
+-----------------------+----------------------------------------+----------+
| | **password**        | Password of device to be licensed.     | string   |
| | *optional*          |                                        |          |
+-----------------------+----------------------------------------+----------+
| | **username**        | Username of device to be licensed.     | string   |
| | *optional*          |                                        |          |
+-----------------------+----------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_offering
   :name: _properties_offering

+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| Name                        | Description                                                                                                                                                     | Schema              |
+=============================+=================================================================================================================================================================+=====================+
| | **dossier**               | The dossier is an encrypted list of key characteristics used to identify the platform. https://support.f5.com/kb/en-us/solutions/public/7000/700/sol7752.html   | string              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **encryptedPrivateKey**   | Encypted private key used for decrypt / encrypt of data.                                                                                                        | < integer > array   |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **generation**            | A integer that will track change made to a license registration key object. generation.                                                                         | integer(int64)      |
| | *optional*                |                                                                                                                                                                 |                     |
| | *read-only*               |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **internalPrivateKey**    | Internal private key used for encryption.                                                                                                                       | string              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **kind**                  | Type information for this license registration key object.                                                                                                      | string              |
| | *optional*                |                                                                                                                                                                 |                     |
| | *read-only*               |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **lastUpdateMicros**      | Update time (micros) for last change made to an license registration key object. time.                                                                          | integer(int64)      |
| | *optional*                |                                                                                                                                                                 |                     |
| | *read-only*               |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **licenseState**          | State object of license registration key.                                                                                                                       | object              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **licenseText**           | Text base string for licence registration key proivded during activation process.                                                                               | string              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **message**               | The message provided to the user of this licensing. ex. Activated.                                                                                              | string              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **name**                  | General name for license registration key. ex. License for Q0168-94118-59282-63288-2594214                                                                      | string              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **publicKey**             | Public key used for encryption.                                                                                                                                 | < integer > array   |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **regKey**                | License registration key generated.                                                                                                                             | string              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **selfLink**              | Reference link to license registration key object.                                                                                                              | string              |
| | *optional*                |                                                                                                                                                                 |                     |
| | *read-only*               |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **sortName**              | Sort by unique name of registration key pool used to (re) activate license devices using registration key.                                                      | string              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| | **status**                | License registration key status. ex. READY                                                                                                                      | string              |
| | *optional*                |                                                                                                                                                                 |                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_regkey
   :name: _properties_regkey

+--------------------------+--------------------------------------------------------------------------------------------------------------+------------------+
| Name                     | Description                                                                                                  | Schema           |
+==========================+==============================================================================================================+==================+
| | **generation**         | A integer that will track change made to a license registration key pool object. generation.                 | integer(int64)   |
| | *optional*             |                                                                                                              |                  |
| | *read-only*            |                                                                                                              |                  |
+--------------------------+--------------------------------------------------------------------------------------------------------------+------------------+
| | **id**                 | Unique id assigned to a license registration key pool object.                                                | string           |
| | *optional*             |                                                                                                              |                  |
| | *read-only*            |                                                                                                              |                  |
+--------------------------+--------------------------------------------------------------------------------------------------------------+------------------+
| | **kind**               | Type information for this license registration key pool object.                                              | string           |
| | *optional*             |                                                                                                              |                  |
| | *read-only*            |                                                                                                              |                  |
+--------------------------+--------------------------------------------------------------------------------------------------------------+------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an license registration key pool object. time.                  | integer(int64)   |
| | *optional*             |                                                                                                              |                  |
| | *read-only*            |                                                                                                              |                  |
+--------------------------+--------------------------------------------------------------------------------------------------------------+------------------+
| | **name**               | Name of registration key pool used to (re) activate license devices using registration key.                  | string           |
| | *optional*             |                                                                                                              |                  |
+--------------------------+--------------------------------------------------------------------------------------------------------------+------------------+
| | **selfLink**           | Reference link to license registration key pool object.                                                      | string           |
| | *optional*             |                                                                                                              |                  |
| | *read-only*            |                                                                                                              |                  |
+--------------------------+--------------------------------------------------------------------------------------------------------------+------------------+
| | **sortName**           | Sort by unique name of registration key pool used to (re) activate license devices using registration key.   | string           |
| | *optional*             |                                                                                                              |                  |
| | *read-only*            |                                                                                                              |                  |
+--------------------------+--------------------------------------------------------------------------------------------------------------+------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_regkey\_collection
   :name: _properties_regkey_collection

+--------------------------+-------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                 | Schema             |
+==========================+=============================================================================================================+====================+
| | **generation**         | A integer that will track change made to a license regoistration keys pool collection object. generation.   | integer(int64)     |
| | *optional*             |                                                                                                             |                    |
| | *read-only*            |                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Collection of license registration key pool object.                                                         | < object > array   |
| | *optional*             |                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for a license registration key pool collection object.                                     | string             |
| | *optional*             |                                                                                                             |                    |
| | *read-only*            |                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an license registration key pool collection object. time.      | integer(int64)     |
| | *optional*             |                                                                                                             |                    |
| | *read-only*            |                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to a license registration key pool collection object.                                  | string             |
| | *optional*             |                                                                                                             |                    |
| | *read-only*            |                                                                                                             |                    |
+--------------------------+-------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_regkey\_member
   :name: _properties_regkey_member

+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| Name                                | Description                                                                                                                                                                            | Schema                                                                       |
+=====================================+========================================================================================================================================================================================+==============================================================================+
| | **auditRecordReference**          | A reference link to the license audit object. Will provide audit logs id, regKey, offering, machineId, address, hostname, type, grantDateTime, status.                                 | `auditRecordReference <#_properties_regkey_member_auditrecordreference>`__   |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **deviceAddress**                 | Device (BIGIP) IP address.                                                                                                                                                             | string                                                                       |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **deviceMachineId**               | Unique device id assigned to BIGIP that is a member of this registration key pool.                                                                                                     | string                                                                       |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **generation**                    | A integer that will track change made to a license registration key pool memeber object. generation.                                                                                   | integer(int64)                                                               |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
| | *read-only*                       |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **healthCheckFailureCount**       | Count of last check or poll for health failed.                                                                                                                                         | integer                                                                      |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **id**                            | Unique id assigned to a registration key license pool device (member) object.                                                                                                          | string                                                                       |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
| | *read-only*                       |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **kind**                          | Type information for this license registration key pool member (device) object, cm:device:licensing:pool:regkey:licenses:item:offerings:regkey:members:regkeypoollicensememberstate.   | string                                                                       |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
| | *read-only*                       |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **lastGoodHealthCheckDateTime**   | Last date/time for device license health. 2016-11-16T21:20:49.368Z                                                                                                                     | string                                                                       |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **lastUpdateMicros**              | Update time (micros) for last change made to an license registration key pool member object.                                                                                           | integer(int64)                                                               |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **message**                       | The message provided to the user of this licensing task state. ex. Device licensed.                                                                                                    | string                                                                       |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
| | *read-only*                       |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **selfLink**                      | Reference link to license registration key pool member (device) object.                                                                                                                | string                                                                       |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
| | *read-only*                       |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
| | **status**                        | The status of this licensing task. ex INSTALLING, LICENSED.                                                                                                                            | string                                                                       |
| | *optional*                        |                                                                                                                                                                                        |                                                                              |
+-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_regkey_member_auditrecordreference"
   class="paragraph">

**auditRecordReference**

.. raw:: html

   </div>

+----------------+----------------------------------------------------------------+----------+
| Name           | Description                                                    | Schema   |
+================+================================================================+==========+
| | **link**     | Reference link to audit record for license registration key.   | string   |
| | *optional*   |                                                                |          |
+----------------+----------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_regkey\_members\_collection
   :name: _properties_regkey_members_collection

+--------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                              | Schema             |
+==========================+==========================================================================================================================+====================+
| | **generation**         | A integer that will track change made to a license registration key for a device member collection object. generation.   | integer(int64)     |
| | *optional*             |                                                                                                                          |                    |
| | *read-only*            |                                                                                                                          |                    |
+--------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Collection of license registration key member objects                                                                    | < object > array   |
| | *optional*             |                                                                                                                          |                    |
+--------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for a license registration key for a device member collection object.                                   | string             |
| | *optional*             |                                                                                                                          |                    |
| | *read-only*            |                                                                                                                          |                    |
+--------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an license registration key device object collection object. time.          | integer(int64)     |
| | *optional*             |                                                                                                                          |                    |
| | *read-only*            |                                                                                                                          |                    |
+--------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to a license registration key for a device member collection object.                                | string             |
| | *optional*             |                                                                                                                          |                    |
| | *read-only*            |                                                                                                                          |                    |
+--------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_regkey\_offerings\_collection
   :name: _properties_regkey_offerings_collection

+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                      | Schema             |
+==========================+==================================================================================================================+====================+
| | **generation**         | A integer that will track change made to a license registration keys properties collection object. generation.   | integer(int64)     |
| | *optional*             |                                                                                                                  |                    |
| | *read-only*            |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | Collection of license registration key objects.                                                                  | < object > array   |
| | *optional*             |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for a license registration keys properties collection object.                                   | string             |
| | *optional*             |                                                                                                                  |                    |
| | *read-only*            |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an license registration keys collection object. time.               | integer(int64)     |
| | *optional*             |                                                                                                                  |                    |
| | *read-only*            |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to a license registration keys properties collection object.                                | string             |
| | *optional*             |                                                                                                                  |                    |
| | *read-only*            |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+

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
