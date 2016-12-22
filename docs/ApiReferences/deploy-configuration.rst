= BIG-IQ Deploy Configuration

[[\_overview]] == Overview API used to deploy configuration changes made
on BIG-IQ or BIG-IP devices.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/firewall/tasks
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_deploy-configuration\_get]] === GET all deployment tasks. .... GET
/deploy-configuration ....

==== Description Returns the collection of firewall namespace specific
deployment tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of deployment tasks
for firewall
namespace.\|<<\_properties\_deploy\_collection,properties\_deploy\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_deploy-configuration\_objectid\_post]] === POST deployment task
policy for firewall namespace. .... POST
/deploy-configuration/{objectId} ....

==== Description Will POST a new deployment task within the firewall
namespace.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Policy object id.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a deploy task to BIGIQ
firewall namespace.\|<<\_properties\_deploy,properties\_deploy>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_deploy-configuration\_objectid\_get]] === Used to get a specific
deployment configuration task identified by id. .... GET
/deploy-configuration/{objectId} ....

==== Description Returns deployment configuration task within the
firewall namespace identified by id.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Policy object id.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Deploy
object\|<<\_properties\_deploy,properties\_deploy>> \|\ *400*\ \|Error
response "Bad Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_error\_collection]] === error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of deployment tasks-error.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for deployment
task object.\|string \|\ *message* + *optional* + *read-only*\ \|Error
message returned from server.\|string \|\ *requestBody* + *optional* +
*read-only*\ \|The data in the request body. GET (None)\|string
\|\ *requestOperationId* + *optional* + *read-only*\ \|Unique id
assigned to rest operation.\|integer(int64) \|===

[[\_properties\_deploy]] === properties\_deploy

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *childDeployTasks* + *optional*\ \|Child
state of deploy task (currentStep, deviceReference, snapshotReference,
status.)\|< <<\_properties\_deploy\_childdeploytasks,childDeployTasks>>
> array \|\ *childSnapshotReference* + *optional*\ \|Shared namespace
snapshot that was created during this deploy
task.\|<<\_properties\_deploy\_childsnapshotreference,childSnapshotReference>>
\|\ *currentStep* + *optional*\ \|Step of task during deploy
process.\|string \|\ *deviceDetails* + *optional*\ \|Detail of device
(deviceReference, difference count, verify error count, verify critical
error count, post deploy error count, hostname).\|<
<<\_properties\_deploy\_devicedetails,deviceDetails>> > array
\|\ *differenceReference* + *optional*\ \|Reference link to config
differences.\|<<\_properties\_deploy\_differencereference,differenceReference>>
\|\ *differenceTaskReference* + *optional*\ \|Reference link to task
config
differences.\|<<\_properties\_deploy\_differencetaskreference,differenceTaskReference>>
\|\ *discoveryTaskReferences* + *optional*\ \|Reference link to
collection of discovery tasks.\|<
<<\_properties\_deploy\_discoverytaskreferences,discoveryTaskReferences>>
> array \|\ *distributeTaskReference* + *optional*\ \|Deploy needed,
reference link to firewall distribute rest
configuration.\|<<\_properties\_deploy\_distributetaskreference,distributeTaskReference>>
\|\ *distributeTaskReferences* + *optional*\ \|Deploy needed, reference
link to shared security distribute rest
configuration.\|<<\_properties\_deploy\_distributetaskreferences,distributeTaskReferences>>
\|\ *endDateTime* + *optional*\ \|End time, in date format, the
deployment task completed.\|string \|\ *firewallIpAddress* +
*optional*\ \|Firewall IP Address\|string \|\ *firewallType* +
*optional*\ \|Firewall Type (VIP, SIP, RD, Mgmt etc..)\|string
\|\ *generation* + *optional* + *read-only*\ \|A unique integer that
allows admin track change to deploy object.\|integer(int64) \|\ *id* +
*optional* + *read-only*\ \|Unique id assigned to a deploy task
object.\|string \|\ *identityReferences* + *optional*\ \|Reference link
table to authz users.\|<
<<\_properties\_deploy\_identityreferences,identityReferences>> > array
\|\ *isChildTask* + *optional*\ \|Defines if a task is a child object
noted by childDeployTasks. (True/False)\|boolean \|\ *kind* + *optional*
+ *read-only*\ \|Identification of resource ex.
cm:firewall:tasks:deploy-configuration:deployconfigtaskstate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Time, in microsec,
when deploy task was updated.\|integer(int64) \|\ *name* +
*optional*\ \|Name of deployment task\|string \|\ *ownerMachineId* +
*optional*\ \|A unique id generated by software if idenftiy device
object using hardware address.\|string \|\ *parentTaskReference* +
*optional*\ \|Reference link to parent deploy-configuration
task.\|<<\_properties\_deploy\_parenttaskreference,parentTaskReference>>
\|\ *partition* + *optional*\ \|BIGIP partition, default Common.\|string
\|\ *selfLink* + *optional* + *read-only*\ \|URI link used to identify
the deploy task object.\|string \|\ *skipVerifyConfig* +
*optional*\ \|Skip verification of configuration for
deployment.\|boolean \|\ *snapshotReference* + *optional*\ \|Reference
to snapshot for deploy
task.\|<<\_properties\_deploy\_snapshotreference,snapshotReference>>
\|\ *snapshotTaskReference* + *optional*\ \|Reference link to
snapshot-config
task.\|<<\_properties\_deploy\_snapshottaskreference,snapshotTaskReference>>
\|\ *startDateTime* + *optional*\ \|Start time, in date format, the
depolyment task began.\|string \|\ *status* + *optional*\ \|Status or
actual state of task in state machine.\|string \|\ *userReference* +
*optional*\ \|Reference link to authz
user.\|<<\_properties\_deploy\_userreference,userReference>>
\|\ *username* + *optional*\ \|Username of user.\|string
\|\ *verifyConfigReference* + *optional*\ \|Reference to the verify
configuration.\|<<\_properties\_deploy\_verifyconfigreference,verifyConfigReference>>
\|\ *verifyConfigTaskReference* + *optional*\ \|Reference to the
verification
task.\|<<\_properties\_deploy\_verifyconfigtaskreference,verifyConfigTaskReference>>
\|===

[[\_properties\_deploy\_childdeploytasks]] *childDeployTasks*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *deviceReference* + *optional*\ \|Device
reference link for each child task of deploy.\|<
<<\_properties\_deploy\_devicereference,deviceReference>> > array
\|\ *skipDistribution* + *optional*\ \|Skip distribution of
configuration during deployment.(True/False) Verfication only
prior.\|boolean \|===

[[\_properties\_deploy\_devicereference]] *deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
device object for deploy task.\|string \|===

[[\_properties\_deploy\_childsnapshotreference]]
*childSnapshotReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is
subcollection of snapshots created by the deploy task.
(True/False)\|boolean \|\ *link* + *optional*\ \|Reference link to
snapshot for deploy task.\|string \|===

[[\_properties\_deploy\_devicedetails]] *deviceDetails*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *deviceReference* +
*optional*\ \|Reference link to device object for deploy
task.\|<<\_properties\_deploy\_devicereference,deviceReference>>
\|\ *differenceCount* + *optional*\ \|A count of the number of
difference during evaluation.\|integer \|\ *hostname* +
*optional*\ \|Hostname of device deploying configuration to. \|string
\|\ *postDeploymentErrorCount* + *optional*\ \|A count of the errors
encountered post deploy.\|integer \|\ *verificationCriticalErrorCount* +
*optional*\ \|A count of critical errors encountered during
verification.\|integer \|\ *verificationErrorCount* + *optional*\ \|A
count of errors encountered during verification.\|integer \|===

[[\_properties\_deploy\_devicereference]] *deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
device object for deploy task.\|string \|===

[[\_properties\_deploy\_differencereference]] *differenceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is
subcollection of differences (True/False)\|boolean \|\ *link* +
*optional*\ \|Reference link to difference array object.\|string \|===

[[\_properties\_deploy\_differencetaskreference]]
*differenceTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
differencer task.\|string \|===

[[\_properties\_deploy\_differencetaskreferences]]
*differenceTaskReferences*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is
subcollection of diffencer tasks.\|boolean \|\ *link* +
*optional*\ \|Reference links to differencer tasks.\|string \|===

[[\_properties\_deploy\_discoverytaskreferences]]
*discoveryTaskReferences*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is
subcollection of discovery tasks.\|boolean \|\ *link* +
*optional*\ \|Reference links to discovery tasks.\|string \|===

[[\_properties\_deploy\_distributetaskreference]]
*distributeTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference links
to distribute task.\|string \|===

[[\_properties\_deploy\_distributetaskreferences]]
*distributeTaskReferences*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is
subcollection of distribute tasks.\|boolean \|\ *link* +
*optional*\ \|Reference links to distribute tasks.\|string \|===

[[\_properties\_deploy\_identityreferences]] *identityReferences*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is
subcollection of identity reference object.\|boolean \|\ *link* +
*optional*\ \|Reference links to identity reference object.\|string
\|===

[[\_properties\_deploy\_parenttaskreference]] *parentTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference links
to deploy-configuration task.\|string \|===

[[\_properties\_deploy\_snapshotreference]] *snapshotReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference links
to snapshot object.\|string \|===

[[\_properties\_deploy\_snapshottaskreference]] *snapshotTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is
subcollection of snapshot tasks.\|boolean \|\ *link* +
*optional*\ \|Reference links to snapshot task.\|string \|===

[[\_properties\_deploy\_userreference]] *userReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference links
to user reference object.\|string \|===

[[\_properties\_deploy\_verifyconfigreference]] *verifyConfigReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference links
to verification reference object.\|string \|===

[[\_properties\_deploy\_verifyconfigtaskreference]]
*verifyConfigTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference links
to verifcation reference task.\|string \|===

[[\_properties\_deploy\_collection]] === properties\_deploy\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A unique integer that tracks changes to deploy collection
object.\|integer(int64) \|\ *items* + *optional*\ \|Collection of deploy
tasks-properties.\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for this deploy collection
object.\|string \|\ *lastUpdateMicros* + *optional* +
*read-only*\ \|Update time (micros) for last change made to an deploy
task collection object-time.\|integer(int64) \|\ *selfLink* + *optional*
+ *read-only*\ \|A reference link URI to the deploy task collection
object.\|string \|===
