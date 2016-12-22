= BIG-IQ Discovery for Firewall Management.

[[\_overview]] == Overview API used for discovery task management of
BIGIP for the AFM (Firewall) namespace by BIGIQ. Re import will use this
task as well.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/firewall/tasks
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_declare-mgmt-authority\_post]] === Create a device discovery
declare-mgmt-authority task managed by BIGIQ module (AFM). .... POST
/declare-mgmt-authority ....

==== Description Create a device discovery declare-mgmt-authority task
and add to collection.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a device discovery
declare-mgmt-authority
task.\|<<\_properties\_declare\_mgmt\_authority\_collection,properties\_declare\_mgmt\_authority\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_declare-mgmt-authority\_get]] === List of device
declare-mgmt-authority collection tasks managed by BIGIQ module (AFM).
.... GET /declare-mgmt-authority ....

==== Description Returns the collection of device discover
declare-mgmt-authority tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Returns a collection of device
discover declare-mgmt-authority
tasks.\|<<\_properties\_declare\_mgmt\_authority\_collection,properties\_declare\_mgmt\_authority\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_declare-mgmt-authority\_objectid\_get]] === Used to get a single
device discovery declare-mgmt-authority task (AFM). .... GET
/declare-mgmt-authority/{objectId} ....

==== Description Returns the device discovery declare-mgmt-authority
task identified by a endpoint URI (AFM).

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assinged to declare-mgmt-authority firewall task
object.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Device discovery
declare-mgmt-authority task object.
(AFM)\|<<\_properties\_declare-mgmt-authority,properties\_declare-mgmt-authority>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_error\_collection]] === error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of device discovery firewall task objects.\|<
object > array \|\ *kind* + *optional* + *read-only*\ \|Type information
for this device discovery firewall task collection object.
cm:firewall:tasks:declare-mgmt-authority:dmataskcollectionstate\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_properties\_declare-mgmt-authority]] ===
properties\_declare-mgmt-authority

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *childTaskReference* +
*optional*\ \|Reference link to child task. shared-object security
discovery.\|<
<<\_properties\_declare-mgmt-authority\_childtaskreference,childTaskReference>>
> array \|\ *childTaskStates* + *optional*\ \|Description of child task
state properties using by declare-mgmt-authority task object.\|<
<<\_properties\_declare-mgmt-authority\_childtaskstates,childTaskStates>>
> array \|\ *copyTaskReference* + *optional*\ \|Enable / Disable
declare-mgmt-authority firewall copy difference between
working-configuration (BIGIQ) and current-configuration
(BIGIP).\|<<\_properties\_declare-mgmt-authority\_copytaskreference,copyTaskReference>>
\|\ *createChildTasks* + *optional*\ \|To create a child task as part of
this declare-mgmt-authority for firewall.\|boolean \|\ *currentStep* +
*optional*\ \|The current step of device declare-mgmt-authority firewall
task as predicated by state.\|string \|\ *deviceReference* +
*optional*\ \|Reference link to resolver for device firewall to be
managed by BIGIQ.
(AFM)\|<<\_properties\_declare-mgmt-authority\_devicereference,deviceReference>>
\|\ *differenceReference* + *optional*\ \|Reference link to differences
object containing differences between working-configuration (BIGIQ) and
current-configuration
(BIGIP)\|<<\_properties\_declare-mgmt-authority\_differencereference,differenceReference>>
\|\ *differencerTaskReference* + *optional*\ \|Reference link to
differencer task. Used to manage difference between
working-configuration (BIGIQ) and current-configuration
(BIGIP)\|<<\_properties\_declare-mgmt-authority\_differencertaskreference,differencerTaskReference>>
\|\ *endDateTime* + *optional*\ \|Date/Time when device discovery task
declare-mgmt-authority firewall ended.
2016-10-11T10:30:17.834-0400\|string \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a device
discovery declare-mgmt-authority task object. (AFM)
generation.\|integer(int64) \|\ *id* + *optional* +
*read-only*\ \|Unique id assigned to a device declare-mgmt-authority
firewall task object.\|string \|\ *identityReference* +
*optional*\ \|Array of reference links to user used to discover device
declare-mgmt-authority firewall. mgmt/shared/authz/users/admin\|<
<<\_properties\_declare-mgmt-authority\_identityreference,identityReference>>
> array \|\ *kind* + *optional* + *read-only*\ \|Type information for
this device discovery declare-mgmt-authority firewall task object.
cm:firewall:tasks:declare-mgmt-authority:dmataskitemstate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an device discovery firewall task
object. time (1476742109026835).\|integer(int64) \|\ *name* +
*optional*\ \|Name of device declare-mgmt-authority task.\|string
\|\ *ownerMachineId* + *optional*\ \|A unique id string for the BIGIQ
acting as a device owner for declare-mgmt-authority. (AFM)\|string
\|\ *reImport* + *optional*\ \|Flag to enable / disable re import
configuration.\|boolean \|\ *selfLink* + *optional* + *read-only*\ \|A
reference link URI to the device discovery declare-mgmt-authority task
object. (AFM)\|string \|\ *skipDiscovery* + *optional*\ \|Skip discovery
for re import configuration.\|boolean \|\ *snapshotWorkingConfig* +
*optional*\ \|To snapshot the working-configuration (BIGIQ) during
firewall module discovery.\|boolean \|\ *startDateTime* +
*optional*\ \|Date/Time when device discovery declare-mgmt-authority
firewall task began. 2016-10-11T10:30:17.834-0400\|string \|\ *status* +
*optional*\ \|Status of device declare-mgmt-authority task predicated on
state.\|string \|\ *useBigiqSync* + *optional*\ \|Flag to sync BIGIP
cluster management (True / False)\|boolean \|\ *userReference* +
*optional*\ \|Reference link to user used to discover device
declare-mgmt-authority firewall.
mgmt/shared/authz/users/admin\|<<\_properties\_declare-mgmt-authority\_userreference,userReference>>
\|\ *username* + *optional*\ \|User name of device firewall object to be
managed. (Firewall)\|string \|\ *validationBypassMode* +
*optional*\ \|Enable / Disable validation check when importing
configuration device. BYPASS\_NONE - no bypass (default), BYPASS\_FINAL
- skip final validation phase, BYPASS\_ALL - skip all validation
phases.\|string \|===

[[\_properties\_declare-mgmt-authority\_childtaskreference]]
*childTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
shared-security declare-mgmt-authority child task.\|string \|===

[[\_properties\_declare-mgmt-authority\_childtaskstates]]
*childTaskStates*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *copyTaskReference* +
*optional*\ \|Enable / Disable declare-mgmt-authority firewall copy
difference between working-configuration (BIGIQ) and
current-configuration
(BIGIP).\|<<\_properties\_declare-mgmt-authority\_copytaskreference,copyTaskReference>>
\|\ *createChildTasks* + *optional*\ \|To create a child task as part of
this declare-mgmt-authority for firewall.\|boolean \|\ *currentStep* +
*optional*\ \|The current step of device declare-mgmt-authority firewall
task as predicated by state.\|string \|\ *deviceIp* +
*optional*\ \|Device ip address this task is running on.\|string
\|\ *deviceReference* + *optional*\ \|Reference link to the device in
the shared allAsmDevices resolver device
group.\|<<\_properties\_declare-mgmt-authority\_devicereference,deviceReference>>
\|\ *differenceReference* + *optional*\ \|Reference link to differences
object containing differences between working-configuration (BIGIQ) and
current-configuration
(BIGIP)\|<<\_properties\_declare-mgmt-authority\_differencereference,differenceReference>>
\|\ *differencerTaskReference* + *optional*\ \|Reference link to
differencer task. Used to manage difference between
working-configuration (BIGIQ) and current-configuration
(BIGIP)\|<<\_properties\_declare-mgmt-authority\_differencertaskreference,differencerTaskReference>>
\|\ *endDateTime* + *optional*\ \|Date/Time when device discovery task
declare-mgmt-authority firewall ended.
2016-10-11T10:30:17.834-0400\|string \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a device
discovery declare-mgmt-authority firewall task object.
generation.\|integer(int64) \|\ *id* + *optional*\ \|Unique id for child
task.\|string \|\ *identityReference* + *optional*\ \|Array of reference
links to user used to discover device declare-mgmt-authority firewall.
mgmt/shared/authz/users/admin\|<
<<\_properties\_declare-mgmt-authority\_identityreference,identityReference>>
> array \|\ *isChildTask* + *optional*\ \|Identify if task is a child of
this declare-mgmt-authority for firewall.\|boolean \|\ *kind* +
*optional* + *read-only*\ \|Type information for this device discovery
declare-mgmt-authority firewall task object.
cm:security-shared:tasks:declare-mgmt-authority:dmataskitemstate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an device discovery firewall task
object. time (1476742109026835).\|integer(int64) \|\ *ownerMachineId* +
*optional*\ \|A unique id string for the BIGIQ acting as a device owner
for declare-mgmt-authority firewall. (Firewall)\|string
\|\ *parentTaskReference* + *optional*\ \| Reference link to parent
process. The declare-mgmt-authority
task.\|<<\_properties\_declare-mgmt-authority\_parenttaskreference,parentTaskReference>>
\|\ *reImport* + *optional*\ \|Flag to enable / disable re import
configuration.\|boolean \|\ *selfLink* + *optional* + *read-only*\ \|A
reference link URI to the device discovery declare-mgmt-authority
firewall task object.\|string \|\ *skipDiscovery* + *optional*\ \|Skip
discovery for re import configuration.\|boolean \|\ *startDateTime* +
*optional*\ \|Date/Time when device discovery declare-mgmt-authority
firewall task began. 2016-10-11T10:30:17.834-0400\|string \|\ *status* +
*optional*\ \|Status of device discovery declare-mgmt-authority firewall
task during state transistion. (Firewall)\|string \|\ *useBigiqSync* +
*optional*\ \|Flag to sync BIGIP cluster management (True /
False)\|boolean \|\ *userReference* + *optional*\ \|Reference link to
user used to discover device declare-mgmt-authority firewall.
mgmt/shared/authz/users/admin\|<<\_properties\_declare-mgmt-authority\_userreference,userReference>>
\|\ *username* + *optional*\ \|User name of device firewall object to be
managed. (Firewall)\|string \|\ *validationBypassMode* +
*optional*\ \|Enable / Disable validation check when importing
configuration device. BYPASS\_NONE - no bypass (default), BYPASS\_FINAL
- skip final validation phase, BYPASS\_ALL - skip all validation
phases.\|string \|===

[[\_properties\_declare-mgmt-authority\_copytaskreference]]
*copyTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
declare-mgmt-authority difference copy task.\|string \|===

[[\_properties\_declare-mgmt-authority\_devicereference]]
*deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
declare-mgmt-authority task device.\|string \|===

[[\_properties\_declare-mgmt-authority\_differencereference]]
*differenceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
shared security configuration difference report.

\|string \|===

[[\_properties\_declare-mgmt-authority\_differencertaskreference]]
*differencerTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
differencer task. Used to manage difference between
working-configuration (BIGIQ) and current-configuration (BIGIP)\|string
\|===

[[\_properties\_declare-mgmt-authority\_identityreference]]
*identityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
shared security configuration difference task object.

\|string \|===

[[\_properties\_declare-mgmt-authority\_parenttaskreference]]
*parentTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
parent task. This declare-mgmt-authority task object.\|string \|===

[[\_properties\_declare-mgmt-authority\_userreference]] *userReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
users. /mgmt/shared/authz/users/admin\|string \|===

[[\_properties\_declare-mgmt-authority\_copytaskreference]]
*copyTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
declare-mgmt-authority difference copy task.\|string \|===

[[\_properties\_declare-mgmt-authority\_devicereference]]
*deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
the device in the shared allFirewallDevices resolver device
group.\|string \|===

[[\_properties\_declare-mgmt-authority\_differencereference]]
*differenceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
delcare-mgmt-authority differences found (current-config (BIGIP) and
working-config (BIGIQ)) during task.\|string \|===

[[\_properties\_declare-mgmt-authority\_differencertaskreference]]
*differencerTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
delcare-mgmt-authority differences task object.\|string \|===

[[\_properties\_declare-mgmt-authority\_identityreference]]
*identityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Array of
reference links to users. mgmt/shared/authz/users/admin\|string \|===

[[\_properties\_declare-mgmt-authority\_userreference]] *userReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference links
to user. mgmt/shared/authz/user\|string \|===

[[\_properties\_declare\_mgmt\_authority\_collection]] ===
properties\_declare\_mgmt\_authority\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a device
discovery firewall task collection object. generation.\|integer(int64)
\|\ *items* + *optional*\ \|Array of device discovery firewall task
object.\|< object > array \|\ *kind* + *optional* + *read-only*\ \|Type
information for this device discover firewall task collection object.
cm:firewall:tasks:declare-mgmt-authority:dmataskcollectionstate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an device discovery firewall task
collection object. time.\|integer(int64) \|\ *selfLink* + *optional* +
*read-only*\ \|A reference link URI to the device discovery firewall
task collection object.\|string \|===
