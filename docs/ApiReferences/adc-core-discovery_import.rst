= BIG-IQ Device Discovery for ADC Core Management.

[[\_overview]] == Overview API used for discovery task management of
BIGIP for the ADC namespace by BIGIQ. This task will be used for import
as well.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/adc-core/tasks
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_declare-mgmt-authority\_post]] === Create a device discovery
declare-mgmt-authority task managed by BIGIQ module (LTM/ADC). .... POST
/declare-mgmt-authority ....

==== Description Create a device discovery declare-mgmt-authority task
and add to collection.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to device discovery task
object.\|string(UUID)\|None \|\ *Body*\ \|\ *Json string request body.*
+ *required*\ \|Input parameter list in json format. Ex. {}
\|<<\_post\_discovery\_body,post\_discovery\_body>>\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a device discovery
declare-mgmt-authority
task.\|<<\_properties\_declare\_mgmt\_authority\_collection,properties\_declare\_mgmt\_authority\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_declare-mgmt-authority\_get]] === List of device
declare-mgmt-authority collection tasks managed by BIGIQ module
(LTM/ADC). .... GET /declare-mgmt-authority ....

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
device discovery declare-mgmt-authority task (LTM/ADC). .... GET
/declare-mgmt-authority/{objectId} ....

==== Description Returns the device discovery declare-mgmt-authority
task identified by a endpoint URI (LTM/ADC).

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to this declare-mgmt-authority task
object.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Device discovery
declare-mgmt-authority task object.
(LTM/ADC)\|<<\_properties\_declare-mgmt-authority,properties\_declare-mgmt-authority>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_error\_collection]] === error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of device discovery declare-mgmt-authority task
objects.\|< object > array \|\ *kind* + *optional* + *read-only*\ \|Type
information for this device discovery declare-mgmt-authority task
collection object.
cm:adc-core:tasks:declare-mgmt-authority:dmataskcollectionstate\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_properties\_declare-mgmt-authority]] ===
properties\_declare-mgmt-authority

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *copyTaskReference* +
*optional*\ \|Enable / Disable declare-mgmt-authority copy difference
between working-configuration (BIGIQ) and current-configuration
(BIGIP).\|<<\_properties\_declare-mgmt-authority\_copytaskreference,copyTaskReference>>
\|\ *currentStep* + *optional*\ \|The current step of device
declare-mgmt-authority task as predicated by state.\|string
\|\ *deviceReference* + *optional*\ \|Reference link to resolver for
device declare-mgmt-authority to be managed by BIGIQ. (LTM /
ADC)\|<<\_properties\_declare-mgmt-authority\_devicereference,deviceReference>>
\|\ *differenceReference* + *optional*\ \|Reference link to differences
object containing differences between working-configuration (BIGIQ) and
current-configuration
(BIGIP)\|<<\_properties\_declare-mgmt-authority\_differencereference,differenceReference>>
\|\ *differencerTaskReference* + *optional*\ \|Reference link to
differencer task. Used to manage difference between
working-configuration (BIGIQ) and current-configuration
(BIGIP)\|<<\_properties\_declare-mgmt-authority\_differencertaskreference,differencerTaskReference>>
\|\ *endDateTime* + *optional*\ \|Date/Time when device discovery task
declare-mgmt-authority ended. 2016-10-11T10:30:17.834-0400\|string
\|\ *generation* + *optional* + *read-only*\ \|A integer that will track
change made to a device discovery declare-mgmt-authority task object.
generation.\|integer(int64) \|\ *id* + *optional* +
*read-only*\ \|Unique id assigned to a device discovery
declare-mgmt-authority task object.\|string \|\ *identityReference* +
*optional*\ \|Array of reference links to user used to discover device
declare-mgmt-authority. mgmt/shared/authz/users/admin\|<
<<\_properties\_declare-mgmt-authority\_identityreference,identityReference>>
> array \|\ *kind* + *optional* + *read-only*\ \|Type information for
this device discovery declare-mgmt-authority task object.
cm:adc-core:tasks:declare-mgmt-authority:dmataskitemstate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an device discovery task object. time
(1476742109026835).\|integer(int64) \|\ *ownerMachineId* +
*optional*\ \|A unique id string for the BIGIQ acting as a device owner
for declare-mgmt-authority. (LTM / ADC)\|string \|\ *reImport* +
*optional*\ \|Flag to enable / disable re import configuration.\|boolean
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
device discovery declare-mgmt-authority task object.\|string
\|\ *startDateTime* + *optional*\ \|Date/Time when device discovery
declare-mgmt-authority task began. 2016-10-11T10:30:17.834-0400\|string
\|\ *status* + *optional*\ \|Status of device discovery
declare-mgmt-authority task during state transistion. (LTM /
ADC)\|string \|\ *userReference* + *optional*\ \|Reference link to user
used to discover device declare-mgmt-authority.
mgmt/shared/authz/users/admin\|<<\_properties\_declare-mgmt-authority\_userreference,userReference>>
\|\ *username* + *optional*\ \|User name of device
declare-mgmt-authority object to be managed. (LTM / ADC)\|string
\|\ *validationBypassMode* + *optional*\ \|Enable / Disable validation
check when importing configuration device. BYPASS\_NONE - no bypass
(default), BYPASS\_FINAL - skip final validation phase, BYPASS\_ALL -
skip all validation phases.\|string \|===

[[\_properties\_declare-mgmt-authority\_copytaskreference]]
*copyTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
a declare-mgmt-authority copy task object. \|string \|===

[[\_properties\_declare-mgmt-authority\_devicereference]]
*deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
declare-mgmt-authority adc task device.\|string \|===

[[\_properties\_declare-mgmt-authority\_differencereference]]
*differenceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
shared security configuration difference report for adc-core.\|string
\|===

[[\_properties\_declare-mgmt-authority\_differencertaskreference]]
*differencerTaskReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
shared security configuration difference adc-core task object.\|string
\|===

[[\_properties\_declare-mgmt-authority\_identityreference]]
*identityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
users. /mgmt/shared/authz/users/admin\|string \|===

[[\_properties\_declare-mgmt-authority\_userreference]] *userReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
users. /mgmt/shared/authz/users/admin\|string \|===

[[\_properties\_declare\_mgmt\_authority\_collection]] ===
properties\_declare\_mgmt\_authority\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a device
discovery declare-mgmt-authority task collection object.
generation.\|integer(int64) \|\ *items* + *optional*\ \|Array of device
discovery task object.\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for this device discovery
declare-mgmt-authority task collection object.
cm:adc-core:tasks:declare-mgmt-authority:dmataskcollectionstate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an device discovery
declare-mgmt-authority task collection object. time.\|integer(int64)
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
device discovery declare-mgmt-authority task collection object.\|string
\|===

[[\_post\_discovery\_body]] === post\_discovery\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *deviceReference* +
*required*\ \|Reference link to device in resolver group.\|string
\|\ *moduleList* + *required*\ \|List of modules to discover. ex.
adc\_core, asm, shared\_security, firewall\|string \|\ *userName* +
*required*\ \|Username of device.\|string \|\ *password* +
*required*\ \|Password of device.\|string \|\ *rootUser* +
*required*\ \|Root user of device.\|string \|\ *rootPassword* +
*required*\ \|Root password of device.\|string
\|\ *automaticallyUpdateFramework* + *required*\ \|To update rest
framework automatically. It is recommended to do so if using REST
API.\|boolean \|===
