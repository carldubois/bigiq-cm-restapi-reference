= BIG-IQ Firewall Contexts API

[[\_overview]] == Overview API used to create and modify firewall
contexts on BIG-IQ

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* :
/mgmt/cm/firewalls/working-config *Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_firewalls\_get]] === List of firewall collections. .... GET
/firewalls ....

==== Description Returns the collection of firewalls.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of
firewalls.\|<<\_properties\_firewall\_collection,properties\_firewall\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_firewalls\_objectid\_get]] === Used to get a single firewall
context. .... GET /firewalls/{objectId} ....

==== Description Returns the firewall context identified by a endpoint
URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Firewall object id\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Firewall context
object\|<<\_properties\_firewall,properties\_firewall>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_firewalls\_objectid\_patch]] === PATCH firewall context into
firewall context. .... PATCH /firewalls/{objectId} ....

==== Description Will patch enforced policy reference link into firewall
context.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Firewall object id\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Patch firewall policies to
firewalls success.\|<<\_properties\_firewall,properties\_firewall>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_error\_collection]] === error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of firewalls-error.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for firewalls
object.\|string \|\ *message* + *optional* + *read-only*\ \|Error
message returned from server.\|string \|\ *requestBody* + *optional* +
*read-only*\ \|The data in the request body. GET (None)\|string
\|\ *requestOperationId* + *optional* + *read-only*\ \|Unique id
assigned to rest operation.\|integer(int64) \|===

[[\_properties\_firewall]] === properties\_firewall

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *firewallIpAddress* +
*optional*\ \|Firewall IP Address\|string \|\ *firewallType* +
*optional*\ \|Firewall Type (VIP, SIP, RD, Mgmt etc..)\|string
\|\ *generation* + *optional* + *read-only*\ \|A integer that will track
change made to a firewall object. generation.\|integer(int64) \|\ *id* +
*optional* + *read-only*\ \|Unique id assigned to a firewall
object.\|string \|\ *kind* + *optional* + *read-only*\ \|Type
information for this firewall object.\|string \|\ *lastUpdateMicros* +
*optional* + *read-only*\ \|Update time (micros) for last change made to
an firewall object. time.\|integer(int64) \|\ *name* +
*optional*\ \|Name of object.\|string \|\ *partition* +
*optional*\ \|BIGIP partition this object exists.\|string
\|\ *rulesCollectionReference* + *optional*\ \|Reference link to
firewall rules assigned to this firewall
object.\|<<\_properties\_firewall\_rulescollectionreference,rulesCollectionReference>>
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
firewall object.\|string \|===

[[\_properties\_firewall\_rulescollectionreference]]
*rulesCollectionReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \| Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to rules collection object. (In-line rules for firewalls not
supported.)\|string \|===

[[\_properties\_firewall\_collection]] ===
properties\_firewall\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a firewall
collection object-generation.\|integer(int64) \|\ *items* +
*optional*\ \|Collection of firewall-properties.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for this
firewall collection object.\|string \|\ *lastUpdateMicros* + *optional*
+ *read-only*\ \|Update time (micros) for last change made to an
firewall collection object-time.\|integer(int64) \|\ *selfLink* +
*optional* + *read-only*\ \|A reference link URI to the firewall
collection object.\|string \|===
