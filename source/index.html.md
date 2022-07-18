---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---



# Introduction

Welcome to the Plinu ML API! 

You can use our API to access the Machine Learning endpoints, which will give you predictions based on the models created for you.

We have language bindings in Shell, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

The menu on the right contains the index for all the endpoints currently created and has a search bar.

<aside class="success">
Make sure to replace <code>{server_ip}</code> with your ip address, <code>{user} {password}</code> with the correct information, <code>{token}</code> with the correct token and <code>{model_id}</code> with the correct model.
</aside>



## Authentication
<aside class="notice">
All <strong>Authentication</strong> endpoints do <strong>NOT</strong> require <code>ADMIN</code> user type to access. 
</aside>

Plinu, when used inside a secure infrastructure, uses HTTPBasicAuth to allow access to the API. The port used to comunicate with the API is:

`Port 80`

Plinu expects a **Authentication Token** to be used for **all endpoints** requests, but user and password can still be used:

`Authorization: Basic {token}`

`Authorization: Basic {user}:{password}`


## Get Token

> To receive a token use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $user:$password -i -X GET http://$server_ip/api/v1/get_token
# or
curl -u $token:none -i -X GET http://$server_ip/api/v1/get_token  
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/get_token'
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
# command
response = requests.request('GET', url, auth=basic_auth, allow_redirects=False)
print(response.text)
```
```javascript
// variables to be used
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/get_token";
// command settings
var settings = {
    url: url,
    method: "GET",
    dataType: 'json',
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> The above request should return a JSON structured like this:

```json
{
  "data":{
    "duration": 600,
    "token": "{token with 600 sec duration}"
  }
}
``` 

This endpoint returns a **Authentication Token** for further calls. You can receive a new token using <code>{user} {password}</code> information or a <code>previous {token}</code>.

### HTTP Request

`GET http://{server_ip}/api/v1/get_token`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
None | none | No parameters needed for this endpoint.



# Administration Endpoints
<aside class="warning">
All <strong>Administration</strong> endpoints require <code>ADMIN</code> user type to access.
</aside>

The following endpoint are all focused on **user administration**. All endpoints are named after the action they will perform.


## Get All Users
> To get a JSON with all the users in the DB use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $token:none -i -X GET http://$server_ip/api/v1/get_users
# or
curl -u $user:$password -i -X GET http://$server_ip/api/v1/get_users   
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/get_users'
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
response = requests.request('GET', url, auth=basic_auth, allow_redirects=False)
print(response.text)
```
```javascript
// variables to be used
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/get_users";
// command settings
var settings = {
    url: url,
    method: "GET",
    dataType: 'json',
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> JSON Response:

```json
{
  "data": {
    "users": [
      {
        "company": "Plinu",
        "email": "admin",
        "name": "Admin",
        "status active": true,
        "user type": "Admin"
      },
      {
        "company": "Plinu",
        "email": "email_1@plinu.com",
        "name": "User 1",
        "status active": true,
        "user type": "User"
      },
      {
        "company": "Plinu",
        "email": "email_2@plinu.com",
        "name": "User 2",
        "status active": true,
        "user type": "User"
      }
    ]
  }
}
```

This endpoint retrieves all users in the DB and presents them as a JSON.

### HTTP Request

`GET http://{server_ip}/api/v1/get_users`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
None | none | No parameters needed for this endpoint.


## Create a User
> To create a new user in the DB use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $token:none -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"test_user@plinu.com","name":"user","password":"python","type":"User"}' \
  http://$server_ip/api/v1/signup
# or
curl -u $user:$password -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"test_user@plinu.com","name":"user","password":"python","type":"User"}' \
  http://$server_ip/api/v1/signup 
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/signup'
data = {"email": "test_user2@plinu.com", "name": "user", "password": "python","type": "User"}
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
# command
response = requests.post(url, json=data, auth=basic_auth)
print(response.text)
```
```javascript
// variables to be used
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/signup";
var data = JSON.stringify({"email": "test_user@plinu.com", "name": "user", "password": "python","type": "User"});
// command settings
var settings = {
    url: url,
    method: "POST",
    dataType: 'json',
    data: data,
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> JSON Response:

```json
{
  "data": "test_user@plinu.com created"
}
```

This endpoint creates new users in the DB. All new users will have the active status as **true** by default and will be assigned to the **company** of the **Admin user** that created them.

### HTTP Request

`POST http://{server_ip}/api/v1/singup`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
email | string (100) | **Primary key**: Unique email address for new user. 
name | string (100) | New user name.
password | string (100) | New user password.
type | string (Admin, User)| User type for the new user.


## Change Password for a User
> To change the password for a user in the DB use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $token:none -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"test_user@plinu.com","new password":"pythons"}' \
  http://$server_ip/api/v1/change_pass  
# or
curl -u $user:$password -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"test_user@plinu.com","new password":"pythons"}' \
  http://$server_ip/api/v1/change_pass  
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/change_pass'
data = {"email": "test_user@plinu.com", "new password": "pythons"}
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
# command
response = json.loads(requests.post(url, json=data ,auth=basic_auth))
print(response.text)
```
```javascript
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/change_pass";
var data = JSON.stringify({"email": "test_user@plinu.com", "new password": "pythons"});
// command settings
var settings = {
    url: url,
    method: "POST",
    dataType: 'json',
    data: data,
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> JSON Response:

```json
{
  "data": "password changed"
}
```

This endpoint changes a specific users's password. At this point there are no restrictions for the password in terms of characters that should be used, just the length to 100 characters.

### HTTP Request

`POST http://{server_ip}/api/v1/change_pass`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
email | string (100) | **Primary key**: Unique email address for new user.
new password | string (100) | New password for user.


## Change Type of User
> To change the user type in the DB use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $token:none -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"test_user@plinu.com","type":"Admin"}' \
  http://$server_ip/api/v1/change_user_type
# or
curl -u $user:$password -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"test_user@plinu.com","type":"Admin"}' \
  http://$server_ip/api/v1/change_user_type  
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/change_user_type'
data = {"email": "test_user@plinu.com", "type": "Admin"}
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
# command
response = json.loads(requests.post(url, json=data ,auth=basic_auth))
print(response.text)
```
```javascript
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/change_user_type";
var data = JSON.stringify({"email": "test_user@plinu.com", "type": "Admin"});
// command settings
var settings = {
    url: url,
    method: "POST",
    dataType: 'json',
    data: data,
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> JSON Response:

```json
{
  "data": "type changed to {Admin, User}"
}
```

This endpoint changes the user type for a specific user. The types of users allowed are **"Admin"** or **"User"**.

### HTTP Request

`POST http://{server_ip}/api/v1/change_user_type`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
email | string (100) | **Primary key**: Unique email address for new user.
new type | string ("Admin", "User") | New type for user.


## Change Active Status for a User
> To change the active status for a user in the DB use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $token:none -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"test_user@plinu.com","active":"false"}' \
  http://$server_ip/api/v1/change_user_status
# or
curl -u $user:$password -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"test_user@plinu.com","active":"false"}' \
  http://$server_ip/api/v1/change_user_status  
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/change_user_status'
data = {"email": "test_user@plinu.com", "active": "false"}
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
# command
response = json.loads(requests.post(url, json=data ,auth=basic_auth))
print(response.text)

```
```javascript
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/change_user_status";
var data = JSON.stringify({"email": "test_user@plinu.com", "active": "true"});
// command settings
var settings = {
    url: url,
    method: "POST",
    dataType: 'json',
    data: data,
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> JSON Response:

```json
{
  "data": "status changed to {true, false}"
}
```

This endpoint changes the active status for a specific user. The active status allowed are **"true"** or **"false"**.

### HTTP Request

`POST http://{server_ip}/api/v1/change_user_status`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
email | string (100) | **Primary key**: Unique email address for new user.
new status | boolean ("true", "false") | New status for user.



# Rule Endpoints

<aside class="notice">
All <strong>Prediction</strong> endpoints do <strong>NOT</strong> require <code>ADMIN</code> user type to access. 
</aside>

The following endpoints give you the ability to add usernames, get stats, and get categories based on rules:

* **new_usernames**: check a new username or group of usernames stats in *grin.co* and insert them into the DB.
* **get_stats**: get a username or group of usernames stats if they exist in the DB.
* **get_category**: check a username or group of usernames stats already in DB

Each endpoint can either have a **GET** method or a **POST** method but not both.

**HTTP Request**

`POST http://{server_ip}/api/v1/new_usernames`

`GET http://{server_ip}/api/v1/get_stats`

`GET http://{server_ip}/api/v1/get_category`


## Endpoint: New Usernames
> To add a new username or a group of usernames into the db and get their stats use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $token:none -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"usernames":["username1","username2", ...]}' \
  http://$server_ip/api/v1/new_usernames
# or
curl -u $user:$password -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"usernames":["username1","username2", ...]}' \
  http://$server_ip/api/v1/new_usernames
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/new_usernames'
data = {"usernames": ["username1","username2", ...]}
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
# command
response = json.loads(requests.post(url, json=data ,auth=basic_auth))
print(response.text)
```
```javascript
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/new_usernames;
var data = JSON.stringify({"usernames":["username1","username2", ...]});
// command settings
var settings = {
    url: url,
    method: "POST",
    dataType: 'json',
    data: data,
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> JSON Response:

```json
{
	"data": [{
		"category": "Br",
		"stats": ["159.0", "7.55", "33.0"],
		"username": "username1"
	}, {
		"category": "Gl",
		"stats": ["324900000.0", "0.32", "6600.0"],
		"username": "username2"
	},...]
}
```

This endpoint is for **New Usernames** and using the backend will check if they are already in the DB, if not, it will 
use *grin.co* to extract their stats and add them to the DB, returning the stats and category. If a username is 
already in the DB, it will reply with an error.

<aside class="warning">
<strong>Caution</strong> this endpoint can take long to answer depending on webpage <code>grin.co</code> response.
</aside>

### HTTP Request

`POST http://{server_ip}/api/v1/new_usernames`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
usernames | Array<String> | Array containing a username or group of usernames in **String** values


## Endpoint: Get Stats
> To get the statistics of a username or a group of usernames already in the db use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $token:none -i -X GET \
  -H "Content-Type: application/json" \
  -d '{"usernames":["username1","username2", ...]}' \
  http://$server_ip/api/v1/get_stats
# or
curl -u $user:$password -i -X GET \
  -H "Content-Type: application/json" \
  -d '{"usernames":["username1","username2", ...]}' \
  http://$server_ip/api/v1/get_stats
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/get_stats'
data = {"usernames": ["username1","username2", ...]}
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
# command
response = json.loads(requests.get(url, json=data ,auth=basic_auth))
print(response.text)
```
```javascript
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/get_stats;
var data = JSON.stringify({"usernames":["username1","username2", ...]});
// command settings
var settings = {
    url: url,
    method: "GET",
    dataType: 'json',
    data: data,
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> JSON Response:

```json
{
	"data": [{
		"category": "Br",
		"stats": ["159.0", "7.55", "33.0"],
		"username": "username1"
	}, {
		"category": "Gl",
		"stats": ["324900000.0", "0.32", "6600.0"],
		"username": "username2"
	},...]
}
```

This endpoint is for **Get Stats** and will return the stats and category of a user or group of users if they are 
already in the DB. If a username is **NOT** in the DB, it will reply with an error.

### HTTP Request

`GET http://{server_ip}/api/v1/get_stats`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
usernames | Array<String> | Array containing a username or group of usernames in **String** values


## Endpoint: Get Category
> To get the category of a username or a group of usernames already in the db use this code:

```shell
# variables to be used
user={user}
password={password}
server_ip={server_ip}
token={token}
# command
curl -u $token:none -i -X GET \
  -H "Content-Type: application/json" \
  -d '{"usernames":["username1","username2", ...]}' \
  http://$server_ip/api/v1/get_category
# or
curl -u $user:$password -i -X GET \
  -H "Content-Type: application/json" \
  -d '{"usernames":["username1","username2", ...]}' \
  http://$server_ip/api/v1/get_category
```
```python
# variables to be used
user = {user}
password = {password}
server_ip = {server_ip}
token = {token}
url = 'http://' + server_ip + '/api/v1/get_category'
data = {"usernames": ["username1","username2", ...]}
# imports
import requests
# auth using User Password
basic_auth = (user, password)
# auth using Token
basic_auth = (token, None)
# command
response = json.loads(requests.get(url, json=data ,auth=basic_auth))
print(response.text)
```
```javascript
var user = {user}
var password = {password}
var server_ip = {server_ip}
var token = {token}
var url = "http://"+server_ip+"/api/v1/get_category;
var data = JSON.stringify({"usernames":["username1","username2", ...]});
// command settings
var settings = {
    url: url,
    method: "GET",
    dataType: 'json',
    data: data,
    headers: {
        "Content-Type": "application/json",
        // for User Password Auth use
        "Authorization": "Basic " + btoa(user + ":" + password)
        // for Token Auth use
        "Authorization": "Basic " + btoa(token + ":None")
    },
    timeout: 0,
    success: function (response) {
        console.log(JSON.stringify(response));
    },
    error: function (error) {
        console.log(JSON.stringify(error));
    }
};
// command
$.ajax(settings);
```

> JSON Response:

```json
{
	"data": {
		"group_category": "Gl",
		"ind_categories": [{
			"category": "Br",
			"username": "username1"
		}, {
			"category": "Gl",
			"username": "username2"
		},...]
	}
}
```

This endpoint is for **Get Category** and will return the category of a user or group of users if they are 
already in the DB. If a username is **NOT** in the DB, it will reply with an error.

### HTTP Request

`GET http://{server_ip}/api/v1/get_category`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
usernames | Array<String> | Array containing a username or group of usernames in **String** values