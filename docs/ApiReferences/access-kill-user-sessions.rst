Access-kill-user-sessions
^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ APM kill active access sessions.
   :name: big-iq-apm-kill-active-access-sessions.

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

API used to kill active access sessions on BIGIP using a BIGIQ
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

.. rubric:: Kill all active session by access-group match.
   :name: _kill-sessions_access-groups_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /kill-sessions (access-groups)

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

Kill all active access sessions by access-group match.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                   | Schema                                                                           | Default   |
+============+=======================================+===============================================================================================================================================+==================================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {{"action":"KILL\_BY\_USER", "userName":"user2", "accessGroupNames":["TestGroup1", "TestGroup2"]}}   | `post\_kill\_access\_by\_access\_group <#_post_kill_access_by_access_group>`__   |           |
|            | | *required*                          |                                                                                                                                               |                                                                                  |           |
+------------+---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+-----------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                         | Schema                                                                                            |
+=============+=====================================================+===================================================================================================+
| **200**     | POST to kill all active access session of a user.   | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+-----------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response Bad Request                          | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+-----------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.      | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+-----------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all kill-session tasks as part of a collection.
   :name: _kill-sessions_access-groups_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /kill-sessions (access-groups)

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

Returns the collection of kill-session tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                            |
+=============+==================================================+===================================================================================================+
| **200**     | GET collection of session tasks to kill.         | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Kill all active session.
   :name: _kill-sessions_all_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /kill-sessions (all)

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

Kill all active access sessions.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                                                                                                                                                                               | Schema                                                 | Default   |
+============+=======================================+===========================================================================================================================================================================================================================================================================================================+========================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {"action":"KILL\_ALL\_SESSIONS", "deviceReferences":[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"}, {"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"}]}   | `post\_kill\_access\_all <#_post_kill_access_all>`__   |           |
|            | | *required*                          |                                                                                                                                                                                                                                                                                                           |                                                        |           |
+------------+---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                            |
+=============+==================================================+===================================================================================================+
| **200**     | POST to kill all active access sessions.         | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response Bad Request                       | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all kill-session tasks as part of a collection.
   :name: _kill-sessions_all_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /kill-sessions (all)

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

Returns the collection of kill-session tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_4

+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                            |
+=============+==================================================+===================================================================================================+
| **200**     | GET collection of session tasks to kill.         | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Kill all active kill-session by access-group match.
   :name: _kill-sessions_bigip_clusters_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /kill-sessions (bigip clusters)

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

Kill all active access kill-sessions by access-group match.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_3

+------------+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                | Schema                                                                           | Default   |
+============+=======================================+============================================================================================================================================+==================================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {{"action":"KILL\_BY\_USER", "userName":"user2", "clusterNames":["BlueCluster", "RedCluster"]}}   | `post\_kill\_access\_by\_cluster\_name <#_post_kill_access_by_cluster_name>`__   |           |
|            | | *required*                          |                                                                                                                                            |                                                                                  |           |
+------------+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_5

+-------------+----------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                              | Schema                                                                                            |
+=============+==========================================================+===================================================================================================+
| **200**     | POST to kill all active access kill-session of a user.   | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+----------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response Bad Request                               | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+----------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.           | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+----------------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all kill-session tasks as part of a collection.
   :name: _kill-sessions_bigip_clusters_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /kill-sessions (bigip clusters)

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

Returns the collection of kill-session tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_6

+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                            |
+=============+==================================================+===================================================================================================+
| **200**     | GET collection of kill-session tasks to kill.    | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Kill all active kill-session by access-group match.
   :name: _kill-sessions_bigip_clusters_access-groups_and_device_reference_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /kill-sessions (bigip clusters, access-groups and device reference)

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

Kill all active access kill-sessions by access-group match.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_4

+------------+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                              | Schema                                                                                                                                           | Default   |
+============+=======================================+==========================================================================================================================================================================================================================================================================================================================================================================================================================+==================================================================================================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {"action":"KILL\_BY\_USER", "userName":"user2", "accessGroupNames":["TestGroup1", "TestGroup2"], "clusterNames":["BlueCluster", "RedCluster"], "deviceReferences": [{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"}, {"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"}]}   | `post\_kill\_access\_by\_cluster\_name\_access\_group\_device\_reference <#_post_kill_access_by_cluster_name_access_group_device_reference>`__   |           |
|            | | *optional*                          |                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                  |           |
+------------+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_7

+-------------+----------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                              | Schema                                                                                            |
+=============+==========================================================+===================================================================================================+
| **200**     | POST to kill all active access kill-session of a user.   | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+----------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response Bad Request                               | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+----------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.           | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+----------------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all kill-session tasks as part of a collection.
   :name: _kill-sessions_bigip_clusters_access-groups_and_device_reference_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /kill-sessions (bigip clusters, access-groups and device reference)

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

Returns the collection of kill-session tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_8

+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                            |
+=============+==================================================+===================================================================================================+
| **200**     | GET collection of kill-session tasks to kill.    | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Kill active sessions by session id.
   :name: _kill-sessions_session_id_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /kill-sessions (session id)

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

Kill active access sessions by session id for a device.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_5

+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                   | Schema                                                                  | Default   |
+============+=======================================+===============================================================================================================================================================================================================================================================================================================================================================================================================================+=========================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {"action":"KILL\_BY\_LIST\_OF\_SESSIONS", "sessions":[{"deviceReference":{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"}, "sessionIds":["2a5d7604", "875f7fed"]}, {"deviceReference":{"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"}, "sessionIds":["2hjj234", "9as3323"]}}   | `post\_kill\_access\_by\_sessions <#_post_kill_access_by_sessions>`__   |           |
|            | | *required*                          |                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                         |           |
+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_9

+-------------+------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                          | Schema                                                                                            |
+=============+======================================================+===================================================================================================+
| **200**     | POST to kill active access sessions by session id.   | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response Bad Request                           | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+------------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.       | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+------------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all kill-session tasks as part of a collection.
   :name: _kill-sessions_session_id_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /kill-sessions (session id)

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

Returns the collection of kill-session tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_10

+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                            |
+=============+==================================================+===================================================================================================+
| **200**     | GET collection of session tasks to kill.         | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Kill all active session by a user.
   :name: _kill-sessions_user_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /kill-sessions (user)

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

Kill all active access sessions by a user.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_6

+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+-----------+
| Type       | Name                                  | Description                                                                                                                                                                                                                                                                                                             | Schema                                                                     | Default   |
+============+=======================================+=========================================================================================================================================================================================================================================================================================================================+============================================================================+===========+
| **Body**   | | **Json string for request body.**   | Input parameter list in json format. ex. {{"action":"KILL\_BY\_USER","userName":"user2","deviceReferences":[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"}, {"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"}}}   | `post\_kill\_access\_by\_user\_body <#_post_kill_access_by_user_body>`__   |           |
|            | | *required*                          |                                                                                                                                                                                                                                                                                                                         |                                                                            |           |
+------------+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_11

+-------------+-----------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                         | Schema                                                                                            |
+=============+=====================================================+===================================================================================================+
| **200**     | POST to kill all active access session of a user.   | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+-----------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response Bad Request                          | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+-----------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.      | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+-----------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: List all kil-session tasks as part of a collection.
   :name: _kill-sessions_user_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /kill-sessions (user)

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_12

.. raw:: html

   <div class="paragraph">

Returns the collection of kill-session tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_12

+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                                            |
+=============+==================================================+===================================================================================================+
| **200**     | GET collection of session tasks to kill.         | `properties\_kill\_access\_session\_collection <#_properties_kill_access_session_collection>`__   |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                     | `400\_error\_collection <#_400_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                                               |
+-------------+--------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single instance of a kill access session task.
   :name: _kill-sessions_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /kill-sessions/{objectId}

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Description
   :name: _description_13

.. raw:: html

   <div class="paragraph">

Returns a object for kill access session task identified by id for an
endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_7

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
   :name: _responses_13

+-------------+--------------------------------------------------+----------------------------------------------------------------------------+
| HTTP Code   | Description                                      | Schema                                                                     |
+=============+==================================================+============================================================================+
| **200**     | APM kill sessions task object.                   | `properties\_kill\_access\_session <#_properties_kill_access_session>`__   |
+-------------+--------------------------------------------------+----------------------------------------------------------------------------+
| **400**     | Server error response "Bad Request".             | `400\_error\_collection <#_400_error_collection>`__                        |
+-------------+--------------------------------------------------+----------------------------------------------------------------------------+
| **404**     | Error response Public URI path not registered.   | `404\_error\_collection <#_404_error_collection>`__                        |
+-------------+--------------------------------------------------+----------------------------------------------------------------------------+

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

+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                                      | Schema             |
+============================+==================================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                              | string             |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                |                                                                                                                                                  | < object > array   |
| | *optional*               |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for a collection of tasks used to kill access sessions - cm:access:tasks:kill-sessions:accesskillsessionstaskcollectionstate.   | string             |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                              | string             |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                                         | string             |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                                            | integer(int64)     |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: 404\_error\_collection
   :name: _404_error_collection

+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                                      | Schema             |
+============================+==================================================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                                              | string             |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                |                                                                                                                                                  | < object > array   |
| | *optional*               |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for a collection of tasks used to kill access sessions - cm:access:tasks:kill-sessions:accesskillsessionstaskcollectionstate.   | string             |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                                              | string             |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                                         | string             |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                                            | integer(int64)     |
| | *optional*               |                                                                                                                                                  |                    |
| | *read-only*              |                                                                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_kill\_access\_all
   :name: _post_kill_access_all

+--------------------------+-------------------------------------------------------------------------------+----------+
| Name                     | Description                                                                   | Schema   |
+==========================+===============================================================================+==========+
| | **action**             | Action used to kill all access sessions. ex. "KILL\_ALL\_SESSIONS"            | string   |
| | *optional*             |                                                                               |          |
+--------------------------+-------------------------------------------------------------------------------+----------+
| | **deviceReferences**   | Reference link to one or more devices in which active access sessions live.   | string   |
| | *optional*             |                                                                               |          |
+--------------------------+-------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_kill\_access\_by\_access\_group
   :name: _post_kill_access_by_access_group

+--------------------------+-------------------------------------------------------------------------------------------------+----------+
| Name                     | Description                                                                                     | Schema   |
+==========================+=================================================================================================+==========+
| | **accessGroupNames**   | One or more access group names. All sessions in these groups will be killed by invoking task.   | string   |
| | *optional*             |                                                                                                 |          |
+--------------------------+-------------------------------------------------------------------------------------------------+----------+
| | **action**             | Action used to kill access session by access\_group. ex action. "KILL\_BY\_USER"                | string   |
| | *optional*             |                                                                                                 |          |
+--------------------------+-------------------------------------------------------------------------------------------------+----------+
| | **userName**           | User name defined to all sessions owned.                                                        | string   |
| | *optional*             |                                                                                                 |          |
+--------------------------+-------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_kill\_access\_by\_cluster\_name
   :name: _post_kill_access_by_cluster_name

+----------------------+----------------------------------------------------------------------------------------------------+----------+
| Name                 | Description                                                                                        | Schema   |
+======================+====================================================================================================+==========+
| | **action**         | Action used to kill access session by access\_group. ex action. "KILL\_BY\_USER"                   | string   |
| | *optional*         |                                                                                                    |          |
+----------------------+----------------------------------------------------------------------------------------------------+----------+
| | **clusterNames**   | One or more cluster names. All sessions in these bigip clusters will be killed by invoking task.   | string   |
| | *optional*         |                                                                                                    |          |
+----------------------+----------------------------------------------------------------------------------------------------+----------+
| | **userName**       | User name defined to all sessions owned.                                                           | string   |
| | *optional*         |                                                                                                    |          |
+----------------------+----------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_kill\_access\_by\_cluster\_name\_access\_group\_device\_reference
   :name: _post_kill_access_by_cluster_name_access_group_device_reference

+--------------------------+----------------------------------------------------------------------------------------------------+----------+
| Name                     | Description                                                                                        | Schema   |
+==========================+====================================================================================================+==========+
| | **accessGroupNames**   | One or more access group names. All sessions in these groups will be killed by invoking task.      | string   |
| | *optional*             |                                                                                                    |          |
+--------------------------+----------------------------------------------------------------------------------------------------+----------+
| | **action**             | Action used to kill access session by access\_group. ex action. "KILL\_BY\_USER"                   | string   |
| | *optional*             |                                                                                                    |          |
+--------------------------+----------------------------------------------------------------------------------------------------+----------+
| | **clusterNames**       | One or more cluster names. All sessions in these bigip clusters will be killed by invoking task.   | string   |
| | *optional*             |                                                                                                    |          |
+--------------------------+----------------------------------------------------------------------------------------------------+----------+
| | **deviceReferences**   | Reference link to one or more devices in which active access sessions live.                        | string   |
| | *optional*             |                                                                                                    |          |
+--------------------------+----------------------------------------------------------------------------------------------------+----------+
| | **userName**           | User name defined to all sessions owned.                                                           | string   |
| | *optional*             |                                                                                                    |          |
+--------------------------+----------------------------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_kill\_access\_by\_sessions
   :name: _post_kill_access_by_sessions

+------------------+-------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
| Name             | Description                                                                                     | Schema                                                             |
+==================+=================================================================================================+====================================================================+
| | **action**     | Action used to kill all access sessions identified by a session id. ex. "KILL\_ALL\_SESSIONS"   | string                                                             |
| | *optional*     |                                                                                                 |                                                                    |
+------------------+-------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
| | **sessions**   |                                                                                                 | < `sessions <#_post_kill_access_by_sessions_sessions>`__ > array   |
| | *optional*     |                                                                                                 |                                                                    |
+------------------+-------------------------------------------------------------------------------------------------+--------------------------------------------------------------------+

.. raw:: html

   <div id="_post_kill_access_by_sessions_sessions" class="paragraph">

**sessions**

.. raw:: html

   </div>

+--------------------------+-------------------------------------------------------------------------------+--------------------------------------------------------------------------+
| Name                     | Description                                                                   | Schema                                                                   |
+==========================+===============================================================================+==========================================================================+
| | **deviceReferences**   | Reference link to one or more devices in which active access sessions live.   | `deviceReferences <#_post_kill_access_by_sessions_devicereferences>`__   |
| | *optional*             |                                                                               |                                                                          |
+--------------------------+-------------------------------------------------------------------------------+--------------------------------------------------------------------------+
| | **sessionIds**         |                                                                               | < string > array                                                         |
| | *optional*             |                                                                               |                                                                          |
+--------------------------+-------------------------------------------------------------------------------+--------------------------------------------------------------------------+

.. raw:: html

   <div id="_post_kill_access_by_sessions_devicereferences"
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

.. rubric:: post\_kill\_access\_by\_user\_body
   :name: _post_kill_access_by_user_body

+--------------------------+-------------------------------------------------------------------------------+----------+
| Name                     | Description                                                                   | Schema   |
+==========================+===============================================================================+==========+
| | **action**             | Action used to kill access session by a user. ex. "KILL\_BY\_USER"            | string   |
| | *optional*             |                                                                               |          |
+--------------------------+-------------------------------------------------------------------------------+----------+
| | **deviceReferences**   | Reference link to one or more devices in which active access sessions live.   | string   |
| | *optional*             |                                                                               |          |
+--------------------------+-------------------------------------------------------------------------------+----------+
| | **userName**           | User name defined to all sessions owned.                                      | string   |
| | *optional*             |                                                                               |          |
+--------------------------+-------------------------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_kill\_access\_session
   :name: _properties_kill_access_session

+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| Name                      | Description                                                                                                                  | Schema                                                                                 |
+===========================+==============================================================================================================================+========================================================================================+
| | **action**              | Unique id assigned to a access kill user session task object.                                                                | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **currentStep**         | BIG-IQ maintains a version # to track changes of ASM signatures.                                                             | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
| | *read-only*             |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **deviceReferences**    | Reference link to one or more devices in which active access sessions live.                                                  | < `deviceReferences <#_properties_kill_access_session_devicereferences>`__ > array     |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **generation**          | A integer that will track change made to a kill-sessions task object. generation.                                            | integer(int64)                                                                         |
| | *optional*              |                                                                                                                              |                                                                                        |
| | *read-only*             |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **id**                  | Unique id assocaited with kill-sessions task object.                                                                         | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **identityReference**   | Reference link to the user who issued the rest call.                                                                         | < `identityReference <#_properties_kill_access_session_identityreference>`__ > array   |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **kind**                | Type information for access kill user session task object - cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate.   | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **lastUpdateMicros**    | Update time (micros) for last change made to a kill-sessions task object. time.                                              | integer(int64)                                                                         |
| | *optional*              |                                                                                                                              |                                                                                        |
| | *read-only*             |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **name**                | Name of access kill user session task object.                                                                                | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **ownerMachineId**      | Device machine id used by the kill user session task object. Sessions that live on this device will be killed.               | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **selfLink**            | A reference link URI to the kill-sessions task object.                                                                       | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
| | *read-only*             |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **startDateTime**       | Date / Time of when this kill user session task began.                                                                       | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **status**              | Status of kill user session task state. - ex. STARTED, FINISHED.                                                             | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **userName**            | User name defined to all sessions owned.                                                                                     | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **userReference**       | Refernece link to user issing the rest call to start kill-session task.                                                      | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
| | **username**            |                                                                                                                              | string                                                                                 |
| | *optional*              |                                                                                                                              |                                                                                        |
+---------------------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_kill_access_session_devicereferences"
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

   <div id="_properties_kill_access_session_identityreference"
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

.. rubric:: properties\_kill\_access\_session\_collection
   :name: _properties_kill_access_session_collection

+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                                                   | Schema             |
+==========================+===============================================================================================================================================+====================+
| | **generation**         | A integer that will track change made to the access kill user session task collection object. generation.                                     | integer(int64)     |
| | *optional*             |                                                                                                                                               |                    |
| | *read-only*            |                                                                                                                                               |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              |                                                                                                                                               | < object > array   |
| | *optional*             |                                                                                                                                               |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for access kill user session task collection object - cm:access:tasks:kill-sessions:accesskillsessionstaskcollectionstate.   | string             |
| | *optional*             |                                                                                                                                               |                    |
| | *read-only*            |                                                                                                                                               |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change to the access kill user session task collection object. time.                                            | integer(int64)     |
| | *optional*             |                                                                                                                                               |                    |
| | *read-only*            |                                                                                                                                               |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI for the access kill user session task collection object.                                                                 | string             |
| | *optional*             |                                                                                                                                               |                    |
| | *read-only*            |                                                                                                                                               |                    |
+--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------+

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

Last updated 2016-12-06 12:21:22 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
