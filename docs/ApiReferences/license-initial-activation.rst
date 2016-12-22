= BIG-IQ Licensing inital activation.

[[\_overview]] == Overview API used activate a BIG-IP license of varying
types.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* :
/mgmt/cm/device/licensing/pool/ *Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_initial-activation\_post]] === BIG-IQ initial activation using API.
.... POST /initial-activation ....

==== Description Using this BIG-IQ API you can activate a BIG-IP license
of varying types. This endpoint is a common starting point for
activating a pool-style regkey (utility, volume, purchased, etc..)

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"regkey": "MY-REGISTRATION-KEY", "name": "freeform name", "status":
"ACTIVATING\_AUTOMATIC"}\|<<\_post\_initial\_activation\_body,post\_initial\_activation\_body>>\|
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to create license activation
task.\|<<\_properties\_initial\_activation,properties\_initial\_activation>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_initial-activation\_get]] === BIG-IQ initial activation using API.
.... GET /initial-activation ....

==== Description Using this BIG-IQ API you can activate a BIG-IP license
of varying types. This endpoint is a common starting point for
activating a pool-style regkey (utility, volume, purchased, etc..)

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to create license activation
task.\|<<\_properties\_initial\_activation\_collection,properties\_initial\_activation\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_initial-activation\_objectid\_get]] === BIG-IQ returns the
activation task using for licensing. .... GET
/initial-activation/{objectId} ....

==== Description Returns the activation task allowing the user to poll
for status.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to activation task.\|string(UUID)\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|BIG-IQ activation
task.\|<<\_properties\_initial\_activation,properties\_initial\_activation>>
\|\ *400*\ \|Server error response Bad
Request.\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of activation task objects\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for initial
activation task -
cm:device:licensing:pool:initial-activation:initialactivationworkercollectionstate\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of activation task objects.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for initial
activation task -
cm:device:licensing:pool:initial-activation:initialactivationworkercollectionstate\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_post\_initial\_activation\_body]] ===
post\_initial\_activation\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *name* + *optional*\ \|Name of
activation process.\|string \|\ *regKey* + *optional*\ \|Base
registration key.\|string \|\ *status* + *optional*\ \|The state or type
of activation process to use. ex. ACTIVATING\_AUTOMATIC.\|string \|===

[[\_properties\_initial\_activation]] ===
properties\_initial\_activation

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *items* + *optional*\ \|Activation task
properties.\|< <<\_properties\_initial\_activation\_items,items>> >
array \|===

[[\_properties\_initial\_activation\_items]] *items*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *dossier* + *optional*\ \|Auto-generated
passphrase used for activation.\|string \|\ *encryptedPrivateKey* +
*optional*\ \|Encrypted private key used during calculation.\|< integer
> array \|\ *generation* + *optional*\ \|A integer that will track
change made.\|string \|\ *internalPrivateKey* + *optional*\ \|Internal
encrypted key used during calculation.\|string \|\ *kind* +
*optional*\ \|Type information for initial activation.
cm:device:licensing:pool:initial-activation:initialactivationworkeritemstate.\|string
\|\ *lastUpdateMicros* + *optional*\ \|Update time (micros) for last
change made to a activation task.\|integer \|\ *licenseReference* +
*optional*\ \|Reference link to pool license used for
activation.\|<<\_properties\_initial\_activation\_licensereference,licenseReference>>
\|\ *licenseText* + *optional*\ \|Contents of license file.\|string
\|\ *message* + *optional*\ \|Status message to user. ex. License
BASE-REG-KEY ready.\|string \|\ *name* + *optional*\ \|Name of initial
activation task license type. ex. Purchased-Pools\|string
\|\ *publicKey* + *optional*\ \|Public key used during calculation.\|<
integer > array \|\ *regKey* + *optional*\ \|Base registration
key.\|string \|\ *selfLink* + *optional*\ \|Reference link to activation
task.\|string \|\ *sortName* + *optional*\ \|Name used to intentify
sorting status. ex. Pending\|string \|\ *status* + *optional*\ \|Status
of license key activation. ex. READY\|string \|===

[[\_properties\_initial\_activation\_licensereference]]
*licenseReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
license data.\|string \|===

[[\_properties\_initial\_activation\_collection]] ===
properties\_initial\_activation\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional*\ \|A integer
that will track change made.\|string \|\ *items* + *optional*\ \|Array
of initial activation task properties.\|< object > array \|\ *kind* +
*optional*\ \|Type information for initial activation task.
cm:device:licensing:pool:initial-activation:initialactivationworkeritemstate\|string
\|\ *lastUpdateMicros* + *optional*\ \|Update time (micros) for last
change made to a initial activation task object. time.\|string
\|\ *selfLink* + *optional*\ \|Reference link to initial activation task
object.\|string \|===
