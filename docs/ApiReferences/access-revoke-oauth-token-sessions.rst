= BIG-IQ APM OAuth Token Revocation on BIG-IP devices.

[[\_overview]] == Overview API for OAuth Token Revocation on BIG-IP
devices using a BIG-IQ centralized management system.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/access/tasks
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_revoke-tokens\_access-groups\_post]] === Revoke all oauth token by
access groups for a specified user. .... POST /revoke-tokens
(access-groups) ....

==== Description Revoke all active oauth tokens by access groups by a
specified user.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"action":"REVOKE\_TOKEN\_FOR\_USER", "userName":"user1",
"accessGroupNames":["TestGroup1",
"TestGroup2"]}\|<<\_post\_revoke\_oauth\_token\_by\_access\_group,post\_revoke\_oauth\_token\_by\_access\_group>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to revoke all oauth tokens
by access
group.\|<<\_properties\_revoke\_oauth\_token,properties\_revoke\_oauth\_token>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_access-groups\_get]] === List all oauth token
revocation tasks as part of a collection. .... GET /revoke-tokens ....

==== Description Returns the collection of oauth token revocation tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of oauth token
revocation
tasks.\|<<\_properties\_revoke\_oauth\_token\_collection,properties\_revoke\_oauth\_token\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_bigip\_clusters\_post]] === Revoke all oauth-token
sessions by cluster-name match for a specified user. .... POST
/revoke-tokens (bigip clusters) ....

==== Description Revoke all oauth-token sessions by cluster-name match
for specified devices.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"action":"REVOKE\_TOKEN\_FOR\_USER", "userName":"user1",
"clusterNames":["BlueCluster",
"RedCluster"]}\|<<\_post\_revoke\_oauth\_token\_by\_cluster\_name,post\_revoke\_oauth\_token\_by\_cluster\_name>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to revoke oauth-token
sessions within a cluster-name for a specfic
device.\|<<\_properties\_revoke\_oauth\_token,properties\_revoke\_oauth\_token>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_bigip\_clusters\_get]] === List all
revoke-oauth-token tasks as part of a collection. .... GET
/revoke-tokens ....

==== Description Returns the collection of revoke-oauth-token tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of
revoke-oauth-token
tasks.\|<<\_properties\_revoke\_oauth\_token\_collection,properties\_revoke\_oauth\_token\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_bigip\_clusters\_access-groups\_and\_device\_reference\_post]]
=== Revoke all oauth-token sessions by access group, cluster name and
device reference match for a specified user. .... POST /revoke-tokens
(bigip clusters, access-groups and device reference) ....

==== Description Revoke all oauth-token sessions by access group,
cluster name match for specified devices.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"action":"REVOKE\_TOKEN\_FOR\_USER", "userName":"user1",
"accessGroupNames":["TestGroup1", "TestGroup2"],
"clusterNames":["BlueCluster", "RedCluster"], "deviceReferences":
[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"},{"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"}]}\|<<\_post\_revoke\_oauth\_token\_by\_cluster\_name\_access\_group\_device\_reference,post\_revoke\_oauth\_token\_by\_cluster\_name\_access\_group\_device\_reference>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to revoke oauth-token
sessions within a access-group and cluster-name for a specfic
device.\|<<\_properties\_revoke\_oauth\_token,properties\_revoke\_oauth\_token>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_bigip\_clusters\_access-groups\_and\_device\_reference\_get]]
=== List all revoke-oauth-token tasks as part of a collection. .... GET
/revoke-tokens ....

==== Description Returns the collection of revoke-oauth-token tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of
revoke-oauth-token
tasks.\|<<\_properties\_revoke\_oauth\_token\_collection,properties\_revoke\_oauth\_token\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_oauth\_token\_id\_post]] === Revoke-oauth-token by
oauth client id. .... POST /revoke-tokens (oauth client id) ....

==== Description Revoke-oauth-token sessions by oauth token id for a
device.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"action":"REVOKE\_TOKEN\_FOR\_CLIENT\_ID",
"clientId":"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457",
"deviceReferences":[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"}]}\|<<\_post\_revoke\_oauth\_token\_by\_oauth\_id,post\_revoke\_oauth\_token\_by\_oauth\_id>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to revoke-oauth-token
sessions by oauth token
id.\|<<\_properties\_revoke\_oauth\_token,properties\_revoke\_oauth\_token>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_oauth\_token\_id\_get]] === List all
revoke-oauth-token tasks as part of a collection. .... GET
/revoke-tokens ....

==== Description Returns the collection of revoke-oauth-token tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of
revoke-oauth-token
tasks.\|<<\_properties\_revoke\_oauth\_token\_collection,properties\_revoke\_oauth\_token\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_user\_post]] === Revoke all oauth token by user. ....
POST /revoke-tokens (user) ....

==== Description Revoke all active oauth tokens by user.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. { "action":"REVOKE\_TOKEN\_FOR\_USER", "userName":"user1",
"deviceReferences":[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"}]}\|<<\_post\_revoke\_oauth\_token\_by\_user\_body,post\_revoke\_oauth\_token\_by\_user\_body>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to revoke all oauth tokens
by
user.\|<<\_properties\_revoke\_oauth\_token,properties\_revoke\_oauth\_token>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_user\_get]] === List all oauth token revocation tasks
as part of a collection. .... GET /revoke-tokens ....

==== Description Returns the collection of oauth token revocation tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of oauth token
revocation
tasks.\|<<\_properties\_revoke\_oauth\_token\_collection,properties\_revoke\_oauth\_token\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_list\_of\_tokens\_post]] === Revoke a list oauth
token by user. .... POST /revoke-tokens (list of tokens) ....

==== Description Revoke a list of active oauth tokens for a specified
user.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"action":"REVOKE\_LIST\_OF\_TOKENS", "perDeviceOauthIds":
[{"oauthIds": [{"id":
"da6d57ffab9decbe9d75b7fdd4440ad43bedc7a475f3105b", "clientId":
"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"}, {"id":
"0df998ae62ace6fb6a82bb745b8586e7306afb94e3ca146a", "clientId":
"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457"}], "deviceReference":
{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"}},
{ "oauthIds": [{"id":
"e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457", "clientId":
"bb745b8586e7306afb94"}, {"id": "8586e7306afb8586e7306afb8586e7306afb",
"clientId": "8ad92cbb970dd500"}], "deviceReference": {
"link":"https://localhost/mgmt/cm/system/machineid-resolver/23h4jkhk324-f405-489f-kj3434-98234"}}]}\|<<\_post\_revoke\_list\_of\_tokens\_body,post\_revoke\_list\_of\_tokens\_body>>\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to revoke a list of active
oauth tokens by
user.\|<<\_properties\_revoke\_oauth\_token,properties\_revoke\_oauth\_token>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_list\_of\_tokens\_get]] === Returns a list of oauth
token by user. .... GET /revoke-tokens ....

==== Description Returns a list of active oauth tokens for a specified
user.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET to revoke a list oauth tokens
by
user.\|<<\_properties\_revoke\_oauth\_token\_collection,properties\_revoke\_oauth\_token\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_revoke-tokens\_objectid\_get]] === Used to get a single instance of
a revoke-oauth-token task. .... GET /revoke-tokens/{objectId} ....

==== Description Returns a object for revoke-oauth-token session task
identified by id for an endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id refering to a token.\|string(UUID)\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|APM revoke-oauth-token task
object.\|<<\_properties\_revoke\_oauth\_token,properties\_revoke\_oauth\_token>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection or list of tokens.\|< object > array \|\ *kind*
+ *optional* + *read-only*\ \|Type information for a collection of tasks
used to revoke-oauth-token sessions -
cm:access:tasks:revoke-tokens:oauthrevoketokentaskcollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection or list of tokens.\|< object > array \|\ *kind*
+ *optional* + *read-only*\ \|Type information for a collection of tasks
used to revoke-oauth-token sessions -
cm:access:tasks:revoke-tokens:oauthrevoketokentaskcollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_post\_revoke\_oauth\_token\_by\_access\_group]] ===
post\_revoke\_oauth\_token\_by\_access\_group

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *accessGroupNames* + *optional*\ \|One
or more access group names. All oauth-token sessions in these groups
will be revoked by invoking task.\|string \|\ *action* +
*required*\ \|Action used to revoke-oauth-token session by
access\_group. ex action. "REVOKE\_TOKEN\_FOR\_USER"\|string
\|\ *userName* + *optional*\ \|User name defined for revoke-oauth-token
sessions owned.\|string \|===

[[\_post\_revoke\_oauth\_token\_by\_cluster\_name]] ===
post\_revoke\_oauth\_token\_by\_cluster\_name

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
revoke-oauth-token session by cluster\_name. ex action.
"REVOKE\_TOKEN\_FOR\_USER"\|string \|\ *clusterName* + *optional*\ \|One
or more cluster names. All oauth token sessions in these bigip clusters
will be revoked by invoking task.\|string \|\ *userName* +
*optional*\ \|User name defined for revoke-oauth-token sessions
owned.\|string \|===

[[\_post\_revoke\_oauth\_token\_by\_cluster\_name\_access\_group\_device\_reference]]
===
post\_revoke\_oauth\_token\_by\_cluster\_name\_access\_group\_device\_reference

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *accessGroupNames* + *optional*\ \|One
or more access group names. All oauth token sessions in these groups
will be revoked by invoking task.\|string \|\ *action* +
*required*\ \|Action used to revoke-oauth-token session by
cluster\_name. ex action. "REVOKE\_TOKEN\_FOR\_USER"\|string
\|\ *clusterNames* + *optional*\ \|One or more cluster names. All oauth
token sessions in these bigip clusters will be revoked by invoking
task.\|string \|\ *deviceReferences* + *optional*\ \|Reference link to
one or more devices in which active revoke-oauth-token sessions
live.\|string \|\ *userName* + *optional*\ \|User name defined to all
revoke-oauth-token sessions owned.\|string \|===

[[\_post\_revoke\_oauth\_token\_by\_oauth\_id]] ===
post\_revoke\_oauth\_token\_by\_oauth\_id

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
revoke-oauth-token identified by a oauth token id. ex.
"REVOKE\_TOKEN\_FOR\_CLIENT\_ID"\|string \|\ *clientId* +
*optional*\ \|Unique id associated with the revoke-oauth-token. ex.
e3f3e7204d00d88ad92cbb970dd5005056b093adfa6d7457\|string \|===

[[\_post\_revoke\_oauth\_token\_by\_user\_body]] ===
post\_revoke\_oauth\_token\_by\_user\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
revoke-oauth-token session by a user. ex.
"REVOKE\_TOKEN\_FOR\_USER"\|string \|\ *deviceReferences* +
*optional*\ \|Reference link to one or more devices in which active
revoke-oauth-token sessions live.\|<
<<\_post\_revoke\_oauth\_token\_by\_user\_body\_devicereferences,deviceReferences>>
> array \|\ *userName* + *optional*\ \|User name defined for
revoke-oauth-tokens owned.\|string \|===

[[\_post\_revoke\_oauth\_token\_by\_user\_body\_devicereferences]]
*deviceReferences*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
device in resolver group.\|string \|===

[[\_post\_revoke\_oauth\_token\_by\_list\_body]] ===
post\_revoke\_oauth\_token\_by\_list\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
revoke-oauth-token by a user. ex. "REVOKE\_LIST\_OF\_TOKENS"\|string
\|\ *perDeviceOauthIds* + *optional*\ \|Device specfic oauth token
id."\|< <<\_per\_device\_oauth\_ids,perDeviceOauthIds>> >array
\|\ *deviceReferences* + *optional*\ \|Reference link to one or more
devices in which active revoke-oauth-token sessions live.\|<
<<\_post\_revoke\_oauth\_token\_by\_user\_body\_devicereferences,deviceReferences>>
> array \|\ *userName* + *optional*\ \|User name defined for
revoke-oauth-token sessions owned.\|string \|===

[[\_post\_revoke\_oauth\_token\_by\_user\_body\_devicereferences]]
*deviceReferences*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
device in resolver group.\|string \|===

[[\_properties\_revoke\_oauth\_token]] ===
properties\_revoke\_oauth\_token

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *accessGroupNames* + *optional*\ \|One
or more access group names. All revoke-oauth-tokens in these groups will
be killed by invoking task.\|string \|\ *action* + *required*\ \|Action
used to revoke-oauth-tokens identified by a oauth token id. ex.
"REVOKE\_TOKEN\_FOR\_CLIENT\_ID" "REVOKE\_TOKEN\_FOR\_USER"\|string
\|\ *clientId* + *optional* + *read-only*\ \|Unique id used as a
reference for client session to BIGIP.\|string \|\ *currentStep* +
*optional* + *read-only*\ \|Current internal step for revoke-oauth-token
task.\|string \|\ *generation* + *optional* + *read-only*\ \|A integer
that will track change made to a revoke-oauth-token task object.
generation.\|integer(int64) \|\ *id* + *optional*\ \|Unique id
assocaited with revoke-oauth-token task object.\|string
\|\ *identityReference* + *optional*\ \|Reference link to the user who
issued the rest call.\|<
<<\_properties\_revoke\_oauth\_token\_identityreference,identityReference>>
> array \|\ *kind* + *optional*\ \|Type information for
revoke-oauth-token task object -
cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to a revoke-oauth-token task object.
time.\|integer(int64) \|\ *name* + *optional*\ \|Name of
revoke-oauth-token session task object.\|string \|\ *ownerMachineId* +
*optional*\ \|Device machine id used by revoke-oauth-token task object.
Sessions that live on this device will be revoked.\|string
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
revoke-oauth-token task object.\|string \|\ *startDateTime* +
*optional*\ \|Date / Time of when this revoke-oauth-token task
began.\|string \|\ *status* + *optional*\ \|Status of revoke-oauth-token
task state. - ex. STARTED, FINISHED.\|string \|\ *userName* +
*optional*\ \|User name defined to all revoke-oauth-tokens
owned.\|string \|\ *userReference* + *optional*\ \|Refernece link to
user issuing the rest call to start revoke-oauth-token task.\|string
\|\ *username* + *optional*\ \|User username.\|string \|===

[[\_properties\_revoke\_oauth\_token\_identityreference]]
*identityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
user indenity.\|string \|===

[[\_properties\_revoke\_oauth\_token\_collection]] ===
properties\_revoke\_oauth\_token\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to
revoke-oauth-tokens task collection object. generation.\|integer(int64)
\|\ *items* + *optional*\ \|Collection of revoke oauth tokens.\|< object
> array \|\ *kind* + *optional* + *read-only*\ \|Type information for
revoke-oauth-token task collection object -
cm:access:tasks:revoke-tokens:oauthrevoketokentaskitemstate.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change to revoke-oauth-token task collection object.
time.\|integer(int64) \|\ *selfLink* + *optional* + *read-only*\ \|A
reference link URI for revoke-oauth-token task collection
object.\|string \|===

[[\_post\_revoke\_list\_of\_tokens\_body]] ===
post\_revoke\_list\_of\_tokens\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
revoke-oauth-token by a user. ex. "REVOKE\_LIST\_OF\_TOKENS".\|string
\|\ *deviceReference* + *optional*\ \|Reference link to device in
resolver groups.\|object \|\ *perDeviceOauthIds* + *optional*\ \|Per
device ids assocated with token.\|<
<<\_post\_revoke\_list\_of\_tokens\_body\_perdeviceoauthids,perDeviceOauthIds>>
> array \|===

[[\_post\_revoke\_list\_of\_tokens\_body\_perdeviceoauthids]]
*perDeviceOauthIds*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *oauthIds* + *optional*\ \|Id refering
to oauth token.\|<
<<\_post\_revoke\_list\_of\_tokens\_body\_oauthids,oauthIds>> > array
\|===

[[\_post\_revoke\_list\_of\_tokens\_body\_oauthids]] *oauthIds*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *clientId* + *optional*\ \|Unique id
refering to a client.\|string \|\ *id* + *optional*\ \|Unique if
referint a token.\|string \|===
