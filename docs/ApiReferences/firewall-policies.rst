Firewall policy
^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ Firewall Policy API
   :name: big-iq-firewall-policy-api

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

API used to create and modify firewall policies on BIG-IQ

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

.. rubric:: List of policy collections.
   :name: _policies_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /policies

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

Returns the collection of firewall policies.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+------------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                        | Schema                                                 |
+=============+====================================+========================================================+
| **200**     | Collection of firewall policies.   | `properties\_collection <#_properties_collection>`__   |
+-------------+------------------------------------+--------------------------------------------------------+
| **400**     | Error response "Bad Request"       | `error\_collection <#_error_collection>`__             |
+-------------+------------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a single firewall policy.
   :name: _policies_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /policies/{objectId}

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

Returns the firewall policy identified by id for an endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+------------------+--------------------+----------------+-----------+
| Type       | Name             | Description        | Schema         | Default   |
+============+==================+====================+================+===========+
| **Path**   | | **objectId**   | Policy object ID   | string(UUID)   | None      |
|            | | *required*     |                    |                |           |
+------------+------------------+--------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+----------------------------------------+------------------------------------------------+
| HTTP Code   | Description                            | Schema                                         |
+=============+========================================+================================================+
| **200**     | Firewall policy object.                | `properties\_policy <#_properties_policy>`__   |
+-------------+----------------------------------------+------------------------------------------------+
| **400**     | Server error response "Bad Request".   | `error\_collection <#_error_collection>`__     |
+-------------+----------------------------------------+------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get the rules for a firewall policy.
   :name: _policies_objectid_rules_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /policies/{objectId}/rules

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

Returns the firewall rules subcollection for a policy.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+------------------+---------------------------------------+----------------+-----------+
| Type       | Name             | Description                           | Schema         | Default   |
+============+==================+=======================================+================+===========+
| **Path**   | | **objectId**   | Collection of policy rule object id   | string(UUID)   | None      |
|            | | *required*     |                                       |                |           |
+------------+------------------+---------------------------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+---------------------------------+--------------------------------------------------------+
| HTTP Code   | Description                     | Schema                                                 |
+=============+=================================+========================================================+
| **200**     | Collection of firewall rules.   | `properties\_collection <#_properties_collection>`__   |
+-------------+---------------------------------+--------------------------------------------------------+
| **400**     | Error response "Bad Request"    | `properties\_collection <#_properties_collection>`__   |
+-------------+---------------------------------+--------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Get a single rule for a firewall policy.
   :name: _policies_objectid_rules_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /policies/{objectId}/rules/{objectId}

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

Returns the firewall rule identified by a endpoint URI.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_3

+------------+------------------+--------------------+----------------+-----------+
| Type       | Name             | Description        | Schema         | Default   |
+============+==================+====================+================+===========+
| **Path**   | | **objectId**   | Policy object id   | string(UUID)   | None      |
|            | | *required*     |                    |                |           |
+------------+------------------+--------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_4

+-------------+--------------------------------+----------------------------------------------+
| HTTP Code   | Description                    | Schema                                       |
+=============+================================+==============================================+
| **200**     | Firewall rule object           | `properties\_rule <#_properties_rule>`__     |
+-------------+--------------------------------+----------------------------------------------+
| **400**     | Error response "Bad Request"   | `error\_collection <#_error_collection>`__   |
+-------------+--------------------------------+----------------------------------------------+

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
| | **items**                | Collection of policies-error.              | < object > array   |
| | *optional*               |                                            |                    |
+----------------------------+--------------------------------------------+--------------------+
| | **kind**                 | Type information for policy object.        | string             |
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

.. rubric:: properties\_collection
   :name: _properties_collection

+--------------------------+-------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                             | Schema             |
+==========================+=========================================================================+====================+
| | **generation**         | A integer that will track change made to a policy object. generation.   | integer(int64)     |
| | *optional*             |                                                                         |                    |
| | *read-only*            |                                                                         |                    |
+--------------------------+-------------------------------------------------------------------------+--------------------+
| | **items**              | Collection of policies-properties.                                      | < object > array   |
| | *optional*             |                                                                         |                    |
+--------------------------+-------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this policy object.                                | string             |
| | *optional*             |                                                                         |                    |
| | *read-only*            |                                                                         |                    |
+--------------------------+-------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an policy object. time.    | integer(int64)     |
| | *optional*             |                                                                         |                    |
| | *read-only*            |                                                                         |                    |
+--------------------------+-------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the policy object.                              | string             |
| | *optional*             |                                                                         |                    |
| | *read-only*            |                                                                         |                    |
+--------------------------+-------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_policy
   :name: _properties_policy

+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| Name                             | Description                                                             | Schema                                                                        |
+==================================+=========================================================================+===============================================================================+
| | **description**                | Description of object.                                                  | string                                                                        |
| | *optional*                     |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| | **generation**                 | A integer that will track change made to a policy object. generation.   | integer(int64)                                                                |
| | *optional*                     |                                                                         |                                                                               |
| | *read-only*                    |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| | **id**                         | Unique id assigned to a policy object.                                  | string                                                                        |
| | *optional*                     |                                                                         |                                                                               |
| | *read-only*                    |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| | **kind**                       | Type information for this policy object.                                | string                                                                        |
| | *optional*                     |                                                                         |                                                                               |
| | *read-only*                    |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| | **lastUpdateMicros**           | Update time (micros) for last change made to an policy object. time.    | integer(int64)                                                                |
| | *optional*                     |                                                                         |                                                                               |
| | *read-only*                    |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| | **name**                       | Name of object.                                                         | string                                                                        |
| | *optional*                     |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| | **partition**                  | BIGIP partition this object exists.                                     | string                                                                        |
| | *optional*                     |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| | **rulesCollectionReference**   | Reference link to firewall rules assigned to this policy object.        | `rulesCollectionReference <#_properties_policy_rulescollectionreference>`__   |
| | *optional*                     |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+
| | **selfLink**                   | A reference link URI to the policy object.                              | string                                                                        |
| | *optional*                     |                                                                         |                                                                               |
| | *read-only*                    |                                                                         |                                                                               |
+----------------------------------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_policy_rulescollectionreference"
   class="paragraph">

**rulesCollectionReference**

.. raw:: html

   </div>

+-------------------------+----------------------------------------------+-----------+
| Name                    | Description                                  | Schema    |
+=========================+==============================================+===========+
| | **isSubcollection**   | Is a subcollection (True/False)              | boolean   |
| | *optional*            |                                              |           |
+-------------------------+----------------------------------------------+-----------+
| | **link**              | Reference link to rules collection object.   | string    |
| | *optional*            |                                              |           |
+-------------------------+----------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_rule
   :name: _properties_rule

+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| Name                           | Description                                                                                                                  | Schema           |
+================================+==============================================================================================================================+==================+
| | **action**                   | Action taken for rule match (accept, accept-decisively, drop, reject).                                                       | string           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **destination**              | Destination object used by rule, usually specified by (address-list, address, address-range, domain-name, country/region).   | object           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **evalOrder**                | Order in which server evaluates rules referenced in a policy object.                                                         | integer          |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **generation**               | A integer that will track change made to a policy rule object. generation.                                                   | integer(int64)   |
| | *optional*                   |                                                                                                                              |                  |
| | *read-only*                  |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **hitCountStatReference**    | Reference link to a object that maintains an interger for rule hit counts.                                                   | object           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **iRule**                    | Link to F5 iRule to a firewall policy.                                                                                       | string           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **iRuleSampleRate**          | Sample rate of iRule.                                                                                                        | integer          |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **id**                       | Unique id assigned to a policy rule object.                                                                                  | string           |
| | *optional*                   |                                                                                                                              |                  |
| | *read-only*                  |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **kind**                     | Type information for this policy rule object.                                                                                | string           |
| | *optional*                   |                                                                                                                              |                  |
| | *read-only*                  |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **lastUpdateMicros**         | pdate time (micros) for last change made to an policy rule object. time.                                                     | integer(int64)   |
| | *optional*                   |                                                                                                                              |                  |
| | *read-only*                  |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **log**                      | Boolean used to enable / disable server logging for actions taken on packets.                                                | boolean          |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **name**                     | Name of the policy rule object.                                                                                              | string           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **protocol**                 | IP protocol to match against packet.                                                                                         | string           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **ruleListReference**        | Reference link to a rule-list object (list of rules managed in a single object.)                                             | object           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **scheduleReference**        | Reference link to a schedule object used by this policy object.                                                              | object           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **selfLink**                 | A reference link URI to the policy rule object.                                                                              | string           |
| | *optional*                   |                                                                                                                              |                  |
| | *read-only*                  |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **servicePolicyReference**   | Reference link to a service-policy object (used as a container for network idle timers and/or port misuse policies).         | object           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **source**                   | Source object used by rule, usually specified by (address-list, address, address-range, domain-name, country/region).        | object           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+
| | **state**                    | State of rule. (disabled, enabled, scheduled)                                                                                | string           |
| | *optional*                   |                                                                                                                              |                  |
+--------------------------------+------------------------------------------------------------------------------------------------------------------------------+------------------+

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
