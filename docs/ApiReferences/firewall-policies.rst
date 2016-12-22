= BIG-IQ Firewall Policy API

[[\_overview]] == Overview API used to create and modify firewall
policies on BIG-IQ

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* :
/mgmt/cm/firewalls/working-config *Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_policies\_get]] === List of policy collections. .... GET /policies
....

==== Description Returns the collection of firewall policies.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of firewall
policies.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_policies\_objectid\_get]] === Used to get a single firewall policy.
.... GET /policies/{objectId} ....

==== Description Returns the firewall policy identified by id for an
endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Policy object ID\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Firewall policy
object.\|<<\_properties\_policy,properties\_policy>> \|\ *400*\ \|Server
error response "Bad Request".\|<<\_error\_collection,error\_collection>>
\|===

[[\_policies\_objectid\_rules\_get]] === Used to get the rules for a
firewall policy. .... GET /policies/{objectId}/rules ....

==== Description Returns the firewall rules subcollection for a policy.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Collection of policy rule object id\|string(UUID)\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of firewall
rules.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_properties\_collection,properties\_collection>> \|===

[[\_policies\_objectid\_rules\_objectid\_get]] === Get a single rule for
a firewall policy. .... GET /policies/{objectId}/rules/{objectId} ....

==== Description Returns the firewall rule identified by a endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Policy object id\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Firewall rule
object\|<<\_properties\_rule,properties\_rule>> \|\ *400*\ \|Error
response "Bad Request"\|<<\_error\_collection,error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_error\_collection]] === error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of policies-error.\|< object > array \|\ *kind*
+ *optional* + *read-only*\ \|Type information for policy
object.\|string \|\ *message* + *optional* + *read-only*\ \|Error
message returned from server.\|string \|\ *requestBody* + *optional* +
*read-only*\ \|The data in the request body. GET (None)\|string
\|\ *requestOperationId* + *optional* + *read-only*\ \|Unique id
assigned to rest operation.\|integer(int64) \|===

[[\_properties\_collection]] === properties\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a policy object.
generation.\|integer(int64) \|\ *items* + *optional*\ \|Collection of
policies-properties.\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for this policy object.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an policy object. time.\|integer(int64)
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
policy object.\|string \|===

[[\_properties\_policy]] === properties\_policy

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *description* +
*optional*\ \|Description of object.\|string \|\ *generation* +
*optional* + *read-only*\ \|A integer that will track change made to a
policy object. generation.\|integer(int64) \|\ *id* + *optional* +
*read-only*\ \|Unique id assigned to a policy object.\|string \|\ *kind*
+ *optional* + *read-only*\ \|Type information for this policy
object.\|string \|\ *lastUpdateMicros* + *optional* +
*read-only*\ \|Update time (micros) for last change made to an policy
object. time.\|integer(int64) \|\ *name* + *optional*\ \|Name of
object.\|string \|\ *partition* + *optional*\ \|BIGIP partition this
object exists.\|string \|\ *rulesCollectionReference* +
*optional*\ \|Reference link to firewall rules assigned to this policy
object.\|<<\_properties\_policy\_rulescollectionreference,rulesCollectionReference>>
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
policy object.\|string \|===

[[\_properties\_policy\_rulescollectionreference]]
*rulesCollectionReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to rules collection object.\|string \|===

[[\_properties\_rule]] === properties\_rule

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *optional*\ \|Action taken
for rule match (accept, accept-decisively, drop, reject).\|string
\|\ *destination* + *optional*\ \|Destination object used by rule,
usually specified by (address-list, address, address-range, domain-name,
country/region).\|object \|\ *evalOrder* + *optional*\ \|Order in which
server evaluates rules referenced in a policy object.\|integer
\|\ *generation* + *optional* + *read-only*\ \|A integer that will track
change made to a policy rule object. generation.\|integer(int64)
\|\ *hitCountStatReference* + *optional*\ \|Reference link to a object
that maintains an interger for rule hit counts.\|object \|\ *iRule* +
*optional*\ \|Link to F5 iRule to a firewall policy.\|string
\|\ *iRuleSampleRate* + *optional*\ \|Sample rate of iRule.\|integer
\|\ *id* + *optional* + *read-only*\ \|Unique id assigned to a policy
rule object.\|string \|\ *kind* + *optional* + *read-only*\ \|Type
information for this policy rule object.\|string \|\ *lastUpdateMicros*
+ *optional* + *read-only*\ \|pdate time (micros) for last change made
to an policy rule object. time.\|integer(int64) \|\ *log* +
*optional*\ \|Boolean used to enable / disable server logging for
actions taken on packets.\|boolean \|\ *name* + *optional*\ \|Name of
the policy rule object.\|string \|\ *protocol* + *optional*\ \|IP
protocol to match against packet.\|string \|\ *ruleListReference* +
*optional*\ \|Reference link to a rule-list object (list of rules
managed in a single object.)\|object \|\ *scheduleReference* +
*optional*\ \|Reference link to a schedule object used by this policy
object.\|object \|\ *selfLink* + *optional* + *read-only*\ \|A reference
link URI to the policy rule object.\|string \|\ *servicePolicyReference*
+ *optional*\ \|Reference link to a service-policy object (used as a
container for network idle timers and/or port misuse policies).\|object
\|\ *source* + *optional*\ \|Source object used by rule, usually
specified by (address-list, address, address-range, domain-name,
country/region).\|object \|\ *state* + *optional*\ \|State of rule.
(disabled, enabled, scheduled)\|string \|===
