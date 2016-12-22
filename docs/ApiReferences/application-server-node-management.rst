Application node management
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ LTM Application Server Node.
   :name: big-iq-ltm-application-server-node.

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

API used to create/manage LTM application server nodes allowing for
distribution into pools.

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

.. rubric:: Create a LTM application server node.
   :name: _node_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /node

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

POST to create a BIGIP application server node.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+-----------------------------------+---------------------------------------------------------+--------------------------------------------------------------------+-----------+
| Type       | Name                              | Description                                             | Schema                                                             | Default   |
+============+===================================+=========================================================+====================================================================+===========+
| **Path**   | | **objectId**                    | Unique id assigned to application server node object.   | string(UUID)                                                       | None      |
|            | | *required*                      |                                                         |                                                                    |           |
+------------+-----------------------------------+---------------------------------------------------------+--------------------------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. Ex. {}             | `post\_application\_node\_body <#_post_application_node_body>`__   | None      |
|            | | *required*                      |                                                         |                                                                    |           |
+------------+-----------------------------------+---------------------------------------------------------+--------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+----------------------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                 |
+=============+====================================================+========================================================+
| **200**     | POST a BIGIP LTM application server node.          | `properties\_collection <#_properties_collection>`__   |
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

.. rubric:: List all application server node items as a collection.
   :name: _node_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /node

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

Returns the collection of nodes.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+----------------------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                 |
+=============+====================================================+========================================================+
| **200**     | Collection of nodes.                               | `properties\_collection <#_properties_collection>`__   |
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

.. rubric:: Used to get a single application server node object.
   :name: _node_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /node/{objectId}

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

Returns the application server node object identified by id for an
endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+------------------+----------------------------------------------------+----------------+-----------+
| Type       | Name             | Description                                        | Schema         | Default   |
+============+==================+====================================================+================+===========+
| **Path**   | | **objectId**   | Unique id assigned to a application server node.   | string(UUID)   |           |
|            | | *required*     |                                                    |                |           |
+------------+------------------+----------------------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+----------------------------------------------------+-------------------------------------------------------+
| HTTP Code   | Description                                        | Schema                                                |
+=============+====================================================+=======================================================+
| **200**     | Application server node object.                    | `properties\_node <#_properties_node>`__              |
+-------------+----------------------------------------------------+-------------------------------------------------------+
| **400**     | Server error response "Bad Request".               | `400\_error\_collection <#_400_error_collection>`__   |
+-------------+----------------------------------------------------+-------------------------------------------------------+
| **404**     | Error response "Public URI path not registered."   | `404\_error\_collection <#_404_error_collection>`__   |
+-------------+----------------------------------------------------+-------------------------------------------------------+

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

+----------------------------+----------------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                                                                | Schema             |
+============================+============================================================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                                                        | string             |
| | *optional*               |                                                                                                                            |                    |
| | *read-only*              |                                                                                                                            |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of application server nodes. Errored response from server.                                                      | < object > array   |
| | *optional*               |                                                                                                                            |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for LTM application server nodes - errors – cm:adc-core:working-config:ltm:node:adcnodecollectionstate.   | string             |
| | *optional*               |                                                                                                                            |                    |
| | *read-only*              |                                                                                                                            |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                                                        | string             |
| | *optional*               |                                                                                                                            |                    |
| | *read-only*              |                                                                                                                            |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                                                   | string             |
| | *optional*               |                                                                                                                            |                    |
| | *read-only*              |                                                                                                                            |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                                                      | integer(int64)     |
| | *optional*               |                                                                                                                            |                    |
| | *read-only*              |                                                                                                                            |                    |
+----------------------------+----------------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: 404\_error\_collection
   :name: _404_error_collection

+----------------------------+-------------------------------------------------------------------------------------------+--------------------+
| Name                       | Description                                                                               | Schema             |
+============================+===========================================================================================+====================+
| | **errorStack**           | Error stack trace returned by java.                                                       | string             |
| | *optional*               |                                                                                           |                    |
| | *read-only*              |                                                                                           |                    |
+----------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **items**                | Collection of application server nodes. Errored response from server.                     | < object > array   |
| | *optional*               |                                                                                           |                    |
+----------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **kind**                 | Type information for node - cm:adc-core:working-config:ltm:node:adcnodecollectionstate.   | string             |
| | *optional*               |                                                                                           |                    |
| | *read-only*              |                                                                                           |                    |
+----------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.                                                       | string             |
| | *optional*               |                                                                                           |                    |
| | *read-only*              |                                                                                           |                    |
+----------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)                                                  | string             |
| | *optional*               |                                                                                           |                    |
| | *read-only*              |                                                                                           |                    |
+----------------------------+-------------------------------------------------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.                                                     | integer(int64)     |
| | *optional*               |                                                                                           |                    |
| | *read-only*              |                                                                                           |                    |
+----------------------------+-------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_collection
   :name: _properties_collection

+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                                                      | Schema             |
+==========================+==================================================================================================================+====================+
| | **generation**         | A integer that will track change made to a node collection object. generation.                                   | integer(int64)     |
| | *optional*             |                                                                                                                  |                    |
| | *read-only*            |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| | **items**              | A collection of application server nodes. Properties defining items.                                             | < object > array   |
| | *optional*             |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this node collection object - cm:adc-core:working-config:ltm:node:adcnodecollectionstate.   | string             |
| | *optional*             |                                                                                                                  |                    |
| | *read-only*            |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an node collection object. time.                                    | integer(int64)     |
| | *optional*             |                                                                                                                  |                    |
| | *read-only*            |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the application server node collection object.                                           | string             |
| | *optional*             |                                                                                                                  |                    |
| | *read-only*            |                                                                                                                  |                    |
+--------------------------+------------------------------------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_node
   :name: _properties_node

+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| Name                     | Description                                                                                                                   | Schema                                                    |
+==========================+===============================================================================================================================+===========================================================+
| | **address**            | Network address for application server used for node object.                                                                  | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **connectionLimit**    | Specifies the maximum number of connections allowed for the node or node address.                                             | integer                                                   |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **deviceReference**    | Reference link to BIGIP device assiociated to application server node.                                                        | `deviceReference <#_properties_node_devicereference>`__   |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **fqdn**               | Specifies the node’s fully qualified domain name (FQDN) attributes.                                                           | `fqdn <#_properties_node_fqdn>`__                         |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **generation**         | A integer that will track change made to a LTM application server node object. - generation.                                  | integer(int64)                                            |
| | *optional*             |                                                                                                                               |                                                           |
| | *read-only*            |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **id**                 | Unique id assigned to a virtual server object.                                                                                | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
| | *read-only*            |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **isEphemeral**        | Is this node short lived when fowarding application traffic.                                                                  | boolean                                                   |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **kind**               | Type information for this application server node object. - cm:adc-core:working-config:ltm:node:adcnodestate                  | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an LTN application server node object - time.                                    | integer(int64)                                            |
| | *optional*             |                                                                                                                               |                                                           |
| | *read-only*            |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **name**               | Name of LTM application server node.                                                                                          | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **partition**          | Displays the administrative partition within which this node resides.                                                         | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **rateLimit**          | Specifies the maximum number of connections per second allowed for a node or node address. The default value is 'disabled'.   | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **ratio**              | Specifies the fixed ratio value used for a node during ratio load balancing.                                                  | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **selfLink**           | A reference link URI to the LTM application server node object.                                                               | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
| | *read-only*            |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **sessionConfig**      | Enables or disables the node for new sessions. The default value is user-enabled.                                             | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+
| | **stateConfig**        | Marks the node up or down. The default value is user-up.                                                                      | string                                                    |
| | *optional*             |                                                                                                                               |                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------+

.. raw:: html

   <div id="_properties_node_devicereference" class="paragraph">

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

   <div id="_properties_node_fqdn" class="paragraph">

**fqdn**

.. raw:: html

   </div>

+------------------------+-------------------------------------------------------------------------------------+-----------+
| Name                   | Description                                                                         | Schema    |
+========================+=====================================================================================+===========+
| | **addressFamily**    | Specifies the node’s address family. The default is 'unspecified', or IP-agnostic   | string    |
| | *optional*           |                                                                                     |           |
+------------------------+-------------------------------------------------------------------------------------+-----------+
| | **downInterval**     | Specifies the number of attempts to resolve a domain name. The default is 5.        | integer   |
| | *optional*           |                                                                                     |           |
+------------------------+-------------------------------------------------------------------------------------+-----------+
| | **interval**         | Specifies the amount of time before sending the next DNS query.                     | string    |
| | *optional*           |                                                                                     |           |
+------------------------+-------------------------------------------------------------------------------------+-----------+
| | **isAutoPolulate**   | Specifies whether the node should scale to the IP address set returned by DNS.      | boolean   |
| | *optional*           |                                                                                     |           |
+------------------------+-------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_application\_node\_body
   :name: _post_application_node_body

+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| Name                                 | Description                                                                             | Schema    |
+======================================+=========================================================================================+===========+
| | **partition**                      | Partition where this application node lives. default Common                             | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **noLock**                         | Application node locking.                                                               | boolean   |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **deviceReference**                | Reference link to device in resolver group.                                             | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **address**                        | IP Addres of device.                                                                    | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **appService**                     | link uri to application servce.                                                         | string    |
| | *required*                         |                                                                                         |           |
+--------------------------------------+-----------------------------------------------------------------------------------------+-----------+
| | **connectionLimit**                | Password of device.                                                                     | string    |
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

Last updated 2016-11-22 17:27:55 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
