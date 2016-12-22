= BIG-IQ LTM Virtual Server.

[[\_overview]] == Overview API used to create/manage LTM virutal server.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* :
/mgmt/cm/adc-core/working-config/ltm *Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_virtual\_post]] === Create a LTM virtual server. .... POST /virtual
....

==== Description POST to create a BIGIP virtual server.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST a BIGIP virtual
server.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_virtual\_get]] === List all virtual server items as a collection.
.... GET /virtual ....

==== Description Returns the collection of virtual servers.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Collection of virtual
servers.\|<<\_properties\_collection,properties\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_virtual\_objectid\_get]] === Used to get a single virtual server
object. .... GET /virtual/{objectId} ....

==== Description Returns the virtual server object identified by id for
an endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id assigned to a virtual
server.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|Virtual Server
object.\|<<\_properties\_virtual,properties\_virtual>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response "Public URI path not
registered."\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of virtual servers. Errored response from
server.\|< object > array \|\ *kind* + *optional* + *read-only*\ \|Type
information for LTM virtual servers - errors
cm:adc-core:working-config:ltm:virtual:adcvirtualcollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of virtual servers. Errored response from
server.\|< object > array \|\ *kind* + *optional* + *read-only*\ \|Type
information for virtual server -
cm:adc-core:working-config:ltm:virtual:adcvirtualcollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_properties\_collection]] === properties\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a virtual server
collection object. generation.\|integer(int64) \|\ *items* +
*optional*\ \|A collection of virtual servers. Properties defining
items.\|< object > array \|\ *kind* + *optional* + *read-only*\ \|Type
information for this virutal servers collection object -
cm:adc-core:working-config:ltm:virtual:adcvirtualcollectionstate.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an virtual server collection object.
time.\|integer(int64) \|\ *selfLink* + *optional* + *read-only*\ \|A
reference link URI to the virtual server collection object.\|string
\|===

[[\_properties\_virtual]] === properties\_virtual

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *addressStatus* +
*optional*\ \|Specither the virtual will contribute to the operational
status of the associated virtual-address. The default is 'yes'.\|string
\|\ *autoLasthop* + *optional*\ \|Specifies whether to automatically map
last hop for pools or not. The default is to use next level's
default.\|string \|\ *connectionLimit* + *optional*\ \|Specifies the
maximum number of concurrent connections you want to allow for the
virtual server.\|integer \|\ *defaultCookiePersistenceReference* +
*optional*\ \|Reference link to profiles that the virtual server uses to
manage connection
persistence.\|<<\_properties\_virtual\_defaultcookiepersistencereference,defaultCookiePersistenceReference>>
\|\ *description* + *optional*\ \|Description of LTM virtual
server.\|string \|\ *destinationFullPath* + *optional*\ \|Destination
address / port used for client access - ex. 10.44.100.100:80.\|string
\|\ *deviceReference* + *optional*\ \|Reference link to BIGIP device
assiociated to virtual
server.\|<<\_properties\_virtual\_devicereference,deviceReference>>
\|\ *fallbackSourceAddrPersistenceReference* + *optional*\ \|Reference
link fallback persistence profile for the virtual server to use when the
default persistence profile is not
available.\|<<\_properties\_virtual\_fallbacksourceaddrpersistencereference,fallbackSourceAddrPersistenceReference>>
\|\ *generation* + *optional* + *read-only*\ \|A integer that will track
change made to a LTM virtual server object. -
generation.\|integer(int64) \|\ *gtmScore* + *optional*\ \|Specifies a
score that is associated with the virtual server. Global Traffic Manager
(GTM) can rely on this value to load balance traffic in a proportional
manner.\|integer \|\ *id* + *optional* + *read-only*\ \|Unique id
assigned to a virtual server object.\|string \|\ *ipProtocol* +
*optional*\ \|Specifies the IP protocol for which you want the virtual
server to direct traffic. Sample protocol names are tcp and udp.\|string
\|\ *kind* + *optional*\ \|Type information for this virutal server
object. cm:adc-core:working-config:ltm:virtual:adcvirtualstate\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an LTN virtual server object -
time.\|integer(int64) \|\ *mask* + *optional*\ \|Destination netmask
used for client access - ex. 255.255.255.255 or 32.\|string \|\ *mirror*
+ *optional*\ \|Enables or disables state mirroring. You can use state
mirroring to maintain the same state information in the standby unit
that is in the active unit, allowing transactions such as FTP file
transfers to continue as though uninterrupted. The default value is
disabled.\|string \|\ *name* + *optional*\ \|Name of LTM virtual
server.\|string \|\ *nat64* + *optional*\ \|Specifies whether this
virtual does NAT64 translation.\|string \|\ *partition* +
*optional*\ \|Displays the administrative partition within which this
virtual server profile resides.\|string \|\ *poolReference* +
*optional*\ \|Reference link to virtual pool in which you want the
virtual server to automatically direct
traffic.\|<<\_properties\_virtual\_poolreference,poolReference>>
\|\ *profilesCollectionReference* + *optional*\ \|Reference link to
profiles for the virtual server to use when directing and managing
traffic.\|<<\_properties\_virtual\_profilescollectionreference,profilesCollectionReference>>
\|\ *rateLimit* + *optional*\ \|Specifies the maximum number of
connections per second allowed for a virtual server. The default value
is disabled.\|string \|\ *rateLimitMode* + *optional*\ \|Indicates
whether the rate limit is applied per virtual object, per source
address, per destination address, or some combination thereof. The
default value is object, which does not use the source or destination
address as part of the key.\|string \|\ *selfLink* + *optional* +
*read-only*\ \|A reference link URI to the LTM virtual server
object.\|string \|\ *sourceAddress* + *optional*\ \|Source address used
for client access to virtual server object.\|string
\|\ *sourceAddressTranslation* + *optional*\ \|Type of address
translation pool used for implementing selective and intellegent source
address
translation.\|<<\_properties\_virtual\_sourceaddresstranslation,sourceAddressTranslation>>
\|\ *sourcePort* + *optional*\ \|Specifies whether the system preserves
the source port of the connection. The default is preserve. Use of the
preserve-strict setting should be restricted to UDP only under very
special circumstances such as nPath or transparent (that is, no
translation of any other L3/L3 field), where there is a 1:1 relationship
between virtual IP addresses and node addresses, or when clustered
multi-processing (CMP) is disabled. The change setting is useful for
obfuscating internal network addresses.\|string \|\ *state* +
*optional*\ \|State of virtual server. enabled / disabled.\|string
\|\ *subPath* + *optional*\ \|Path to virtual server. Partition /
app.app. ex. Common /app-service\_1.app\|string \|\ *translatePort* +
*optional*\ \|Enables or disables port translation. Turn port
translation off for a virtual server if you want to use the virtual
server to load balance. connections to any service.\|string
\|\ *vlansEnabled* + *optional*\ \|Enables the virtual server on the
VLANs specified by the VLANs option.\|string \|===

[[\_properties\_virtual\_defaultcookiepersistencereference]]
*defaultCookiePersistenceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
profiles that the virtual server uses to manage connection
persistence.\|string \|===

[[\_properties\_virtual\_devicereference]] *deviceReference*

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

[[\_properties\_virtual\_fallbacksourceaddrpersistencereference]]
*fallbackSourceAddrPersistenceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link
fallback persistence profile for the virtual server to use when the
default persistence profile is not available.\|string \|===

[[\_properties\_virtual\_poolreference]] *poolReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
virtual pool in which you want the virtual server to automatically
direct traffic.\|string \|===

[[\_properties\_virtual\_profilescollectionreference]]
*profilesCollectionReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is
this a collection of objects. In this case profiles. default:
true\|boolean \|\ *link* + *optional*\ \|Reference link to profiles for
the virtual server to use when directing and managing traffic.\|string
\|===

[[\_properties\_virtual\_sourceaddresstranslation]]
*sourceAddressTranslation*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *type* + *optional*\ \|Type of address
translation pool used for implementing selective and intellegent source
address translation.\|string \|===
