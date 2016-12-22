= BIG-IQ APM kill active access sessions.

[[\_overview]] == Overview API used to kill active access sessions on
BIGIP using a BIGIQ centralized management system.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/access/tasks
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_kill-sessions\_access-groups\_post]] === Kill all active session by
access-group match. .... POST /kill-sessions (access-groups) ....

==== Description Kill all active access sessions by access-group match.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {{"action":"KILL\_BY\_USER", "userName":"user2",
"accessGroupNames":["TestGroup1",
"TestGroup2"]}}\|<<\_post\_kill\_access\_by\_access\_group,post\_kill\_access\_by\_access\_group>>\|
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to kill all active access
session of a
user.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_access-groups\_get]] === List all kill-session tasks
as part of a collection. .... GET /kill-sessions (access-groups) ....

==== Description Returns the collection of kill-session tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of session tasks
to
kill.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_all\_post]] === Kill all active session for specified
devices. .... POST /kill-sessions (devices) ....

==== Description Kill all active access sessions for specified devices.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"action":"KILL\_ALL\_SESSIONS",
"deviceReferences":[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"},
{"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"}]}\|<<\_post\_kill\_access\_all,post\_kill\_access\_all>>\|
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to kill all active access
sessions.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_all\_get]] === List all kill-session tasks as part of
a collection. .... GET /kill-sessions (devices) ....

==== Description Returns the collection of kill-session tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of session tasks
to
kill.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_bigip\_clusters\_post]] === Kill all active
kill-session by cluster-name match. .... POST /kill-sessions (bigip
clusters) ....

==== Description Kill all active access kill-sessions by cluster-name
match.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {{"action":"KILL\_BY\_SESSIONS", "userName":"user2",
"clusterNames":["BlueCluster",
"RedCluster"]}}\|<<\_post\_kill\_access\_by\_cluster\_name,post\_kill\_access\_by\_cluster\_name>>\|
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to kill all active access
kill-session of a
user.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_bigip\_clusters\_get]] === List all kill-session
tasks as part of a collection. .... GET /kill-sessions (bigip clusters)
....

==== Description Returns the collection of kill-session tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of kill-session
tasks to
kill.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_bigip\_clusters\_access-groups\_and\_device\_reference\_post]]
=== Kill all active kill-session by access-group match. .... POST
/kill-sessions (bigip clusters, access-groups and device reference) ....

==== Description Kill all active access kill-sessions by access-group
match.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *optional*\ \|Input parameter list in json format.
ex. {"action":"KILL\_BY\_USER", "userName":"user2",
"accessGroupNames":["TestGroup1", "TestGroup2"],
"clusterNames":["BlueCluster", "RedCluster"], "deviceReferences":
[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"},
{"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"}]}\|<<\_post\_kill\_access\_by\_cluster\_name\_access\_group\_device\_reference,post\_kill\_access\_by\_cluster\_name\_access\_group\_device\_reference>>\|
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to kill all active access
kill-session of a
user.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_bigip\_clusters\_access-groups\_and\_device\_reference\_get]]
=== List all kill-session tasks as part of a collection. .... GET
/kill-sessions (bigip clusters, access-groups and device reference) ....

==== Description Returns the collection of kill-session tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of kill-session
tasks to
kill.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_session\_id\_post]] === Kill active sessions by
session id. .... POST /kill-sessions (session id) ....

==== Description Kill active access sessions by session id for a device.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"action":"KILL\_BY\_LIST\_OF\_SESSIONS",
"sessions":[{"deviceReference":{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"},
"sessionIds":["2a5d7604", "875f7fed"]},
{"deviceReference":{"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"},
"sessionIds":["2hjj234",
"9as3323"]}}\|<<\_post\_kill\_access\_by\_sessions,post\_kill\_access\_by\_sessions>>\|
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to kill active access
sessions by session
id.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_session\_id\_get]] === List all kill-session tasks as
part of a collection. .... GET /kill-sessions (session id) ....

==== Description Returns the collection of kill-session tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of session tasks
to
kill.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_user\_post]] === Kill all active session by a user.
.... POST /kill-sessions (user) ....

==== Description Kill all active access sessions by a user.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex.
{{"action":"KILL\_BY\_USER","userName":"user2","deviceReferences":[{"link":"https://localhost/mgmt/cm/system/machineid-resolver/901695c8-f405-489f-9996-54f7b21da642"},
{"link":"https://localhost/mgmt/cm/system/machineid-resolver/3f320100-2177-42e0-8a46-2e33cd3366d"}}}\|<<\_post\_kill\_access\_by\_user\_body,post\_kill\_access\_by\_user\_body>>\|
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to kill all active access
session of a
user.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_user\_get]] === List all kil-session tasks as part of
a collection. .... GET /kill-sessions (user) ....

==== Description Returns the collection of kill-session tasks.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET collection of session tasks
to
kill.\|<<\_properties\_kill\_access\_session\_collection,properties\_kill\_access\_session\_collection>>
\|\ *400*\ \|Error response "Bad
Request"\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_kill-sessions\_objectid\_get]] === Used to get a single instance of
a kill access session task. .... GET /kill-sessions/{objectId} ....

==== Description Returns a object for kill access session task
identified by id for an endpoint URI.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|\|string(UUID)\| \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|APM kill sessions task
object.\|<<\_properties\_kill\_access\_session,properties\_kill\_access\_session>>
\|\ *400*\ \|Server error response "Bad
Request".\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for a collection of tasks used to kill
access sessions -
cm:access:tasks:kill-sessions:accesskillsessionstaskcollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for a collection of tasks used to kill
access sessions -
cm:access:tasks:kill-sessions:accesskillsessionstaskcollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_post\_kill\_access\_all]] === post\_kill\_access\_all

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
kill all access sessions. ex. "KILL\_ALL\_SESSIONS"\|string
\|\ *deviceReferences* + *optional*\ \|Reference link to one or more
devices in which active access sessions live.\|string \|===

[[\_post\_kill\_access\_by\_access\_group]] ===
post\_kill\_access\_by\_access\_group

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *accessGroupNames* + *optional*\ \|One
or more access group names. All sessions in these groups will be killed
by invoking task.\|string \|\ *action* + *required*\ \|Action used to
kill access session by access\_group. ex action.
"KILL\_BY\_USER"\|string \|\ *userName* + *optional*\ \|User name
defined to all sessions owned.\|string \|===

[[\_post\_kill\_access\_by\_cluster\_name]] ===
post\_kill\_access\_by\_cluster\_name

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
kill access session by access\_group. ex action.
"KILL\_BY\_USER"\|string \|\ *clusterNames* + *optional*\ \|One or more
cluster names. All sessions in these bigip clusters will be killed by
invoking task.\|string \|\ *userName* + *optional*\ \|User name defined
to all sessions owned.\|string \|===

[[\_post\_kill\_access\_by\_cluster\_name\_access\_group\_device\_reference]]
===
post\_kill\_access\_by\_cluster\_name\_access\_group\_device\_reference

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *accessGroupNames* + *optional*\ \|One
or more access group names. All sessions in these groups will be killed
by invoking task.\|string \|\ *action* + *required*\ \|Action used to
kill access session by access\_group. ex action.
"KILL\_BY\_USER"\|string \|\ *clusterNames* + *optional*\ \|One or more
cluster names. All sessions in these bigip clusters will be killed by
invoking task.\|string \|\ *deviceReferences* + *optional*\ \|Reference
link to one or more devices in which active access sessions
live.\|string \|\ *userName* + *optional*\ \|User name defined to all
sessions owned.\|string \|===

[[\_post\_kill\_access\_by\_sessions]] ===
post\_kill\_access\_by\_sessions

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
kill all access sessions identified by a session id. ex.
"KILL\_ALL\_SESSIONS"\|string \|\ *sessions* + *optional*\ \|\|<
<<\_post\_kill\_access\_by\_sessions\_sessions,sessions>> > array \|===

[[\_post\_kill\_access\_by\_sessions\_sessions]] *sessions*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *deviceReference* +
*optional*\ \|Reference link to one device in which active access
sessions
live.\|<<\_post\_kill\_access\_by\_sessions\_devicereference,deviceReference>>
\|\ *sessionIds* + *optional*\ \|Unique id referencing a session.\|<
string > array \|===

[[\_post\_kill\_access\_by\_sessions\_devicereference]]
*deviceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
device in resolver group.\|string \|===

[[\_post\_kill\_access\_by\_user\_body]] ===
post\_kill\_access\_by\_user\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Action used to
kill access session by a user. ex. "KILL\_BY\_USER"\|string
\|\ *deviceReferences* + *optional*\ \|Reference link to one or more
devices in which active access sessions live.\|string \|\ *userName* +
*optional*\ \|User name defined to all sessions owned.\|string \|===

[[\_properties\_kill\_access\_session]] ===
properties\_kill\_access\_session

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *action* + *required*\ \|Unique id
assigned to a access kill user session task object.\|string
\|\ *currentStep* + *optional* + *read-only*\ \|Current step used to
track state of session.\|string \|\ *deviceReferences* +
*optional*\ \|Reference link to one or more devices in which active
access sessions live.\|<
<<\_properties\_kill\_access\_session\_devicereferences,deviceReferences>>
> array \|\ *generation* + *optional* + *read-only*\ \|A integer that
will track change made to a kill-sessions task object.
generation.\|integer(int64) \|\ *id* + *optional*\ \|Unique id
assocaited with kill-sessions task object.\|string
\|\ *identityReference* + *optional*\ \|Reference link to the user who
issued the rest call.\|<
<<\_properties\_kill\_access\_session\_identityreference,identityReference>>
> array \|\ *kind* + *optional*\ \|Type information for access kill user
session task object -
cm:access:tasks:kill-sessions:accesskillsessionstaskitemstate.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to a kill-sessions task object.
time.\|integer(int64) \|\ *name* + *optional*\ \|Name of access kill
user session task object.\|string \|\ *ownerMachineId* +
*optional*\ \|Device machine id used by the kill user session task
object. Sessions that live on this device will be killed.\|string
\|\ *selfLink* + *optional* + *read-only*\ \|A reference link URI to the
kill-sessions task object.\|string \|\ *startDateTime* +
*optional*\ \|Date / Time of when this kill user session task
began.\|string \|\ *status* + *optional*\ \|Status of kill user session
task state. - ex. STARTED, FINISHED.\|string \|\ *userName* +
*optional*\ \|User name defined to all sessions owned.\|string
\|\ *userReference* + *optional*\ \|Refernece link to user issing the
rest call to start kill-session task.\|string \|\ *username* +
*optional*\ \|\|string \|===

[[\_properties\_kill\_access\_session\_devicereferences]]
*deviceReferences*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
device in resolver group.\|string \|===

[[\_properties\_kill\_access\_session\_identityreference]]
*identityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *link* + *optional*\ \|Reference link to
user identity.\|string \|===

[[\_properties\_kill\_access\_session\_collection]] ===
properties\_kill\_access\_session\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to the access kill
user session task collection object. generation.\|integer(int64)
\|\ *items* + *optional*\ \|A collection of kill-session tasks.\|<
object > array \|\ *kind* + *optional* + *read-only*\ \|Type information
for access kill user session task collection object -
cm:access:tasks:kill-sessions:accesskillsessionstaskcollectionstate.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change to the access kill user session task collection
object. time.\|integer(int64) \|\ *selfLink* + *optional* +
*read-only*\ \|A reference link URI for the access kill user session
task collection object.\|string \|===
