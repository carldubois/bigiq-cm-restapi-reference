## Retrieving a Web Application Security Event Log record using a support_id.

### Overview
Describes how you use the REST API to retrieve a Web Application Security Event Log record using a support_id.

### Prerequisites
1. A Logging Node is configured with the Web Application Security service enabled.
2. Events are sent from BIG-IP to the Logging Node.
### Description
Describes how you use the REST API to retrieve a Web Application Security Event Log record using a support_id.
Perform the REST API actions in the following order:
1. Perform a POST operation to perform a search of the logs by a given support_id.

The following extended example shows each of these REST API actions.
### Example
#### 1. Perform a POST operation to perform a search of the logs by a given support_id.
Perform a POST operation to perform a search of the logs by a given support_id.
```
POST: https:/<mgmtip>//mgmt/cm/shared/es/logiq/asmindex/_search
{  
   "query":{  
      "query_string":{  
         "query":"support_id: 10961136626817826933"
      }
   },
   "from":0,
   "size":50,
   "sort":{  
      "date_time":"desc"
   }
}
```
The following is the JSON response from the POST operation:
```
{
    "took": 19,
    "timed_out": false,
    "_shards": {
        "total": 5,
        "successful": 5,
        "failed": 0
    },
    "hits": {
        "total": 1,
        "max_score": null,
        "hits": [
            {
                "_index": "asmindex_2016-11-13t05-05-22-0800",
                "_type": "syslog",
                "_id": "AVho9JvuqfHiZKdO7Wah",
                "_score": null,
                "_source": {
                    "unit_hostname": "omar.olympus.f5net.com",
                    "management_ip_address": "172.29.41.125",
                    "http_class_name": "/Common/EVENTlOGtEST",
                    "web_application_name": "/Common/EVENTlOGtEST",
                    "policy_name": "/Common/EVENTlOGtEST",
                    "policy_apply_date": "2016-11-13 09:31:59",
                    "violations": [
                        "HTTP protocol compliance failed",
                        "JSON data does not comply with format settings",
                        "Access from disallowed User/Session/IP",
                        "Mandatory HTTP header is missing"
                    ],
                    "support_id": "10961136626817826933",
                    "request_status": "alerted",
                    "response_code": "200",
                    "ip_client": "192.168.188.148",
                    "route_domain": "0",
                    "method": "GET",
                    "protocol": "HTTP",
                    "query_string": "json_qs={%22N%22[%20%221]%20}",
                    "x_forwarded_for_header_value": "N/A",
                    "sig_ids": [],
                    "sig_names": "",
                    "date_time": "2016-11-15 10:46:02",
                    "severity": "Error",
                    "attack_type": [
                        "Other Application Attacks",
                        "Abuse of Functionality",
                        "HTTP Parser Attack",
                        "JSON Parser Attack"
                    ],
                    "geo_location": "N/A",
                    "ip_address_intelligence": "N/A",
                    "username": "N/A",
                    "session_id": "e7d07a35478f97c9",
                    "src_port": "55262",
                    "dest_port": "8080",
                    "dest_ip": "172.29.43.8",
                    "sub_violations": [
                        "HTTP protocol compliance failed:Host header contains IP address"
                    ],
                    "virus_name": "N/A",
                    "uri": "/index2.php",
                    "violation_details": "<?xml version='1.0' encoding='UTF-8'?><BAD_MSG><violation_masks><block>0000000000000000-0000000000000000</block><alarm>7cffffffffdffffb-c002000000000000</alarm><learn>7cffffffffdffffb-c000000000000000</learn><staging>0000000000000000-0000000000000000</staging></violation_masks><request-violations><violation><viol_index>14</viol_index><viol_name>VIOL_HTTP_PROTOCOL</viol_name><http_sanity_checks_status>2048</http_sanity_checks_status><http_sub_violation_status>2048</http_sub_violation_status><http_sub_violation>SG9zdCBoZWFkZXIgd2l0aCBJUCB2YWx1ZTogMTcyLjI5LjQzLjg=</http_sub_violation></violation><violation><viol_index>64</viol_index><viol_name>VIOL_MANDATORY_HEADER</viol_name><header_data><header_name>mandatory_header</header_name></header_data></violation><violation><viol_index>28</viol_index><viol_name>VIOL_JSON_FORMAT</viol_name><context>parameter</context><param_data><param_name>anNvbl9xcw==</param_name><staging>0</staging><param_value>eyJOIjogIjEiLCJNIjogWyAiMSIsICIyIiwgIjMiLCAiNCIsICI1IiwgIjYiLCAiNyIsICI4IiwgIjkiLCAiMTAiIF0gfQ==</param_value></param_data><staging>0</staging><content_profile_data><type>JSON</type><content_id>15</content_id><content_profile_id>12</content_profile_id><content_profile_name>json1_qs</content_profile_name><location>element value</location><error_code>32</error_code><specific_desc>Defense alert</specific_desc></content_profile_data><failed_defense>/policy/json/max_children</failed_defense><failed_defense_xpath>/policy/json/max_children</failed_defense_xpath><allowed_value>9</allowed_value><actual_value>10</actual_value></violation><violation><viol_index>50</viol_index><viol_name>VIOL_SESSION_AWARENESS</viol_name></violation></request-violations><info_violations><violation><session_awareness><violation_data><scope>sid</scope><flag>block_all</flag></violation_data><violation_data><scope>ip</scope><flag>block_all</flag></violation_data></session_awareness></violation></info_violations></BAD_MSG>",
                    "violation_rating": "5",
                    "websocket_direction": "N/A",
                    "websocket_message_type": "N/A",
                    "device_id": "N/A",
                    "staged_sig_ids": "",
                    "staged_sig_names": "",
                    "blocking_exception_reason": "N/A",
                    "header": "Host: a.com:8080\\r\\nConnection: keep-alive\\r\\nCache-Control: max-age=0\\r\\nUpgrade-Insecure-Requests: 1\\r\\nUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36\\r\\nAccept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8\\r\\nAccept-Encoding: gzip, deflate, sdch\\r\\nAccept-Language: en-US,en;q=0.8,he;q=0.6\\r\\n\\r\\n",
                    "request": "GET /index2.php?json_qs={%22N%22:%20%221%22,%22M%22:%20[%20%221%22,%20%222%22,%20%223%22,%20%224%22,%20%225%22,%20%226%22,%20%227%22,%20%228%22,%20%229%22,%20%2210%22%20]%20} HTTP/1.1\\r\\nHost: a.com:8080\\r\\nConnection: keep-alive\\r\\nCache-Control: max-age=0\\r\\nUpgrade-Insecure-Requests: 1\\r\\nUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36\\r\\nAccept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8\\r\\nAccept-Encoding: gzip, deflate, sdch\\r\\nAccept-Language: en-US,en;q=0.8,he;q=0.6\\r\\n\\r\\n",
                    "response": "HTTP/1.1 200 OK\\r\\nDate: Tue, 15 Nov 2016 20:30:39 GMT\\r\\nVary: User-Agent\\r\\nContent-Length: 13\\r\\nKeep-Alive: timeout=15, max=97\\r\\nConnection: Keep-Alive\\r\\nContent-Type: text/html; charset=UTF-8\\r\\n\\r\\n<html></html>"
                },
                "sort": [
                    1479206762000
                ]
            }
        ]
    }
}
```

