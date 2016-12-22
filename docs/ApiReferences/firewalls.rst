.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ Firewall Contexts API
   :name: big-iq-firewall-contexts-api

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

API used to create and modify firewall contexts on BIG-IQ

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

| *BasePath* : /mgmt/cm/firewalls/working-config
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

.. rubric:: List of firewall collections.
   :name: _firewalls_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /firewalls

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

Returns the collection of firewalls.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+--------------------------------+---------------------------------------------------------------------------+
| HTTP Code   | Description                    | Schema                                                                    |
+=============+================================+===========================================================================+
| **200**     | Collection of firewalls.       | `properties\_firewall\_collection <#_properties_firewall_collection>`__   |
+-------------+--------------------------------+---------------------------------------------------------------------------+
| **400**     | Error response "Bad Request"   | `error\_collection <#_error_collection>`__                                |
+-------------+--------------------------------+---------------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single firewall context.
   :name: _firewalls_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /firewalls/{objectId}

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

Returns the firewall context identified by a endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+------------------+----------------------+----------------+-----------+
| Type       | Name             | Description          | Schema         | Default   |
+============+==================+======================+================+===========+
| **Path**   | | **objectId**   | Firewall object id   | string(UUID)   | None      |
|            | | *required*     |                      |                |           |
+------------+------------------+----------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+--------------------------------+----------------------------------------------------+
| HTTP Code   | Description                    | Schema                                             |
+=============+================================+====================================================+
| **200**     | Firewall context object        | `properties\_firewall <#_properties_firewall>`__   |
+-------------+--------------------------------+----------------------------------------------------+
| **400**     | Error response "Bad Request"   | `error\_collection <#_error_collection>`__         |
+-------------+--------------------------------+----------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: PATCH firewall context into firewall context.
   :name: _firewalls_objectid_patch

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    PATCH /firewalls/{objectId}

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

Will patch enforced policy reference link into firewall context.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+------------------+----------------------+----------------+-----------+
| Type       | Name             | Description          | Schema         | Default   |
+============+==================+======================+================+===========+
| **Path**   | | **objectId**   | Firewall object id   | string(UUID)   | None      |
|            | | *required*     |                      |                |           |
+------------+------------------+----------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+-------------------------------------------------+----------------------------------------------------+
| HTTP Code   | Description                                     | Schema                                             |
+=============+=================================================+====================================================+
| **200**     | Patch firewall policies to firewalls success.   | `properties\_firewall <#_properties_firewall>`__   |
+-------------+-------------------------------------------------+----------------------------------------------------+
| **400**     | Error response "Bad Request"                    | `error\_collection <#_error_collection>`__         |
+-------------+-------------------------------------------------+----------------------------------------------------+

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

+----------------------------+--------------------------------------------+--------------------+
| Name                       | Description                                | Schema             |
+============================+============================================+====================+
| | **errorStack**           | Error stack trace returned by java.        | string             |
| | *optional*               |                                            |                    |
| | *read-only*              |                                            |                    |
+----------------------------+--------------------------------------------+--------------------+
| | **items**                | Collection of firewalls-error.             | < object > array   |
| | *optional*               |                                            |                    |
+----------------------------+--------------------------------------------+--------------------+
| | **kind**                 | Type information for firewalls object.     | string             |
| | *optional*               |                                            |                    |
| | *read-only*              |                                            |                    |
+----------------------------+--------------------------------------------+--------------------+
| | **message**              | Error message returned from server.        | string             |
| | *optional*               |                                            |                    |
| | *read-only*              |                                            |                    |
+----------------------------+--------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)   | string             |
| | *optional*               |                                            |                    |
| | *read-only*              |                                            |                    |
+----------------------------+--------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.      | integer(int64)     |
| | *optional*               |                                            |                    |
| | *read-only*              |                                            |                    |
+----------------------------+--------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_firewall
   :name: _properties_firewall

+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| Name                             | Description                                                               | Schema                                                                          |
+==================================+===========================================================================+=================================================================================+
| | **firewallIpAddress**          | Firewall IP Address                                                       | string                                                                          |
| | *optional*                     |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **firewallType**               | Firewall Type (VIP, SIP, RD, Mgmt etc..)                                  | string                                                                          |
| | *optional*                     |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **generation**                 | A integer that will track change made to a firewall object. generation.   | integer(int64)                                                                  |
| | *optional*                     |                                                                           |                                                                                 |
| | *read-only*                    |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **id**                         | Unique id assigned to a firewall object.                                  | string                                                                          |
| | *optional*                     |                                                                           |                                                                                 |
| | *read-only*                    |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **kind**                       | Type information for this firewall object.                                | string                                                                          |
| | *optional*                     |                                                                           |                                                                                 |
| | *read-only*                    |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **lastUpdateMicros**           | Update time (micros) for last change made to an firewall object. time.    | integer(int64)                                                                  |
| | *optional*                     |                                                                           |                                                                                 |
| | *read-only*                    |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **name**                       | Name of object.                                                           | string                                                                          |
| | *optional*                     |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **partition**                  | BIGIP partition this object exists.                                       | string                                                                          |
| | *optional*                     |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **rulesCollectionReference**   | Reference link to firewall rules assigned to this firewall object.        | `rulesCollectionReference <#_properties_firewall_rulescollectionreference>`__   |
| | *optional*                     |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+
| | **selfLink**                   | A reference link URI to the firewall object.                              | string                                                                          |
| | *optional*                     |                                                                           |                                                                                 |
| | *read-only*                    |                                                                           |                                                                                 |
+----------------------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_firewall_rulescollectionreference"
   class="paragraph">

**rulesCollectionReference**

.. raw:: html

   </div>

+-------------------------+-------------------------------------------------------------------------------------------+-----------+
| Name                    | Description                                                                               | Schema    |
+=========================+===========================================================================================+===========+
| | **isSubcollection**   | Is a subcollection (True/False)                                                           | boolean   |
| | *optional*            |                                                                                           |           |
+-------------------------+-------------------------------------------------------------------------------------------+-----------+
| | **link**              | Reference link to rules collection object. (In-line rules for firewalls not supported.)   | string    |
| | *optional*            |                                                                                           |           |
+-------------------------+-------------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_firewall\_collection
   :name: _properties_firewall_collection

+--------------------------+-------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                         | Schema             |
+==========================+=====================================================================================+====================+
| | **generation**         | A integer that will track change made to a firewall collection object-generation.   | integer(int64)     |
| | *optional*             |                                                                                     |                    |
| | *read-only*            |                                                                                     |                    |
+--------------------------+-------------------------------------------------------------------------------------+--------------------+
| | **items**              | Collection of firewall-properties.                                                  | < object > array   |
| | *optional*             |                                                                                     |                    |
+--------------------------+-------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this firewall collection object.                               | string             |
| | *optional*             |                                                                                     |                    |
| | *read-only*            |                                                                                     |                    |
+--------------------------+-------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an firewall collection object-time.    | integer(int64)     |
| | *optional*             |                                                                                     |                    |
| | *read-only*            |                                                                                     |                    |
+--------------------------+-------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the firewall collection object.                             | string             |
| | *optional*             |                                                                                     |                    |
| | *read-only*            |                                                                                     |                    |
+--------------------------+-------------------------------------------------------------------------------------+--------------------+

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

Last updated 2016-11-18 10:40:00 EST

.. raw:: html

   </div>

.. raw:: html

   </div>
