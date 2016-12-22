= BIG-IQ ASM Signatures

[[\_overview]] == Overview API used to list all ASM signatures.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/asm/working-config
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_signatures\_get]] === List all ASM signatures as a collection. ....
GET /signatures ....

==== Description Returns the collection of ASM signatures.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of ASM
signatures.\|<<\_properties\_signature\_collection,properties\_signature\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_signatures\_objectid\_get]] === Used to get a single instance of a
ASM signature object. .... GET /signatures/{objectId} ....

==== Description Returns a ASM signature object identified by id for an
endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id associated with the
signature.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|ASM signature
object.\|<<\_properties\_signature,properties\_signature>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection if attack signatures.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for ASM web
application security signatures -
cm:asm:working-config:signatures:signaturecollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of attack signatures.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for ASM web
application security signatures -
cm:asm:working-config:signatures:signaturecollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_properties\_signature]] === properties\_signature

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *accuracy* + *optional*\ \|Indicates the
ability of the attack signature to identify the attack including
susceptibility to false-positive alarms: Low: Indicates a high
likelihood of false positives. Medium: Indicates some likelihood of
false positives. High: Indicates a low likelihood of false
positives.\|string \|\ *attackTypeReference* + *optional*\ \|Reference
link to attack type properties. ex. uuid, name,
bigipAttackId\|<<\_properties\_signature\_attacktypereference,attackTypeReference>>
\|\ *bundleVersion* + *optional*\ \|Indicates the bundle version of the
attack signature.\|integer \|\ *description* + *optional*\ \|Description
of ASM attack signature.\|string \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a ASM attack
signature object. generation.\|integer(int64) \|\ *id* +
*optional*\ \|Unique id assocaited with ASM attack signature.\|string
\|\ *isUserDefined* + *optional*\ \|Is this ASM signature created by a
user or pre packaged by the system.\|boolean \|\ *lastUpdateMicros* +
*optional* + *read-only*\ \|Update time (micros) for last change made to
a ASM attack signature object. time.\|integer(int64)
\|\ *matchesWihtinJson* + *optional*\ \|A unique id string for the BIGIQ
acting as a device owner.\|boolean \|\ *matchesWithinCookie* +
*optional*\ \|Array of reference links to user used to create
self-service task. mgmt/shared/authz/users/admin\|boolean
\|\ *matchesWithinGwt* + *optional*\ \|Type information for this
self-service task object.\|boolean(kind) \|\ *matchesWithinParameter* +
*optional*\ \|Use this built-in filter to display only signatures that
match the attack type that you select.\|boolean
\|\ *matchesWithinPlainText* + *optional*\ \|Type information for this
self-service task object.\|boolean(kind) \|\ *matchesWithinRequest* +
*optional*\ \|Type information for this self-service task
object.\|boolean(kind) \|\ *matchesWithinUri* + *optional*\ \|Type
information for this self-service task object.\|boolean(kind)
\|\ *matchesWithinXml* + *optional*\ \|Type information for this
self-service task object.\|boolean(kind) \|\ *modificationDateMicros* +
*optional*\ \|Type information for this self-service task
object.\|integer \|\ *name* + *optional*\ \|Name of ASM attack
signature.\|string \|\ *partition* + *optional*\ \|BIGIP partition this
ASM attack signature object exists.\|string \|\ *revision* +
*optional*\ \|BIG-IQ maintains a version # to track changes of ASM
signatures.\|string \|\ *risk* + *optional*\ \|Indicates the level of
potential damage this attack might cause if it is successful: Low:
Indicates the attack does not cause direct damage or reveal highly
sensitive data. Medium: Indicates the attack may reveal sensitive data
or cause moderate damage. High: Indicates the attack may cause a full
system compromise.\|string \|\ *selfLink* + *optional* +
*read-only*\ \|A reference link URI to the ASM attack signature
object.\|string \|\ *signatureId* + *optional* + *read-only*\ \|Unique
id assigned to a ASM signature object.\|string \|\ *signatureType* +
*optional*\ \|Attack types describes common web application attacks that
signatures can detect. Table 11.1 lists types -
https://support.f5.com/kb/en-us/products/big-ip\_asm/manuals/product/config\_guide\_asm\_10\_2\_0/asm\_attack\_sigs.html\|string
\|\ *systems* + *optional*\ \|Displays which systems (for example web
applications, web servers databases, and application frameworks) the
signature protects.\|< <<\_properties\_signature\_systems,systems>> >
array \|===

[[\_properties\_signature\_attacktypereference]] *attackTypeReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
attack type.\|string \|===

[[\_properties\_signature\_systems]] *systems*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *systemReference* +
*optional*\ \|Reference link to ASM
system.\|<<\_properties\_signature\_systemreference,systemReference>>
\|===

[[\_properties\_signature\_systemreference]] *systemReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
ASM system.\|string \|===

[[\_properties\_signature\_collection]] ===
properties\_signature\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to web application
security signatures collection object. generation.\|integer(int64)
\|\ *items* + *optional*\ \|Collection of ASM attack signatures.\|<
object > array \|\ *kind* + *optional* + *read-only*\ \|Type information
for web application security signatures collection object.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to web application security signatures
collection object. time.\|integer(int64) \|\ *selfLink* + *optional* +
*read-only*\ \|A reference link URI to web application security
signatures collection object.\|string \|===
