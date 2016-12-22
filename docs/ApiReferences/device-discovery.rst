= BIG-IQ Device Discovery

[[\_overview]] == Overview API used for discovery task management of
BIGIP by BIGIQ.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/global/tasks
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_device-discovery\_post]] === Create a device discovery task managed
by BIGIQ module (LTM, AFM, ASM). .... POST /device-discovery ....

==== Description Create a device discovery task and add to collection.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to device discovery
task.\|string(UUID)\|None \|\ *Body*\ \|\ *Json string request body.* +
*required*\ \|Input parameter list in json format. Ex.
{"moduleList":[{"module":"adc\_core"}],"deviceReference":{"link":"https://localhost/mgmt/cm/system/machineid-resolver/2a2baaf0-b22f-49dc-81c6-4711fa189820"}}\|<<\_post\_device\_discovery\_body,post\_device\_discovery\_body>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a device discovery
task.\|<<\_properties\_device\_discovery\_collection,properties\_device\_discovery\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_device-discovery\_get]] === List of device discovery collections
managed by BIGIQ module (LTM, AFM, ASM). .... GET /device-discovery ....

==== Description Returns the collection of device discovery tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Returns a collection of device
discovery
tasks.\|<<\_properties\_device\_discovery\_collection,properties\_device\_discovery\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_device-discovery\_objectid\_get]] === Used to get a single device
discovery task. .... GET /device-discovery/{objectId} ....

==== Description Returns the device discovery task identified by a
endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to device discovery
task.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Device discovery task
object\|<<\_properties\_device\_discovery,properties\_device\_discovery>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_error\_collection]] === error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of device-discovery task objects.\|< object >
array \|\ *kind* + *optional* + *read-only*\ \|Type information for this
device discovery task collection object.
cm:global:tasks:device-discovery:discoverysupertaskcollectionstate\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_properties\_device\_discovery]] === properties\_device\_discovery

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *allModuleStatus* +
*optional*\ \|Discovery module status and information. (module type,
discovery start time and end time 2016-10-17T22:07:31.633Z)\|<
<<\_properties\_device\_discovery\_allmodulestatus,allModuleStatus>> >
array \|\ *deviceReference* + *optional*\ \|Reference link to resolver
for device to be managed by
BIGIQ.\|<<\_properties\_device\_discovery\_devicereference,deviceReference>>
\|\ *endDateTime* + *optional*\ \|Date/Time when device discovery task
ended. 2016-10-11T10:30:17.834-0400\|string \|\ *generation* +
*optional* + *read-only*\ \|A integer that will track change made to a
device discovery task object. generation.\|integer(int64) \|\ *id* +
*optional* + *read-only*\ \|Unique id assigned to a device discovery
task object.\|string \|\ *identityReference* + *optional*\ \|Array of
reference links to user used to discover device.
mgmt/shared/authz/users/admin\|<
<<\_properties\_device\_discovery\_identityreference,identityReference>>
> array \|\ *kind* + *optional* + *read-only*\ \|Type information for
this device discovery task object.\|string \|\ *lastUpdateMicros* +
*optional* + *read-only*\ \|Update time (micros) for last change made to
an device discovery task object. time
(1476742109026835).\|integer(int64) \|\ *name* + *optional*\ \|Name of
device discovery task.\|string \|\ *ownerMachineId* + *optional*\ \|A
unique id string for the BIGIQ acting as a device owner.\|string
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
device discovery task object.\|string \|\ *startDateTime* +
*optional*\ \|Date/Time when device discovery task began.
2016-10-11T10:30:17.834-0400\|string \|\ *status* + *optional*\ \|Status
of device discovery task during state transistion.\|string
\|\ *userReference* + *optional*\ \|Reference link to user used to
discover device.
mgmt/shared/authz/users/admin\|<<\_properties\_device\_discovery\_userreference,userReference>>
\|\ *username* + *optional*\ \|User name of device object to be
managed.\|string \|===

[[\_properties\_device\_discovery\_allmodulestatus]] *allModuleStatus*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *endTime* + *optional*\ \|End time of
device discovery task, per module.\|string \|\ *module* +
*optional*\ \|Module type of device discovery task, (Module List-
access, adc-core, firewall, asm, security\_shared, dns)\|string
\|\ *startTime* + *optional*\ \|Start time of device discovery task, per
module\|string \|===

[[\_properties\_device\_discovery\_devicereference]] *deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Device reference
link to device resolver.\|string \|===

[[\_properties\_device\_discovery\_identityreference]]
*identityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Array of user
reference links used to discovery devices.\|string \|===

[[\_properties\_device\_discovery\_userreference]] *userReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
a user used to discover devices.\|string \|===

[[\_properties\_device\_discovery\_collection]] ===
properties\_device\_discovery\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a device
discovery task collection object. generation.\|integer(int64)
\|\ *items* + *optional*\ \|Array of device discovery task object.\|<
object > array \|\ *kind* + *optional* + *read-only*\ \|Type information
for this device discovery task collection object.
cm:global:tasks:device-discovery:discoverysupertaskcollectionstate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an device discovery task collection
object. time.\|integer(int64) \|\ *selfLink* + *optional* +
*read-only*\ \|A reference link URI to the device discovery task
collection object.\|string \|===

[[\_post\_device\_discovery\_body]] === post\_device\_discovery\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *moduleList* + *required*\ \|A list of
all modules to discover. ex. access, adc-core, firewall, asm,
security\_shared, dns\|array \|\ *deviceReference* +
*required*\ \|Reference link to device in resolver.\|string \|===
