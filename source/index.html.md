---
title: Target API v1.0

language_tabs:
  - shell: Shell
  - http: HTTP
  - html: JavaScript
  - javascript: Node.JS
  - python: Python
  - ruby: Ruby
  - java: Java

toc_footers: []
includes: []
search: true
highlight_theme: darkula
---

# Target API v1.0

Target has three groups of APIs:

- Delivery
- Admin APIs
- Legacy admin APIs

Delivery APIs are publicly accessible and can be used to deliver content from Target edge servers to customer websites and servers. Legacy admin APIs require authentication credentials to be passed with every request. The current generation of APIs require both an API Key and a token in the headers to authenticate. See the Authentication page on how to obtain an API Key and token.

Target’s admin APIs follow the same URL schema as the rest of the marketing cloud:

https://mc-api.adobe.io/{tenant}/target/{rest-of-url}

REST apis to list, create and modify Target Activities, Audiences and Offers.

Base URL = mc.adobe.io

<a href="https://mc.adobe.io/target/">Terms of service</a>

License: <a href="https://mc.adobe.io/target/">Adobe Target License Version 1.0</a>

# Authentication

You must go through Adobe's Developer Portal (see link above to 'API Keys') to get a set of credentials before
using the following APIs:

- All APIs listed under the 'AB and XT' dropdown

-Collection, Feed, and Entity APIs under the 'Recommendations' dropdown

The other APIs listed here either don’t require authentication or have an authentication option that is specific to the API.   

To get started with these APIs you must be authorized by your organization to use the administrative login for your organization. Only users who are designa

# Activities

Activity List Controller

## Get Activities

> Code samples

````shell
# You can also use wget
curl -X get ://mc.adobe.io//{tenant}/target/activities
````

````http
GET ://mc.adobe.io//{tenant}/target/activities HTTP/1.1
Host: mc.adobe.io
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://mc.adobe.io//{tenant}/target/activities',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://mc.adobe.io//{tenant}/target/activities', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/activities`

*List activities*

Get a list of AB and Experience Targeted activities created in Target, with the ability to filter and sort by attributes.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
parameters|query|ref|true|parameters



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Create Activity

> Code samples

````shell
# You can also use wget
curl -X post ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab
````

````http
POST ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab',
    method: 'post',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab', { method: 'POST'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`POST /{tenant}/target/activities/ab`

*Create an AB activity*

Creates a new AB activity with the specified contents and returns the created activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
abActivity|body|ABActivity|true|abActivity



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|There was an error creating the AB activity. Most probably invalid data was provided by the user.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Get Activities

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/activities/ab/{id}`

*Get AB activity by id*

Fetch the current definition of a AB activity if it is found as referenced by the id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Update Activity

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/ab/{id}`

*Update an AB activity*

Updates the AB activity definition with the contents as provided in the request. This can change the state and behaviour of an existing activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
abActivity|body|ABActivity|true|abActivity



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Delete Activity

> Code samples

````shell
# You can also use wget
curl -X delete ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}
````

````http
DELETE ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}',
    method: 'delete',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', { method: 'DELETE'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.delete '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.delete('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`DELETE /{tenant}/target/activities/ab/{id}`

*Delete an AB activity*

Deletes the activity that is referenced by the id, if it is found.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Update AB activity

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/name
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/name HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/name',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/name', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/name', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/name', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/name");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/ab/{id}/name`

*Rename an AB activity*

Updates the name of the AB activity that is referenced by the supplied id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.ab.priority.updatePriorityUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/priority
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/priority HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/priority',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/priority', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/priority', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/priority', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/priority");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/ab/{id}/priority`

*Change priority for AB activity*

Change priority for the AB activity that is referenced by the supplied id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Update Activity Schedule

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/schedule
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/schedule HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/schedule',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/schedule', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/schedule', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/schedule', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/schedule");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/ab/{id}/schedule`

*Update the an AB activity's schedule*

Update the startsAt and endsAt fields of the AB activity referenced by the provided id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Update Activity State

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/state
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/state HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/state',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/state', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/state', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/state', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/state");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/ab/{id}/state`

*Update state for an AB activity*

Update state for the AB activity that is referenced by the provided id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## XT activities

> Code samples

````shell
# You can also use wget
curl -X post ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt
````

````http
POST ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt',
    method: 'post',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt', { method: 'POST'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`POST /{tenant}/target/activities/xt`

*Create a XT activity*

Create an Experience Targeted activity based on the provided contents.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
abActivity|body|ABActivity|true|abActivity



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|There was an error creating the Experience Targeted activity. Most probably invalid data was provided by the user.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Get XT Activity

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/activities/xt/{id}`

*Get a XT activity by id*

Gets a Experience Targeted activity that is referenced by the id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Update XT Activity

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/xt/{id}`

*Update a XT activity*

Updates the Experience Targeted activity definition with the contents as provided in the request. This can change the state and behaviour of an existing activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
abActivity|body|ABActivity|true|abActivity



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Delete XT Activity

> Code samples

````shell
# You can also use wget
curl -X delete ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}
````

````http
DELETE ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}',
    method: 'delete',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', { method: 'DELETE'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.delete '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.delete('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`DELETE /{tenant}/target/activities/xt/{id}`

*Delete a XT activity*

Delete a Experience Targeted activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## Update XT Activity

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/name
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/name HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/name',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/name', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/name', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/name', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/name");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/xt/{id}/name`

*Rename a XT activity*

Rename a Experience Targeted activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.xt.priority.updatePriorityUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/priority
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/priority HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/priority',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/priority', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/priority', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/priority', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/priority");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/xt/{id}/priority`

*Change priority for an XT activity*

Change priority for the Experience Targeted activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.xt.schedule.updateScheduleUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/schedule
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/schedule HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/schedule',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/schedule', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/schedule', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/schedule', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/schedule");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/xt/{id}/schedule`

*Update schedule of an XT activity*

Update the startsAt and endsAt fields of an Experience Targeted activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.xt.state.updateStateUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/state
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/state HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/state',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/state', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/state', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/state', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/state");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/xt/{id}/state`

*Update state for an XT activity*

Update the state for the Experience Targeted activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.changelog.getChangelogUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/changelog
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/changelog HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/changelog',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/changelog', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/changelog', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/changelog', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/changelog");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/activities/{id}/changelog`

*List activity changelog*

documentation.notes.activities.changelog.getChangelog

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
parametersMap|query|ref|true|parametersMap



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.name.updateNameUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/name
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/name HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/name',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/name', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/name', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/name', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/name");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/{id}/name`

*Rename an activity*

Rename an activity. This change will be reflected on the Target user interface after the next refresh.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.priority.updatePriorityUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/priority
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/priority HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/priority',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/priority', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/priority', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/priority', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/priority");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/{id}/priority`

*Change priority for an activity*

Changes the priority for an activity, which will affect the way Target will evaluate the activity selection at runtime.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.schedule.updateScheduleUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/schedule
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/schedule HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/schedule',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/schedule', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/schedule', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/schedule', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/schedule");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/{id}/schedule`

*Update the schedule of an activity*

Update the startsAt and endsAt fields of an activity which controls when the activity goes live.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.state.updateStateUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/state
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/state HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/state',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/state', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/state', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/state', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/{id}/state");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/{id}/state`

*Update state for an activity*

Update state for an activity. Allowed states are approved, deactivated, deleted, paused, saved.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
activityDescription|body|ActivityDescription|true|activityDescription



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# Reports

AP Performance Reports

## Get Report

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/report/performance
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/report/performance HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/report/performance',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/report/performance', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/report/performance', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/report/performance', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/ab/{id}/report/performance");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/activities/ab/{id}/report/performance`

*AB activity performance report*

Retrieve the performance report data for the AB activity referenced by the provided id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
parameters|query|ref|true|parameters



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.abt.report.performance.getReportByIdUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}/report/performance
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}/report/performance HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}/report/performance',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}/report/performance', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}/report/performance', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}/report/performance', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}/report/performance");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/activities/abt/{id}/report/performance`

*Behavior Targeted activity performance report*

Retrieve the performance report data for the Behavior Targeted activity referenced by the provided id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
parameters|query|ref|true|parameters



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.xt.report.performance.getReportByIdUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/report/performance
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/report/performance HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/report/performance',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/report/performance', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/report/performance', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/report/performance', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/xt/{id}/report/performance");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/activities/xt/{id}/report/performance`

*XT activity performance report*

Retrieve the performance report data for the Experience activity referenced by the provided id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
parameters|query|ref|true|parameters



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# Automated Personalization Activities

ABT Campaign Controller

## activities.abt.createActivityUsingPOST

> Code samples

````shell
# You can also use wget
curl -X post ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt
````

````http
POST ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt',
    method: 'post',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt', { method: 'POST'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`POST /{tenant}/target/activities/abt`

*Create a Behavior Targeted activity*

Creates a new Behavior Targeted activity with the specified contents and returns the created activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
abtActivity|body|ABTActivity|true|abtActivity



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.abt.getActivityUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/activities/abt/{id}`

*Get Behavior Targeted activity by id*

Fetch the current definition of a Behavior Targeted  activity if it is found as referenced by the id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.abt.createActivityUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/activities/abt/{id}`

*Create a Behavior Targeted activity*

Creates a new Behavior Targeted activity with the specified contents and returns the created activity.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
abtActivity|body|ABTActivity|true|abtActivity



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## activities.abt.deleteActivityUsingDELETE

> Code samples

````shell
# You can also use wget
curl -X delete ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}
````

````http
DELETE ://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}',
    method: 'delete',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', { method: 'DELETE'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.delete '://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.delete('://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/activities/abt/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`DELETE /{tenant}/target/activities/abt/{id}`

*Delete an Behavior Targeted activity*

Deletes the Behavior Targeted activity that is referenced by the id, if it is found.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# /audiences

Audience List Controller

## audiences.getAudiencesUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/audiences`

*List audiences*

List all available audiences with options to filter and sort by each available field.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
parameters|query|ref|true|parameters



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|You are not authorized to perform this request
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## audiences.createAudienceUsingPOST

> Code samples

````shell
# You can also use wget
curl -X post ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences
````

````http
POST ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v2+json
Accept: application/vnd.adobe.target.v2+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences',
    method: 'post',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences', { method: 'POST'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`POST /{tenant}/target/audiences`

*Create an audience*

Create a new audience as specified by the contents of the request and return the newly-created audience definition.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
audience|body|Audience|true|audience



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## audiences.getAudienceUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v2+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/audiences/{id}`

*Get an audience by id*

Get the audience definition specified by the provided id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## audiences.updateAudienceUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v2+json
Accept: application/vnd.adobe.target.v2+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/audiences/{id}`

*Update an audience*

Update an audience with the new rules specified by the request data.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
audience|body|Audience|true|audience



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## audiences.deleteAudienceUsingDELETE

> Code samples

````shell
# You can also use wget
curl -X delete ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}
````

````http
DELETE ://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v2+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}',
    method: 'delete',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', { method: 'DELETE'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.delete '://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.delete('://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/audiences/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`DELETE /{tenant}/target/audiences/{id}`

*Delete an audience*

Delete the audience referenced by the specified id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# /batch

Batch Controller

## batch.processBatchOperationsUsingPOST

> Code samples

````shell
# You can also use wget
curl -X post ://api1.staging.testandtarget.omniture.com//{tenant}/target/batch
````

````http
POST ://api1.staging.testandtarget.omniture.com//{tenant}/target/batch HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: */*
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/batch',
    method: 'post',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/batch', { method: 'POST'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post '://api1.staging.testandtarget.omniture.com//{tenant}/target/batch', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('://api1.staging.testandtarget.omniture.com//{tenant}/target/batch', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/batch");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`POST /{tenant}/target/batch`

*Execute a batch of REST API calls*

Stack multiple API calls together and execute them in a single batch.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
batchRequest|body|BatchRequest|true|batchRequest



> Body parameter

````json
{}
````
### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# /environments

Environment List Controller

## environments.getEnvironmentsUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/environments
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/environments HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/environments',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/environments', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/environments', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/environments', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/environments");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/environments`

*List environments*

List all available environments with the options to filter and sort.

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# /mbox

Mbox Controller

## mbox.getMboxUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/mbox/{mboxName}
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/mbox/{mboxName} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/mbox/{mboxName}',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/mbox/{mboxName}', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/mbox/{mboxName}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/mbox/{mboxName}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/mbox/{mboxName}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/mbox/{mboxName}`

*Get mbox parameters*

documentation.notes.mbox.getMbox

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
mboxName|path|string|true|mboxName



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# /mboxes

Mbox List Controller

## mboxes.getMboxesUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/mboxes
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/mboxes HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/mboxes',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/mboxes', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/mboxes', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/mboxes', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/mboxes");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/mboxes`

*List available mboxes*

List all available mboxes for a specific client with the options to filter and sort.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
parametersMap|query|ref|true|parametersMap



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# /offers

Offer List Controller

## offers.getOffersUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/offers");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/offers`

*List offers*

Retrieve the list of previously-created content offers. The parameters passed through the query string are optional and are used to indicate the sorting and filtering options.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
parametersMap|query|ref|true|parametersMap



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request was invalid. Check the parameters list and try again
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Forbidden
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## offers.content.createOfferUsingPOST

> Code samples

````shell
# You can also use wget
curl -X post ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content
````

````http
POST ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content',
    method: 'post',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content', { method: 'POST'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`POST /{tenant}/target/offers/content`

*Create a new content offer*

Creates a new content offer as defined by the request data.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
offer|body|ContentOffer|true|offer



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## offers.content.getOfferUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/offers/content/{id}`

*Get offer by id*

Retrieves the contents of an offer by providing it's id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|You are not authorized to perform this request
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The offer was not found or the offer type is different than "content"

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## offers.content.updateOfferUsingPUT

> Code samples

````shell
# You can also use wget
curl -X put ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}
````

````http
PUT ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}',
    method: 'put',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', { method: 'PUT'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`PUT /{tenant}/target/offers/content/{id}`

*Update a content offer by id*

Updates the content offer referenced by the id specified in the URL.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id
offer|body|ContentOffer|true|offer



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

## offers.content.deleteOfferUsingDELETE

> Code samples

````shell
# You can also use wget
curl -X delete ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}
````

````http
DELETE ://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id} HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}',
    method: 'delete',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', { method: 'DELETE'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.delete '://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.delete('://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/offers/content/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`DELETE /{tenant}/target/offers/content/{id}`

*Delete a content offer by id*

Deletes the content offer referenced by the provided id.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
id|path|integer|true|id



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# /profileattributes/mbox

Mbox Profile Attribute Controller

## profileattributes.mbox.getMboxProfileAttributesUsingGET

> Code samples

````shell
# You can also use wget
curl -X get ://api1.staging.testandtarget.omniture.com//{tenant}/target/profileattributes/mbox
````

````http
GET ://api1.staging.testandtarget.omniture.com//{tenant}/target/profileattributes/mbox HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/profileattributes/mbox',
    method: 'get',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/profileattributes/mbox', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get '://api1.staging.testandtarget.omniture.com//{tenant}/target/profileattributes/mbox', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('://api1.staging.testandtarget.omniture.com//{tenant}/target/profileattributes/mbox', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/profileattributes/mbox");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`GET /{tenant}/target/profileattributes/mbox`

*List the available profile attributes*

Retrieve the list of available profile attributes and mbox parameters of type profile

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
parameters|query|ref|true|parameters



### Responses

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>

# /users

Ims User Controller

## users.ims.provisionUserUsingPOST

> Code samples

````shell
# You can also use wget
curl -X post ://api1.staging.testandtarget.omniture.com//{tenant}/target/users/ims
````

````http
POST ://api1.staging.testandtarget.omniture.com//{tenant}/target/users/ims HTTP/1.1
Host: api1.staging.testandtarget.omniture.com
Content-Type: application/vnd.adobe.target.v1+json
Accept: application/vnd.adobe.target.v1+json
````

````html
<script>
  $.ajax({
    url: '://api1.staging.testandtarget.omniture.com//{tenant}/target/users/ims',
    method: 'post',
    success: function(data) {
      console.log(JSON.stringify(data));
    }
  })
</script>
````

````javascript
const request = require('node-fetch');
fetch('://api1.staging.testandtarget.omniture.com//{tenant}/target/users/ims', { method: 'POST'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post '://api1.staging.testandtarget.omniture.com//{tenant}/target/users/ims', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('://api1.staging.testandtarget.omniture.com//{tenant}/target/users/ims', params={
  # TODO
})

print r.json()
````

````java
URL obj = new URL("://api1.staging.testandtarget.omniture.com//{tenant}/target/users/ims");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());
````

`POST /{tenant}/target/users/ims`

*Provision a technical user account*

Creates a new technical user. This user can later be used for invoking REST API operations.

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
imsUserRequest|body|ImsUserRequest|true|imsUserRequest



> Body parameter

### Responses

Status|Meaning|Description
---|---|---|
201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.

> Example responses

<aside class="success">
This operation does not require authentication
</aside>




