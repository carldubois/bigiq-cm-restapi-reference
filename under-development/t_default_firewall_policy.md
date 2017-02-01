## To create a firewall policy to use when referenced by a firewall context (virtual)

### Overview
This task workflow will describe the steps nessasaey to create and manage a firewall policy and its components (address-lists, port-lists).

In general, brief steps described below: 

Example
- step 1: create a address-list
- step 2: create a port-list
- step 3: create a firewall-policy 
- step 4: reference a address-list to firewall-policy
- step 5: reference a port-list to a firewall-policy
- step 6: attach firewall-policy to firewall context (example, virtual server(vip))


### Prerequisites
You should be sure the following prerequisites have been met.

- All BIG-IP devices are operational.
- The BIG-IQ Centralized Management system is operational.
- Firewall contexts are imported into firewall namespace using device configuration import firewall.

### Description

#### 1. Create a address-list:
```
POST https://ip/mgmt/cm/firewall/working-config/address-lists

Request body:
{  
   "addresses":[  
      {  
         "address":"10.128.10.1",
         "description":"Test Address-List"
      }
   ],
   "partition":"Common",
   "name":"Api_created-address-list"
}
```

When the POST command is completed successfully, it will create a address-list in working config and responds with the selfLink of the object. Here is the POST response example,
```
{
  "addresses": [
    {
      "address": "10.128.10.1",
      "description": "Test"
    }
  ],
  "partition": "Common",
  "name": "Api_created-address-list",
  "id": "41dfdf8e-51e9-34de-93ae-d98dd800ff94",
  "generation": 1,
  "lastUpdateMicros": 1484067159489554,
  "kind": "cm:firewall:working-config:address-lists:addressliststate",
  "selfLink": "https://localhost/mgmt/cm/firewall/working-config/address-lists/41dfdf8e-51e9-34de-93ae-d98dd800ff94"
}
```
Take a note on the selfLink property, you'll need this to PATCH the virtual server in later steps.

#### 2. Create a port-list
```
POST https://ip/mgmt/cm/firewall/working-config/port-lists

Request Body:
{  
   "ports":[  
      {  
         "port":"22",
         "description":"SSH port"
      },
      {  
         "port":"23",
         "description":"Telnet port"
      }
   ],
   "partition":"Common",
   "name":"API_created_ports"
}
```
When the POST command is completed successfully, it will create a port-list in working config and responds with the selfLink of the object. Here is the POST response example,

```
{
  "ports": [
    {
      "port": "22",
      "description": "SSH port"
    },
    {
      "port": "23",
      "description": "Telnet port"
    }
  ],
  "partition": "Common",
  "name": "API_created_ports",
  "id": "bfbfd424-66c8-3137-a4d0-3dddf78d3011",
  "generation": 1,
  "lastUpdateMicros": 1484068237654496,
  "kind": "cm:firewall:working-config:port-lists:portliststate",
  "selfLink": "https://localhost/mgmt/cm/firewall/working-config/port-lists/bfbfd424-66c8-3137-a4d0-3dddf78d3011"
}
```
Take a note on the selfLink property, you'll need this to PATCH the virtual server in later steps.

#### 3. Create a firewall policy

```
POST https://ip/mgmt/cm/firewall/working-config/policies

Request Body:
{  
   "partition":"Common",
   "name":"API_Created_Policy"
}
```
When the POST command is completed successfully, it will create a firewall-policy in working config and responds with the selfLink of the object. Here is the POST response example,
```
{  
   "rulesCollectionReference":{  
      "link":"https://localhost/mgmt/cm/firewall/working-config/policies/eeff8d53-e978-3f81-a00c-875f33599fcb/rules",
      "isSubcollection":true
   },
   "partition":"Common",
   "name":"API_Created_Policy",
   "id":"eeff8d53-e978-3f81-a00c-875f33599fcb",
   "generation":1,
   "lastUpdateMicros":1484069469329296,
   "kind":"cm:firewall:working-config:policies:policystate",
   "selfLink":"https://localhost/mgmt/cm/firewall/working-config/policies/eeff8d53-e978-3f81-a00c-875f33599fcb"
}
```
Take a note on the selfLink property for the firewall-policy create. You'll need it in step 4.

#### 4. Create a firewall-policy rule reference. In order to accomplish you will need the selfLink of the firewall policy. Append rules to firewall-policy selfLink to create URI endpoint for rule reference.

```
POST https://ip/mgmt/cm/firewall/working-config/policies/eeff8d53-e978-3f81-a00c-875f33599fcb/rules

Request Body:
{  
   "name":"newRule0_164",
   "rowHeight":45,
   "editRowHeight":125,
   "action":"accept",
   "protocol":"tcp",
   "state":"enabled",
   "log":false,
   "$isNew":true,
   "clientOrder":1,
   "source":{  
      "addressListReferences":[  
         {  
            "name":"Api_created-address-list",
            "link":"https://localhost/mgmt/cm/firewall/working-config/address-lists/e8f37851-300b-34ff-811b-7fbc921c8472",
            "$isNew":true
         }
      ],
      "portListReferences":[  
         {  
            "name":"API_created_ports",
            "link":"https://localhost/mgmt/cm/firewall/working-config/port-lists/bfbfd424-66c8-3137-a4d0-3dddf78d3011",
            "$isNew":true
         }
      ]
   },
   "evalOrder":1000
}
```
When the POST command is completed successfully, it will create a firewall-policy rule reference with an address-list created in step 1 and an port-list created in step 2. Here is the POST response example,
```
{
  "action": "accept",
  "evalOrder": 1000,
  "log": false,
  "protocol": "udp",
  "source": {
    "addressListReferences": [
      {
        "link": "https://localhost/mgmt/cm/firewall/working-config/address-lists/e8f37851-300b-34ff-811b-7fbc921c8472"
      }
    ],
    "portListReferences": [
      {
        "link": "https://localhost/mgmt/cm/firewall/working-config/port-lists/bfbfd424-66c8-3137-a4d0-3dddf78d3011"
      }
    ]
  },
  "state": "enabled",
  "name": "newRule0_carl",
  "id": "735f1c33-10e2-3905-9083-a3112c712db1",
  "generation": 1,
  "lastUpdateMicros": 1484076226043608,
  "kind": "cm:firewall:working-config:policies:rules:rulestate",
  "selfLink": "https://localhost/mgmt/cm/firewall/working-config/policies/eeff8d53-e978-3f81-a00c-875f33599fcb/rules/735f1c33-10e2-3905-9083-a3112c712db1"
}
```


#### 5. Attach a firewall policy to a virtual server firewall context.
##### GET virtual server firewall context selfLink.
```
GET https://ip/mgmt/cm/firewall/working-config/firewalls

Request Response:
{
   {
      "firewallType": "vip",
      "firewallIpAddress": "10.200.10.2%0:80",
      "rulesCollectionReference": {
        "link": "https://localhost/mgmt/cm/firewall/working-config/firewalls/e20a4ff3-1f22-3aea-8f57-094848cdee69/rules",
        "isSubcollection": true
      },
      "partition": "Common",
      "subPath": "app_serv-2.app",
      "deviceReference": {
        "id": "2a2baaf0-b22f-49dc-81c6-4711fa189820",
        "name": "bigip_apm_03.demonet.com",
        "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
        "machineId": "2a2baaf0-b22f-49dc-81c6-4711fa189820",
        "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/2a2baaf0-b22f-49dc-81c6-4711fa189820"
      },
      "name": "app_serv-2_default_vs_80",
      "id": "e20a4ff3-1f22-3aea-8f57-094848cdee69",
      "generation": 1,
      "lastUpdateMicros": 1484077647958684,
      "kind": "cm:firewall:working-config:firewalls:firewallstate",
      "selfLink": "https://localhost/mgmt/cm/firewall/working-config/firewalls/e20a4ff3-1f22-3aea-8f57-094848cdee69"
    }
}
```

##### PATCH firewall policy to global firewall context.
```
PATCH https://ip/mgmt/cm/firewall/working-config/firewalls/27aef5b5-f83b-3cdd-a8b2-372e7d65c6ea

Request Body:
{  
   "enforcedPolicyReference":{
      "link":"https://localhost/mgmt/cm/firewall/working-config/policies/c8c358a9-f996-375e-8bd5-8681974bd7c0"
   }
}
```
When the PATCH command is completed successfully, it will reference or attach the firewall-policy rule with the vip (virtual) firewall context. Here is the POST response example,
```
Request Response
{
  "firewallType": "vip",
  "firewallIpAddress": "10.100.1.100%0:80",
  "enforcedPolicyReference": {
    "link": "https://localhost/mgmt/cm/firewall/working-config/policies/c8c358a9-f996-375e-8bd5-8681974bd7c0"
  },
  "rulesCollectionReference": {
    "link": "https://localhost/mgmt/cm/firewall/working-config/firewalls/27aef5b5-f83b-3cdd-a8b2-372e7d65c6ea/rules",
    "isSubcollection": true
  },
  "partition": "Common",
  "subPath": "app_serv-1.app",
  "deviceReference": {
    "id": "2a2baaf0-b22f-49dc-81c6-4711fa189820",
    "name": "bigip_apm_03.demonet.com",
    "kind": "shared:resolver:device-groups:restdeviceresolverdevicestate",
    "machineId": "2a2baaf0-b22f-49dc-81c6-4711fa189820",
    "link": "https://localhost/mgmt/shared/resolver/device-groups/cm-firewall-allFirewallDevices/devices/2a2baaf0-b22f-49dc-81c6-4711fa189820"
  },
  "name": "app_serv-1_vs",
  "description": "vsdescr",
  "id": "27aef5b5-f83b-3cdd-a8b2-372e7d65c6ea",
  "generation": 3,
  "lastUpdateMicros": 1484079197640302,
  "kind": "cm:firewall:working-config:firewalls:firewallstate",
  "selfLink": "https://localhost/mgmt/cm/firewall/working-config/firewalls/27aef5b5-f83b-3cdd-a8b2-372e7d65c6ea"
}
```


### API references:
[Api reference - firewall policy](../doc/firewall-policies.doc)
[Api reference - firewalls](../doc/firewalls.doc)

