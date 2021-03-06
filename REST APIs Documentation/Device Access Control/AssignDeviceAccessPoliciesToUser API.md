
## ***POST*** /V1/CMDB/UserDeviceAccessPolicy/AssignDeviceAccessPolicies
Call this API to assign device access policies to user.<br>
***Note:*** Customer can call this API if only want to assign new policies to accounts without delete the already existing policy in accounts. And customer needs to have **Share Policy Management** privilege at least to call this API.

## Detail Information

> **Title** : Assign Device Access Policies to User API<br>

> **Version** : 08/19/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/UserDeviceAccessPolicy/AssignDeviceAccessPolicies

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|authenticationServer|	string|	The authentication server name. |
|userName*	|string	|The user name. |
|policies*	|List of string	|The list of policy name. |
>***Note:*** <br> 1. The authentication server is optional<br> 2. The program will looks for users on all servers(including local  and external servers) when the authentication server name is null or empty.<br> 3. The program will looks for users on local server when the authentication server name is "NetBrain", otherwise will looks for users on the specified server.

***Example:*** 


```python
{
 
  "authenticationServer":"AD ServerName",
  "userName":"user1",
  "policies" : ["policyName1", "policyName2"]              
 
}
```

## Parameters(****required***)

> No required parameter.

## Headers

> **Data Format Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Content-Type | string  | support "application/json" |
| Accept | string  | support "application/json" |

> **Authorization Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| token | string  | Authentication token, get from login API. |

## Response
|**Name**|**Type**|**Description**|
|------|------|------|
|statusCode| integer | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |


***Example:***


```python
{
    "statusCode": 790200,
    "statusDescription": "Success."
}
```

## Full Example:


```python
# import python modules 
import requests
import time
import urllib3
import pprint
import json
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

# Set the request inputs
token = "9dbd05fa-2630-4c2f-bfd2-86973e886bf2"
nb_url = "https://10.10.7.209"

body = {
 
  "authenticationServer":"NetBrain",
  "userName":"deviceAPAPI",
  "policies" : ["New_DeviceAccessPolicy_GL1", "New_DeviceAccessPolicy_GL2"]              
 
}

headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

def AssignDeviceAccessPoliciesToUser(headers, body, nb_url):
    full_url = nb_url + "/ServicesAPI/API/V1/CMDB/UserDeviceAccessPolicy/AssignDeviceAccessPolicies"
    try:
        response = requests.post(full_url, data = json.dumps(body), headers=headers, verify=False)
        if response.status_code == 200:
            res = response.json()
            return (res)
        else:
            return ("Assign user to device access policy Failed! - " + str(response.text))

    except Exception as e:
            return (str(e)) 
        
result = AssignDeviceAccessPoliciesToUser(headers, body, nb_url)
result
```
    {"statusCode": 790200, "statusDescription": "Success"}

# cURL Code from Postman


```python
curl -X POST \
  https://10.10.7.209/ServicesAPI/API/V1/CMDB/UserDeviceAccessPolicy/AssignDeviceAccessPolicies \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: f22d31e9-6a4f-4746-841e-905babca7460' \
  -H 'cache-control: no-cache' \
  -H 'token: 9dbd05fa-2630-4c2f-bfd2-86973e886bf2' \
  -d '{
  "authenticationServer":"NetBrain",
  "userName":"deviceAPAPI",
  "policies" : ["New_DeviceAccessPolicy_GL1", "New_DeviceAccessPolicy_GL2"]              
 
}'
```
