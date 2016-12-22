= BIG-IQ ASM Policies.

[[\_overview]] == Overview API used to create / edit BIGIQ web
application policies in ASM.

=== Version information [%hardbreaks] *Version* : 5.2

=== URI scheme [%hardbreaks] *BasePath* : /mgmt/cm/asm/working-config
*Schemes* : HTTPS

=== Consumes

-  ``application/json``

=== Produces

-  ``application/json``

[[\_paths]] == Paths

[[\_policies\_post]] === Create a new BIG-IQ web application security
policy for ASM. .... POST /policies ....

==== Description Add a new web application security policy.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Body*\ \|\ *Json string
for request body.* + *required*\ \|Input parameter list in json format.
ex. {"name":"Policy\_3", "partition":"Common",
"fullPath":"/Common/Policy\_3", "applicationLanguage":
"utf-8"}\|<<\_post\_asm\_body,post\_asm\_body>>\|None \|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|POST to create a web application
security policy.\|<<\_properties\_asm,properties\_asm>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_policies\_get]] === Used to GET the BIG-IQ web application security
policies for ASM. .... GET /policies ....

==== Description Returns all web application security policies as part
of a item collection.

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|GET BIG-IQ web application
security
policies.\|<<\_properties\_asm\_collection,properties\_asm\_collection>>
\|\ *400*\ \|Error response Bad
Request\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_policies\_objectid\_get]] === Used to GET the BIG-IQ web application
policy. .... GET /policies/{objectId} ....

==== Description Returns a web application policy defined by a object
id.

==== Parameters

[options="header", cols=".\ :sup:`2,.`\ 3,.\ :sup:`9,.`\ 4,.^2"] \|===
\|Type\|Name\|Description\|Schema\|Default \|\ *Path*\ \|\ *objectId* +
*required*\ \|Unique id associated with policy.\|string(UUID)\|None
\|===

==== Responses

[options="header", cols=".\ :sup:`2,.`\ 14,.^4"] \|=== \|HTTP
Code\|Description\|Schema \|\ *200*\ \|BIG-IQ web application
policy.\|<<\_properties\_asm,properties\_asm>> \|\ *400*\ \|Server error
response Bad
Request.\|<<\_400\_error\_collection,400\_error\_collection>>
\|\ *404*\ \|Error response Public URI path not
registered.\|<<\_404\_error\_collection,404\_error\_collection>> \|===

[[\_definitions]] == Definitions

[[\_400\_error\_collection]] === 400\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection if policies. 400 error.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for ASM web
application security policies -
cm:asm:working-config:policies:policycollectionstate.\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_404\_error\_collection]] === 404\_error\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *errorStack* + *optional* +
*read-only*\ \|Error stack trace returned by java.\|string \|\ *items* +
*optional*\ \|Collection of policies. 404 error.\|< object > array
\|\ *kind* + *optional* + *read-only*\ \|Type information for ASM web
application security policies -
cm:asm:working-config:policies:policycollectionstate\|string
\|\ *message* + *optional* + *read-only*\ \|Error message returned from
server.\|string \|\ *requestBody* + *optional* + *read-only*\ \|The data
in the request body. GET (None)\|string \|\ *requestOperationId* +
*optional* + *read-only*\ \|Unique id assigned to rest
operation.\|integer(int64) \|===

[[\_post\_asm\_body]] === post\_asm\_body

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *applicationLanguage* +
*optional*\ \|Character encoding used by BIGIQ to create the policy
object. ex. utf8\|string \|\ *fullPath* + *optional*\ \|BIGIP full path
which includes partition / policy name. ex. /Common/Policy\_3\|string
\|\ *name* + *optional*\ \|Name of ASM web application security
policy.\|string \|\ *partition* + *optional*\ \|BIGIP partition name as
to where this policy will reside. default. Common\|string \|===

[[\_properties\_asm]] === properties\_asm

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *allowedResponseCodes* +
*optional*\ \|Array of response codes from server.\|< integer > array
\|\ *applicationLanguage* + *optional*\ \|Character encoding used by
BIGIQ to create the policy object. ex. utf8\|string \|\ *attributes* +
*optional*\ \|\|<<\_properties\_asm\_attributes,attributes>>
\|\ *bruteForceAttackPreventionReference* + *optional*\ \|Reference link
to brute force attach prevention configuration preventing brute force
attacks performed when a hacker tries to log on to a URL numerous times,
running many combinations of user names and passwords, until
successfully logs
on.\|<<\_properties\_asm\_bruteforceattackpreventionreference,bruteForceAttackPreventionReference>>
\|\ *caseInsensitive* + *optional*\ \|Is the ASM web application policy
elements case sensitive. True / False\|boolean
\|\ *characterSetReference* + *optional*\ \|Reference link to character
set configuration which lists characters (letters, digits, and symbols)
available, and how the security policy responds when that character
appears in the value field of an HTTP header in a request, and an
uncommon header
name.\|<<\_properties\_asm\_charactersetreference,characterSetReference>>
\|\ *cookieReference* + *optional*\ \|Reference link to cookie
configuration which handles the cookies in a list based on the specific
cookie type
(Enforced/Allowed).\|<<\_properties\_asm\_cookiereference,cookieReference>>
\|\ *createDateTime* + *optional* + *read-only*\ \|Date / Time when web
application policy was created. ex. 2016-11-28T20:50:12Z\|string
\|\ *creatorName* + *optional*\ \|Name of user that created the web
application policy.\|string \|\ *csrfProtectionReference* +
*optional*\ \|Reference link to configured cross site request forgery.
Unauthorized user access to authenticated accounts using cross-site
request forgery (CSRF) Proerty as defined by the
policy.\|<<\_properties\_asm\_csrfprotectionreference,csrfProtectionReference>>
\|\ *customXffHeaders* + *optional*\ \|Additional HTTP header, the
X-Forwarded-For header, to proxy an HTTP request to another server.\|<
string > array \|\ *dataGuardReference* + *optional*\ \|Reference link
to policy data guard configuration which protects sensitive data. If a
web server response contains a credit card number, U.S. Social Security
number, or pattern that matches a user-defined pattern, then the system
responds based on the enforcement mode
setting.\|<<\_properties\_asm\_dataguardreference,dataGuardReference>>
\|\ *description* + *optional*\ \|Description of security
policy.\|string \|\ *disallowedGeolocationReference* +
*optional*\ \|Reference link to configured countries that can access
your web application. Property as defined by the
policy.\|<<\_properties\_asm\_disallowedgeolocationreference,disallowedGeolocationReference>>
\|\ *enforcementMode* + *optional*\ \|Specifies how the system processes
a request that triggers a security policy violation. options.
Transparent / Blocking\|string \|\ *evasionsReference* +
*optional*\ \|Reference link to list of evasion technique detected,
which is triggered when the BIG-IP ASM system fails to normalize
requests. Normalization is the process of decoding requests that are
encoded.\|<<\_properties\_asm\_evasionsreference,evasionsReference>>
\|\ *extractionsReference* + *optional*\ \|Reference link to extraction
service configuration which manages how the system extracts dynamic
values for dynamic parameters from the responses returned by the web
application
server.\|<<\_properties\_asm\_extractionsreference,extractionsReference>>
\|\ *filetypeReference* + *optional*\ \|Reference link to a list allow /
disallow file types in the web application that the security policy
considers
legal.\|<<\_properties\_asm\_filetypereference,filetypeReference>>
\|\ *fullPath* + *optional*\ \|Full path containing BIG-IP partition and
name of web application security policy. ex. /Common/Policy\_3\|string
\|\ *generation* + *optional*\ \|\|string \|\ *gwtProfileReference* +
*optional*\ \|Reference link to gwt configuration used to protect web
applications created by google web toolkit (gwt). Google Web Toolkit
(GWT) is a Java framework that is used to create AJAX applications. When
you add GWT enforcement to a security policy, the Security Enforcer can
detect malformed GWT data, request payloads and parameter
values.\|<<\_properties\_asm\_gwtprofilereference,gwtProfileReference>>
\|\ *hasParent* + *optional*\ \|Does this policy contain a parent to
inherit configuration. True / False\|boolean \|\ *headerReference* +
*optional*\ \|Reference link to policy header configuration. Each
parameter can perform normalization and attack signature checks on HTTP
headers.\|<<\_properties\_asm\_headerreference,headerReference>>
\|\ *hostNameReference* + *optional*\ \|Reference link to a list of
allow / disallow host name that are used to access the web application
that this security policy
protects.\|<<\_properties\_asm\_hostnamereference,hostNameReference>>
\|\ *httpProtocolsReference* + *optional*\ \|Reference link to a http
protocol compliance option which are validation checks that are
performed on HTTP requests to ensure the requests are properly
formatted.\|<<\_properties\_asm\_httpprotocolsreference,httpProtocolsReference>>
\|\ *id* + *optional*\ \|Unique id associated with security
policy.\|string \|\ *ipIntelligenceReference* + *optional*\ \|Reference
link to configured ASM ip intellegence functions, such as log and block
requests from source IP addresses that, according to an IP Address
Intelligence database, have a bad
reputation.\|<<\_properties\_asm\_ipintelligencereference,ipIntelligenceReference>>
\|\ *jsonProfileReference* + *optional*\ \|Reference link to json
profiles which defines what the security policy enforces and considers
legal when it detects traffic that contains JSON
data.\|<<\_properties\_asm\_jsonprofilereference,jsonProfileReference>>
\|\ *kind* + *optional*\ \|Type information for security policy.
cm:asm:working-config:policies:policystate.\|string
\|\ *lastUpdateMicros* + *optional*\ \|Update time (micros) for last
change made to a security policy object. time.\|string
\|\ *learningMode* + *optional*\ \|ASM will attempt to adapt to changing
patterms in learning mode. options Automatic makes suggestions, and
enforces most suggestions after sufficient traffic over a period of
time, Manual. The system examines traffic and makes suggestions on what
to add to the policy. You manually examine the changes and accept,
delete, or ignore the suggestions. Disabled. The system does not do any
learning for the security policy, and makes no suggestions.\|string
\|\ *loginEnforcementReference* + *optional*\ \|Reference link to login
enforcement configuration which will allow a user to create or edit the
properties of authenticated URLs. Authenticated URLs are URLs that
become accessible to users only after they successfully log in to the
login
URL.\|<<\_properties\_asm\_loginenforcementreference,loginEnforcementReference>>
\|\ *loginPageReference* + *optional*\ \|Reference link to session login
page configuration used to protect restricted parts of the web
application by forcing users to pass through the login page before
viewing the restricted (authenticated)
URL.\|<<\_properties\_asm\_loginpagereference,loginPageReference>>
\|\ *methodReference* + *optional*\ \|Reference link to configured ASM
methods. Allowable - GET, POST and HEAD. Methods settings are used to
specify the HTTP methods that are acceptable within the context of the
web application and to specify whether the method should act as the GET
method or as the POST
method.\|<<\_properties\_asm\_methodreference,methodReference>>
\|\ *modifierName* + *optional*\ \|ASM policy modifiers from the custom
syntax.\|string \|\ *name* + *optional*\ \|Name of security
policy.\|string \|\ *parameterReference* + *optional*\ \|Reference link
to configured ASM parameters that the policy permits, such as attack
signature check, perform staging and enable regular expressions and
other pieces of information within a web
application.\|<<\_properties\_asm\_parameterreference,parameterReference>>
\|\ *partition* + *optional*\ \|The BIG-IP partition which this policy
lives.\|string \|\ *plainTextProfileReference* + *optional*\ \|Reference
link to plain text content profile that defines the properties that a
security policy enforces for unstructured text content, such as those
used in websocket
messages.\|<<\_properties\_asm\_plaintextprofilereference,plainTextProfileReference>>
\|\ *policyBuilderReference* + *optional*\ \|Reference link to policy
builder configuration which provides functions such as traffic learning
and enforcement
readiness.\|<<\_properties\_asm\_policybuilderreference,policyBuilderReference>>
\|\ *protocolIndependent* + *optional*\ \|Does the user want to allow
for protocol independent URLs? True / False\|boolean
\|\ *redirectionProtectionReference* + *optional*\ \|Reference link to
redirection protection configuration to prevent open redirect
vulnerability where the server tries to redirect the user to a target
domain that is not defined in the security policy. The server redirects
a user to a different web application, without any validation. This
vulnerability is used in phishing attacks to get users to visit
malicious sites without realizing
it.\|<<\_properties\_asm\_redirectionprotectionreference,redirectionProtectionReference>>
\|\ *responsePageReference* + *optional*\ \|Reference link to policy
response page configuration, where the user can edit the default
response page, the login response page, the XML response page, the AJAX
blocking response page, and the AJAX login response page for a web
application.\|<<\_properties\_asm\_responsepagereference,responsePageReference>>
\|\ *sectionReference* + *optional*\ \|Reference link to a list of each
ASC property sections. Such as evasion techniques, policy-building,
websocket protocol, general settings
etc..\|<<\_properties\_asm\_sectionreference,sectionReference>>
\|\ *selfLink* + *optional*\ \|Reference link to security policy
object.\|string \|\ *sensitiveParameterReference* +
*optional*\ \|Reference link to sensitive parameter configuration used
to protect sensitive user input, such as a password or a credit card
number, in a validated
request.\|<<\_properties\_asm\_sensitiveparameterreference,sensitiveParameterReference>>
\|\ *sessionTrackingReference* + *optional*\ \|Reference link to
configured ASM session tracking to track, enforce, and report on user
sessions and IP
addresses.\|<<\_properties\_asm\_sessiontrackingreference,sessionTrackingReference>>
\|\ *signatureReference* + *optional*\ \|Reference link to configured
attach signitures. Property as defined by the
policy.\|<<\_properties\_asm\_signaturereference,signatureReference>>
\|\ *signatureSetReference* + *optional*\ \|Reference link to signature
sets used by ASM to mitigate attack. Attack signatures belong to
signature sets assigned to the security policy. A user can enable or
disable security policy attack
signatures.\|<<\_properties\_asm\_signaturesetreference,signatureSetReference>>
\|\ *stagingSettings* + *optional*\ \|Staging allows you to test the
policy entities and the attack signatures for false positives without
enforcing them.\|<<\_properties\_asm\_stagingsettings,stagingSettings>>
\|\ *trustXff* + *optional*\ \|Trust flag for XFF HTTP request
header.\|boolean \|\ *type* + *optional*\ \|This is a descripive type of
policy. ex. security\|string \|\ *urlReference* +
*optional*\ \|Reference link to policy url configuration which will
match URLs, or URLs specified string to manage the flow allow /
disallow.\|<<\_properties\_asm\_urlreference,urlReference>>
\|\ *versionDatetime* + *optional*\ \|Date time of provisioned security
policy.\|string \|\ *versionDeviceName* + *optional*\ \|Security Policy
name as represented by version of BIGIP.\|string \|\ *versionLastChange*
+ *optional*\ \|Operation of last change to a security policy
represented.\|string \|\ *versionPolicyName* + *optional*\ \|Partition
and security policy full path.\|string \|\ *violationsReference* +
*optional*\ \|Reference link to a list of violations that occur when
some aspect of a request or response does not comply with the security
policy for a web
application.\|<<\_properties\_asm\_violationsreference,violationsReference>>
\|\ *webScrapingReference* + *optional*\ \|Reference link to policy web
scraping configuation detection such as prevent web data extraction by
detecting session anomalies in web application
usage.\|<<\_properties\_asm\_webscrapingreference,webScrapingReference>>
\|\ *webServicesSecurityReference* + *optional*\ \|Reference link to a
web service with will verify XML format, and validate XML document
integrity against a WSDL or XSD file. The security policy can also
handle encryption and decryption for web
services.\|<<\_properties\_asm\_webservicessecurityreference,webServicesSecurityReference>>
\|\ *websocketUrlReference* + *optional*\ \|Reference link to web socket
url list used to simplifies and speeds up communication between clients
and
servers.\|<<\_properties\_asm\_websocketurlreference,websocketUrlReference>>
\|\ *whitelistIpReference* + *optional*\ \|Reference link to configured
white list ip list used to identify source IP addresses for the system
to consider safe even if it found in the IP Address Intelligence
database.\|<<\_properties\_asm\_whitelistipreference,whitelistIpReference>>
\|\ *xmlProfileReference* + *optional*\ \|Reference link to policy xml
profile configuration. An XML profile is a set of content definitions
that determine whether the system allows or disallows requests that
contain
XML.\|<<\_properties\_asm\_xmlprofilereference,xmlProfileReference>>
\|\ *xmlValidationFileReference* + *optional*\ \|Reference link to xml
validation configuration used to enforce or validate xml content for web
application.\|<<\_properties\_asm\_xmlvalidationfilereference,xmlValidationFileReference>>
\|===

[[\_properties\_asm\_attributes]] *attributes*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *inspectHttpUploads* +
*optional*\ \|Flag to enable inspection of all http uploads. default
false\|boolean \|\ *maskCreditCardNumbersInRequest* + *optional*\ \|If
enabled, the system masks credit card numbers. If disabled (cleared),
the system does not mask credit card numbers.\|boolean
\|\ *maximumCookieHeaderLength* + *optional*\ \|0<= number<=8192
default. 8192\|string \|\ *maximumHttpHeaderLength* +
*optional*\ \|Maximum length of an HTTP header name and value that the
system processes. The default setting is 8192 bytes. The system
calculates and enforces the HTTP header length based on the sum of the
length of the HTTP header name and value.\|string
\|\ *pathParameterHandling* + *optional*\ \|Specifies how the system
handles path parameters that are attached to path segments in URIs.
options. as parameter, as url, ignore.\|string
\|\ *triggerAsmIruleEvent* + *optional*\ \|Enable irule event. List of
values. disabled, enabled-compatibility, enabled-normal.\|string
\|\ *useDynamicSessionIdInUrl* + *optional*\ \|Specifies how the
security policy processes URLs that use dynamic sessions. options.
disabled, default pattern, custom pattern.\|boolean \|===

[[\_properties\_asm\_bruteforceattackpreventionreference]]
*bruteForceAttackPreventionReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_charactersetreference]] *characterSetReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_cookiereference]] *cookieReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_csrfprotectionreference]] *csrfProtectionReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_dataguardreference]] *dataGuardReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_disallowedgeolocationreference]]
*disallowedGeolocationReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_evasionsreference]] *evasionsReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_extractionsreference]] *extractionsReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_filetypereference]] *filetypeReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_gwtprofilereference]] *gwtProfileReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_headerreference]] *headerReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_hostnamereference]] *hostNameReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_httpprotocolsreference]] *httpProtocolsReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_ipintelligencereference]] *ipIntelligenceReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_jsonprofilereference]] *jsonProfileReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_loginenforcementreference]]
*loginEnforcementReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_loginpagereference]] *loginPageReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_methodreference]] *methodReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_parameterreference]] *parameterReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_plaintextprofilereference]]
*plainTextProfileReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_policybuilderreference]] *policyBuilderReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_redirectionprotectionreference]]
*redirectionProtectionReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_responsepagereference]] *responsePageReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_sectionreference]] *sectionReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_sensitiveparameterreference]]
*sensitiveParameterReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_sessiontrackingreference]]
*sessionTrackingReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_signaturereference]] *signatureReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_signaturesetreference]] *signatureSetReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_stagingsettings]] *stagingSettings*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *enforcementReadinessPeriod* +
*optional*\ \|Period in days both security policy entities and attack
signatures remain in staging mode before the system suggests you enforce
them.\|integer \|\ *placeSignaturesInStaging* + *optional*\ \|Signature
staging - the system places new or updated signatures in staging for the
number of days specified in the enforcement readiness period.\|boolean
\|\ *signatureStaging* + *optional*\ \|Signature staging is supported on
the security policy. True / False\|boolean \|===

[[\_properties\_asm\_urlreference]] *urlReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to url asm signature.\|string \|===

[[\_properties\_asm\_violationsreference]] *violationsReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_webscrapingreference]] *webScrapingReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_webservicessecurityreference]]
*webServicesSecurityReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_websocketurlreference]] *websocketUrlReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_whitelistipreference]] *whitelistIpReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_xmlprofilereference]] *xmlProfileReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_xmlvalidationfilereference]]
*xmlValidationFileReference*

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *isSubcollection* + *optional*\ \|Is a
subcollection (True/False)\|boolean \|\ *link* + *optional*\ \|Reference
link to asm signature.\|string \|===

[[\_properties\_asm\_collection]] === properties\_asm\_collection

[options="header", cols=".\ :sup:`3,.`\ 11,.^4"] \|===
\|Name\|Description\|Schema \|\ *generation* + *optional* +
*read-only*\ \|A integer that will track change made to a ASM web
application security policy collection object.
generation.\|integer(int64) \|\ *items* + *optional*\ \|Collection if
asm signatures.\|< object > array \|\ *kind* + *optional* +
*read-only*\ \|Type information for a ASM web application security
policy collection object -
cm:asm:working-config:policies:policycollectionstate.\|string
\|\ *lastUpdateMicros* + *optional* + *read-only*\ \|Update time
(micros) for last change made to an ASM web application security policy
collection object. time.\|integer(int64) \|\ *selfLink* + *optional* +
*read-only*\ \|A reference link URI to a ASM web application security
policy collection object.\|string \|===
