Pool member management
^^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ LTM/ADC Pool Member Management.
   :name: big-iq-ltmadc-pool-member-management.

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

API used to manage LTM pool members.

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

| *BasePath* : /mgmt/cm/adc-core/working-config/ltm
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

.. rubric:: List all virtual pools items as a collection.
   :name: _pool_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /pool

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

Returns the collection of virtual pools.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+--------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                    | Schema                                                 |
+=============+================================+========================================================+
| **200**     | Collection of virtual pools.   | `properties\_collection <#_properties_collection>`__   |
+-------------+--------------------------------+--------------------------------------------------------+
| **400**     | Error response "Bad Request"   | `error\_collection <#_error_collection>`__             |
+-------------+--------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single pool object.
   :name: _pool_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /pool/{objectId}

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

Returns the pool object identified by id for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+------------------+-----------------------------------------+----------------+-----------+
| Type       | Name             | Description                             | Schema         | Default   |
+============+==================+=========================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to a virtual pool.   | string(UUID)   | None      |
|            | | *required*     |                                         |                |           |
+------------+------------------+-----------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+----------------------------------------+----------------------------------------------+
| HTTP Code   | Description                            | Schema                                       |
+=============+========================================+==============================================+
| **200**     | Virtual pool object.                   | `properties\_pool <#_properties_pool>`__     |
+-------------+----------------------------------------+----------------------------------------------+
| **400**     | Server error response "Bad Request".   | `error\_collection <#_error_collection>`__   |
+-------------+----------------------------------------+----------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Add a LTM node as a member of an virtual application pool.
   :name: _pool_objectid_members_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /pool/{objectId}/members

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

Add a application server node to a specific virtual pool.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+-----------------------------------+-----------------------------------------------+----------------------------------------------------------+-----------+
| Type       | Name                              | Description                                   | Schema                                                   | Default   |
+============+===================================+===============================================+==========================================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to pool member object.     | string(UUID)                                             | None      |
|            | | *required*                      |                                               |                                                          |           |
+------------+-----------------------------------+-----------------------------------------------+----------------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. Ex. {}   | `post\_pool\_member\_body <#_post_pool_member_body>`__   | None      |
|            | | *required*                      |                                               |                                                          |           |
+------------+-----------------------------------+-----------------------------------------------+----------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+----------------------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                 |
+=============+====================================================+========================================================+
| **200**     | POST a node to an application pool.                | `properties\_collection <#_properties_collection>`__   |
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

.. rubric:: Add a LTM node as a member of an virtual application pool.
   :name: _pool_objectid_members_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    DEL /pool/{objectId}/members

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

Delete a application server node for a specific virtual pool.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_3

+------------+------------------+---------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                 | Schema         | Default   |
+============+==================+=============================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to pool member object.   | string(UUID)   | None      |
|            | | *required*     |                                             |                |           |
+------------+------------------+---------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_4

+-------------+----------------------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                 |
+=============+====================================================+========================================================+
| **200**     | Delete a node for an application pool.             | `properties\_collection <#_properties_collection>`__   |
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

.. rubric:: List all pool members are part of a collection.
   :name: _pool_objectid_members_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /pool/{objectId}/members

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

Returns a collection of pool members.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_4

+------------+------------------+-----------------------------------------+----------------+-----------+
| Type       | Name             | Description                             | Schema         | Default   |
+============+==================+=========================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to a virtual pool.   | string(UUID)   |           |
|            | | *required*     |                                         |                |           |
+------------+------------------+-----------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_5

+-------------+-------------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                               | Schema                                                 |
+=============+===========================================+========================================================+
| **200**     | Virtual pool members collection object.   | `properties\_collection <#_properties_collection>`__   |
+-------------+-------------------------------------------+--------------------------------------------------------+
| **400**     | Server error response "Bad Request".      | `error\_collection <#_error_collection>`__             |
+-------------+-------------------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single pool member (node) object.
   :name: _pool_objectid_members_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /pool/{objectId}/members/{objectId}

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

Returns the pool memeber object identified by id for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_5

+------------+------------------+------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                    | Schema         | Default   |
+============+==================+================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to a virtual pool member.   | string(UUID)   |           |
|            | | *required*     |                                                |                |           |
+------------+------------------+------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_6

+-------------+----------------------------------------+-------------------------------------------------------------+
| HTTP Code   | Description                            | Schema                                                      |
+=============+========================================+=============================================================+
| **200**     | Virtual pool member (node) object.     | `properties\_pool\_members <#_properties_pool_members>`__   |
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

+----------------------------+--------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                      | Schema             |
+============================+==================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                              | string             |
| | *optional*               |                                                                                                  |                    |
| | *read-only*              |                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of pool members. error response from server.                                          | < object > array   |
| | *optional*               |                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for pool member collections-cm:adc-core:working-config:ltm:pool:adcpoolstate.   | string             |
| | *optional*               |                                                                                                  |                    |
| | *read-only*              |                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                              | string             |
| | *optional*               |                                                                                                  |                    |
| | *read-only*              |                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                         | string             |
| | *optional*               |                                                                                                  |                    |
| | *read-only*              |                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                            | integer(int64)     |
| | *optional*               |                                                                                                  |                    |
| | *read-only*              |                                                                                                  |                    |
+----------------------------+--------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_collection
   :name: _properties_collection

+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                              | Schema             |
+==========================+==========================================================================================+====================+
| | **generation**         | A integer that will track change made to a virtual pool collection object. generation.   | integer(int64)     |
| | *optional*             |                                                                                          |                    |
| | *read-only*            |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| | **items**              | A collection of pool members. properties defining items.                                 | < object > array   |
| | *optional*             |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this virtual pool collection object.                                | string             |
| | *optional*             |                                                                                          |                    |
| | *read-only*            |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an virtual pool collection object. time.    | integer(int64)     |
| | *optional*             |                                                                                          |                    |
| | *read-only*            |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the virtual pool collection object.                              | string             |
| | *optional*             |                                                                                          |                    |
| | *read-only*            |                                                                                          |                    |
+--------------------------+------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_pool
   :name: _properties_pool

+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Name                                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Schema                                                                          |
+======================================+================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+=================================================================================+
| | **allowNat**                       | Is NAT (addess translation) allowed for application servers in this pool.                                                                                                                                                                                                                                                                                                                                                                                                                                                      | boolean                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **deviceReference**                | A reference link to a device (BIGIP) that virtual pool exists. Also additional data such as id, name, kind and machine id is provided.                                                                                                                                                                                                                                                                                                                                                                                         | `deviceReference <#_properties_pool_devicereference>`__                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **enableQueueOnConnectionLimit**   | Enable or disable queuing connections when pool member or node connection limits are reached.                                                                                                                                                                                                                                                                                                                                                                                                                                  | boolean                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **generation**                     | A integer that will track change made to a virtual pool object. generation.                                                                                                                                                                                                                                                                                                                                                                                                                                                    | integer(int64)                                                                  |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
| | *read-only*                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **id**                             | Unique id assigned to a virtual pool object.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
| | *read-only*                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **ignorePersistedWeight**          | Is the weight of persisted connections on pool members when making load balancing decisions counted.                                                                                                                                                                                                                                                                                                                                                                                                                           | boolean                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **ipTosToClientControl**           | Specifies the Type of Service (ToS) level to use when sending packets to a client. possible values on bigiq: 0 ~ 255                                                                                                                                                                                                                                                                                                                                                                                                           | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **ipTosToServerControl**           | Specifies the Type of Service (ToS) level to use when sending packets to a server. possible values on bigiq: 0 ~ 255                                                                                                                                                                                                                                                                                                                                                                                                           | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **kind**                           | Type information for this virtual pool object.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
| | *read-only*                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **lastUpdateMicros**               | Update time (micros) for last change made to an virtual pool object. time.                                                                                                                                                                                                                                                                                                                                                                                                                                                     | integer(int64)                                                                  |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
| | *read-only*                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **linkQosToClient**                | Specifies the Quality of Service (QoS) level to use when sending packets to a client. 0 ~ 7, 65535 (passthrough)                                                                                                                                                                                                                                                                                                                                                                                                               | integer                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **linkQosToServer**                | Specifies the Quality of Service (QoS) level to use when sending packets to a server. 0 ~ 7, 65535 (passthrough)                                                                                                                                                                                                                                                                                                                                                                                                               | integer                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **loadBalancingMode**              | Specifies the modes that the system uses to load balance name resolution requests among the members of this pool. dynamic-ratio-member, least-connections-member, observed-node, ratio-least-connections-node, round-robin, dynamic-ratio-node, least-connections-node, predictive-member, ratio-member, weighted-least-connections-member, fastest-app-response, least-sessions, predictive-node, ratio-node, weighted-least-connections-node, fastest-node, observed-member, ratio-least-connections-member, ratio-session   | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **membersCollectionReference**     | Reference link to collection of pool members (nodes).                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `membersCollectionReference <#_properties_pool_memberscollectionreference>`__   |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **minActiveMembers**               | Specifies the minimum number of members that must be up for traffic to be confined to a priority group when using priority-based activation.                                                                                                                                                                                                                                                                                                                                                                                   | integer                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **name**                           | Name of virtual pool.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **partition**                      | Partition location that pool and members are located. default Common                                                                                                                                                                                                                                                                                                                                                                                                                                                           | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **queueDepthLimit**                | Specifies the maximum number of connections that may simultaneously be queued to go to any member of this pool.                                                                                                                                                                                                                                                                                                                                                                                                                | integer                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **queueTimeLimit**                 | Specifies the maximum time, in milliseconds, a connection will remain enqueued. When unset, there is no limit.                                                                                                                                                                                                                                                                                                                                                                                                                 | integer                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **reselectTries**                  | Specifies the number of times the system tries to contact a pool member after a passive failure.                                                                                                                                                                                                                                                                                                                                                                                                                               | integer                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **selfLink**                       | A reference link URI to the virtual pool object.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
| | *read-only*                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **serviceDownAction**              | Specifies the action to take if the service specified in the pool is marked down. The default value is none.                                                                                                                                                                                                                                                                                                                                                                                                                   | string                                                                          |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **slowRampTime**                   | Specifies, in seconds, the ramp time for the pool. This provides the ability to cause a pool member that has just been enabled, or marked up, to receive proportionally less traffic than other members in the pool.                                                                                                                                                                                                                                                                                                           | integer                                                                         |
| | *optional*                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                 |
+--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_pool_devicereference" class="paragraph">

**deviceReference**

.. raw:: html

   </div>

+-------------------+--------------------------------------------------------------------------------------------+----------+
| Name              | Description                                                                                | Schema   |
+===================+============================================================================================+==========+
| | **id**          | Unique id assigned to a device referenced by this object.                                  | string   |
| | *optional*      |                                                                                            |          |
+-------------------+--------------------------------------------------------------------------------------------+----------+
| | **kind**        | Type information for device. shared:resolver:device-groups:restdeviceresolverdevicestate   | string   |
| | *optional*      |                                                                                            |          |
+-------------------+--------------------------------------------------------------------------------------------+----------+
| | **link**        | Reference link to adc-core-allbigipDevices in shared resolver device-groups.               | string   |
| | *optional*      |                                                                                            |          |
+-------------------+--------------------------------------------------------------------------------------------+----------+
| | **machineId**   | Unique id assigned to the hardware device. If virtual could be the same as id object.      | string   |
| | *optional*      |                                                                                            |          |
+-------------------+--------------------------------------------------------------------------------------------+----------+
| | **name**        | A name used to identify this device.                                                       | string   |
| | *optional*      |                                                                                            |          |
+-------------------+--------------------------------------------------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_pool_memberscollectionreference"
   class="paragraph">

**membersCollectionReference**

.. raw:: html

   </div>

+-------------------------+-------------------------------------------------------------+-----------+
| Name                    | Description                                                 | Schema    |
+=========================+=============================================================+===========+
| | **isSubcollection**   | Does a sub-collection for this object exist. True / False   | boolean   |
| | *optional*            |                                                             |           |
+-------------------------+-------------------------------------------------------------+-----------+
| | **link**              | Reference link to a collection of pool members.             | string    |
| | *optional*            |                                                             |           |
+-------------------------+-------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_pool\_members
   :name: _properties_pool_members

+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| Name                     | Description                                                                                                        | Schema                                                        |
+==========================+====================================================================================================================+===============================================================+
| | **connectionLimit**    | Number of connection allowed for pool member.                                                                      | integer                                                       |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **generation**         | A integer that will track change made to a virtual pool member object. generation.                                 | integer(int64)                                                |
| | *optional*             |                                                                                                                    |                                                               |
| | *read-only*            |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **id**                 | Unique id assigned to a virtual pool collection object.                                                            | string                                                        |
| | *optional*             |                                                                                                                    |                                                               |
| | *read-only*            |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **kind**               | Type information for this virtual pool member object.                                                              | string                                                        |
| | *optional*             |                                                                                                                    |                                                               |
| | *read-only*            |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an virtual pool member object. time.                                  | integer(int64)                                                |
| | *optional*             |                                                                                                                    |                                                               |
| | *read-only*            |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **name**               | Name of pool member.                                                                                               | string                                                        |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **nodeReference**      | Reference link to ltm nodes.                                                                                       | `nodeReference <#_properties_pool_members_nodereference>`__   |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **partition**          | Partition location that pool and members are located. default Common                                               | string                                                        |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **port**               | Port used for application connect.                                                                                 | integer                                                       |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **priortyGroup**       | Specifies the priority group within the pool for this pool member.                                                 | integer                                                       |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **rateLimit**          | Specifies the maximum number of connections per second allowed for a pool member. The default value is 'disabled   | string                                                        |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **ratio**              | Specifies the ratio weight that you want to assign to the pool member. The default value is 1.                     | integer                                                       |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **selfLink**           | A reference link URI to the virtual pool member object.                                                            | string                                                        |
| | *optional*             |                                                                                                                    |                                                               |
| | *read-only*            |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+
| | **sessionConfig**      | Enables or disables the node for new sessions. The default value is user-enabled.                                  | string                                                        |
| | *optional*             |                                                                                                                    |                                                               |
+--------------------------+--------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------+

.. raw:: html

   <div id="_properties_pool_members_nodereference" class="paragraph">

**nodeReference**

.. raw:: html

   </div>

+----------------+-----------------------------------------------------------------+----------+
| Name           | Description                                                     | Schema   |
+================+=================================================================+==========+
| | **link**     | Reference link to node specific to pool member configuration.   | string   |
| | *optional*   |                                                                 |          |
+----------------+-----------------------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_pool\_member\_body
   :name: _post_pool_member_body

+-----------------------+---------------------------------------------------------------+-----------+
| Name                  | Description                                                   | Schema    |
+=======================+===============================================================+===========+
| | **partition**       | Partition where this application node lives. default Common   | string    |
| | *required*          |                                                               |           |
+-----------------------+---------------------------------------------------------------+-----------+
| | **name**            | Name of application node.                                     | string    |
| | *required*          |                                                               |           |
+-----------------------+---------------------------------------------------------------+-----------+
| | **port**            | Port to request connection to node.                           | integer   |
| | *required*          |                                                               |           |
+-----------------------+---------------------------------------------------------------+-----------+
| | **nodeReference**   | Reference link to application node.                           | string    |
| | *required*          |                                                               |           |
+-----------------------+---------------------------------------------------------------+-----------+

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
