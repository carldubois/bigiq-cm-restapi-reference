= BIG-IQ LTM Application Server Node.

[[\_overview]] == Overview API used to create/manage LTM application
server nodes allowing for distribution into pools.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* :
/mgmt/cm/adc-core/working-config/ltm *Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_node\_post]] === Create a LTM application server node. .... POST
/node ....

==== Description POST to create a BIGIP application server node.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to application server node
object.\|string(UUID)\|None \|\ *Body*\ \|\ *Json string request body.*
+ *required*\ \|Input parameter list in json format. Ex. {}
\|<<\_post\_application\_node\_body,post\_application\_node\_body>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a BIGIP LTM application
server node.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_node\_get]] === List all application server node items as a
collection. .... GET /node ....

==== Description Returns the collection of nodes.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of
nodes.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_node\_objectid\_get]] === Used to get a single application server
node object. .... GET /node/{objectId} ....

==== Description Returns the application server node object identified
by id for an endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to a application server
node.\|string(UUID)\| \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Application server node
object.\|<<\_properties\_node,properties\_node>> \|\ *400*\ \|Server
error response "Bad
Request".\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of application server nodes. Errored response
from server.\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for LTM application server nodes -
errors –
cm:adc-core:working-config:ltm:node:adcnodecollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of application server nodes. Errored response
from server.\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for node -
cm:adc-core:working-config:ltm:node:adcnodecollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_properties\_collection]] === properties\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a node
collection object. generation.\|integer(int64) \|\ *items* +
*optional*\ \|A collection of application server nodes. Properties
defining items.\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for this node collection object -
cm:adc-core:working-config:ltm:node:adcnodecollectionstate.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an node collection object.
time.\|integer(int64) \|\ *selfLink* + *optional* + *read-only*\ \|A
reference link URI to the application server node collection
object.\|string \|===

[[\_properties\_node]] === properties\_node

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *address* + *optional*\ \|Network
address for application server used for node object.\|string
\|\ *connectionLimit* + *optional*\ \|Specifies the maximum number of
connections allowed for the node or node address.\|integer
\|\ *deviceReference* + *optional*\ \|Reference link to BIGIP device
assiociated to application server
node.\|<<\_properties\_node\_devicereference,deviceReference>>
\|\ *fqdn* + *optional*\ \|Specifies the node's fully qualified domain
name (FQDN) attributes.\|<<\_properties\_node\_fqdn,fqdn>>
\|\ *generation* + *optional* + *read-only*\ \|A integer that will track
change made to a LTM application server node object. -
generation.\|integer(int64) \|\ *id* + *optional* +
*read-only*\ \|Unique id assigned to a virtual server object.\|string
\|\ *isEphemeral* + *optional*\ \|Is this node short lived when
fowarding application traffic.\|boolean \|\ *kind* + *optional*\ \|Type
information for this application server node object. -
cm:adc-core:working-config:ltm:node:adcnodestate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an LTN application server node object -
time.\|integer(int64) \|\ *name* + *optional*\ \|Name of LTM application
server node.\|string \|\ *partition* + *optional*\ \|Displays the
administrative partition within which this node resides.\|string
\|\ *rateLimit* + *optional*\ \|Specifies the maximum number of
connections per second allowed for a node or node address. The default
value is 'disabled'.\|string \|\ *ratio* + *optional*\ \|Specifies the
fixed ratio value used for a node during ratio load balancing.\|string
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
LTM application server node object.\|string \|\ *sessionConfig* +
*optional*\ \|Enables or disables the node for new sessions. The default
value is user-enabled.\|string \|\ *stateConfig* + *optional*\ \|Marks
the node up or down. The default value is user-up.\|string \|===

[[\_properties\_node\_devicereference]] *deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *id* + *optional*\ \|Unique id assigned
to a device referenced by this object.\|string \|\ *kind* +
*optional*\ \|Type information for device.
shared:resolver:device-groups:restdeviceresolverdevicestate\|string
\|\ *link* + *optional*\ \|Reference link to adc-core-allbigipDevices in
shared resolver device-groups.\|string \|\ *machineId* +
*optional*\ \|Unique id assigned to the hardware device. If virtual
could be the same as id object.\|string \|\ *name* + *optional*\ \|A
name used to identify this device.\|string \|===

[[\_properties\_node\_fqdn]] *fqdn*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *addressFamily* +
*optional*\ \|Specifies the node's address family. The default is
'unspecified', or IP-agnostic\|string \|\ *downInterval* +
*optional*\ \|Specifies the number of attempts to resolve a domain name.
The default is 5.\|integer \|\ *interval* + *optional*\ \|Specifies the
amount of time before sending the next DNS query.\|string
\|\ *isAutoPolulate* + *optional*\ \|Specifies whether the node should
scale to the IP address set returned by DNS.\|boolean \|===

[[\_post\_application\_node\_body]] === post\_application\_node\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *partition* + *required*\ \|Partition
where this application node lives. default Common\|string \|\ *noLock* +
*required*\ \|Application node locking.\|boolean \|\ *deviceReference* +
*required*\ \|Reference link to device in resolver group.\|string
\|\ *address* + *required*\ \|IP Addres of device.\|string
\|\ *appService* + *required*\ \|link uri to application servce.\|string
\|\ *connectionLimit* + *required*\ \|Password of device.\|string
\|\ *rootUser* + *required*\ \|Root user of device.\|string
\|\ *rootPassword* + *required*\ \|Root password of device.\|string
\|\ *automaticallyUpdateFramework* + *required*\ \|To update rest
framework automatically. It is recommended to do so if using REST
API.\|boolean \|===
