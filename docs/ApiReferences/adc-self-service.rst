= BIG-IQ LTM/ADC Self-Service Task. (enable/disable pool member)

[[\_overview]] == Overview API used create a self-service task to
perform functions such as enable/disable pool member.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/adc-core/tasks
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_self-service\_post]] === Create a adc self-service task managed by
BIGIQ module. .... POST /self-service ....

==== Description Create a adc self-service task and add to collection.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to a self-service
task.\|string(UUID)\|None \|\ *Body*\ \|\ *Json string request body.* +
*required*\ \|Input parameter list in json format. Ex.
{"resourceReference":{"link":"https://localhost/mgmt/cm/adc-core/working-config/ltm/pool/3a3361a8-64fa-33d7-bc1a-d6658f31e687/members/a0fd9118-b58c-339f-8085-e92f1f75ec1e"},"operation":"enable"}
\|<<\_post\_adc\_self\_service\_body,post\_adc\_self\_service\_body>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a self-service
task.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_self-service\_get]] === List all collections of self-service tasks.
.... GET /self-service ....

==== Description Returns the collection of self-service tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of self-service
tasks.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_self-service\_objectid\_get]] === Used to get a single instance of a
self-service task object. .... GET /self-service/{objectId} ....

==== Description Returns a self-service task object identified by id for
an endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to a self-service
task.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Self-service task
object.\|<<\_properties\_self\_service,properties\_self\_service>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_error\_collection,error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_error\_collection]] === error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of self-service task errors.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for
device-trust
collections-cm:global:tasks:device-trust:bigiptrusttaskstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_properties\_collection]] === properties\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a self-service
collection object. generation.\|integer(int64) \|\ *items* +
*optional*\ \|Self-serivce task properties associated with the
collection.\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for this self-service task collection
object.\|string \|\ *lastUpdateMicros* + *optional* +
*read-only*\ \|Update time (micros) for last change made to an
self-service collection object. time.\|integer(int64) \|\ *selfLink* +
*optional* + *read-only*\ \|A reference link URI to the self-service
task collection object.\|string \|===

[[\_properties\_self\_service]] === properties\_self\_service

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *deviceReference* +
*optional*\ \|Reference link to device object in
resolver.\|<<\_properties\_self\_service\_devicereference,deviceReference>>
\|\ *endDateTime* + *optional*\ \|Date/Time when self-service task end.
2016-10-11T10:30:17.834-0400\|string \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a self-service
task object. generation.\|integer(int64) \|\ *id* + *optional* +
*read-only*\ \|Unique id assigned to a self-service task object.\|string
\|\ *identityReference* + *optional*\ \|Array of reference links to user
used to create self-service task. mgmt/shared/authz/users/admin\|<
<<\_properties\_self\_service\_identityreference,identityReference>> >
array \|\ *kind* + *optional* + *read-only*\ \|Type information for this
self-service task object.\|string \|\ *lastUpdateMicros* + *optional* +
*read-only*\ \|Update time (micros) for last change made to an
self-service task object. time.\|integer(int64) \|\ *name* +
*optional*\ \|Name of self-service task object. example.
'Self-Service\_10.55.2.20:80'\|string \|\ *operation* +
*optional*\ \|Description of operation type. example.
(enable/disable/force offline).\|string \|\ *ownerMachineId* +
*optional* + *read-only*\ \|A unique id string for the BIGIQ acting as a
device owner.\|string \|\ *resourceReference* + *optional*\ \|Reference
link to resource used. example. pool member
enable/disable\|<<\_properties\_self\_service\_resourcereference,resourceReference>>
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
self-service task object.\|string \|\ *stateDateTime* +
*optional*\ \|Date/Time when self-service task began.
2016-10-11T10:30:17.834-0400\|string \|\ *status* + *optional*\ \|Status
if self-service task based on state. STARTED; FINSIHED etc..\|string
\|\ *userReference* + *optional*\ \|Reference link to user used to
create self-service task.
mgmt/shared/authz/users/admin\|<<\_properties\_self\_service\_userreference,userReference>>
\|\ *username* + *optional*\ \|Username of user whom iniated the
task.\|string \|===

[[\_properties\_self\_service\_devicereference]] *deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
device assocated with this self-service task in the device
resolver.\|string \|===

[[\_properties\_self\_service\_identityreference]] *identityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link
table to authz users.\|string \|===

[[\_properties\_self\_service\_resourcereference]] *resourceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
the resource in which the task is mananging. \|string \|===

[[\_properties\_self\_service\_userreference]] *userReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link
table to authz user.\|string \|===

[[\_post\_adc\_self\_service\_body]] === post\_adc\_self\_service\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *resourceReference* +
*required*\ \|Reference link to the pool member resource for self
service.\|string \|\ *operation* + *required*\ \|Enable, Disable or
Force Offline.\|string \|===
