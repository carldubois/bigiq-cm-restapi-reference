Access revoke oauth token
^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ APM OAuth Token Revocation on BIG-IP devices.
   :name: big-iq-apm-oauth-token-revocation-on-big-ip-devices.

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

API for OAuth Token Revocation on BIG-IP devices using a BIG-IQ
centralized management system.

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

| *BasePath* : /mgmt/cm/access/tasks
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

.. rubric:: Revoke all oauth token by access groups.
   :name: _revoke-tokens_access-groups_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /revoke-tokens (access-groups)

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

Revoke all active oauth tokens by access groups.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                           | Schema                                                                                          | Default   |
+============+=======================================+=======================================================================================================================================================+=================================================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {"action":"REVOKE\_TOKEN\_FOR\_USER", "userName":"user1", "accessGroupNames":["TestGroup1", "TestGroup2"]}   | `post\_revoke\_oauth\_token\_by\_access\_group <#_post_revoke_oauth_token_by_access_group>`__   |           |
|            | | *required*                          |                                                                                                                                                       |                                                                                                 |           |
+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+----------------------------------------------------+--------------------------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                                   |
+=============+====================================================+==========================================================================+
| **200**     | POST to revoke all oauth tokens by access group.   | `properties\_revoke\_oauth\_token <#_properties_revoke_oauth_token>`__   |
+-------------+----------------------------------------------------+--------------------------------------------------------------------------+
| **400**     | Error response Bad Request                         | `400\_error\_collection <#_400_error_collection>`__                      |
+-------------+----------------------------------------------------+--------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.     | `404\_error\_collection <#_404_error_collection>`__                      |
+-------------+----------------------------------------------------+--------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all oauth token revocation tasks as part of a
   collection.
   :name: _revoke-tokens_access-groups_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /revoke-tokens (access-groups)

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

Returns the collection of oauth token revocation tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+---------------------------------------------------+-------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                       | Schema                                                                                          |
+=============+===================================================+=================================================================================================+
| **200**     | GET collection of oauth token revocation tasks.   | `properties\_revoke\_oauth\_token\_collection <#_properties_revoke_oauth_token_collection>`__   |
+-------------+---------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                      | `400\_error\_collection <#_400_error_collection>`__                                             |
+-------------+---------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.    | `404\_error\_collection <#_404_error_collection>`__                                             |
+-------------+---------------------------------------------------+-------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Revoke all oauth-token sessions by access group, cluster
   name and device reference match.
   :name: _revoke-tokens_bigip_clusters_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /revoke-tokens (bigip clusters)

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

Revoke all oauth-token sessions by access group, cluster name match for
specified devices.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                        | Schema                                                                                          | Default   |
+============+=======================================+====================================================================================================================================================+=================================================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {"action":"REVOKE\_TOKEN\_FOR\_USER", "userName":"user1", "clusterNames":["BlueCluster", "RedCluster"]}   | `post\_revoke\_oauth\_token\_by\_cluster\_name <#_post_revoke_oauth_token_by_cluster_name>`__   |           |
|            | | *required*                          |                                                                                                                                                    |                                                                                                 |           |
+------------+---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+
| HTTP Code   | Description                                                                       | Schema                                                                   |
+=============+===================================================================================+==========================================================================+
| **200**     | POST to revoke oauth-token sessions within a cluster-name for a specfic device.   | `properties\_revoke\_oauth\_token <#_properties_revoke_oauth_token>`__   |
+-------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+
| **400**     | Error response Bad Request                                                        | `400\_error\_collection <#_400_error_collection>`__                      |
+-------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.                                    | `404\_error\_collection <#_404_error_collection>`__                      |
+-------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all revoke-oauth-token tasks as part of a collection.
   :name: _revoke-tokens_bigip_clusters_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /revoke-tokens (bigip clusters)

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

Returns the collection of revoke-oauth-token tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_4

+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                          |
+=============+==================================================+=================================================================================================+
| **200**     | GET collection of revoke-oauth-token tasks.      | `properties\_revoke\_oauth\_token\_collection <#_properties_revoke_oauth_token_collection>`__   |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                             |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                             |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Revoke all oauth-token sessions by access group, cluster
   name and device reference match.
   :name: _revoke-tokens_bigip_clusters_access-groups_and_device_reference_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /revoke-tokens (bigip clusters, access-groups and device reference)

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

Revoke all oauth-token sessions by access group, cluster name match for
specified devices.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_3

+------------+---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Schema                                                                                                                                                          | Default   |
+============+=======================================+==================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+=================================================================================================================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {"action":"REVOKE\_TOKEN\_FOR\_USER", "userName":"user1", "accessGroupNames":["TestGroup1", "TestGroup2"], "clusterNames":["BlueCluster", "RedCluster"], "deviceReferences": [{"link":"`https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"},{"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"} <https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642>`__]}   | `post\_revoke\_oauth\_token\_by\_cluster\_name\_access\_group\_device\_reference <#_post_revoke_oauth_token_by_cluster_name_access_group_device_reference>`__   |           |
|            | | *required*                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                                                                 |           |
+------------+---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_5

+-------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------+
| HTTP Code   | Description                                                                                        | Schema                                                                   |
+=============+====================================================================================================+==========================================================================+
| **200**     | POST to revoke oauth-token sessions within a access-group and cluster-name for a specfic device.   | `properties\_revoke\_oauth\_token <#_properties_revoke_oauth_token>`__   |
+-------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------+
| **400**     | Error response Bad Request                                                                         | `400\_error\_collection <#_400_error_collection>`__                      |
+-------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.                                                     | `404\_error\_collection <#_404_error_collection>`__                      |
+-------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all revoke-oauth-token tasks as part of a collection.
   :name: _revoke-tokens_bigip_clusters_access-groups_and_device_reference_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /revoke-tokens (bigip clusters, access-groups and device reference)

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

Returns the collection of revoke-oauth-token tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_6

+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                          |
+=============+==================================================+=================================================================================================+
| **200**     | GET collection of revoke-oauth-token tasks.      | `properties\_revoke\_oauth\_token\_collection <#_properties_revoke_oauth_token_collection>`__   |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                             |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                             |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Revoke-oauth-token by oauth token id.
   :name: _revoke-tokens_oauth_token_id_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /revoke-tokens (oauth token id)

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

Revoke-oauth-token sessions by oauth token id for a device.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_4

+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                                                                                                                                                         | Schema                                                                                  | Default   |
+============+=======================================+=====================================================================================================================================================================================================================================================================================+=========================================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {"action":"REVOKE\_TOKEN\_FOR\_CLIENT\_ID", "clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457", "deviceReferences":[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642%22%7D]}   | `post\_revoke\_oauth\_token\_by\_oauth\_id <#_post_revoke_oauth_token_by_oauth_id>`__   |           |
|            | | *required*                          |                                                                                                                                                                                                                                                                                     |                                                                                         |           |
+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_7

+-------------+----------------------------------------------------------+--------------------------------------------------------------------------+
| HTTP Code   | Description                                              | Schema                                                                   |
+=============+==========================================================+==========================================================================+
| **200**     | POST to revoke-oauth-token sessions by oauth token id.   | `properties\_revoke\_oauth\_token <#_properties_revoke_oauth_token>`__   |
+-------------+----------------------------------------------------------+--------------------------------------------------------------------------+
| **400**     | Error response Bad Request                               | `400\_error\_collection <#_400_error_collection>`__                      |
+-------------+----------------------------------------------------------+--------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.           | `404\_error\_collection <#_404_error_collection>`__                      |
+-------------+----------------------------------------------------------+--------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all revoke-oauth-token tasks as part of a collection.
   :name: _revoke-tokens_oauth_token_id_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /revoke-tokens (oauth token id)

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

Returns the collection of revoke-oauth-token tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_8

+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                          |
+=============+==================================================+=================================================================================================+
| **200**     | GET collection of revoke-oauth-token tasks.      | `properties\_revoke\_oauth\_token\_collection <#_properties_revoke_oauth_token_collection>`__   |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                             |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                             |
+-------------+--------------------------------------------------+-------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Revoke all oauth token by user.
   :name: _revoke-tokens_user_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /revoke-tokens (user)

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

Revoke all active oauth tokens by user.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_5

+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                                                                                                         | Schema                                                                                    | Default   |
+============+=======================================+=====================================================================================================================================================================================================================================+===========================================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. { "action":"REVOKE\_TOKEN\_FOR\_USER", "userName":"user1", "deviceReferences":[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642%22%7D]}   | `post\_revoke\_oauth\_token\_by\_user\_body <#_post_revoke_oauth_token_by_user_body>`__   |           |
|            | | *required*                          |                                                                                                                                                                                                                                     |                                                                                           |           |
+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_9

+-------------+--------------------------------------------------+--------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                   |
+=============+==================================================+==========================================================================+
| **200**     | POST to revoke all oauth tokens by user.         | `properties\_revoke\_oauth\_token <#_properties_revoke_oauth_token>`__   |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------+
| **400**     | Error response Bad Request                       | `400\_error\_collection <#_400_error_collection>`__                      |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                      |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all oauth token revocation tasks as part of a
   collection.
   :name: _revoke-tokens_user_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /revoke-tokens (user)

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_10

.. raw:: html

   <div class="paragraph">

Returns the collection of oauth token revocation tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_10

+-------------+---------------------------------------------------+-------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                       | Schema                                                                                          |
+=============+===================================================+=================================================================================================+
| **200**     | GET collection of oauth token revocation tasks.   | `properties\_revoke\_oauth\_token\_collection <#_properties_revoke_oauth_token_collection>`__   |
+-------------+---------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                      | `400\_error\_collection <#_400_error_collection>`__                                             |
+-------------+---------------------------------------------------+-------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.    | `404\_error\_collection <#_404_error_collection>`__                                             |
+-------------+---------------------------------------------------+-------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single instance of a revoke-oauth-token task.
   :name: _revoke-tokens_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /revoke-tokens/{objectId}

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_11

.. raw:: html

   <div class="paragraph">

Returns a object for revoke-oauth-token session task identified by id
for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_6

+------------+------------------+---------------+----------------+-----------+
| Type       | Name             | Description   | Schema         | Default   |
+============+==================+===============+================+===========+
| **Path**   | | **objectId**   |               | string(UUID)   |           |
|            | | *required*     |               |                |           |
+------------+------------------+---------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_11

+-------------+--------------------------------------------------+--------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                   |
+=============+==================================================+==========================================================================+
| **200**     | APM revoke-oauth-token task object.              | `properties\_revoke\_oauth\_token <#_properties_revoke_oauth_token>`__   |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------+
| **400**     | Server error response "Bad Request".             | `400\_error\_collection <#_400_error_collection>`__                      |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                      |
+-------------+--------------------------------------------------+--------------------------------------------------------------------------+

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

+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                                           | Schema             |
+============================+=======================================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                                   | string             |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                |                                                                                                                                                       | < object > array   |
| | *optional*               |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for a collection of tasks used to revoke-oauth-token sessions - cm:access:tasks:revoke-tokens:oauthrevoketokentaskcollectionstate.   | string             |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                                   | string             |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                                              | string             |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                                                 | integer(int64)     |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: 404\_error\_collection
   :name: _404_error_collection

+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                                           | Schema             |
+============================+=======================================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                                   | string             |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                |                                                                                                                                                       | < object > array   |
| | *optional*               |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for a collection of tasks used to revoke-oauth-token sessions - cm:access:tasks:revoke-tokens:oauthrevoketokentaskcollectionstate.   | string             |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                                   | string             |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                                              | string             |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                                                 | integer(int64)     |
| | *optional*               |                                                                                                                                                       |                    |
| | *read-only*              |                                                                                                                                                       |                    |
+----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_revoke\_oauth\_token\_by\_access\_group
   :name: _post_revoke_oauth_token_by_access_group

+--------------------------+--------------------------------------------------------------------------------------------------------------+----------+
| Name                     | Description                                                                                                  | Schema   |
+==========================+==============================================================================================================+==========+
| | **accessGroupNames**   | One or more access group names. All oauth-token sessions in these groups will be revoked by invoking task.   | string   |
| | *optional*             |                                                                                                              |          |
+--------------------------+--------------------------------------------------------------------------------------------------------------+----------+
| | **action**             | Action used to revoke-oauth-token session by access\_group. ex action. "REVOKE\_TOKEN\_FOR\_USER"            | string   |
| | *optional*             |                                                                                                              |          |
+--------------------------+--------------------------------------------------------------------------------------------------------------+----------+
| | **userName**           | User name defined for revoke-oauth-token sessions owned.                                                     | string   |
| | *optional*             |                                                                                                              |          |
+--------------------------+--------------------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_revoke\_oauth\_token\_by\_cluster\_name
   :name: _post_revoke_oauth_token_by_cluster_name

+---------------------+-----------------------------------------------------------------------------------------------------------------+----------+
| Name                | Description                                                                                                     | Schema   |
+=====================+=================================================================================================================+==========+
| | **action**        | Action used to revoke-oauth-token session by cluster\_name. ex action. "REVOKE\_TOKEN\_FOR\_USER"               | string   |
| | *optional*        |                                                                                                                 |          |
+---------------------+-----------------------------------------------------------------------------------------------------------------+----------+
| | **clusterName**   | One or more cluster names. All oauth token sessions in these bigip clusters will be revoked by invoking task.   | string   |
| | *optional*        |                                                                                                                 |          |
+---------------------+-----------------------------------------------------------------------------------------------------------------+----------+
| | **userName**      | User name defined for revoke-oauth-token sessions owned.                                                        | string   |
| | *optional*        |                                                                                                                 |          |
+---------------------+-----------------------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_revoke\_oauth\_token\_by\_cluster\_name\_access\_group\_device\_reference
   :name: _post_revoke_oauth_token_by_cluster_name_access_group_device_reference

+--------------------------+-----------------------------------------------------------------------------------------------------------------+----------+
| Name                     | Description                                                                                                     | Schema   |
+==========================+=================================================================================================================+==========+
| | **accessGroupNames**   | One or more access group names. All oauth token sessions in these groups will be revoked by invoking task.      | string   |
| | *optional*             |                                                                                                                 |          |
+--------------------------+-----------------------------------------------------------------------------------------------------------------+----------+
| | **action**             | Action used to revoke-oauth-token session by cluster\_name. ex action. "REVOKE\_TOKEN\_FOR\_USER"               | string   |
| | *optional*             |                                                                                                                 |          |
+--------------------------+-----------------------------------------------------------------------------------------------------------------+----------+
| | **clusterNames**       | One or more cluster names. All oauth token sessions in these bigip clusters will be revoked by invoking task.   | string   |
| | *optional*             |                                                                                                                 |          |
+--------------------------+-----------------------------------------------------------------------------------------------------------------+----------+
| | **deviceReferences**   | Reference link to one or more devices in which active revoke-oauth-token sessions live.                         | string   |
| | *optional*             |                                                                                                                 |          |
+--------------------------+-----------------------------------------------------------------------------------------------------------------+----------+
| | **userName**           | User name defined to all revoke-oauth-token sessions owned.                                                     | string   |
| | *optional*             |                                                                                                                 |          |
+--------------------------+-----------------------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_revoke\_oauth\_token\_by\_oauth\_id
   :name: _post_revoke_oauth_token_by_oauth_id

+------------------+-------------------------------------------------------------------------------------------------------------------+----------+
| Name             | Description                                                                                                       | Schema   |
+==================+===================================================================================================================+==========+
| | **action**     | Action used to revoke-oauth-token sessions identified by a oauth token id. ex. "REVOKE\_TOKEN\_FOR\_CLIENT\_ID"   | string   |
| | *optional*     |                                                                                                                   |          |
+------------------+-------------------------------------------------------------------------------------------------------------------+----------+
| | **clientId**   | Unique id associated with the revoke-oauth-token session. ex. e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457    | string   |
| | *optional*     |                                                                                                                   |          |
+------------------+-------------------------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_revoke\_oauth\_token\_by\_user\_body
   :name: _post_revoke_oauth_token_by_user_body

+--------------------------+-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| Name                     | Description                                                                               | Schema                                                                                     |
+==========================+===========================================================================================+============================================================================================+
| | **action**             | Action used to revoke-oauth-token session by a user. ex. "REVOKE\_TOKEN\_FOR\_USER"       | string                                                                                     |
| | *optional*             |                                                                                           |                                                                                            |
+--------------------------+-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| | **deviceReferences**   | Reference link to one or more devices in which active revoke-oauth-token sessions live.   | < `deviceReferences <#_post_revoke_oauth_token_by_user_body_devicereferences>`__ > array   |
| | *optional*             |                                                                                           |                                                                                            |
+--------------------------+-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| | **userName**           | User name defined for revoke-oauth-token sessions owned.                                  | string                                                                                     |
| | *optional*             |                                                                                           |                                                                                            |
+--------------------------+-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+

.. raw:: html

   <div id="_post_revoke_oauth_token_by_user_body_devicereferences"
   class="paragraph">

**deviceReferences**

.. raw:: html

   </div>

+----------------+---------------+----------+
| Name           | Description   | Schema   |
+================+===============+==========+
| | **link**     |               | string   |
| | *optional*   |               |          |
+----------------+---------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_revoke\_oauth\_token
   :name: _properties_revoke_oauth_token

+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| Name                      | Description                                                                                                                                  | Schema                                                                                |
+===========================+==============================================================================================================================================+=======================================================================================+
| | **accessGroupNames**    | One or more access group names. All revoke-oauth-token sessions in these groups will be killed by invoking task.                             | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **action**              | Action used to revoke-oauth-token sessions identified by a oauth token id. ex. "REVOKE\_TOKEN\_FOR\_CLIENT\_ID" "REVOKE\_TOKEN\_FOR\_USER"   | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **clientId**            | Unique id used as a reference for client session to BIGIP.                                                                                   | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
| | *read-only*             |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **currentStep**         | Current status of state for revoke-oauth-token task. ex. STARTED, FINSIHED                                                                   | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
| | *read-only*             |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **generation**          | A integer that will track change made to a revoke-oauth-token task object. generation.                                                       | integer(int64)                                                                        |
| | *optional*              |                                                                                                                                              |                                                                                       |
| | *read-only*             |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **id**                  | Unique id assocaited with revoke-oauth-token task object.                                                                                    | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **identityReference**   | Reference link to the user who issued the rest call.                                                                                         | < `identityReference <#_properties_revoke_oauth_token_identityreference>`__ > array   |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **kind**                | Type information for revoke-oauth-token task object - cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate.                           | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **lastUpdateMicros**    | Update time (micros) for last change made to a revoke-oauth-token task object. time.                                                         | integer(int64)                                                                        |
| | *optional*              |                                                                                                                                              |                                                                                       |
| | *read-only*             |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **name**                | Name of revoke-oauth-token session task object.                                                                                              | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **ownerMachineId**      | Device machine id used by revoke-oauth-token task object. Sessions that live on this device will be revoked.                                 | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **selfLink**            | A reference link URI to the revoke-oauth-token task object.                                                                                  | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
| | *read-only*             |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **startDateTime**       | Date / Time of when this revoke-oauth-token task began.                                                                                      | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **status**              | Status of revoke-oauth-token task state. - ex. STARTED, FINISHED.                                                                            | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **userName**            | User name defined to all revoke-oauth-token sessions owned.                                                                                  | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **userReference**       | Refernece link to user issuing the rest call to start revoke-oauth-token task.                                                               | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **username**            |                                                                                                                                              | string                                                                                |
| | *optional*              |                                                                                                                                              |                                                                                       |
+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_revoke_oauth_token_identityreference"
   class="paragraph">

**identityReference**

.. raw:: html

   </div>

+----------------+---------------+----------+
| Name           | Description   | Schema   |
+================+===============+==========+
| | **link**     |               | string   |
| | *optional*   |               |          |
+----------------+---------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_revoke\_oauth\_token\_collection
   :name: _properties_revoke_oauth_token_collection

+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                                              | Schema             |
+==========================+==========================================================================================================================================+====================+
| | **generation**         | A integer that will track change made to revoke-oauth-token sessions task collection object. generation.                                 | integer(int64)     |
| | *optional*             |                                                                                                                                          |                    |
| | *read-only*            |                                                                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              |                                                                                                                                          | < object > array   |
| | *optional*             |                                                                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for revoke-oauth-token sessions task collection object - cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate.   | string             |
| | *optional*             |                                                                                                                                          |                    |
| | *read-only*            |                                                                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change to revoke-oauth-token sessions task collection object. time.                                        | integer(int64)     |
| | *optional*             |                                                                                                                                          |                    |
| | *read-only*            |                                                                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI for revoke-oauth-token sessions task collection object.                                                             | string             |
| | *optional*             |                                                                                                                                          |                    |
| | *read-only*            |                                                                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

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

Last updated 2016-12-06 17:03:22 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
