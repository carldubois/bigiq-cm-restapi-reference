# BigIqDeployConfiguration.DefaultApi

All URIs are relative to *https://localhost/mgmt/cm/firewall/tasks*

Method | HTTP request | Description
------------- | ------------- | -------------
[**deployConfigurationGet**](DefaultApi.md#deployConfigurationGet) | **GET** /deploy-configuration | GET all deployment tasks.
[**deployConfigurationObjectIdGet**](DefaultApi.md#deployConfigurationObjectIdGet) | **GET** /deploy-configuration/{objectId} | Used to get a specific deployment configuration task identified by id.
[**deployConfigurationObjectIdPost**](DefaultApi.md#deployConfigurationObjectIdPost) | **POST** /deploy-configuration/{objectId} | POST deployment task policy for firewall namespace.


<a name="deployConfigurationGet"></a>
# **deployConfigurationGet**
> PropertiesDeployCollection deployConfigurationGet()

GET all deployment tasks.

Returns the collection of firewall namespace specific deployment tasks.

### Example
```javascript
var BigIqDeployConfiguration = require('big_iq_deploy_configuration');

var apiInstance = new BigIqDeployConfiguration.DefaultApi();

var callback = function(error, data, response) {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
};
apiInstance.deployConfigurationGet(callback);
```

### Parameters
This endpoint does not need any parameter.

### Return type

[**PropertiesDeployCollection**](PropertiesDeployCollection.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

<a name="deployConfigurationObjectIdGet"></a>
# **deployConfigurationObjectIdGet**
> PropertiesDeploy deployConfigurationObjectIdGet(objectId)

Used to get a specific deployment configuration task identified by id.

Returns deployment configuration task within the firewall namespace identified by id.

### Example
```javascript
var BigIqDeployConfiguration = require('big_iq_deploy_configuration');

var apiInstance = new BigIqDeployConfiguration.DefaultApi();

var objectId = "objectId_example"; // String | 


var callback = function(error, data, response) {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
};
apiInstance.deployConfigurationObjectIdGet(objectId, callback);
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **objectId** | **String**|  | 

### Return type

[**PropertiesDeploy**](PropertiesDeploy.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

<a name="deployConfigurationObjectIdPost"></a>
# **deployConfigurationObjectIdPost**
> PropertiesDeploy deployConfigurationObjectIdPost(objectId)

POST deployment task policy for firewall namespace.

Will POST a new deployment task within the firewall namespace.

### Example
```javascript
var BigIqDeployConfiguration = require('big_iq_deploy_configuration');

var apiInstance = new BigIqDeployConfiguration.DefaultApi();

var objectId = "objectId_example"; // String | 


var callback = function(error, data, response) {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
};
apiInstance.deployConfigurationObjectIdPost(objectId, callback);
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **objectId** | **String**|  | 

### Return type

[**PropertiesDeploy**](PropertiesDeploy.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

