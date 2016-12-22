= BIG-IQ LTM/ADC Pool Member Management.

[[\_overview]] == Overview API used to manage LTM pool members.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* :
/mgmt/cm/adc-core/working-config/ltm *Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_pool\_get]] === List all virtual pools items as a collection. ....
GET /pool ....

==== Description Returns the collection of virtual pools.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of virtual
pools.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_pool\_objectid\_get]] === Used to get a single pool object. .... GET
/pool/{objectId} ....

==== Description Returns the pool object identified by id for an
endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to a virtual pool.\|string(UUID)\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Virtual pool
object.\|<<\_properties\_pool,properties\_pool>> \|\ *400*\ \|Server
error response "Bad Request".\|<<\_error\_collection,error\_collection>>
\|===

[[\_pool\_objectid\_members\_post]] === Add a LTM node as a member of an
virtual application pool.

.... POST /pool/{objectId}/members ....

==== Description Add a application server node to a specific virtual
pool.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to pool member
object.\|string(UUID)\|None \|\ *Body*\ \|\ *Json string request body.*
+ *required*\ \|Input parameter list in json format. Ex. {}
\|<<\_post\_pool\_member\_body,post\_pool\_member\_body>>\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a node to an application
pool.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_pool\_objectid\_members\_post]] === Add a LTM node as a member of an
virtual application pool.

.... DEL /pool/{objectId}/members ....

==== Description Delete a application server node for a specific virtual
pool.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to pool member
object.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Delete a node for an application
pool.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_pool\_objectid\_members\_get]] === List all pool members are part of
a collection. .... GET /pool/{objectId}/members ....

==== Description Returns a collection of pool members.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to a virtual pool.\|string(UUID)\|
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Virtual pool members collection
object.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_error\_collection,error\_collection>> \|===

[[\_pool\_objectid\_members\_objectid\_get]] === Used to get a single
pool member (node) object. .... GET /pool/{objectId}/members/{objectId}
....

==== Description Returns the pool memeber object identified by id for an
endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to a virtual pool
member.\|string(UUID)\| \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Virtual pool member (node)
object.\|<<\_properties\_pool\_members,properties\_pool\_members>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_error\_collection,error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_error\_collection]] === error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of pool members. error response from server.\|<
object > array \|\ *kind* + *optional* + *read-only*\ \|Type information
for pool member
collections-cm:adc-core:working-config:ltm:pool:adcpoolstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_properties\_collection]] === properties\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a virtual pool
collection object. generation.\|integer(int64) \|\ *items* +
*optional*\ \|A collection of pool members. properties defining
items.\|< object > array \|\ *kind* + *optional* + *read-only*\ \|Type
information for this virtual pool collection object.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an virtual pool collection object.
time.\|integer(int64) \|\ *selfLink* + *optional* + *read-only*\ \|A
reference link URI to the virtual pool collection object.\|string \|===

[[\_properties\_pool]] === properties\_pool

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *allowNat* + *optional*\ \|Is NAT
(addess translation) allowed for application servers in this
pool.\|boolean \|\ *deviceReference* + *optional*\ \|A reference link to
a device (BIGIP) that virtual pool exists. Also additional data such as
id, name, kind and machine id is
provided.\|<<\_properties\_pool\_devicereference,deviceReference>>
\|\ *enableQueueOnConnectionLimit* + *optional*\ \|Enable or disable
queuing connections when pool member or node connection limits are
reached.\|boolean \|\ *generation* + *optional* + *read-only*\ \|A
integer that will track change made to a virtual pool object.
generation.\|integer(int64) \|\ *id* + *optional* +
*read-only*\ \|Unique id assigned to a virtual pool object.\|string
\|\ *ignorePersistedWeight* + *optional*\ \|Is the weight of persisted
connections on pool members when making load balancing decisions
counted.\|boolean \|\ *ipTosToClientControl* + *optional*\ \|Specifies
the Type of Service (ToS) level to use when sending packets to a client.
possible values on bigiq: 0 ~ 255\|string \|\ *ipTosToServerControl* +
*optional*\ \|Specifies the Type of Service (ToS) level to use when
sending packets to a server. possible values on bigiq: 0 ~ 255\|string
\|\ *kind* + *optional* + *read-only*\ \|Type information for this
virtual pool object.\|string \|\ *lastUpdateMicros* + *optional* +
*read-only*\ \|Update time (micros) for last change made to an virtual
pool object. time.\|integer(int64) \|\ *linkQosToClient* +
*optional*\ \|Specifies the Quality of Service (QoS) level to use when
sending packets to a client. 0 ~ 7, 65535 (passthrough)\|integer
\|\ *linkQosToServer* + *optional*\ \|Specifies the Quality of Service
(QoS) level to use when sending packets to a server. 0 ~ 7, 65535
(passthrough)\|integer \|\ *loadBalancingMode* + *optional*\ \|Specifies
the modes that the system uses to load balance name resolution requests
among the members of this pool. dynamic-ratio-member,
least-connections-member, observed-node, ratio-least-connections-node,
round-robin, dynamic-ratio-node, least-connections-node,
predictive-member, ratio-member, weighted-least-connections-member,
fastest-app-response, least-sessions, predictive-node, ratio-node,
weighted-least-connections-node, fastest-node, observed-member,
ratio-least-connections-member, ratio-session\|string
\|\ *membersCollectionReference* + *optional*\ \|Reference link to
collection of pool members
(nodes).\|<<\_properties\_pool\_memberscollectionreference,membersCollectionReference>>
\|\ *minActiveMembers* + *optional*\ \|Specifies the minimum number of
members that must be up for traffic to be confined to a priority group
when using priority-based activation.\|integer \|\ *name* +
*optional*\ \|Name of virtual pool.\|string \|\ *partition* +
*optional*\ \|Partition location that pool and members are located.
default Common\|string \|\ *queueDepthLimit* + *optional*\ \|Specifies
the maximum number of connections that may simultaneously be queued to
go to any member of this pool.\|integer \|\ *queueTimeLimit* +
*optional*\ \|Specifies the maximum time, in milliseconds, a connection
will remain enqueued. When unset, there is no limit.\|integer
\|\ *reselectTries* + *optional*\ \|Specifies the number of times the
system tries to contact a pool member after a passive failure.\|integer
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
virtual pool object.\|string \|\ *serviceDownAction* +
*optional*\ \|Specifies the action to take if the service specified in
the pool is marked down. The default value is none.\|string
\|\ *slowRampTime* + *optional*\ \|Specifies, in seconds, the ramp time
for the pool. This provides the ability to cause a pool member that has
just been enabled, or marked up, to receive proportionally less traffic
than other members in the pool.\|integer \|===

[[\_properties\_pool\_devicereference]] *deviceReference*

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

[[\_properties\_pool\_memberscollectionreference]]
*membersCollectionReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Does a
sub-collection for this object exist. True / False\|boolean \|\ *link* +
*optional*\ \|Reference link to a collection of pool members. \|string
\|===

[[\_properties\_pool\_members]] === properties\_pool\_members

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *connectionLimit* + *optional*\ \|Number
of connection allowed for pool member.\|integer \|\ *generation* +
*optional* + *read-only*\ \|A integer that will track change made to a
virtual pool member object. generation.\|integer(int64) \|\ *id* +
*optional* + *read-only*\ \|Unique id assigned to a virtual pool
collection object.\|string \|\ *kind* + *optional* + *read-only*\ \|Type
information for this virtual pool member object.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an virtual pool member object.
time.\|integer(int64) \|\ *name* + *optional*\ \|Name of pool
member.\|string \|\ *nodeReference* + *optional*\ \|Reference link to
ltm nodes.\|<<\_properties\_pool\_members\_nodereference,nodeReference>>
\|\ *partition* + *optional*\ \|Partition location that pool and members
are located. default Common\|string \|\ *port* + *optional*\ \|Port used
for application connect.\|integer \|\ *priortyGroup* +
*optional*\ \|Specifies the priority group within the pool for this pool
member.\|integer \|\ *rateLimit* + *optional*\ \|Specifies the maximum
number of connections per second allowed for a pool member. The default
value is 'disabled\|string \|\ *ratio* + *optional*\ \|Specifies the
ratio weight that you want to assign to the pool member. The default
value is 1.\|integer \|\ *selfLink* + *optional* + *read-only*\ \|A
reference link URI to the virtual pool member object.\|string
\|\ *sessionConfig* + *optional*\ \|Enables or disables the node for new
sessions. The default value is user-enabled.\|string \|===

[[\_properties\_pool\_members\_nodereference]] *nodeReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
node specific to pool member configuration.\|string \|===

[[\_post\_pool\_member\_body]] === post\_pool\_member\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *partition* + *required*\ \|Partition
where this application node lives. default Common\|string \|\ *name* +
*required*\ \|Name of application node.\|string \|\ *port* +
*required*\ \|Port to request connection to node.\|integer
\|\ *nodeReference* + *required*\ \|Reference link to application
node.\|string \|===
