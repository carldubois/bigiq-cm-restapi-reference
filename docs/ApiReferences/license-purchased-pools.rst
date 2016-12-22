= BIG-IQ licensing - Purchased Pools.

[[\_overview]] == Overview API used to license BIG-IP devices via a
purchased licensed pool.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* :
/mgmt/cm/device/licensing/pool/purchased-pool *Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_pools\_get]] === GET the BIG-IQ purchased license pools. .... GET
/licenses ....

==== Description Returns a BIG-IQ purchaced license pools allowing an
administrator to license BIG-IP devices.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET BIG-IQ purchased license
pools.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_pools\_objectid\_get]] === Used to GET a purchased license pool.
.... GET /licenses/{objectId} ....

==== Description Returns a purchased licensed pool object identified by
id for an endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to purchased licensed pool
object.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Purchased license pool object
returned.\|<<\_properties\_purchased\_pool,properties\_purchased\_pool>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_pools\_objectid\_members\_post]] === License a BIG-IP device and add
to purchased license pool members. .... POST
/licenses/{objectId}/members ....

==== Description Invoke a task to license a BIG-IP and add to this
specific purchased license pool as a member to the pool.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to license purchased pool
object.\|string(UUID)\|None \|\ *Body*\ \|\ *Json string request body.*
+ *required*\ \|Input parameter list in json format. Ex.
{"deviceAddress": "bigip\_address","username": "admin","password":
"admin"}
\|<<\_post\_purchased\_pool\_body,post\_purchased\_pool\_body>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a device level task to
license a BIG-IP
device.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_pools\_objectid\_members\_get]] === Used to GET purchased license
pool members. .... GET /pools/{objectId}/members ....

==== Description Returns all members (BIG-IP) devices that are assingned
to this purchased license pool. Each are identified by id/members for an
endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to purchased license pool
object.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Purchased license pool members
object
returned.\|<<\_properties\_purchased\_pool,properties\_purchased\_pool>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of purchased license pool objects.\|< object >
array \|\ *kind* + *optional* + *read-only*\ \|Type information for
purchased license pools -
cm:shared:licensing:pools:licensepoolworkerstate.\|string \|\ *message*
+ *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of purchased license pool objects.\|< object >
array \|\ *kind* + *optional* + *read-only*\ \|Type information for
purchased license pools -
cm:shared:licensing:pools:licensepoolworkerstate.\|string \|\ *message*
+ *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_post\_purchased\_pool\_body]] === post\_purchased\_pool\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *deviceAddress* + *required*\ \|IP
Address of BIGIP you wish to license.\|string \|\ *username* +
*required*\ \|Username of BIGIP you wish to license.\|string
\|\ *password* + *required*\ \|Password of BIGIP you wish to
license.\|string \|===

[[\_properties\_collection]] === properties\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a purchased
license pool collection object. generation.\|integer(int64) \|\ *items*
+ *optional*\ \|Collection of purchased license pool objects.\|< object
> array \|\ *kind* + *optional* + *read-only*\ \|Type information for a
purchased license pool collection object.\|string \|\ *lastUpdateMicros*
+ *optional* + *read-only*\ \|Update time (micros) for last change made
to an purchaced license pool collection object. time.\|integer(int64)
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to a
purchased license pool collection object.\|string \|===

[[\_properties\_purchased\_pool]] === properties\_purchased\_pool

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *baseRegKey* + *optional*\ \|Based
Registration Key used to (re) activate purchased license pool.\|string
\|\ *freeDeviceLicenses* + *read-only*\ \|Total number of free device
licenses for this purchased license pool.\|integer \|\ *generation* +
*optional* + *read-only*\ \|A integer that will track change made to a
purchased license pool object. generation.\|integer(int64)
\|\ *isInternal* + *BIG-IQ use only*\ \|Is this purchased licensed pool
internal to BIG-IQ.\|boolean \|\ *kind* + *optional* +
*read-only*\ \|Type information for this purchased license pool
object.\|string \|\ *lastUpdateMicros* + *optional* +
*read-only*\ \|Update time (micros) for last change made to an purchased
license pool object. time.\|integer(int64) \|\ *licenseState* +
*read-only*\ \|State representation of what is returned from the license
server.\|<<\_properties\_purchased\_pool\_licensestate,licenseState>>
\|\ *licenseText* + *optional* + *read-only*\ \|Contents of licensed
purchased pool. Spefices for purchased license pool such as Auth
version, Tech support info, license tokens, keys etc..\|string
\|\ *method* + *optional*\ \|Activation method used. (Example - MANUAL /
AUTOMATIC)\|string \|\ *name* + *optional*\ \|Name of purchased license
pool object.\|string \|\ *privateKey* + *optional*\ \|Private key
cryptography keys which are known only to the owner.\|string
\|\ *publicKey* + *optional*\ \|Public key cryptography which may be
disseminated widely.\|< integer > array \|\ *registeredKey* +
*optional*\ \|Registered key post cryptography response from server.\|<
integer > array \|\ *selfLink* + *optional* + *read-only*\ \|Reference
link to ppurchased licensed pool.\|string \|\ *sortName* +
*optional*\ \|Sort string based on BIG-IQ licensing type. (Purchased
Pool)\|string \|\ *state* + *optional*\ \|State of license for purchaced
license pool. (Example - LICENSED)\|string \|\ *totalDeviceLicenses* +
*optional*\ \|Total number of device licenses for this purchased license
pool.\|integer \|\ *uuid* + *optional* + *read-only*\ \|Unique id
assigned to a purchased license pool object.\|string \|===

[[\_properties\_purchased\_pool\_licensestate]] *licenseState*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *activeModules* + *optional*\ \|Modules
activivated for purchased license pool. (Example - VEP1, LTM, 1G, 4
Instances\|V092327-5105381\|IPV6 Gateway\|Rate Shaping\|Ram Cache)\|<
string > array \|\ *authVers* + *optional*\ \|Version of authentication
used by BIG-IQ. (Example - 5b)\|string \|\ *authorization* +
*optional*\ \|Authorization string used by purchased license pool.
Response from license server.\|string \|\ *dossier* +
*optional*\ \|Dossier generated for this purchased license pool.
Response from license server.\|string \|\ *evaluationEndDateTime* +
*optional*\ \|End date and time a license server evaluate took place
(Format - 2016-10-26T00:00:00-04:00)\|string
\|\ *evaluationStartDateTime* + *optional*\ \|Start date and time a
license server evaluate took place (Format -
2016-10-26T00:00:00-04:00)\|string \|\ *exclusivePlatform* +
*optional*\ \|Platfrom description response from server. (Example -
BIG-IQ Pool, Z100, Z100H, Z100K, Z100x)\|< string > array
\|\ *featureFlags* + *optional*\ \|Descritive flags avalible to
purchased license pools.\|<
<<\_properties\_purchased\_pool\_featureflags,featureFlags>> > array
\|\ *licenseDateTime* + *optional*\ \|Date and time license was
generated. (Format - 2016-10-26T00:00:00-04:00)\|string
\|\ *licenseEndDateTime* + *optional*\ \|End date and time a license was
instatiated on BIG-IQ (Format - 2016-10-26T00:00:00-04:00)\|string
\|\ *licenseStartDateTime* + *optional*\ \|Start date and time a license
was instatiated on BIG-IQ (Format - 2016-10-26T00:00:00-04:00)\|string
\|\ *licenseVersion* + *optional*\ \|Version of BIG-IQ this license is
generated for. (Example - 5.1.0)\|string \|\ *optionalModules* +
*optional*\ \|Modules that are optional for purchased license pool.
(Example - VEP1, LTM, 1G, Add 25 Instances)\|< string > array
\|\ *platformId* + *optional*\ \|Type of BIG-IQ platform information.
(Example - BIG-IQ Pool)\|string \|\ *registrationKey* +
*optional*\ \|Registration Key used by this purchased license pool.
Response from license server.\|string \|\ *serviceCheckDateTime* +
*optional*\ \|Data and time the last service check status request /
respose occur from server. (Format - 2016-10-26T00:00:00-04:00)\|string
\|\ *serviceStatus* + *optional*\ \|Server response describing service
status. (Example - As of 2016-10-26 this system has an active service
contract.)\|string \|\ *usage* + *optional*\ \|Organization usage data.
Example - F5 Internal Product Development\|string \|\ *vendor* +
*optional*\ \|Company Name. Example F5 Networks, Inc.\|string \|===

[[\_properties\_purchased\_pool\_featureflags]] *featureFlags*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *featureName* + *optional*\ \|Name of
feature. (Example - purchased\_license\_pool\_count,
apm\_urlf\_limited\_session, apm\_web\_applications)\|string
\|\ *featureValue* + *optional*\ \|Weighted value for each feature.
(Example - 10)\|string \|===
