Deploy configuration
^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <div id="header">

.. rubric:: BIG-IQ Deploy Configuration
   :name: big-iq-deploy-configuration

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

API used to deploy configuration changes made on BIG-IQ to BIG-IP
devices.

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

| *BasePath* : /mgmt/cm/firewall/tasks
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

.. rubric:: GET all deployment tasks.
   :name: _deploy-configuration_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /deploy-configuration

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

Returns the collection of firewall namespace specific deployment tasks.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses

+-------------+----------------------------------------------------------+-----------------------------------------------------------------------+
| HTTP Code   | Description                                              | Schema                                                                |
+=============+==========================================================+=======================================================================+
| **200**     | Collection of deployment tasks for firewall namespace.   | `properties\_deploy\_collection <#_properties_deploy_collection>`__   |
+-------------+----------------------------------------------------------+-----------------------------------------------------------------------+
| **400**     | Error response "Bad Request"                             | `error\_collection <#_error_collection>`__                            |
+-------------+----------------------------------------------------------+-----------------------------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: POST deployment task policy for firewall namespace.
   :name: _deploy-configuration_objectid_post

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    POST /deploy-configuration/{objectId}

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

Will POST a new deployment task within the firewall namespace.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters

+------------+------------------+---------------------+----------------+-----------+
| Type       | Name             | Description         | Schema         | Default   |
+============+==================+=====================+================+===========+
| **Path**   | | **objectId**   | Policy object id.   | string(UUID)   | None      |
|            | | *required*     |                     |                |           |
+------------+------------------+---------------------+----------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_2

+-------------+---------------------------------------------------+------------------------------------------------+
| HTTP Code   | Description                                       | Schema                                         |
+=============+===================================================+================================================+
| **200**     | POST a deploy task to BIGIQ firewall namespace.   | `properties\_deploy <#_properties_deploy>`__   |
+-------------+---------------------------------------------------+------------------------------------------------+
| **400**     | Error response "Bad Request"                      | `error\_collection <#_error_collection>`__     |
+-------------+---------------------------------------------------+------------------------------------------------+

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: Used to get a specific deployment configuration task
   identified by id.
   :name: _deploy-configuration_objectid_get

.. raw:: html

   <div class="literalblock">

.. raw:: html

   <div class="content">

::

    GET /deploy-configuration/{objectId}

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

Returns deployment configuration task within the firewall namespace
identified by id.

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Parameters
   :name: _parameters_2

+------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
| Type       | Name                              | Description                                                                                                                                                                                                                                                                                                                   | Schema                                                                                        | Default   |
+============+===================================+===============================================================================================================================================================================================================================================================================================================================+===============================================================================================+===========+
| **Path**   | | **objectId**                    | Policy object id.                                                                                                                                                                                                                                                                                                             | string(UUID)                                                                                  | None      |
|            | | *required*                      |                                                                                                                                                                                                                                                                                                                               |                                                                                               |           |
+------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
| **Body**   | | **Json string request body.**   | Input parameter list in json format. Ex. {"createChildTasks": true, "description": "Policy Deploy", "deviceReferences": [{"link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/6e932e01-7b5e-431d-b1d3-8ca5e3eb891d"}], "name": "Policy Deploy", "skipDistribution": false}   | `post\_deploy\_configuration\_firewall\_body <#_post_deploy_configuration_firewall_body>`__   | None      |
|            | | *required*                      |                                                                                                                                                                                                                                                                                                                               |                                                                                               |           |
+------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect3">

.. rubric:: Responses
   :name: _responses_3

+-------------+--------------------------------+------------------------------------------------+
| HTTP Code   | Description                    | Schema                                         |
+=============+================================+================================================+
| **200**     | Deploy object                  | `properties\_deploy <#_properties_deploy>`__   |
+-------------+--------------------------------+------------------------------------------------+
| **400**     | Error response "Bad Request"   | `error\_collection <#_error_collection>`__     |
+-------------+--------------------------------+------------------------------------------------+

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

+----------------------------+------------------------------------------------+--------------------+
| Name                       | Description                                    | Schema             |
+============================+================================================+====================+
| | **errorStack**           | Error stack trace returned by java.            | string             |
| | *optional*               |                                                |                    |
| | *read-only*              |                                                |                    |
+----------------------------+------------------------------------------------+--------------------+
| | **items**                | Collection of deployment tasks-error.          | < object > array   |
| | *optional*               |                                                |                    |
+----------------------------+------------------------------------------------+--------------------+
| | **kind**                 | Type information for deployment task object.   | string             |
| | *optional*               |                                                |                    |
| | *read-only*              |                                                |                    |
+----------------------------+------------------------------------------------+--------------------+
| | **message**              | Error message returned from server.            | string             |
| | *optional*               |                                                |                    |
| | *read-only*              |                                                |                    |
+----------------------------+------------------------------------------------+--------------------+
| | **requestBody**          | The data in the request body. GET (None)       | string             |
| | *optional*               |                                                |                    |
| | *read-only*              |                                                |                    |
+----------------------------+------------------------------------------------+--------------------+
| | **requestOperationId**   | Unique id assigned to rest operation.          | integer(int64)     |
| | *optional*               |                                                |                    |
| | *read-only*              |                                                |                    |
+----------------------------+------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_deploy
   :name: _properties_deploy

+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| Name                              | Description                                                                                                                                 | Schema                                                                                |
+===================================+=============================================================================================================================================+=======================================================================================+
| | **childDeployTasks**            | Child state of deploy task (currentStep, deviceReference, snapshotReference, status.)                                                       | < `childDeployTasks <#_properties_deploy_childdeploytasks>`__ > array                 |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **childSnapshotReference**      | Shared namespace snapshot that was created during this deploy task.                                                                         | `childSnapshotReference <#_properties_deploy_childsnapshotreference>`__               |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **currentStep**                 | Step of task during deploy process.                                                                                                         | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **deviceDetails**               | Detail of device (deviceReference, difference count, verify error count, verify critical error count, post deploy error count, hostname).   | < `deviceDetails <#_properties_deploy_devicedetails>`__ > array                       |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **differenceReference**         | Reference link to config differences.                                                                                                       | `differenceReference <#_properties_deploy_differencereference>`__                     |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **differenceTaskReference**     | Reference link to task config differences.                                                                                                  | `differenceTaskReference <#_properties_deploy_differencetaskreference>`__             |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **discoveryTaskReferences**     | Reference link to collection of discovery tasks.                                                                                            | < `discoveryTaskReferences <#_properties_deploy_discoverytaskreferences>`__ > array   |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **distributeTaskReference**     | Deploy needed, reference link to firewall distribute rest configuration.                                                                    | `distributeTaskReference <#_properties_deploy_distributetaskreference>`__             |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **distributeTaskReferences**    | Deploy needed, reference link to shared security distribute rest configuration.                                                             | `distributeTaskReferences <#_properties_deploy_distributetaskreferences>`__           |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **endDateTime**                 | End time, in date format, the deployment task completed.                                                                                    | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **generation**                  | A unique integer that allows admin track change to deploy object.                                                                           | integer(int64)                                                                        |
| | *optional*                      |                                                                                                                                             |                                                                                       |
| | *read-only*                     |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **id**                          | Unique id assigned to a deploy task object.                                                                                                 | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
| | *read-only*                     |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **identityReferences**          | Reference link table to authz users.                                                                                                        | < `identityReferences <#_properties_deploy_identityreferences>`__ > array             |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **isChildTask**                 | Defines if a task is a child object noted by childDeployTasks. (True/False)                                                                 | boolean                                                                               |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **kind**                        | Identification of resource ex. cm:firewall:tasks:deploy-configuration:deployconfigtaskstate                                                 | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
| | *read-only*                     |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **lastUpdateMicros**            | Time, in microsec, when deploy task was updated.                                                                                            | integer(int64)                                                                        |
| | *optional*                      |                                                                                                                                             |                                                                                       |
| | *read-only*                     |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **name**                        | Name of deployment task                                                                                                                     | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **ownerMachineId**              | A unique id generated by software if idenftiy device object using hardware address.                                                         | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **parentTaskReference**         | Reference link to parent deploy-configuration task.                                                                                         | `parentTaskReference <#_properties_deploy_parenttaskreference>`__                     |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **partition**                   | BIGIP partition, default Common.                                                                                                            | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **selfLink**                    | URI link used to identify the deploy task object.                                                                                           | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
| | *read-only*                     |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **skipVerifyConfig**            | Skip verification of configuration for deployment.                                                                                          | boolean                                                                               |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **snapshotReference**           | Reference to snapshot for deploy task.                                                                                                      | `snapshotReference <#_properties_deploy_snapshotreference>`__                         |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **snapshotTaskReference**       | Reference link to snapshot-config task.                                                                                                     | `snapshotTaskReference <#_properties_deploy_snapshottaskreference>`__                 |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **startDateTime**               | Start time, in date format, the depolyment task began.                                                                                      | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **status**                      | Status or actual state of task in state machine.                                                                                            | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **userReference**               | Reference link to authz user.                                                                                                               | `userReference <#_properties_deploy_userreference>`__                                 |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **username**                    | Username of user.                                                                                                                           | string                                                                                |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **verifyConfigReference**       | Reference to the verify configuration.                                                                                                      | `verifyConfigReference <#_properties_deploy_verifyconfigreference>`__                 |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
| | **verifyConfigTaskReference**   | Reference to the verification task.                                                                                                         | `verifyConfigTaskReference <#_properties_deploy_verifyconfigtaskreference>`__         |
| | *optional*                      |                                                                                                                                             |                                                                                       |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_deploy_childdeploytasks" class="paragraph">

**childDeployTasks**

.. raw:: html

   </div>

+--------------------------+---------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
| Name                     | Description                                                                                 | Schema                                                                |
+==========================+=============================================================================================+=======================================================================+
| | **deviceReference**    | Device reference link for each child task of deploy.                                        | < `deviceReference <#_properties_deploy_devicereference>`__ > array   |
| | *optional*             |                                                                                             |                                                                       |
+--------------------------+---------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
| | **skipDistribution**   | Skip distribution of configuration during deployment.(True/False) Verfication only prior.   | boolean                                                               |
| | *optional*             |                                                                                             |                                                                       |
+--------------------------+---------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+

.. raw:: html

   <div id="_properties_deploy_devicereference" class="paragraph">

**deviceReference**

.. raw:: html

   </div>

+----------------+----------------------------------------------------+----------+
| Name           | Description                                        | Schema   |
+================+====================================================+==========+
| | **link**     | Reference link to device object for deploy task.   | string   |
| | *optional*   |                                                    |          |
+----------------+----------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_deploy_childsnapshotreference"
   class="paragraph">

**childSnapshotReference**

.. raw:: html

   </div>

+-------------------------+--------------------------------------------------------------------------+-----------+
| Name                    | Description                                                              | Schema    |
+=========================+==========================================================================+===========+
| | **isSubcollection**   | Is subcollection of snapshots created by the deploy task. (True/False)   | boolean   |
| | *optional*            |                                                                          |           |
+-------------------------+--------------------------------------------------------------------------+-----------+
| | **link**              | Reference link to snapshot for deploy task.                              | string    |
| | *optional*            |                                                                          |           |
+-------------------------+--------------------------------------------------------------------------+-----------+

.. raw:: html

   <div id="_properties_deploy_devicedetails" class="paragraph">

**deviceDetails**

.. raw:: html

   </div>

+----------------------------------------+---------------------------------------------------------------+-------------------------------------------------------------+
| Name                                   | Description                                                   | Schema                                                      |
+========================================+===============================================================+=============================================================+
| | **deviceReference**                  | Reference link to device object for deploy task.              | `deviceReference <#_properties_deploy_devicereference>`__   |
| | *optional*                           |                                                               |                                                             |
+----------------------------------------+---------------------------------------------------------------+-------------------------------------------------------------+
| | **differenceCount**                  | A count of the number of difference during evaluation.        | integer                                                     |
| | *optional*                           |                                                               |                                                             |
+----------------------------------------+---------------------------------------------------------------+-------------------------------------------------------------+
| | **hostname**                         | Hostname of device deploying configuration to.                | string                                                      |
| | *optional*                           |                                                               |                                                             |
+----------------------------------------+---------------------------------------------------------------+-------------------------------------------------------------+
| | **postDeploymentErrorCount**         | A count of the errors encountered post deploy.                | integer                                                     |
| | *optional*                           |                                                               |                                                             |
+----------------------------------------+---------------------------------------------------------------+-------------------------------------------------------------+
| | **verificationCriticalErrorCount**   | A count of critical errors encountered during verification.   | integer                                                     |
| | *optional*                           |                                                               |                                                             |
+----------------------------------------+---------------------------------------------------------------+-------------------------------------------------------------+
| | **verificationErrorCount**           | A count of errors encountered during verification.            | integer                                                     |
| | *optional*                           |                                                               |                                                             |
+----------------------------------------+---------------------------------------------------------------+-------------------------------------------------------------+

.. raw:: html

   <div id="_properties_deploy_devicereference" class="paragraph">

**deviceReference**

.. raw:: html

   </div>

+----------------+----------------------------------------------------+----------+
| Name           | Description                                        | Schema   |
+================+====================================================+==========+
| | **link**     | Reference link to device object for deploy task.   | string   |
| | *optional*   |                                                    |          |
+----------------+----------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_deploy_differencereference" class="paragraph">

**differenceReference**

.. raw:: html

   </div>

+-------------------------+------------------------------------------------+-----------+
| Name                    | Description                                    | Schema    |
+=========================+================================================+===========+
| | **isSubcollection**   | Is subcollection of differences (True/False)   | boolean   |
| | *optional*            |                                                |           |
+-------------------------+------------------------------------------------+-----------+
| | **link**              | Reference link to difference array object.     | string    |
| | *optional*            |                                                |           |
+-------------------------+------------------------------------------------+-----------+

.. raw:: html

   <div id="_properties_deploy_differencetaskreference"
   class="paragraph">

**differenceTaskReference**

.. raw:: html

   </div>

+----------------+---------------------------------------+----------+
| Name           | Description                           | Schema   |
+================+=======================================+==========+
| | **link**     | Reference link to differencer task.   | string   |
| | *optional*   |                                       |          |
+----------------+---------------------------------------+----------+

.. raw:: html

   <div id="_properties_deploy_differencetaskreferences"
   class="paragraph">

**differenceTaskReferences**

.. raw:: html

   </div>

+-------------------------+-----------------------------------------+-----------+
| Name                    | Description                             | Schema    |
+=========================+=========================================+===========+
| | **isSubcollection**   | Is subcollection of diffencer tasks.    | boolean   |
| | *optional*            |                                         |           |
+-------------------------+-----------------------------------------+-----------+
| | **link**              | Reference links to differencer tasks.   | string    |
| | *optional*            |                                         |           |
+-------------------------+-----------------------------------------+-----------+

.. raw:: html

   <div id="_properties_deploy_discoverytaskreferences"
   class="paragraph">

**discoveryTaskReferences**

.. raw:: html

   </div>

+-------------------------+----------------------------------------+-----------+
| Name                    | Description                            | Schema    |
+=========================+========================================+===========+
| | **isSubcollection**   | Is subcollection of discovery tasks.   | boolean   |
| | *optional*            |                                        |           |
+-------------------------+----------------------------------------+-----------+
| | **link**              | Reference links to discovery tasks.    | string    |
| | *optional*            |                                        |           |
+-------------------------+----------------------------------------+-----------+

.. raw:: html

   <div id="_properties_deploy_distributetaskreference"
   class="paragraph">

**distributeTaskReference**

.. raw:: html

   </div>

+----------------+---------------------------------------+----------+
| Name           | Description                           | Schema   |
+================+=======================================+==========+
| | **link**     | Reference links to distribute task.   | string   |
| | *optional*   |                                       |          |
+----------------+---------------------------------------+----------+

.. raw:: html

   <div id="_properties_deploy_distributetaskreferences"
   class="paragraph">

**distributeTaskReferences**

.. raw:: html

   </div>

+-------------------------+-----------------------------------------+-----------+
| Name                    | Description                             | Schema    |
+=========================+=========================================+===========+
| | **isSubcollection**   | Is subcollection of distribute tasks.   | boolean   |
| | *optional*            |                                         |           |
+-------------------------+-----------------------------------------+-----------+
| | **link**              | Reference links to distribute tasks.    | string    |
| | *optional*            |                                         |           |
+-------------------------+-----------------------------------------+-----------+

.. raw:: html

   <div id="_properties_deploy_identityreferences" class="paragraph">

**identityReferences**

.. raw:: html

   </div>

+-------------------------+--------------------------------------------------+-----------+
| Name                    | Description                                      | Schema    |
+=========================+==================================================+===========+
| | **isSubcollection**   | Is subcollection of identity reference object.   | boolean   |
| | *optional*            |                                                  |           |
+-------------------------+--------------------------------------------------+-----------+
| | **link**              | Reference links to identity reference object.    | string    |
| | *optional*            |                                                  |           |
+-------------------------+--------------------------------------------------+-----------+

.. raw:: html

   <div id="_properties_deploy_parenttaskreference" class="paragraph">

**parentTaskReference**

.. raw:: html

   </div>

+----------------+-------------------------------------------------+----------+
| Name           | Description                                     | Schema   |
+================+=================================================+==========+
| | **link**     | Reference links to deploy-configuration task.   | string   |
| | *optional*   |                                                 |          |
+----------------+-------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_deploy_snapshotreference" class="paragraph">

**snapshotReference**

.. raw:: html

   </div>

+----------------+---------------------------------------+----------+
| Name           | Description                           | Schema   |
+================+=======================================+==========+
| | **link**     | Reference links to snapshot object.   | string   |
| | *optional*   |                                       |          |
+----------------+---------------------------------------+----------+

.. raw:: html

   <div id="_properties_deploy_snapshottaskreference" class="paragraph">

**snapshotTaskReference**

.. raw:: html

   </div>

+-------------------------+---------------------------------------+-----------+
| Name                    | Description                           | Schema    |
+=========================+=======================================+===========+
| | **isSubcollection**   | Is subcollection of snapshot tasks.   | boolean   |
| | *optional*            |                                       |           |
+-------------------------+---------------------------------------+-----------+
| | **link**              | Reference links to snapshot task.     | string    |
| | *optional*            |                                       |           |
+-------------------------+---------------------------------------+-----------+

.. raw:: html

   <div id="_properties_deploy_userreference" class="paragraph">

**userReference**

.. raw:: html

   </div>

+----------------+---------------------------------------------+----------+
| Name           | Description                                 | Schema   |
+================+=============================================+==========+
| | **link**     | Reference links to user reference object.   | string   |
| | *optional*   |                                             |          |
+----------------+---------------------------------------------+----------+

.. raw:: html

   <div id="_properties_deploy_verifyconfigreference" class="paragraph">

**verifyConfigReference**

.. raw:: html

   </div>

+----------------+-----------------------------------------------------+----------+
| Name           | Description                                         | Schema   |
+================+=====================================================+==========+
| | **link**     | Reference links to verification reference object.   | string   |
| | *optional*   |                                                     |          |
+----------------+-----------------------------------------------------+----------+

.. raw:: html

   <div id="_properties_deploy_verifyconfigtaskreference"
   class="paragraph">

**verifyConfigTaskReference**

.. raw:: html

   </div>

+----------------+--------------------------------------------------+----------+
| Name           | Description                                      | Schema   |
+================+==================================================+==========+
| | **link**     | Reference links to verifcation reference task.   | string   |
| | *optional*   |                                                  |          |
+----------------+--------------------------------------------------+----------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: properties\_deploy\_collection
   :name: _properties_deploy_collection

+--------------------------+---------------------------------------------------------------------------------------+--------------------+
| Name                     | Description                                                                           | Schema             |
+==========================+=======================================================================================+====================+
| | **generation**         | A unique integer that tracks changes to deploy collection object.                     | integer(int64)     |
| | *optional*             |                                                                                       |                    |
| | *read-only*            |                                                                                       |                    |
+--------------------------+---------------------------------------------------------------------------------------+--------------------+
| | **items**              | Collection of deploy tasks-properties.                                                | < object > array   |
| | *optional*             |                                                                                       |                    |
+--------------------------+---------------------------------------------------------------------------------------+--------------------+
| | **kind**               | Type information for this deploy collection object.                                   | string             |
| | *optional*             |                                                                                       |                    |
| | *read-only*            |                                                                                       |                    |
+--------------------------+---------------------------------------------------------------------------------------+--------------------+
| | **lastUpdateMicros**   | Update time (micros) for last change made to an deploy task collection object-time.   | integer(int64)     |
| | *optional*             |                                                                                       |                    |
| | *read-only*            |                                                                                       |                    |
+--------------------------+---------------------------------------------------------------------------------------+--------------------+
| | **selfLink**           | A reference link URI to the deploy task collection object.                            | string             |
| | *optional*             |                                                                                       |                    |
| | *read-only*            |                                                                                       |                    |
+--------------------------+---------------------------------------------------------------------------------------+--------------------+

.. raw:: html

   </div>

.. raw:: html

   <div class="sect2">

.. rubric:: post\_device\_trust\_body
   :name: _post_deploy_configuration_firewall_body

+-----------------------------------+-------------------------------------------------------------------------------------+-----------+
| Name                              | Description                                                                         | Schema    |
+===================================+=====================================================================================+===========+
| | **createChildTasks**            | This deployment with create child tasks as part of process.                         | boolean   |
| | *optional*                      |                                                                                     |           |
+-----------------------------------+-------------------------------------------------------------------------------------+-----------+
| | **skipVerifyConfig**            | Boolean to allow user to disable verifiation of configuration.                      | boolean   |
| | *optional*                      |                                                                                     |           |
+-----------------------------------+-------------------------------------------------------------------------------------+-----------+
| | **skipDistribution**            | Boolean to allow user to disable distribution of configuration to a BIGIP device.   | boolean   |
| | *optional*                      |                                                                                     |           |
+-----------------------------------+-------------------------------------------------------------------------------------+-----------+
| | **snapshotReference**           | Reference to device snapshot. default: null                                         | string    |
| | *optional*                      |                                                                                     |           |
+-----------------------------------+-------------------------------------------------------------------------------------+-----------+
| | **objectsToDeployReferences**   | Reference to adc objects to be distributed.                                         | string    |
| | *optional*                      |                                                                                     |           |
+-----------------------------------+-------------------------------------------------------------------------------------+-----------+
| | **name**                        | Name of ADC deployment task.                                                        | string    |
| | *required*                      |                                                                                     |           |
+-----------------------------------+-------------------------------------------------------------------------------------+-----------+
| | **deviceReference**             | Reference link to device object.                                                    | string    |
| | *required*                      |                                                                                     |           |
+-----------------------------------+-------------------------------------------------------------------------------------+-----------+
| | **description**                 | Description of deployment task.                                                     | string    |
| | *optional*                      |                                                                                     |           |
+-----------------------------------+-------------------------------------------------------------------------------------+-----------+

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
