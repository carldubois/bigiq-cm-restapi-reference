= BIG-IQ Device Trust

[[\_overview]] == Overview API used to create a device trust certificate
between BIG-IQ and BIG-IP.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/global/tasks
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_device-trust\_post]] === List all device-trust task items. .... POST
/device-trust ....

==== Description Returns the collection of device-trust tasks.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to device trust
task.\|string(UUID)\|None \|\ *Body*\ \|\ *Json string request body.* +
*required*\ \|Input parameter list in json format. Ex.
{"address":"10.90.2.22","userName":"admin","password":"admin","clusterName":"","useBigiqSync":false}
\|<<\_post\_device\_trust\_body,post\_device\_trust\_body>>\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of device-trust
tasks.\|<<\_properties\_device\_trust\_post,properties\_device\_trust\_post>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_device-trust\_get]] === List all device-trust task items. .... GET
/device-trust ....

==== Description Returns the collection of device-trust tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of device-trust
tasks.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_device-trust\_objectid\_get]] === Used to get a single device-trust
task. .... GET /device-trust/{objectId} ....

==== Description Returns the device-trust identified by id for an
endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to device trust
task.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Device-trust
object.\|<<\_properties\_device-trust,properties\_device-trust>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of device-trust task objects.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for
device-trust
collections-cm:global:tasks:device-trust:bigiptrusttaskstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of device-trust task objects.\|< object > array
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
*read-only*\ \|A integer that will track change made to a device trust
collection object. generation.\|integer(int64) \|\ *items* +
*optional*\ \|Collection of device-trust task objects.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for this
device trust collection object.\|string \|\ *lastUpdateMicros* +
*optional* + *read-only*\ \|Update time (micros) for last change made to
an device trust collection object. time.\|integer(int64) \|\ *selfLink*
+ *optional* + *read-only*\ \|A reference link URI to the device trust
collection object.\|string \|===

[[\_properties\_device-trust]] === properties\_device-trust

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *address* + *optional*\ \|IP address of
device object.\|string \|\ *clusterName* + *optional*\ \|DSC cluster
name of device object to be managed. None if not part of a cluster
group.\|string \|\ *currentStep* + *optional*\ \|State machine current
step for device trust task.\|string \|\ *endDateTime* +
*optional*\ \|Date/Time when device trust task end.
2016-10-11T10:30:17.834-0400\|string \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a device-trust
object. generation.\|integer(int64) \|\ *id* + *optional* +
*read-only*\ \|Unique id assigned to a device trust task object.\|string
\|\ *identityReference* + *optional*\ \|Array of reference links to user
used to estabish trust. mgmt/shared/authz/users/admin\|<
<<\_properties\_device-trust\_identityreference,identityReference>> >
array \|\ *isChassisDevice* + *optional*\ \|Is this device virtual or
appliance. (True / False)\|boolean \|\ *kind* + *optional* +
*read-only*\ \|Type information for this device trust object.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an policy object. time.\|integer(int64)
\|\ *machineId* + *optional*\ \|A unique id string for the BIGIP
device.\|string \|\ *ownerMachineId* + *optional* + *read-only*\ \|A
unique id string for the BIGIQ acting as a device owner.\|string
\|\ *password* + *optional*\ \|Password of device object to be
managed.\|string \|\ *selfLink* + *optional* + *read-only*\ \|A
reference link URI to the device trust object.\|string
\|\ *stateDateTime* + *optional*\ \|Date/Time when device trust task
began. 2016-10-11T10:30:17.834-0400\|string \|\ *status* +
*optional*\ \|Status of device trust during state transistion.\|string
\|\ *useBigiqSync* + *optional*\ \|To enable DSC configuration sync.
True / False. When enabled, the BIG-IQ will manually synchronize
configurations changes between members in a DSC group.\|boolean
\|\ *userName* + *optional*\ \|Username of BIGIQ device object.\|string
\|\ *userReference* + *optional*\ \|Reference link to user used to
estabish trust.
mgmt/shared/authz/users/admin\|<<\_properties\_device-trust\_userreference,userReference>>
\|\ *username* + *optional*\ \|User name of device object to be
managed.\|string \|===

[[\_properties\_device-trust\_identityreference]] *identityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Array of user
reference links used to discovery devices.\|string \|===

[[\_properties\_device-trust\_userreference]] *userReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
a user used to discover devices.\|string \|===

[[\_post\_device\_trust\_body]] === post\_device\_trust\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *address* + *required*\ \|IP address of
device object.\|string \|\ *userName* + *required*\ \|Username of BIGIQ
device object.\|string \|\ *password* + *required*\ \|Password of device
object to be managed.\|string \|\ *clusterName* + *required*\ \|DSC
cluster name of device object to be managed. None if not part of a
cluster group.\|string \|\ *useBigiqSync* + *required*\ \|To enable DSC
configuration sync. True / False\|boolean \|===
