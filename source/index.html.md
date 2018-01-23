---
title: Target API v1.0
toc_footers:
    - <a href='https://console.adobe.io'>Adobe I/O Console</a>
    - <a href='https://marketing.adobe.com/resources/help/en_US/target/'>Target Product Docs</a>
    - <a href='http://developers.adobetarget.com'>Developer Portal Homepage</a>
includes: []
search: true
highlight_theme: Xcode
---

# Introduction

Welcome to the Adobe Target API. Adobe Target is a part of the Adobe Experience Cloud that helps you to optimize and personalize your customers' experience.

You can use the Target REST APIs to list, create and modify Target Activities, Audiences and Offers, retreive reports, update profiles etc.


# Server Side Delivery


## Overview
Adobe Target lets your application make mbox calls from any browser, mobile device, or even another server.  The Server Side delivery API is specifically designed to integrate Adobe Target with any server side platform that makes HTTP/s calls.  You can use the API to integrate your custom application with Target.  This is especially valuable for organizations that want to deliver targeting to a non-browser based IoT device, such as a connected TV, kiosk, or
in-store digital screen.  This API implements existing mbox features in a RESTful manner.  This API does not process cookies or redirect calls.

## Authentication

There is no authentication for this API.

There is no notion of a "user role" in the Server Side Delivery API because it represents a call to fetch content or report events to Target edge servers

## Delivery Postman Collection

Postman is a application that makes it easy to fire API calls. This Postman collection contains Server Side Delivery and Profile API calls. Just click on the 'Run in Postman' button to import the Target API collection.

<aside class="notice">
Don't forget to replace the clientcode and the mbox name with your own in the API calls. The APIs in the collection use a demo account.
</aside>

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/94cb2f003ae62aef8136)


## Input Parameters

> Delivery API Sample Request. This is a request with just the mbox name in the POST body.

````shell
curl -X POST \
  'https://adobetargetmobile.tt.omtrdc.net/rest/v1/mbox/my-session-id?client=adobetargetmobile' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{
  "mbox" : "l5-mobile-ab"
}'

````

> Response for Sample Request

````json
{
    "tntId": "111499796294071-449025.28_44",
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "content": "Use 10OFF for $10 off for orders over $100",
    "sessionId": "my-session-id"
}
````


> Delivery API request with all possible inputs

````shell
curl -X POST \
  'https://adobetargetmobile.tt.omtrdc.net/rest/v1/mbox/A210702C-402F-4458-9869-FCE64F318AE6?client=adobetargetmobile' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_3) AppleWebKit/537.75.14 (KHTML, like Gecko) Version/7.0.3 Safari/7046A194A' \
  -d '{
  "mbox" : "a1-mobile-ab",
  "thirdPartyId" : "12345abcde",
  "profileParameters" : {
    "param1" : "value1",
    "param2" : "value2",
    "entity.id" : "entityId",
    "entity.name" : "entityName"
  },
  "mboxParameters" : {
    "screenHeight": 1057,
    "screenWidth": 1920,
    "browserWidth": 1040,
    "browserHeight": 960,
    "browserTimeOffset": 240,
    "colorDepth": 24,
    "mboxXDomain": "enabled",
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36",
    "mboxMCGVID": "91394045728588414913028121188926585416",
    "mboxAAMB": "cIBAx_aQzFEHcPoEv0GwcQ",
    "mboxMCGLH": 7,
    "vst.alias.id" : "2342345364532",
    "vst.alias.authState" : "1"
 },
  "requestLocation" : {
    "pageURL" : "http://demo/demo/store/",
    "referrerURL" : "http://demo/demo/store/",
    "ipAddress" : "128.10.10.1",
    "impressionId" : "15989",
    "host" : "staging-1"
  }
}'

````

> Response for Delivery API request with all inputs

````json
{
    "thirdPartyId": "12345abcde",
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "content": "Get 5% off using code 5OFF!",
    "sessionId": "A210702C-402F-4458-9869-FCE64F318AE6"
}

````

### POST Request

The Server Side Delivery API only supports POST requests.  Here is a sample POST call performed using the API.

`https://your-client-code.tt.omtrdc.net/rest/v1/mbox/my-session-123?client=your-client-code`

In this request,

<table>
    <tbody>
        <tr>
            <td>my-session-123</td>
            <td>
                <p>This is the Session Id that should be generated and maintained by you. The Session Id can be any printable string except a space, ?, or /. It should be between 1 and 128 characters in length.</p>
                <p>For a particular session, its value must stay the same across multiple requests.</p>
                <p>Routing to a particular node in the edge cluster is done using Session Id.</p>
                <p>The session is active for 30 minutes on the server side. Therefore, you should n't use a different Session Id for a particular tntId/thirdPartyId within 30 minutes of the last request made with the tntId/thirdPartyId. Otherwise, changes to the profile could be inconsistent and unpredictable.</p>
                <p>Using the same Session ID with multiple tntIds/thirdPartyIds may cause unpredictable changes to the profiles identified by the tntId/thirdPartyIDs.</p>
            </td>
        </tr>
        <tr>
            <td>your-client-code</td>
            <td>Your account's client code. This parameter is mandatory for each request.</td>
        </tr>
    </tbody>
</table>




The list of parameters that you can supply in the body of the request.

### Request Parameters

<table class="delivery-api">
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Description</th>
            <th>Default Value</th>
            <th>Validation</th>
        </tr>
    </thead>
    <tbody>
        <tr class="odd">
            <td class="first">mbox</td>
            <td>The mbox name.</td>
            <td>None, it cannot be empty.</td>
            <td class="last">
                <p>Same validation as for all mbox calls.</p>
                <p>1 &lt; Length &lt; 250</p>
                <p>Cannot contains any of the following characters: ', ", %22, %27, &lt;, &gt;, %3C, %3E</p>
            </td>
        </tr>
        <tr>
            <td class="first">clicked</td>
            <td>
                <p>Equivalent of using the "-clicked" suffix in mbox names for mbox calls.</p>
                <p><i>Click mboxes only work for campaigns with metrics that have a specific mbox selected, for example "click from homePageHer" and will not work if "click from display mboxes" is selected.</i>
                </p>
                <p>&nbsp;</p>
            </td>
            <td>False</td>
            <td class="last">Can be empty or true/false</td>
        </tr>
        <tr class="odd">
            <td class="first">tntId</td>
            <td>New name for pcId/mboxPC.</td>
            <td>
                <p>Empty.</p>
                <p>If no "thirdPartyId" was provided, a new tntId is generated and returned as part of the response. Otherwise remains empty.</p>
            </td>
            <td class="last">
                <p>1 &lt; Length &lt; 128</p>
                <p>Cannot contain more than a single "." (dot).</p>
                <p>The only dot allowed is for profile location suffix.</p>
            </td>
        </tr>
        <tr>
            <td class="first">thirdPartyId</td>
            <td>Client-provided visitor ID.</td>
            <td>Empty</td>
            <td class="last">1 &lt; Length &lt; 128</td>
        </tr>
        <tr class="odd">
            <td class="first">marketingCloudVisitorId</td>
            <td>Marketing Cloud Visitor ID</td>
            <td>Empty</td>
            <td class="last">1 &lt; Length &lt; 128</td>
        </tr>
        <tr>
            <td class="first">order > total</td>
            <td>Order amount associated with the order</td>
            <td>Empty</td>
            <td class="last">If not empty, should be a valid decimal</td>
        </tr>
        <tr class="odd">
            <td class="first">order.id</td>
            <td>Order reference ID</td>
            <td>Empty</td>
            <td class="last">If not empty, Length &lt; 250</td>
        </tr>
        <tr>
            <td class="first">order > purchasedProductIds</td>
            <td>Order referenced product IDs</td>
            <td>Empty</td>
            <td class="last">
                <p>Each ID cannot exceed 50 char length.</p>
                <p>Total length of comma-delimited IDs as string cannot exceed 250 chars</p>
            </td>
        </tr>
        <tr class="odd">
            <td class="first">profileParameters</td>
            <td>
                <p>Parameters that should be set in the profile.</p>
                <p>The end values in the profile are saved as profile.param=value.</p>
            </td>
            <td>Empty</td>
            <td class="last">Cannot contain more than 50 parameters</td>
        </tr>
        <tr>
            <td class="first">profileParameters.[name]</td>
            <td>Profile parameter name</td>
            <td>Empty</td>
            <td class="last">
                <p>Length &lt; 128</p>
                <p>Should not start with "profile." prefix.</p>
            </td>
        </tr>
        <tr class="odd">
            <td class="first">profileParameters.[value]</td>
            <td>Profile parameter value</td>
            <td>Empty</td>
            <td class="last">Length &lt; 256</td>
        </tr>
        <tr>
            <td class="first">mboxParameters</td>
            <td>Any mbox parameters that may need to be provided. eg. screenWidth.</td>
            <td>Empty</td>
            <td class="last">
                <p>Cannot contain more than 50 parameters.</p>
                <p>Cannot contain order-related parameters that should be set in "order".</p>
                <p>Cannot contain parameters with "profile." prefix. Those should be set in "profileParameters".</p>
            </td>
        </tr>
        <tr class="odd">
            <td class="first">mboxParameters.[name]</td>
            <td>Mbox parameter name</td>
            <td>Empty</td>
            <td class="last">Length &lt; 128</td>
        </tr>
        <tr>
            <td class="first">mboxParameters.[value]</td>
            <td>Mbox parameter value</td>
            <td>Empty</td>
            <td class="last">Length &lt; 256</td>
        </tr>
        <tr class="odd">
            <td class="first">requestLocation > pageURL</td>
            <td>Equivalent to mboxURL mbox parameter</td>
            <td>Empty</td>
            <td class="last">
                <p>Valid URL.</p>
                <p>Length &lt; 3072</p>
            </td>
        </tr>
        <tr>
            <td class="first">requestLocation > referrerURL</td>
            <td>Equivalent to mboxReferrer mbox parameter</td>
            <td>Empty</td>
            <td class="last">
                <p>Valid URL</p>
                <p>Length &lt; 3072</p>
            </td>
        </tr>
        <tr class="odd">
            <td class="first">requestLocation > ipAddress</td>
            <td>Override the IP address of the client server</td>
            <td>IP address or the server making the call</td>
            <td class="last">Valid IP address</td>
        </tr>
        <tr>
            <td class="first">requestLocation > impressionId</td>
            <td>
                <p>Equivalent of pageId.</p>
                <p>A unique one is generated with each request if no value was specified.</p>
            </td>
            <td>Empty</td>
            <td class="last">Length &lt; 128</td>
        </tr>
        <tr class="odd">
            <td class="first">requestLocation > host</td>
            <td>Equivalent of mboxHost</td>
            <td>"unknown"</td>
            <td class="last">Length &lt; 250</td>
        </tr>
        <tr>
            <td class="first">mboxTrace</td>
            <td>Enabled detailed tracing of the call</td>
            <td>False</td>
            <td class="last">Empty/True/False
                <a name="section_E846261F8F28465C91A7217AD11A2EB9"></a>
            </td>
        </tr>
    </tbody>
</table>

### Response Parameteres

<table>
    <thead>
        <tr class="odd">
            <th>Field Path</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="first">sessionId</td>
            <td class="last">Session ID that was provided for this call.</td>
        </tr>
        <tr class="odd">
            <td class="first">tntId</td>
            <td class="last">Provided or generated tntId.</td>
        </tr>
        <tr>
            <td class="first">thirdPartyId</td>
            <td class="last">thirdPartyId if one was provided.</td>
        </tr>
        <tr class="odd">
            <td class="first">mboxTrace</td>
            <td class="last">Serialized mbox trace details.
                <a name="section_D56E60F7655246D295EFD0FBE1E9B490"></a>
            </td>
        </tr>
    </tbody>
</table>

## Identifying Visitors

> Delivery Calls with differnt identifiers - Using a thirdPartyId

````
{
   "mbox" : "homePageHero",
   "thirdPartyId" : "customId-123"
}
````

> Response when a thirdPartyId is provided

````
{
   "content" : "content",
   "sessionId" : "999888",
   "thirdPartyId" : "customId-123"
}

````

> Request using the Marketing Cloud Visitor ID

````
{
   "mbox" : "homePageHero",
   "marketingCloudVisitorId" : "23131312312312123123"
}
````

> Request using all three identifiers

````
{
   "mbox" : "homePageHero",
   "tntId" : "1234343422.17_01",
   "marketingCloudVisitorId" : "23131312312312123123"
}
````

There are a multiple ways in which a Visitor can be identified in Target. Target uses three identifiers

* **tntId** – This is the primary identifier for an individual user. You can supply this id or Target will auto-generate it if the request doesn’t contain one. Also referred to as PCID or mboxPCID.

* **thirdPartyId** – This is your company’s internal identifier that you can send with every call. This could be your frequent flier number, loyalty id, crm id, guid etc,. Also referred as mbox3rdPartyID.

* **marketingCloudVisitorId** – This identifier is used to merge and share data between different Adobe solutions. The marketingCloudVisitorId  is required for features like Marketing Cloud Profiles and Audiences, Analytics for Target, Device graph etc.

Learn how [profiles are merged and synced](https://marketing.adobe.com/resources/help/en_US/target/target/c_3rd-party_id.html) in real time using the different identifiers.

### Using the tntId

A tntId is generated if it isn't provided in the request. See the Sample Request #1 on the right.

Note that a new tntId is generated and provided in the response.  Subsequent requests need to include this TnT ID.

### Using Custom IDs
If you want to use Custom IDs to identify visitors (profiles), use the thirdPartyId. You must provide these IDs with every call.


### Combining IDs

You can combine tntId/thirdPartyId/marketingCloudVisitorId and provide them in the same request. A typical scenario would be to provide tntId along with another ID.


<aside class = "warning">
<b>Returning Visitors</b>: Calls for returning visitors need to include the identifier that was used initially, tntId or thirdPartyId.
</aside>

<aside class = "notice">
<b>SessionID</b>: The sessionId is another identifier that goes hand in hand with visitor identity. Refer to the <a href="#input-parameters">input parameters</a> section to learn more about the sessionId
</aside>

# Server Side Batch Delivery

## Batch Overview

> Example 1 : Batch Delivery Request with multiple mboxes

````shell
curl -X POST \
  https://adobetargetmobile.tt.omtrdc.net/rest/v2/batchmbox/ \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{
   "client": "adobetargetmobile",
   "id": {
		"tntId": "123456789"
   },
   "mboxes": [
   		{
   			"indexId": 0,
   			"mbox": "batch-req-1"
   		},
   		{
   			"indexId": 1,
   			"mbox": "batch-req-2"
   		}
   	]
}'
````

> Example 1 : Batch Delivery Response for multiple mboxes

````shell
{
    "requestId": "1e20ec58-48c9-46a7-a43c-b34aafb1a18b",
    "client": "adobetargetmobile",
    "id": {
        "tntId": "123456789.28_51"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "contentAsJson": false,
    "mboxResponses": [
        {
            "mbox": "batch-req-1",
            "content": "batch-response-1a"
        },
        {
            "mbox": "batch-req-2",
            "content": "batch-response-2a"
        }
    ]
}
````

The Batch Delivery API allows requesting content for multiple mboxes in a single call. It also has a prefetch mode that enables clients like mobile apps, servers etc to fetch content for multiple mboxes in one request, cache it locally and later notify Target when the user visits those mboxes.

<aside class = "warning">
<b>Beta API</b>: This API documenation section is a work in progress and the API is currently in beta. We will be adding more details and examples shortly. If you have any questions, please reach out to Adobe Client Care or your Customer Success Manager.
</aside>

## Batch Postman Collection

<aside class="notice">
Don't forget to replace the clientcode and the mbox name with your own in the API calls. The APIs in the collection use a demo account.
</aside>

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/4db4eefc81c7b5a4d5d4)


## Batch Limitations

<aside class = "warning">
<b>Support for AP and Recs Activities</b>: This API should only be used for AB and XT activities. Support for Automated Personalization, Auto-Allocate, Auto-Target and Recommendations activty types will be added in Q1 2018. The API request and response structure won't change when the support is added.
</aside>

## Batch Terminology

>Example 2 : Batch Delivery Request with one regular mbox and one prefetched mbox

````shell
curl -X POST \
  https://adobetargetmobile.tt.omtrdc.net/rest/v2/batchmbox/ \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{
   "client": "adobetargetmobile",
   "id": {
		"tntId": "123456789"
   },
   "mboxes": [
   		{
   			"indexId": 0,
   			"mbox": "batch-req-1"
   		}
   	],
   	"prefetch": [
   		{
   			"indexId": 0,
   			"mbox": "batch-req-2"
   		}
   	]
}'
````

>Example 2: Batch Delivery Response for one regular mbox and one prefetched mbox

````shell
{
    "requestId": "77a45e19-732f-42ea-98de-e4a36ceecd55",
    "client": "adobetargetmobile",
    "id": {
        "tntId": "123456789.28_3"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "contentAsJson": false,
    "mboxResponses": [
        {
            "mbox": "batch-req-1",
            "content": "batch-response-1a"
        }
    ],
    "prefetchResponses": [
        {
            "mbox": "batch-req-2",
            "content": "batch-response-2a",
            "eventTokens": [
              "OXszbV+Odw+fblLkzmgrW2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE5wM++BveH6AIK0pfQ2QUzsg=="
            ]
        }
    ]
}
````


Here are some common terms that you need to be familiar with.

* **mboxes** – List of mboxes that should be fetched and marked as visited immediately on content delivery. If you just want to get the content for multiple mboxes but don't have a necessary to prefetch and cache them, use this.

* **prefetch** – List of mboxes that should be fetched but shouldn't be marked as visited. The Target edge returns an eventToken for each mbox that is present in the the prefetch array

* **notifications** – List of mboxes that were previously prefetched and should be marked as visited.

* **eventTokens** – A hashed encrypted token that is returned when content is prefetched. This eventToken should be sent back to Target in the notifications array.


## Batch Input Parameters


> Example 3: Batch Delivery with all possible inputs

````shell
curl -X POST \
  https://adobetargetmobile.tt.omtrdc.net/rest/v2/batchmbox/ \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{
   "client": "adobetargetmobile",
   "id": {
		"tntId": "123456789",
		"thirdPartyId": "32jh4jk23h4kj2",
		"marketingCloudVisitorId": "92387492387543875638",
		"customerIds": [
			{
				"id": "32jh4jk23h4kj2",
				"integrationCode": "userid",
				"authenticatedState": "authenticated"
			}
		]
   },
   "aamParameters": {
   		"blob": "32fdghkjh34kj5h43",
   		"uuid": "82394234238798437",
   		"dcsLocationHint": 9,
   		"dataPartnerId": 86567576,
   		"dataPartnerUserId": 348382232423424
   },
   "contentAsJson": true,
   "profileParameters": {
   		"age": "18"
   },
   "prefetch": [
   		{
   			"indexId": 0,
   			"mbox": "batch-req-1",
   			"parameters": {
   				"T_GHY": "7563"
   			},
   			"product": {
   				"id": "54353",
   				"categoryId": "93284230"
   			},
   			"order": {
            	"id": "343",
            	"total": 125.34,
        		"purchasedProductIds": ["762", "1253", "499"]
        	}
   		}
   ],
   "mboxes": [
   		{
   			"indexId": 0,
   			"mbox": "batch-req-2",
   			"parameters": {
   				"T_GHY": "7563333"
   			},
   			"product": {
   				"id": "5431153",
   				"categoryId": "9328114230"
   			},
   			"order": {
            	"id": "34366",
            	"total": 1425.34,
        		"purchasedProductIds": ["7632", "12253", "4949"]
        	}
   		}
   ],
   "notifications": [
   		{
   			"timestamp": 1485216216,
   			"mbox": "batch-req-3",
   			"parameters": {
            	"ad": "1"
        	},
        	"eventTokens": ["OXszbV+Odw+fblLkzmgrWwreqXMfVUcUx0s/BHR5kCKCnQ9Y9OaLL2gsdrWQTvE5wM++BveH6AIK0pfQ2QUzsg=="],
        	"order": {
            	"id": "34",
            	"total": 125.34,
        		"purchasedProductIds": ["76", "125", "99"]
            },
            "product": {
   				"id": "54353",
   				"categoryId": "93284230"
   			}
   		}
   	],
   	"mboxOverride": {
   		"ip": "184.58.98.74",
   		"time": 123654735,
   		"visitorPercentage": 78.54,
   		"aamResponse": "982374982738",
   		"aamSegments": "34,1243,56443"
   	}
}'
````

<table>
    <tbody>
        <tr>
            <th>Field Name</th>
            <th>Required</th>
            <th>Validation</th>
        </tr>
        <tr>
            <td>client</td>
            <td>Y</td>
            <td>Valid client code</td>
        </tr>
        <tr>
            <td>id &rarr; tntId</td>
            <td>N</td>
            <td>
                <ul>
                    <li>Max size 128</li>
                    <li>Should not contain a dot, unless the dot delimits the location hint</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>id &rarr; thirdPartyId</td>
            <td>N</td>
            <td>Max size 128</td>
        </tr>
        <tr>
            <td>id &rarr; marketingCloudVisitorId</td>
            <td>N</td>
            <td>Max size 128</td>
        </tr>
        <tr>
            <td>id &rarr; customerIds</td>
            <td>N</td>
            <td>
                <ul>
                    <li>No null elements</li>
                    <li>Max size 50</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>id &rarr; customerIds &rarr; id</td>
            <td>Y</td>
            <td>Max size 128</td>
        </tr>
        <tr>
            <td>id &rarr; customerIds &rarr; integrationCode</td>
            <td>Y</td>
            <td>Max size 50</td>
        </tr>
        <tr>
            <td>id &rarr; customerIds &rarr; authenticatedState</td>
            <td>Y</td>
            <td>unknown (default) | authenticated | logged_out</td>
        </tr>
        <tr>
            <td>profileParameters</td>
            <td>N</td>
            <td>
                <ul>
                    <li>Max count 50</li>
                    <li>no blank names</li>
                    <li>name size &lt;= 128</li>
                    <li>value size &lt;= 256</li>
                    <li>name should not start with &quot;profile.&quot;</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>environmentId</td>
            <td>N</td>
            <td>Valid client environment id</td>
        </tr>
        <tr>
            <td>contentAsJson</td>
            <td>N</td>
            <td>true | false</td>
        </tr>
        <tr>
            <td>prefetch</td>
            <td>N</td>
            <td>
                <ul>
                    <li>Max count 50</li>
                    <li>No null elements</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>prefetch &rarr; indexId</td>
            <td>Y</td>
            <td>
                <ul>
                    <li>Not null</li>
                    <li>&gt;= 0</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>prefetch &rarr; mbox</td>
            <td>Y</td>
            <td>
                <ul>
                    <li>not blank</li>
                    <li>no '-clicked' suffix</li>
                    <li>max size 250</li>
                    <li>values not allowed: '** display mboxes /**', '** any mbox **', '** click from display mbox **'</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>prefetch &rarr; parameters</td>
            <td>N</td>
            <td>
                <ul>
                    <li>max count 50</li>
                    <li>name not blank</li>
                    <li>name length &lt;= 128</li>
                    <li>value length &lt;= 5000</li>
                    <li>name should not start with &quot;profile.&quot;</li>
                    <li>not allowed names: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>prefetch &rarr; product</td>
            <td>N</td>
            <td>-</td>
        </tr>
        <tr>
            <td>prefetch &rarr; product&nbsp;-&gt; id</td>
            <td>N</td>
            <td>
                <ul>
                    <li>Not blank</li>
                    <li>max size = 128</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>prefetch &rarr; product &rarr; categoryId</td>
            <td>N</td>
            <td>
                <ul>
                    <li>Not blank</li>
                    <li>max size = 128</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>prefetch &rarr; order</td>
            <td>N</td>
            <td>&nbsp;</td>
        </tr>
        <tr>
            <td>prefetch &rarr; order &rarr; id</td>
            <td>N</td>
            <td>max length = 250</td>
        </tr>
        <tr>
            <td>prefetch &rarr; order &rarr; total</td>
            <td>N</td>
            <td>&gt;= 0</td>
        </tr>
        <tr>
            <td>prefetch &rarr; order &rarr; purchasedProductIds</td>
            <td>N</td>
            <td>
                <ul>
                    <li>no blank values</li>
                    <li>each value's max length 50</li>
                    <li>total ids length &lt;= 250</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>


#Profiles

Adobe Target creates and maintains a profile for every individual user. This profile is stored on the Target edge cluster and is updated in real time after every visit.

## Structure of a Target Profile

> Sample Profile Structure

````json
{
    "client": "adobetargetmobile",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}

````


A Target Profile consists of these following objects

* clientcode	- The Target client code to which the profile is associated
* visitorId	- The identifier for the profile. This can be a tntid or thirdpartyid or marketingcloudvisitorid
* modifiedAt	- The timestamp of when the profile was last updated.
* profileAttributes	- List of all the profile attributes stored as key-value pairs on that the individual profile

## Fetching a profile

A Target Profile can be fetched in two ways

### Using a tnt id

Target automatically assigns a tntid for every request.

The request format to fetch a profile using a tntid

`https://yourclientcode.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=yourclientcode`

Replace "yourclientcode" and "your-tnt-id" and fire a GET request. Here is an example profile fetch call using a tntid

`http://adobetargetmobile.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=adobetargetmobile`

### Using a thirdPartyId

Target profiles can be augmented with your own identifier (eg: CRM id, uuid, membership number etc). See the profile update section to learn how you can attach a thirdPartyId to your profile.

The request format to fetch a profile using a thirdPartyId

`https://yourclientcode.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=yourclientcode`

Replace "yourclientcode" and "your-thirdpartyid" and fire a GET request. Here is an example profile fetch call using a thirdpartyid

`http://adobetargetmobile.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=adobetargetmobile`

When this call is made, Target attempts to locate the profile first in the cluster noted in the edge request, or wherever the profile is located and return the content. The profile contents are returned in JSON format.

### Authentication

This API has no authentication.

### Metering

These calls do not count towards your mbox calls.

### Error Handling

In the case of a call to /thirdPartyId with an invalid or an expired thirdPartyId specified:

`{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}`

If the profile can not be located or has expired:

`{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}`

## Updating Profiles

A user profile contains demographic and behavioral information of a web page visitor, such as age, gender, products purchased, last time of visit, and so on that Target uses to personalize the content it serves to the visitor.

The profile information for each visitor is either stored in cookies or in third-party apps.

If your web page implements the Target code, the profile information from the cookies is passed to Target using profile parameters. Target identifies each visitor uniquely through a pcID that it generates the visitor’s cookies. However, you can pass profile parameters from an external app through mbox calls using mbox3rdPartyIds.

Use the profile APIs when you have profile data about your visitors to send to Target that you either can't or don't want to send as part of your page-based integration with Target. This might be data from a CRM or POS that isn't available on the page, or data of a more sensitive nature that does not make sense to pass on the page.

There are two ways to update profiles via API:

* Single profile API
* Bulk profile update via batch

### Single Profile Update

Specify the profile parameters in the format profile.paramName=value.
There is a limit of one million profile updates in a 24-hour period.

To update the profile for a pcId, use :

`https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...`

To update the profile for an mbox3rdPartyId, use:

`shell
http://CLIENT.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...`

The Single Profile Update API is for updates only. If nothing is found, a profile is not created.

**Notes**

* Parameters and values must be URL-encoded using UTF-8.
* Parameter format is profile.paramName.
* Not all parameter values need to exist for all pcIds/mbox3rdPartyId.
* Parameters and values are case sensitive.
* Both GET and POST are supported.
* The current size limitations for limit is 8KB for GET and 60KB for POST.
* The calls to the profile update API do not count toward your mbox charges.

**Response**

A sample response for the above requests looks like this.
`trueRequest successfully submitted`

This response indicates the response has been submitted and will be processed soon. In general, lag time is less than a minute.

### Bulk Profile Update

The Bulk Profile Update API allows you to update user profiles for multiple visitors to a website in bulk using a batch file.

Using Bulk Profile Update API, you can conveniently send detailed visitor profile data in the form of profile parameters for a bunch of users to Target from any external source, including CRM or POS, which isn't usually available on a web page.

<table>
    <tbody>
        <tr>
            <th>Version</th>
            <th>URL Example</th>
            <th>Features</th>
        </tr>
        <tr>
            <td>V1</td>
            <td><em>http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate</em>
            </td>
            <td>Support for bulk profile update only</td>
        </tr>
        <tr>
            <td>V2</td>
            <td><em> http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate</em>
            </td>
            <td>
                <ul>
                    <li>Create profile if not found</li>
                    <li>Per row status update</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

version 2 (v2) of the Bulk Profile Update API is the current version. However, Target still supports version 1 (v1).

### Authentication

The Bulk Update API call requires a valid access token to be passed in the header of the request.

The access token can be obtained in the following way:

* Using the Target Classic UI, go to Configuration > Edit.
* Scroll to the bottom of the page.
* Under Profile API Settings, switch to ‘Enable’ Require Authorization.
* Click Generate Authentication Token.
* Copy the token and include it in the request in the header of the
* request in the format: “Authorization” : “Bearer ”

Optionally, use the following API to generate the token:

`https://admin10.testandtarget.omniture.com/admin/rest/v1/authentication/token?client=clientname&scope=profile_api&email=approver@client.com&password=*****`

Alternatively, use the Basic Authorization API as shown in the following curl example below. Basic Authorization header is a base-64 encoded string with the following structure email:password 'https://admin10.testandtarget.omniture.com/admin/rest/v1/authentication/token?client=clientname&scope=profile_api' -H 'Authorization: Basic bmluYWlyK3N1bW1pdEBhZG9iZXRlc3QuY29tOnN1bW1pdDEyMw=='.
Here is the sample response:

`{ "access_token": "b106da37-301d-4cdd-b25f-59ab4c97b5a0", "scope": "profile_api", "expires_in": 21599, "token_type": "bearer” }`

### Batch File


To update profile data in bulk, create a batch file. The batch file is a text file with values separated by commas similar to the following sample file.

batch=pcId, param1, param2, param3, param4
123, value1
124, value1,,, value4
125,, value2
126, value1, value2, value3, value4

You reference this file in the POST call to Target servers to process the file. When creating the batch file, bear in mind the following:


* The first row of the file must specify column headers.
* The first header should either be a pcId or thirdPartyId. The Marketing Cloud visitor ID is not supported. pcId is a Target-generated visitorID. thirdPartyId is an ID specified by the client application, which is passed to Target through an mbox call as mbox3rdPartyId. It must be referred to here as thirdPartyId.
* Parameters and values you specify in the batch file must be URL-encoded using UTF-8 for security reasons. They can be forwarded to other edge nodes for processing through HTTP requests.
* The parameters must be in the format paramName only. They are displayed in Target as profile.paramName.
* If you are using Bulk Profile Update API v2, you need not specify all parameter values for each pcId. Profiles are created for any pcId or mbox3rdPartyId that is not found in Target. If you are using v1, profiles are not created for missing pcIds or mbox3rdPartyIds.
* The size of the batch file must be less than 50MB. In addition, the total number of rows should not exceed 500,000. This limit ensures that servers don't get flooded with too many requests.
* You can send multiple files. However, the sum total of the rows of all the files that you send in a day should not exceed one million for each client.
* There is no limit on number of attributes you upload. However, the overall size of a profile including system data should not exceed 2000KB. Adobe recommends you use less than 1000KB of storage for profile attributes.
* Parameters and values are case sensitive.

### HTTP Post Request

Make an HTTP POST request to Target edge servers to process the file. Here is a sample HTTP POST request for the file batch.txt using the curl command:

`curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate`

Where:

BATCH.TXT is the filename.
CLIENTCODE is the Target client code.

If you don't know your client code, in the Target UI click Setup > Implementation > Edit Mbox.js Settings. The client code is shown in the Client field.


**Inspect the response.**

v2 returns a profile-by-profile
status and v1 returns only the overall status. The response includes a
link to a different URL that has the profile-by-profile success message.

**Example Response:**

<response> <success>true</success> <batchStatus>http://mboxedge19.tt.omtrdc.net/m2/demo/v2/profile/batchStatus?batchId=demo-1845664501&m2Node=00</batchStatus> <message>Batch submitted for processing</message> </response>

In case of an error, the response will contain success=false and a detailed message for the error.

A successful response will look like the following:

<response>  <batchId>demo-1845664501</batchId>  <profile>   <id>1436187396849-250353.03_03</id>   <status>success</status>  </profile>  <profile>   <id>2403081156529-351655.03_03</id>   <status>success</status>  </profile>  <profile>   <id>2403081156529-351656.03_03</id>   <status>success</status>  </profile>  <profile>   <id>1436187396849-250351.01_00</id>   <status>success</status>  </profile> </response>
Expected values for the status fields are:

* **success**: The profile was updated. If the profile was not found, one was created with the values from the batch.
* **error**: The profile was not updated or created due to a failure, exception, or message loss.
* **pending**: The profile has not been updated or created yet.


# Admin APIs

The Admin APIs will allow you to CRUD (Create, Read, Update and Delete) [Activities](#activities), [Audiences](#audiences) and [Offers](#offers).


## Before you Begin

In all the code examples, you must replace the `{tenant}` variable with your tenant value, `your-bearer-token` with the access token that you generate with your JWT and `your-api-key` with your API key from the Adobe I/O console.


## Adobe I/O Console

The Adobe I/O console (https://console.adobe.io) is where you can configure your API integration and obtain your API keys and access token.

Please refer to the [authentication section](https://docs.campaign.adobe.com/doc/standard/en/api/ACS_API.html#adobeio-configuration) from the Adobe campaign API to learn how to configure Adobe I/O.

<aside class="notice">
All enterprise APIs that can be setup in the Adobe I/O console use the same configuration.
</aside>

<aside class="notice">
You have to be a Experience Cloud Admin to get access to the Adobe I/O console.
</aside>


## Admin Postman Collection

Postman is a application that makes it easy to fire API calls. This Postman collection contains all the Admin API calls in the same order as the docs. Just click on the 'Run in Postman' button to import the Target API collection.

This collection contains all APIs that require authentication using Adobe I/O
* Activities
* Audiences
* Offers
* Reports
* Mboxes and Environments

<aside class="notice">
Don't forget to replace the {{tenant}}, {{access_token}} and {{api_key}} values with your own in the API calls.
</aside>


[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/8df29390f5e380f44a7c)

## Response Codes

Here are the common response codes for the Target Admin APIs

Status|Meaning|Description
---|---|---|
200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK
400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request. Most probably the data provided in the request is invalid.
401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|The user is not allowed to perform this operation.
403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Access to this resource is forbidden.
404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The referenced resource was not found.


# Activities

An activity enables you to test, target or personalize content for your users. An activity can be one of the following types

* AB Test
* Experience Targeting
* Recommendations
* Automated Personalization
* Multi-Variate Test

## List Activities

> Sample Request for GET Activities

````shell

curl -X GET
https://mc.adobe.io/adobetargetmobile/target/activities/ \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````
> Sample Response for GET Activities

````
{
    "total": 5,
    "offset": 0,
    "limit": 2147483647,
    "activities": [
        {
            "id": 168805,
            "thirdPartyId": "2fc846c4-d5c6-4d67-9ef8-939bb907cc71",
            "type": "ab",
            "state": "deactivated",
            "name": "A3 - L4242 - Serversid testing",
            "priority": 0,
            "modifiedAt": "2017-05-11T10:11:35Z"
        },
        {
            "id": 168942,
            "thirdPartyId": "e1cfda1a-5814-4dd9-8624-c33882af114b",
            "type": "xt",
            "state": "deactivated",
            "name": "A3-L4242-XT",
            "priority": 0,
            "modifiedAt": "2017-05-11T10:11:52Z"
        },
        {
            "id": 168816,
            "thirdPartyId": "f7134ab6-ee98-422f-a59d-a1efc3cd85a9",
            "type": "ab",
            "state": "deactivated",
            "name": "A5-L4242",
            "priority": 0,
            "modifiedAt": "2017-05-11T10:11:33Z"
        },
        {
            "id": 168824,
            "thirdPartyId": "60a2f81f-e2bb-45be-9e9a-90162cfcf780",
            "type": "ab",
            "state": "deactivated",
            "name": "A6-L4242 AB Test SG",
            "priority": 0,
            "modifiedAt": "2017-05-11T10:11:18Z"
        }
    ]
}

````

Get a list of activities created in your Target account, with the ability to filter and sort by attributes.

### GET: /{tenant}/target/activities


### Parameters

| Parameter | Required | Description | Example |
| --------- | -------- | ----------- | --------|
limit | False|  Defines the number of items to return. Default value is 2147483647 | Returns the first ten items <br>`?limit=10`
offset| False | Defines the first activity to return from the list of total activities. Used in conjunction with limit, you can provide pagination in your application for users to browse through a large set of activities. | Return the first ten items with an offset <br>`?limit=10&offset=0` <br> `?limit=10&offset=10`
sortBy | False | Defines the sorting criteria on the returned items. You can sort by: <ul> <li>name</li><li>id</li><li>endsAt</li><li>thirdPartyId<li>state<li>type</li><li>priority</li></ul> You can add a "-" modifier to sort by descending order. | Sort Activities <br> `?sortBy=id&limit=10`<br> `/?sortBy=-id&limit=10` <br>  `/?sortBy=id&sortBy=-name&limit=10`

### Some common Examples

GET list of all activities
`https://mc.adobe.io/{tenant}/target/activities/`

GET activity list with limit
`https://mc.adobe.io/{tenant}/target/activities/?limit=1`

GET activity list with limit and offset
`https://mc.adobe.io/{tenant}/target/activities/?limit=2&offset=2`

GET activity list filtered by multiple values
`https://mc.adobe.io/{tenant}/target/activities/?id=3&id=4&name=ab`

GET activity list filtered by negative values
`https://mc.adobe.io/{tenant}/target/activities/?priority=!4`

GET activity list sorted by multiple criteria
`https://mc.adobe.io/{tenant}/target/activities/?sortBy=name&sortBy=id`

GET activity list filtered by a date range
`https://mc.adobe.io/{tenant}/target/activities/?startsAt=1800-09-01T02:04:00.000-07:00/2114-11-30T14:10:00.000-07:00`

## Get AB Activity by ID

> Sample Request for Get AB Activity by ID

````shell
curl -X GET
https://mc.adobe.io/adobetargetmobile/target/activities/ab/168824 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````
> Sample Response for Get AB Activity by ID

````

{
    "id": 168824,
    "thirdPartyId": "60a2f81f-e2bb-45be-9e9a-90162cfcf780",
    "name": "A6-L4242 AB Test SG",
    "state": "deactivated",
    "priority": 0,
    "autoAllocateTraffic": {
        "enabled": false,
        "successEvaluationCriteria": "conversion_rate"
    },
    "locations": {
        "mboxes": [
            {
                "locationLocalId": 0,
                "name": "a6-serverside-ab"
            }
        ]
    },
    "experiences": [
        {
            "experienceLocalId": 0,
            "name": "Experience A",
            "visitorPercentage": 34,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395818
                }
            ]
        },
        {
            "experienceLocalId": 1,
            "name": "Experience B",
            "visitorPercentage": 33,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395819
                }
            ]
        },
        {
            "experienceLocalId": 2,
            "name": "Experience C",
            "visitorPercentage": 33,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395820
                }
            ]
        }
    ],
    "metrics": [
        {
            "metricLocalId": 32767,
            "name": "MY PRIMARY GOAL",
            "conversion": true,
            "mboxes": [
                {
                    "name": "order-complete",
                    "successEvent": "mbox_shown"
                }
            ],
            "action": {
                "type": "count_once"
            }
        }
    ],
    "modifiedAt": "2017-05-11T10:11:18Z"
}

````

Fetch the current definition of an AB activity if it is found as referenced by the id.

### GET /{tenant}/target/activities/ab/{id}



## Delete AB activity by ID

> Sample Request for Delete AB Activity by ID

````shell

curl -X DELETE \
  https://mc.adobe.io/adobetargetmobile/target/activities/ab/168805 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for Delete XT Activity by ID

````

{
    "id": 168805,
    "thirdPartyId": "2fc846c4-d5c6-4d67-9ef8-939bb907cc71_1499636562807",
    "name": "A3 - L4242 - Serversid testing",
    "state": "deleted",
    "priority": 0,
    "autoAllocateTraffic": {
        "enabled": false,
        "successEvaluationCriteria": "conversion_rate"
    },
    "locations": {
        "mboxes": [
            {
                "locationLocalId": 0,
                "name": "a3-serverside-ab"
            }
        ]
    },
    "experiences": [
        {
            "experienceLocalId": 0,
            "name": "Experience A",
            "visitorPercentage": 34,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395818
                }
            ]
        },
        {
            "experienceLocalId": 1,
            "name": "Experience B",
            "visitorPercentage": 33,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395819
                }
            ]
        },
        {
            "experienceLocalId": 2,
            "name": "Experience C",
            "visitorPercentage": 33,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395820
                }
            ]
        }
    ],
    "metrics": [
        {
            "metricLocalId": 32767,
            "name": "MY PRIMARY GOAL",
            "conversion": true,
            "action": {
                "type": "count_once"
            }
        }
    ],
    "modifiedAt": "2017-07-09T21:42:42Z"
}

````

Deletes the AB activity that is referenced by the id, if it is found.

### DELETE: /{tenant}/target/activities/ab/{id}

## Create AB Activity

> Sample Request for Create AB Activity

````shell

curl -X POST \
  https://mc.adobe.io/adobetargetmobile/target/activities/ab/ \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
    "name": "New API Activity",
    "startsAt": "2017-05-01T08:00Z",
    "endsAt": "2017-09-01T07:59:59Z",
    "state": "saved",
    "priority": 100,
    "autoAllocateTraffic": {
        "enabled": false,
        "successEvaluationCriteria": "conversion_rate"
    },
    "locations": {
        "mboxes": [
            {
                "locationLocalId": 0,
                "name": "x1-serverside-ab"
            }
        ]
    },
    "experiences": [
        {
            "experienceLocalId": 0,
            "name": "Experience A",
            "visitorPercentage": 34,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395818
                }
            ]
        },
        {
            "experienceLocalId": 1,
            "name": "Experience B",
            "visitorPercentage": 33,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395819
                }
            ]
        },
        {
            "experienceLocalId": 2,
            "name": "Experience C",
            "visitorPercentage": 33,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395820
                }
            ]
        }
    ],
    "metrics": [
        {
            "metricLocalId": 32767,
            "name": "MY PRIMARY GOAL",
            "conversion": true,
            "mboxes": [
                {
                    "name": "order-complete",
                    "successEvent": "mbox_shown"
                }
            ],
            "action": {
                "type": "count_once"
            }
        }
    ]
}'

````

> Sample Response for Create AB Activity


````
{
    "id": 183916,
    "name": "New API Activity",
    "startsAt": "2017-05-01T08:00Z",
    "endsAt": "2017-09-01T07:59:59Z",
    "state": "saved",
    "priority": 100,
    "autoAllocateTraffic": {
        "enabled": false,
        "successEvaluationCriteria": "conversion_rate"
    },
    "locations": {
        "mboxes": [
            {
                "locationLocalId": 0,
                "name": "x1-serverside-ab"
            }
        ]
    },
    "experiences": [
        {
            "experienceLocalId": 0,
            "name": "Experience A",
            "visitorPercentage": 34,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395818
                }
            ]
        },
        {
            "experienceLocalId": 1,
            "name": "Experience B",
            "visitorPercentage": 33,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395819
                }
            ]
        },
        {
            "experienceLocalId": 2,
            "name": "Experience C",
            "visitorPercentage": 33,
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395820
                }
            ]
        }
    ],
    "metrics": [
        {
            "metricLocalId": 32767,
            "name": "MY PRIMARY GOAL",
            "conversion": true,
            "mboxes": [
                {
                    "name": "order-complete",
                    "successEvent": "mbox_shown"
                }
            ],
            "action": {
                "type": "count_once"
            }
        }
    ],
    "modifiedAt": "2017-07-10T05:11:03Z"
}


````

`POST /{tenant}/target/activities/ab`


Creates a new AB activity with the specified contents and returns the created activity.

<aside class="warning">
Activities created using the API can only be edited using the API. You can't edit it in the UI.
</aside>

### Parameters

<table>
    <thead>
        <tr>
            <th>Attribute</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td> <em>id</em>
            </td>
            <td>Number</td>
            <td>A unique value generated by the server when the activity is created. Subsequently, it is used to identify an activity.</td>
        </tr>
        <tr>
            <td> <em>thirdPartyId</em>
            </td>
            <td>String</td>
            <td>An alternative id to identify an activity, usually generated by the client. If specified, must be unique amongst all activities. Max length is 250 characters.</td>
        </tr>
        <tr>
            <td> <em>name</em>
            </td>
            <td> String</td>
            <td> A string to identify the activity. The name cannot be empty. Max length is 250 characters.</td>
        </tr>
        <tr>
            <td> <em>startsAt</em>
            </td>
            <td> String</td>
            <td> The date and time to start an activity. Supports ISO 8601 style date-hour formats.</td>
        </tr>
        <tr>
            <td> <em>endsAt</em>
            </td>
            <td> String</td>
            <td> The date and time to end an activity. Supports ISO 8601 style date-hour formats.</td>
        </tr>
        <tr>
            <td> <em>state</em>
            </td>
            <td> String</td>
            <td>
                <p>Defines the state of the activity. Possible values are:</p>
                <p>&nbsp;</p>
                <ul>
                    <li>approved</li>
                    <li>deactivated</li>
                    <li>paused</li>
                    <li>saved</li>
                    <li>deleted</li>
                </ul>
                <p>&nbsp;</p>
            </td>
        </tr>
        <tr>
            <td> <em>priority</em>
            </td>
            <td> String</td>
            <td> Defines the priority of the activity. Higher numbers have higher priority.Valid values are between 0 and 999. Default value is 5.</td>
        </tr>
        <tr>
            <td> <em>entryConstraint</em>
            </td>
            <td> String</td>
            <td> Specifies an activity entry constraint via an mbox-audience combination or visitor percentage. Specifies the mbox, audienceId, and visitor percentage required to enter the activity.</td>
        </tr>
        <tr>
            <td> <em>experiences</em>
            </td>
            <td> Array</td>
            <td> A list of locations on the page where the content offer is served. A location contains the following:
                <ul>
                    <li>
                        <p>name – to identify an experience</p>
                    </li>
                    <li>
                        <p>localId – to track the experience across POST/PUT requests</p>
                    </li>
                    <li>
                        <p>audienceId – a set of audiences to filter the visitors for the experience</p>
                    </li>
                    <li>
                        <p>visitorPercentage – the percentage of visitors that is allocated to the experience</p>
                    </li>
                </ul>
            </td>
        </tr>
        <tr>
            <td> <em>locations</em>
            </td>
            <td> Array</td>
            <td> A list of locations on the page where the content offer is served.</td>
        </tr>
        <tr>
            <td> <em>locations</em> &gt; mboxes</td>
            <td> Array</td>
            <td>
                <p>a list of mboxes to serve the offers in.</p>
            </td>
        </tr>
        <tr>
            <td> <em>locations</em> &gt; mboxes &gt; locationLocalId</td>
            <td> String</td>
            <td>
                <p>Used to track the location during PUT/POST requests</p>
            </td>
        </tr>
        <tr>
            <td> <em>locations</em> &gt; mboxes &gt; name</td>
            <td> String</td>
            <td> The name of the mbox.</td>
        </tr>
        <tr>
            <td> <em>locations</em> &gt; mboxes &gt; audienceId</td>
            <td> Array</td>
            <td> A list of audienceIds to target on the mbox</td>
        </tr>
        <tr>
            <td> <em>metrics</em>
            </td>
            <td> Array</td>
            <td> List of metrics to collect for the activity.</td>
        </tr>
        <tr>
            <td> <em>metrics</em> &gt; metricLocalId</td>
            <td> String</td>
            <td> Used to track the metric across POST/PUT requests.</td>
        </tr>
        <tr>
            <td> <em>metrics</em> &gt; name</td>
            <td> Array</td>
            <td> Used to identify the metric</td>
        </tr>
        <tr>
            <td> <em>metrics</em> &gt; conversion</td>
            <td> Boolean</td>
            <td> Used to indicate if the metric is a conversion metric</td>
        </tr>
        <tr>
            <td> <em>metrics</em> &gt; action</td>
            <td> JSON</td>
            <td>
                <p>Used to specify the action to take when the metric number is increased</p>
            </td>
        </tr>
        <tr>
            <td> <em>metrics</em> &gt; action &gt; type</td>
            <td> Enum</td>
            <td>
                <p>Type of action. The valid values are:</p>
                <p>&nbsp;</p>
                <ul>
                    <li>count_once (default if no conversion)</li>
                    <li>count_landings</li>
                    <li>always_convert</li>
                    <li>restart_same_experience (default if conversion)</li>
                    <li>restart_random_experience</li>
                    <li>restart_new_experience</li>
                    <li>exclude_to_same_experience</li>
                    <li>ban_from_campaign</li>
                    <li>experience_frequency_capping</li>
                </ul>
                <p>&nbsp;</p>
            </td>
        </tr>
        <tr>
            <td> <em>metrics</em> &gt; action &gt; conditions</td>
            <td> &nbsp;</td>
            <td> additional conditions applicable for ban_from_campaign and experience_frequency_capping</td>
        </tr>
        <tr>
            <td> <em>metrics</em> &gt; action &gt; conditions &gt; maxVisitCount</td>
            <td> Number</td>
            <td> &nbsp;</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; conditions &gt; maxImpressionCount</em>
            </td>
            <td> Number</td>
            <td> &nbsp;</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; conditions &gt; experiences</em>
            </td>
            <td> &nbsp;</td>
            <td> Used for details of the experiences</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; conditions &gt; experiences</em>
            </td>
            <td> &nbsp;</td>
            <td> Used for details of the experiences</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; conditions &gt; experiences</em> &gt; experienceLocalId</td>
            <td> &nbsp;</td>
            <td> to track the experience across POST/PUT requests</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; conditions &gt; experiences</em> &gt; maxVisitCount</td>
            <td> &nbsp;</td>
            <td> &nbsp;</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; conditions &gt; experiences</em> &gt; maxImpressionCount</td>
            <td> &nbsp;</td>
            <td> &nbsp;</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; onConditionMetAction</em>
            </td>
            <td> &nbsp;</td>
            <td>
                <p>Used to specify the action to take when the condition is met. Valid values are restart_new_experience or restart_random_experience.</p>
                <p>This value is only applicable if action &gt; type=experience_frequence_capping.</p>
            </td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; mboxes</em>
            </td>
            <td> &nbsp;</td>
            <td> An optional list of mboxes for which metrics should be collected</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; mboxes</em> &gt; name</td>
            <td> String</td>
            <td> a text identifier for the mbox</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; mboxes</em> &gt; successEvent</td>
            <td> String</td>
            <td> Used to specify the success metric event. Valid values are: mbox_shown, or mbox_clicked.</td>
        </tr>
        <tr>
            <td> <em><em>metrics</em> &gt; action &gt; mboxes</em> &gt; audienceId</td>
            <td> String</td>
            <td> optional audienceId to only track specific cases.</td>
        </tr>
        <tr>
            <td> reportingAudiences</td>
            <td> &nbsp;</td>
            <td> Segments used for reporting</td>
        </tr>
        <tr>
            <td> reportingAudiences &gt; reportingAudienceLocalId</td>
            <td> &nbsp;</td>
            <td> Used to track metrics across POST/PUT requests</td>
        </tr>
        <tr>
            <td> reportingAudiences &gt; audienceId</td>
            <td> &nbsp;</td>
            <td> Segments used for reporting</td>
        </tr>
        <tr>
            <td> reportingAudiences &gt; metricLocalId</td>
            <td> &nbsp;</td>
            <td> &nbsp;</td>
        </tr>
        <tr>
            <td> analytics</td>
            <td> &nbsp;</td>
            <td> Used to configure integration with Adobe Analytics</td>
        </tr>
        <tr>
            <td> analytics &gt; reportSuite</td>
            <td> &nbsp;</td>
            <td> Report suite configuration for Adobe Analytics</td>
        </tr>
        <tr>
            <td> analytics &gt; dataCollectionHost</td>
            <td> &nbsp;</td>
            <td> Used to denote data collection host for Adobe Analytics</td>
        </tr>
    </tbody>
</table>




## Update AB Activity

> Sample Request for Update AB Activity

````shell
curl -X PUT \
  https://mc.adobe.io/adobetargetmobile/target/activities/ab/183916 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
	"name": "New Activity Name",
	"state": "approved",
	"priority": 10,
	"locations": {
		"mboxes": [
			{
				"locationLocalId": 0,
				"name": "mbox_1"
			},
			{
				"locationLocalId": 1,
				"name": "mbox_2"
			},
			{
				"locationLocalId": 2,
				"name": "mbox_3"
			}
		]
	},
	"experiences": [
		{
			"experienceLocalId": 0,
			"name": "Tom Hanks Cast Away",
			"offerLocations": [
				{
					"locationLocalId": 0,
					"offerId": 400546
				},
				{
					"locationLocalId": 1,
					"offerId": 400547
				},
				{
					"locationLocalId": 2,
					"offerId": 400546
				}
			]
		},
		{
			"experienceLocalId": 1,
			"name": "Default",
			"offerLocations": [
				{
					"locationLocalId": 0,
					"offerId": 400546
				},
				{
					"locationLocalId": 1,
					"offerId": 400547
				},
				{
					"locationLocalId": 2,
					"offerId": 400546
				}
			]
		}
	],
	"metrics": [
		{
			"metricLocalId": 3,
			"name": "display about",
			"mboxes": [
				{
					"name": "event_1",
					"successEvent": "mbox_shown"
				}
			]
		},
		{
			"metricLocalId": 4,
			"name": "display hero",
			"mboxes": [
				{
					"name": "event_2",
					"successEvent": "mbox_shown"
				}
			]
		},
		{
			"metricLocalId": 32767,
			"name": "display userimg",
			"conversion": true,
			"action": {
				"type": "count_once"
			},
			"mboxes": [
				{
					"name": "event_3",
					"successEvent": "mbox_shown"
				}
			]
		}
	],
	"analytics": {
		"reportSuite": "mydemoreportsuite",
		"dataCollectionHost": "mydemoreportsuite.sc.omniture.com"
	}
}'

````

> Sample Response for Update AB Activity

````

{
	"name": "New Activity Name",
	"state": "approved",
	"priority": 10,
	"locations": {
		"mboxes": [
			{
				"locationLocalId": 0,
				"name": "mbox_1"
			},
			{
				"locationLocalId": 1,
				"name": "mbox_2"
			},
			{
				"locationLocalId": 2,
				"name": "mbox_3"
			}
		]
	},
	"experiences": [
		{
			"experienceLocalId": 0,
			"name": "Tom Hanks Cast Away",
			"offerLocations": [
				{
					"locationLocalId": 0,
					"offerId": 400546
				},
				{
					"locationLocalId": 1,
					"offerId": 400547
				},
				{
					"locationLocalId": 2,
					"offerId": 400546
				}
			]
		},
		{
			"experienceLocalId": 1,
			"name": "Default",
			"offerLocations": [
				{
					"locationLocalId": 0,
					"offerId": 400546
				},
				{
					"locationLocalId": 1,
					"offerId": 400547
				},
				{
					"locationLocalId": 2,
					"offerId": 400546
				}
			]
		}
	],
	"metrics": [
		{
			"metricLocalId": 3,
			"name": "display about",
			"mboxes": [
				{
					"name": "event_1",
					"successEvent": "mbox_shown"
				}
			]
		},
		{
			"metricLocalId": 4,
			"name": "display hero",
			"mboxes": [
				{
					"name": "event_2",
					"successEvent": "mbox_shown"
				}
			]
		},
		{
			"metricLocalId": 32767,
			"name": "display userimg",
			"conversion": true,
			"action": {
				"type": "count_once"
			},
			"mboxes": [
				{
					"name": "event_3",
					"successEvent": "mbox_shown"
				}
			]
		}
	],
	"analytics": {
		"reportSuite": "mydemoreportsuite",
		"dataCollectionHost": "mydemoreportsuite.sc.omniture.com"
	}
}

````


`PUT: /{tenant}/target/activities/ab/{id}`

Updates the AB activity definition with the contents as provided in the request. This can change the state and behaviour of an existing activity.

<aside class="notice">
Refer "Create AB Activity" for the available inputs, limitations and the description. The input for "Update AB Activity" method is very similar to the "Create AB Activity" method.
</aside>



## Get XT Activity by ID

> Sample Request for Get XT Activity by ID

````shell
curl -X GET
https://mc.adobe.io/adobetargetmobile/target/activities/xt/168824 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````
> Sample Response for Get XT Activity by ID

````
{
    "id": 166425,
    "thirdPartyId": "04662c10-0831-4306-bb36-5410acc88dff",
    "name": "Master - Mobile - XT",
    "state": "approved",
    "priority": 999,
    "autoAllocateTraffic": {
        "enabled": false,
        "successEvaluationCriteria": "conversion_rate"
    },
    "locations": {
        "mboxes": [
            {
                "locationLocalId": 0,
                "name": "a1-mobile-xt"
            }
        ]
    },
    "experiences": [
        {
            "experienceLocalId": 0,
            "name": "Silver",
            "audienceIds": [
                1209736
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 393707
                }
            ]
        },
        {
            "experienceLocalId": 2,
            "name": "Gold",
            "audienceIds": [
                1209737
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 395545
                }
            ]
        },
        {
            "experienceLocalId": 3,
            "name": "Sapphire",
            "audienceIds": [
                1209738
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 393708
                }
            ]
        }
    ],
    "metrics": [
        {
            "metricLocalId": 32767,
            "name": "metric_placeholder",
            "conversion": true,
            "mboxes": [
                {
                    "name": "conversion_placeholder",
                    "successEvent": "mbox_shown"
                }
            ],
            "action": {
                "type": "count_once"
            }
        }
    ],
    "analytics": {
        "reportSuite": "adobetargetmobileiosdemo",
        "dataCollectionHost": "adobetargetmobile.sc.omtrdc.net"
    },
    "modifiedAt": "2017-06-12T14:27:44Z"
}

````

Gets a Experience Targeted activity that is referenced by the id.



## Delete XT Activity by ID

> Sample Request for Delete XT Activity by ID

````shell

curl -X DELETE \
  https://mc.adobe.io/adobetargetmobile/target/activities/xt/168333 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for Delete XT Activity by ID

````
{
    "id": 168333,
    "thirdPartyId": "60cc9620-999f-4052-bdad-1567838db10d_1499659779896",
    "name": "My XT Activity",
    "state": "deleted",
    "priority": 0,
    "autoAllocateTraffic": {
        "enabled": false,
        "successEvaluationCriteria": "conversion_rate"
    },
    "locations": {
        "mboxes": [
            {
                "locationLocalId": 0,
                "name": "j1-mobile-xt"
            }
        ]
    },
    "experiences": [
        {
            "experienceLocalId": 0,
            "name": "Experience A",
            "audienceIds": [
                1209736
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 393707
                }
            ]
        },
        {
            "experienceLocalId": 1,
            "name": "Experience B",
            "audienceIds": [
                1209737
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 0
                }
            ]
        },
        {
            "experienceLocalId": 2,
            "name": "Experience C",
            "audienceIds": [
                1209738
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 0
                }
            ]
        }
    ],
    "metrics": [
        {
            "metricLocalId": 32767,
            "name": "MY PRIMARY GOAL",
            "conversion": true,
            "mboxes": [
                {
                    "name": "order-complete",
                    "successEvent": "mbox_shown"
                }
            ],
            "action": {
                "type": "count_once"
            }
        }
    ],
    "modifiedAt": "2017-07-10T04:09:39Z"
}

````

`DELETE /{tenant}/target/activities/xt/{id}`

Deletes the XT activity that is referenced by the id, if it is found.

## Create XT Activity

> Sample Request for Create XT Activity

````shell

curl -X POST \
  https://mc.adobe.io/adobetargetmobile/target/activities/xt/ \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
    "name": "New XT API Activity",
    "state": "saved",
    "priority": 10,
    "autoAllocateTraffic": {
        "enabled": false,
        "successEvaluationCriteria": "conversion_rate"
    },
    "locations": {
        "mboxes": [
            {
                "locationLocalId": 0,
                "name": "a1-serverside-xt"
            }
        ]
    },
    "experiences": [
        {
            "experienceLocalId": 0,
            "name": "USA Experience",
            "audienceIds": [
                1224696
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 396067
                }
            ]
        },
        {
            "experienceLocalId": 1,
            "name": "UK Experience",
            "audienceIds": [
                1224698
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 396064
                }
            ]
        },
        {
            "experienceLocalId": 2,
            "name": "France Experience",
            "audienceIds": [
                1224699
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 396065
                }
            ]
        },
        {
            "experienceLocalId": 3,
            "name": "Australia Experience",
            "audienceIds": [
                1224700
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 396066
                }
            ]
        }
    ],
    "metrics": [
        {
            "metricLocalId": 32767,
            "name": "metric_placeholder",
            "conversion": true,
            "mboxes": [
                {
                    "name": "conversion_placeholder",
                    "successEvent": "mbox_shown"
                }
            ],
            "action": {
                "type": "count_once"
            }
        }
    ],
    "analytics": {
        "reportSuite": "adobetargetmobilewesteros",
        "dataCollectionHost": "adobetargetmobile.sc.omtrdc.net"
    }
}'

````

> Sample Response for Create XT Activity

````

{
    "id": 183919,
    "name": "New XT API Activity",
    "state": "saved",
    "priority": 10,
    "autoAllocateTraffic": {
        "enabled": false,
        "successEvaluationCriteria": "conversion_rate"
    },
    "locations": {
        "mboxes": [
            {
                "locationLocalId": 0,
                "name": "a1-serverside-xt"
            }
        ]
    },
    "experiences": [
        {
            "experienceLocalId": 0,
            "name": "USA Experience",
            "audienceIds": [
                1224696
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 396067
                }
            ]
        },
        {
            "experienceLocalId": 1,
            "name": "UK Experience",
            "audienceIds": [
                1224698
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 396064
                }
            ]
        },
        {
            "experienceLocalId": 2,
            "name": "France Experience",
            "audienceIds": [
                1224699
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 396065
                }
            ]
        },
        {
            "experienceLocalId": 3,
            "name": "Australia Experience",
            "audienceIds": [
                1224700
            ],
            "offerLocations": [
                {
                    "locationLocalId": 0,
                    "offerId": 396066
                }
            ]
        }
    ],
    "metrics": [
        {
            "metricLocalId": 32767,
            "name": "metric_placeholder",
            "conversion": true,
            "mboxes": [
                {
                    "name": "conversion_placeholder",
                    "successEvent": "mbox_shown"
                }
            ],
            "action": {
                "type": "count_once"
            }
        }
    ],
    "analytics": {
        "reportSuite": "adobetargetmobilewesteros",
        "dataCollectionHost": "adobetargetmobile.sc.omtrdc.net"
    },
    "modifiedAt": "2017-07-10T06:01:27Z"
}

````

Creates a new XT activity with the specified contents and returns the created activity.

<aside class="notice">
Refer "Create AB Activity" for the available inputs, limitations and the description. The input for "Create XT Activity" method is very similar to the "Create AB Activity" method.
</aside>

<aside class="warning">
Activities created using the API can only be edited using the API. You can't edit it in the UI.
</aside>

## Update XT Activity

`PUT: /{tenant}/target/activities/xt/{id}`

Updates the Experience Targeted activity definition with the contents as provided in the request. This can change the state and behaviour of an existing activity.

<aside class="notice">
To Update an XT Activity use the same input as described in "Create XT Activity". You have to make a <b>PUT</b> request instead of a <b>POST</b> request to update an already existing activity.
</aside>


## Update Activity Name

> Sample Request for Update Activity Name (Rename Activity)

````shell

curl -X PUT \
  https://mc.adobe.io/adobetargetmobile/target/activities/168816/name \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
		"name": "New Name for Activity"
	  }'

````

> Sample Response for Update Activity Name

````
{
    "id": 168816,
    "name": "New Name for Activity",
    "modifiedAt": "2017-01-01T00:00Z"
}

````

Updates the name of the AB activity that is referenced by the supplied id.

`PUT: /{tenant}/target/activities/{id}/name`

<aside class="notice">
You can also use the specific endpoints <b>/activities/ab/{id}/name</b> and /<b>activities/xt/{id}/name</b> for updating the name of an AB or XT activity respectively. Best practice is to use the generic <b>/activities/{id}/name</b> so that you don't have to know or specify the type in the request.
</aside>


## Update Activity State


> Sample Request for Update Activity State

````shell

curl -X PUT \
  https://mc.adobe.io/adobetargetmobile/target/activities/168816/state \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
		"state": "deactivated"
	  }'

````

> Sample Response for Update Activity State

````
{
    "id": 168816,
    "state": "deactivated",
    "modifiedAt": "2017-01-01T00:00Z"
}

````


Update state for an activity that is referenced by the provided id. Valid values are:
* approved
* deactivated
* saved


`PUT: /{tenant}/target/activities/{id}/state`

<aside class="notice">
You can also use the specific endpoints <b>/activities/ab/{id}/state</b> and <b>/activities/xt/{id}/state</b> for updating the state of an AB or XT activity respectively. Best practice is to use the generic <b>/activities/{id}/state</b> so that you don't have to know or specify the type in the request.
</aside>


<aside class="warning">
<b>Known Issue</b> : The Target UI has 5 states and the API only provides 3 out of the 5. Also, they use different terminologoes. Approved = Live, Deactivated = Inactive, Saved = Draft.
</aside>


## Update Activity Priority

> Sample Request for Update Activity Priotity

````shell

curl -X PUT \
  https://mc.adobe.io/adobetargetmobile/target/activities/168816/priority \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
		"priority": "100"
	  }'

````

> Sample Response for Update Activity Priotity

````
{
    "id": 168816,
    "priority": 100,
    "modifiedAt": "2017-01-01T00:00Z"
}

````

Change priority for the AB activity that is referenced by the supplied id. Allowed values for priority are 0-999. If you are using low, medium and high in the Target UI, those correspond to 0,5 and 10 respectively. You need to turn granular priority on in the settings page inorder to use the 0-999 scale.

`PUT: /{tenant}/target/activities/{id}/priority`

<aside class="notice">
You can also use the specific endpoints <b>/activities/ab/{id}/priority</b> and <b>/activities/xt/{id}/priority </b> for updating the priority of an AB or XT activity respectively. Best practice is to use the generic <b>/activities/{id}/priority </b> so that you don't have to know or specify the type in the request.
</aside>




## Update Activity Schedule

> Sample Request for Update Activity Schedule

````shell

curl -X PUT \
  https://mc.adobe.io/adobetargetmobile/target/activities/168816/schedule \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
		"startsAt": "2017-05-01T08:00Z",
		"endsAt": "2017-09-01T07:59:59Z"
	  }'

````

> Sample Response for Update Activity Schedule

````
{
    "id": 168816,
    "startsAt": "2017-05-01T08:00Z",
    "endsAt": "2017-09-01T07:59:59Z",
    "modifiedAt": "2017-01-01T00:00Z"
}

````

`PUT: /{tenant}/target/activities/{id}/schedule`

Update the startsAt and endsAt fields of the AB activity referenced by the provided id. The schedule defines the start and end date and time for the activity. You need to pass the startsAt and endsAt values. If successful, it returns a status code 200. startsAt and endsAt support ISO 8601 style date-hour formats.

* yyyy-MM-dd'T'HH:mm:ssXXX
* yyyy-MM-dd'T'HH:mm:ss
* yyyy-MM-dd'T'HH
* yyyy-MM-dd
* yyyy-MM-dd'T'HH:mm:ss.SSS
* yyyy-MM-dd'T'HH:mm:ss.SSSXXX

<aside class="notice">
You can also use the specific endpoints <b>/activities/ab/{id}/schedule </b> and <b>/activities/xt/{id}/schedule </b> for updating the schedule of an AB or XT activity respectively. Best practice is to use the generic <b>/activities/{id}/schedule </b> so that you don't have to know or specify the type in the request.
</aside>




## Get Activity Changelog

> Sample Request for Get Activity Changelog

````shell

curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/activities/173980/changelog \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for Get Activity Changelog

````

{
    "offset": 0,
    "limit": 2147483647,
    "total": 23,
    "activityChangelogs": [
        {
            "modifiedAt": "2017-05-11T12:16:13Z",
            "activityParameters": {
                "state": {
                    "previousValue": "approved",
                    "changedValue": "saved"
                }
            }
        },
        {
            "modifiedAt": "2017-04-27T14:57:32Z",
            "activityParameters": {
                "activityName": {
                    "previousValue": "Mobile Webinar  - Micro Soft Permission",
                    "changedValue": "Mobile Webinar  - Soft Permission"
                }
            }
        },
        {
            "modifiedAt": "2017-04-27T14:57:32Z",
            "modifiedOffer": {
                "id": 426963,
                "name": "/master_-_mobile_-abcopy/experiences/1/pages/0/zones/0/1493301097428"
            }
        },
        {
            "modifiedAt": "2017-04-27T14:09:44Z",
            "activityParameters": {
                "state": {
                    "previousValue": "approved",
                    "changedValue": "saved"
                }
            }
        },
        {
            "modifiedAt": "2017-04-27T13:56:03Z",
            "activityLocationOfferChange": {
                "changedValue": {
                    "id": 426963,
                    "name": "/master_-_mobile_-abcopy/experiences/1/pages/0/zones/0/1493301097428"
                },
                "previousValue": {
                    "id": 391902,
                    "name": "10OFF"
                },
                "mbox": {
                    "name": "a1-mobile-ab",
                    "locationLocalId": 0
                },
                "experience": {
                    "name": "Always",
                    "experienceLocalId": 1
                }
            }
        },
        {
            "modifiedAt": "2017-04-27T13:56:03Z",
            "modifiedOffer": {
                "id": 426962,
                "name": "/master_-_mobile_-abcopy/experiences/0/pages/0/zones/0/1493301097401"
            }
        },
        {
            "modifiedAt": "2017-04-27T13:51:38Z",
            "activityParameters": {
                "state": {
                    "changedValue": "saved"
                }
            }
        }
    ]
}

````

`GET /{tenant}/target/activities/{id}/changelog`

Returns the changelog for a given activity id.



# Offers

API methods to Create, Read, Update and Delete Offers. Offers are also referred to as Content.


## List Offers

> Sample Request for List Offers

````shell

curl -X GET \
  'https://mc.adobe.io/adobetargetmobile/target/offers?limit=10' \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````
> Sample Response for List Offers

````
{
    "total": 1120,
    "offset": 0,
    "limit": 10,
    "offers": [
        {
            "id": 391769,
            "name": "/l1_a_b_test/experiences/0/pages/0/zones/0/1489440825492",
            "type": "content",
            "modifiedAt": "2017-03-20T03:03:28Z"
        },
        {
            "id": 391902,
            "name": "10OFF",
            "type": "content",
            "modifiedAt": "2017-03-19T00:06:47Z"
        },
        {
            "id": 391903,
            "name": "SHIPFREE",
            "type": "content",
            "modifiedAt": "2017-03-19T00:06:29Z"
        },
        {
            "id": 391904,
            "name": "5OFF",
            "type": "content",
            "modifiedAt": "2017-03-19T00:06:26Z"
        },
        {
            "id": 391905,
            "name": "/a1_-_l4206a_-_ab/experiences/0/pages/0/zones/0/1489468580249",
            "type": "content",
            "modifiedAt": "2017-06-30T19:48:38Z"
        },
        {
            "id": 391906,
            "name": "/a1_-_l4206a_-_ab/experiences/1/pages/0/zones/0/1489468580252",
            "type": "content",
            "modifiedAt": "2017-06-14T20:24:39Z"
        },
        {
            "id": 391907,
            "name": "/a1_-_l4206a_-_ab/experiences/2/pages/0/zones/0/1489468580255",
            "type": "content",
            "modifiedAt": "2017-04-21T21:34:55Z"
        },
        {
            "id": 391910,
            "name": "/a1_-_l4206a_-_xt/experiences/0/pages/0/zones/0/1489470215324",
            "type": "content",
            "modifiedAt": "2017-03-19T03:51:21Z"
        },
        {
            "id": 391911,
            "name": "/a1_-_l4206a_-_xt/experiences/1/pages/0/zones/0/1489470215327",
            "type": "content",
            "modifiedAt": "2017-03-14T05:43:36Z"
        },
        {
            "id": 391919,
            "name": "/a1_-_l4206a_-_xt/experiences/2/pages/0/zones/0/1489474831626",
            "type": "content",
            "modifiedAt": "2017-03-19T03:51:21Z"
        }
    ]
}

````

### `GET /{tenant}/target/offers`

Retrieve the list of previously-created content offers. The parameters passed through the query string are **optional** and are used to indicate the sorting and filtering options.


<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Description</th>
            <th>Example</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><em>limit</em>
            </td>
            <td>
                <p>Defines the number of items to return. Default value is 2147483647.</p>

            </td>
            <td>
                <p><span class="text-code"> Returns the first ten offers
            <code>/target/offers/?limit=10</code></span>
                </p>
            </td>
        </tr>
        <tr>
            <td><em>offset</em>
            </td>
            <td>
                <p>Defines the first offer to return from the list of total offers. Used in conjunction with limit, you can provide pagination in your application for users to browse through a large set of offers.</p>
            </td>
            <td>
                <p><span>Returns the first ten offers<br>
            <code>/target/offers/?limit=10&amp;offset=0 </code><br><br>
            Returns offers between 11-20<br>
			  <code>/target/offers/?limit=10&amp;offset=10</code> </span>
                </p>
            </td>
        </tr>
        <tr>
            <td><em>sortBy</em>
            </td>
            <td>
                <p>Defines the sorting criteria on the returned items. You can add a "-" modifier to sort by descending order.</p>
            </td>
            <td>
                <p><span>

             <p>Returns the first ten offers sorted by ID<br>
            <code>/target/offers/?sortBy=id&amp;limit=10</code><br></p>


			<p>Returns the first ten offers sorted in descending order by ID<br>
			<code>/target/offers/?sortBy=-id&amp;limit=10</code><br></p>

		 <p>Returns the first ten offers sorted by ascending IDs and descending names
		<code>/target/offers/?sortBy=id,-name&amp;limit=10</code><br></p>

</span>
                </p>
            </td>
        </tr>
    </tbody>
</table>


## Get Offer by ID

> Sample Request for Get Offer by ID

````shell
curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/offers/content/391902 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for Get Offer by ID


````
{
    "id": 391902,
    "name": "10OFF",
    "content": "Use 10OFF for $10 off for orders over $100",
    "modifiedAt": "2017-03-19T00:06:47Z"
}

````

### `GET /{tenant}/target/offers/content/{id}`


Retrieves the contents of an offer given an offer id.

## Create Offer

> Sample Request for Create Offer

````shell
curl -X POST \
  https://mc.adobe.io/adobetargetmobile/target/offers/content \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d ' {
	 "name": "My new offer",
	 "content": "<div>The content of the offer</div>"
 }
'

````

> Sample Response for Create Offer

````

{
    "id": 438180,
    "name": "My new offer",
    "content": "<div>The content of the offer</div>",
    "modifiedAt": "2017-07-10T20:46:53Z"
}

````

`POST: /{tenant}/target/offers/content`

Creates a new content offer as defined by the request data.



## Update Offer by ID

> Sample Request for Update Offer by ID

````shell
curl -X PUT \
  https://mc.adobe.io/adobetargetmobile/target/offers/content/438180 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d ' {
	"name": "Your existing offer",
	"content": "<div>Updated content</div>"
 }
'

````

> Sample Response for Update Offer by ID

````

{
    "id": 438180,
    "name": "Your existing offer",
    "content": "<div>Updated content</div>",
    "modifiedAt": "2017-07-10T20:55:41Z"
}

````


`PUT /{tenant}/target/offers/content/{id}`

Updates the content offer referenced by the id specified in the URL.


## Delete Offer by ID

> Sample Request for Delete Offer by ID


````shell

curl -X DELETE \
  https://mc.adobe.io/adobetargetmobile/target/offers/content/438180 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for Delete Offer by ID

````

{
    "id": 438180,
    "name": "Your existing offer",
    "content": "<div>Updated content</div>",
    "modifiedAt": "2017-07-10T20:55:41Z"
}

````

`DELETE /{tenant}/target/offers/content/{id}`

Deletes the content offer referenced by the provided id.



# Audiences

API methods to Create, Read, Update and Delete Audiences.


## List Audiences

> Sample Request for List Audiences

````shell
curl -X GET \
  'https://mc.adobe.io/adobetargetmobile/target/audiences/' \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for List Audiences

````

{
    "offset": 0,
    "limit": 10,
    "total": 289,
    "audiences": [
        {
            "id": 1216090,
            "name": "A1 -  Active account l-1489628809975",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-16T01:47:07Z"
        },
        {
            "id": 1216183,
            "name": "A1 - Current Category -1489642111631",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-16T05:28:33Z"
        },
        {
            "id": 1216184,
            "name": "A1 - Current category -1489642149723",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-16T05:29:11Z"
        },
        {
            "id": 1222658,
            "name": "A1 - Customer Attribute -1489821120208",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-18T07:45:41Z"
        },
        {
            "id": 1238132,
            "name": "A1 - L206 - Profile - -1490293696694",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-23T18:28:19Z"
        },
        {
            "id": 1238133,
            "name": "A1 - L206 - Profile - -1490293722988",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-23T18:28:43Z"
        },
        {
            "id": 1238134,
            "name": "A1 - L206 - Profile - -1490293734000",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-23T18:28:55Z"
        },
        {
            "id": 1238135,
            "name": "A1 - L206 - Profile - -1490293749957",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-23T18:29:12Z"
        },
        {
            "id": 1235754,
            "name": "A1 - L4206 - Alec - Us-1490221177054",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-22T22:19:38Z"
        },
        {
            "id": 1229960,
            "name": "A1 - L4206 - Cart Amou-1490140690240",
            "description": "--",
            "origin": "target",
            "modifiedAt": "2017-03-22T01:40:55Z"
        }
    ]
}

````


### `GET: /{tenant}/target/audiences`

List all available audiences with options to filter and sort by each available field.

You can use the URL parameters to define pagination properties and sorting order of the list of audiences returned by this method.

<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Description</th>
            <th>Example</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><em>limit</em>
            </td>
            <td>
                <p>Defines the number of items to return. Default value is 2147483647.</p>

            </td>
            <td>
                <p><span> Returns the first ten audiences
            <code>/target/audiences/?limit=10</code></span>
                </p>
            </td>
        </tr>
        <tr>
            <td><em>offset</em>
            </td>
            <td>
                <p>Defines the first audience to return from the list of total offers. Used in conjunction with limit, you can provide pagination in your application for users to browse through a large set of offers.</p>
            </td>
            <td>
                <p><span>Returns the first ten audiences<br>
            <code>/target/audiences/?limit=10&amp;offset=0 </code><br><br>
            Returns audiences between 11-20<br>
			  <code>/target/audiences/?limit=10&amp;offset=10</code> </span>
                </p>
            </td>
        </tr>
        <tr>
            <td><em>sortBy</em>
            </td>
            <td>
                <p>Defines the sorting criteria on the returned items. You can add a "-" modifier to sort by descending order.</p>
            </td>
            <td>
                <p><span>

             <p>Returns the first ten audiences sorted by ID<br>
            <code>/target/audiences/?sortBy=id&amp;limit=10</code><br></p>


			<p>Returns the first ten audiences sorted in descending order by ID<br>
			<code>/target/audiences/?sortBy=-id&amp;limit=10</code><br></p>

		 <p>Returns the first ten audiences sorted by ascending IDs and descending names
		<code>/target/audiences/?sortBy=id,-name&amp;limit=10</code><br></p>

</span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

### Some Additonal Examples

GET list of all audiences
`https://mc.adobe.io/{tenant}/target/audiences/`

GET audiences list with limit
`https://mc.adobe.io/{tenant}/target/audiences/?limit=1`

GET audiences list with limit and offset
`https://mc.adobe.io/{tenant}/target/audiences/?limit=2&offset=2`

GET audiences list filtered by multiple values
`https://mc.adobe.io/{tenant}/target/audiences/?id=3&id=4&name=ab`

GET audiences list filtered by negative values
`https://mc.adobe.io/{tenant}/target/audiences/?priority=!4`

GET audiences list sorted by multiple criteria
`https://mc.adobe.io/{tenant}/target/audiences/?sortBy=name&sortBy=id`

GET audiences list filtered by a date range
`https://mc.adobe.io/{tenant}/target/audiences/?startsAt=1800-09-01T02:04:00.000-07:00/2114-11-30T14:10:00.000-07:00`

## Get Audience by ID

> Sample Request for Get Audience by ID

````shell
curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/audiences/1397972 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for Get Audience by ID

````

{
    "id": 1397972,
    "name": "Gold Members in Califo-1495136673062",
    "description": "--",
    "origin": "target",
    "targetRule": {
        "and": [
            {
                "profile": "memberLevel",
                "equals": [
                    "gold"
                ]
            },
            {
                "geo": "region",
                "matches": [
                    "california"
                ]
            }
        ]
    },
    "modifiedAt": "2017-05-18T19:44:34Z"
}

````

`GET: /{tenant}/target/audiences/{id}`

Get the audience definition specified by the provided id.

## Create Audience

> Sample Request for Create Audience

````shell

curl -X POST \
  https://mc.adobe.io/adobetargetmobile/target/audiences \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
	"name": "Homepage visitors from California",
	"description":"Description for my audience",
    "targetRule": {
        "and": [
            {
                "page": "url",
				"equals":[
					"http://www.myhomepage.com/"
				]
            },
            {
                "geo": "region",
                "matches": [
                    "california"
                ]
            }
        ]
    }
}'

````

> Sample Request for Create Audience

````

{
    "id": 1537195,
    "name": "Homepage visitors from California",
    "description": "Description for my audience",
    "origin": "target",
    "targetRule": {
        "and": [
            {
                "page": "url",
                "equals": [
                    "http://www.myhomepage.com/"
                ]
            },
            {
                "geo": "region",
                "matches": [
                    "california"
                ]
            }
        ]
    },
    "modifiedAt": "2017-07-10T22:24:04Z"
}

````


`POST /{tenant}/target/audiences`

<aside class="warning">
Audiences created using the API can only be edited using the API. You can't edit it in the UI. You can use it in your activities though.
</aside>


Create a new audience as specified by the contents of the request and return the newly-created audience definition.

Each audience definition is made up of either target or audience rules.

* Target rules allow the API caller to define conjunctions (OR) or disjunctions (AND) between various targeting conditions.
* Audience rules allow the API caller to build conjunctions (OR) or disjunctions over pre-built audiences (referred by ids) to create even more powerful definitions

**targetRules** and **audienceRule** cannot be mixed within the same audience definition.


<table>
    <thead>
        <tr>
            <th>Attribute</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td valign="top"><em>name</em>
            </td>
            <td>String</td>
            <td>A unique name for the audience</td>
        </tr>
        <tr>
            <td valign="top"><em>description</em>
            </td>
            <td>String</td>
            <td>A description for the audience</td>
        </tr>
        <tr>
            <td valign="top"><em>targetRule</em>
            </td>
            <td>Array</td>
            <td>An array of rule objects containing logical target statements using operators such as AND, OR, EQUALS, etc.</td>
        </tr>
        <tr>
            <td valign="top"><em>audienceRule</em>
            </td>
            <td>Array</td>
            <td>
                <p>An array of rule objects that refer to pre-built audiences referred by their IDs</p>
            </td>
        </tr>
    </tbody>
</table>


## Update Audience by ID

> Sample Request for Update Audience by ID

````shell
curl -X PUT \
  https://mc.adobe.io/adobetargetmobile/target/audiences/1537195 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
	"name": "Homepage visitors from California",
	"description":"Description for my audience",
    "targetRule": {
        "and": [
            {
                "page": "url",
				"equals":[
					"http://www.mynewhomepage.com/"
				]
            },
            {
                "geo": "region",
                "matches": [
                    "california"
                ]
            }
        ]
    }
}'

````

> Sample Request for Update Audience by ID

````
{
    "id": 1537195,
    "name": "Homepage visitors from California",
    "description": "Description for my audience",
    "origin": "target",
    "targetRule": {
        "and": [
            {
                "page": "url",
                "equals": [
                    "http://www.mynewhomepage.com/"
                ]
            },
            {
                "geo": "region",
                "matches": [
                    "california"
                ]
            }
        ]
    },
    "modifiedAt": "2017-07-10T22:29:28Z"
}


````



`PUT /{tenant}/target/audiences/{id}`


Update an audience with the new rules specified by the request data.


## Delete Audience by ID

> Sample Request for Delete Audience by ID

````shell
curl -X DELETE \
  https://mc.adobe.io/adobetargetmobile/target/audiences/1537214 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Request for Delete Audience by ID

````
{
    "id": 1537214,
    "name": "New Audience",
    "description": "Description for my audience",
    "origin": "target",
    "targetRule": {
        "and": [
            {
                "page": "url",
                "equals": [
                    "http://www.myhomepage.com/"
                ]
            },
            {
                "geo": "region",
                "matches": [
                    "california"
                ]
            }
        ]
    },
    "modifiedAt": "2017-07-10T22:31:18Z"
}

````


`DELETE /{tenant}/target/audiences/{id}`


Delete the audience referenced by the specified id.



# Reports


## Get AB Performance Report

> Sample Request for Get AB Performance Report

````shell

curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/activities/ab/166423/report/performance \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'


````

> Sample Response for Get AB Performance Report

````
{
    "reportParameters": {
        "activityId": 166423,
        "environmentId": 8818,
        "conversionMetricLocalIds": [
            32767
        ],
        "reportInterval": "2017-03-14T05:00Z/2017-07-10T07:00Z"
    },
    "activity": {
        "id": 166423,
        "thirdPartyId": "f79c0aa0-44e4-4766-ab93-1bf11b781f84",
        "type": "ab",
        "state": "approved",
        "name": "Master - Mobile - AB",
        "priority": 999,
        "modifiedAt": "2017-06-30T19:48:38Z",
        "metrics": [
            {
                "name": "Entry",
                "metricLocalId": 0
            },
            {
                "name": "Display mboxes",
                "metricLocalId": 2
            },
            {
                "name": "metric_placeholder",
                "metricLocalId": 32767
            }
        ],
        "experiences": [
            {
                "name": "5OFF",
                "experienceLocalId": 0
            },
            {
                "name": "SHIPFREE",
                "experienceLocalId": 2
            },
            {
                "name": "10OFF",
                "experienceLocalId": 1,
                "deletedAt": "2017-06-14T21:02:12.000Z"
            }
        ]
    },
    "report": {
        "statistics": {
            "totals": {
                "visitor": {
                    "totals": {
                        "entries": 115,
                        "conversions": 0
                    }
                },
                "visit": {
                    "totals": {
                        "entries": 274,
                        "conversions": 0
                    }
                },
                "impression": {
                    "totals": {
                        "entries": 328,
                        "conversions": 0
                    }
                },
                "landing": {
                    "totals": {
                        "entries": 328,
                        "conversions": 0
                    }
                }
            },
            "experiences": [
                {
                    "experienceLocalId": 0,
                    "totals": {
                        "visitor": {
                            "totals": {
                                "entries": 31,
                                "conversions": 0
                            }
                        },
                        "visit": {
                            "totals": {
                                "entries": 85,
                                "conversions": 0
                            }
                        },
                        "impression": {
                            "totals": {
                                "entries": 102,
                                "conversions": 0
                            }
                        },
                        "landing": {
                            "totals": {
                                "entries": 102,
                                "conversions": 0
                            }
                        }
                    }
                },
                {
                    "experienceLocalId": 1,
                    "totals": {
                        "visitor": {
                            "totals": {
                                "entries": 34,
                                "conversions": 0
                            }
                        },
                        "visit": {
                            "totals": {
                                "entries": 123,
                                "conversions": 0
                            }
                        },
                        "impression": {
                            "totals": {
                                "entries": 140,
                                "conversions": 0
                            }
                        },
                        "landing": {
                            "totals": {
                                "entries": 140,
                                "conversions": 0
                            }
                        }
                    }
                },
                {
                    "experienceLocalId": 2,
                    "totals": {
                        "visitor": {
                            "totals": {
                                "entries": 50,
                                "conversions": 0
                            }
                        },
                        "visit": {
                            "totals": {
                                "entries": 66,
                                "conversions": 0
                            }
                        },
                        "impression": {
                            "totals": {
                                "entries": 86,
                                "conversions": 0
                            }
                        },
                        "landing": {
                            "totals": {
                                "entries": 86,
                                "conversions": 0
                            }
                        }
                    }
                }
            ]
        }
    }
}

````

`GET /{tenant}/target/activities/ab/{id}/report/performance`

Retrieve the performance report data for the AB activity referenced by the provided id.


## Get XT Performance Report

> Sample Request for Get XT Performance Report

````shell

curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/activities/xt/167169/report/performance \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'


````

> Sample Response for Get XT Performance Report

````

{
    "reportParameters": {
        "activityId": 167169,
        "environmentId": 8818,
        "conversionMetricLocalIds": [
            32767
        ],
        "reportInterval": "2017-03-20T16:00Z/2017-07-10T07:00Z"
    },
    "activity": {
        "id": 167169,
        "thirdPartyId": "6116ec53-5a2b-4f5d-9268-41e4c153e494",
        "type": "xt",
        "state": "approved",
        "name": "Master - Serverside - XT",
        "priority": 0,
        "modifiedAt": "2017-06-06T22:00:25Z",
        "metrics": [
            {
                "name": "Entry",
                "metricLocalId": 0
            },
            {
                "name": "Display mboxes",
                "metricLocalId": 2
            },
            {
                "name": "metric_placeholder",
                "metricLocalId": 32767
            }
        ],
        "experiences": [
            {
                "name": "USA Experience",
                "experienceLocalId": 0
            },
            {
                "name": "UK Experience",
                "experienceLocalId": 1
            },
            {
                "name": "France Experience",
                "experienceLocalId": 2
            },
            {
                "name": "Australia Experience",
                "experienceLocalId": 3
            }
        ]
    },
    "report": {
        "statistics": {
            "totals": {
                "visitor": {
                    "totals": {
                        "entries": 41,
                        "conversions": 0
                    }
                },
                "visit": {
                    "totals": {
                        "entries": 52,
                        "conversions": 0
                    }
                },
                "impression": {
                    "totals": {
                        "entries": 72,
                        "conversions": 0
                    }
                },
                "landing": {
                    "totals": {
                        "entries": 72,
                        "conversions": 0
                    }
                }
            },
            "experiences": [
                {
                    "experienceLocalId": 0,
                    "totals": {
                        "visitor": {
                            "totals": {
                                "entries": 11,
                                "conversions": 0
                            }
                        },
                        "visit": {
                            "totals": {
                                "entries": 16,
                                "conversions": 0
                            }
                        },
                        "impression": {
                            "totals": {
                                "entries": 27,
                                "conversions": 0
                            }
                        },
                        "landing": {
                            "totals": {
                                "entries": 27,
                                "conversions": 0
                            }
                        }
                    }
                },
                {
                    "experienceLocalId": 1,
                    "totals": {
                        "visitor": {
                            "totals": {
                                "entries": 9,
                                "conversions": 0
                            }
                        },
                        "visit": {
                            "totals": {
                                "entries": 11,
                                "conversions": 0
                            }
                        },
                        "impression": {
                            "totals": {
                                "entries": 13,
                                "conversions": 0
                            }
                        },
                        "landing": {
                            "totals": {
                                "entries": 13,
                                "conversions": 0
                            }
                        }
                    }
                },
                {
                    "experienceLocalId": 2,
                    "totals": {
                        "visitor": {
                            "totals": {
                                "entries": 9,
                                "conversions": 0
                            }
                        },
                        "visit": {
                            "totals": {
                                "entries": 12,
                                "conversions": 0
                            }
                        },
                        "impression": {
                            "totals": {
                                "entries": 17,
                                "conversions": 0
                            }
                        },
                        "landing": {
                            "totals": {
                                "entries": 17,
                                "conversions": 0
                            }
                        }
                    }
                },
                {
                    "experienceLocalId": 3,
                    "totals": {
                        "visitor": {
                            "totals": {
                                "entries": 12,
                                "conversions": 0
                            }
                        },
                        "visit": {
                            "totals": {
                                "entries": 13,
                                "conversions": 0
                            }
                        },
                        "impression": {
                            "totals": {
                                "entries": 15,
                                "conversions": 0
                            }
                        },
                        "landing": {
                            "totals": {
                                "entries": 15,
                                "conversions": 0
                            }
                        }
                    }
                }
            ]
        }
    }
}


````

`GET /{tenant}/target/activities/xt/{id}/report/performance`

Retrieve the performance report data for the Experience activity referenced by the provided id.


## Get AP Activity Performance Report


`GET /{tenant}/target/activities/abt/{id}/report/performance`

Retrieve the performance report data for the Automated Personalization activity referenced by the provided id.

<aside class="notice">
The request format is similar to AB and XT performance report. Change /ab or /xt to <b>/abt</b> in the request url. <b>abt</b> is the request paramater for Automated Personalization activities.
</aside>

## Get Audit Report

> Sample Request for AB Audit Report

````shell

curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/activities/ab/167169/orders/performance \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for AB and XT Audit Reports

````json
{
    "reportParameters": {
        "activityId": 167169,
        "environmentId": 8818,
        "reportInterval": "2017-03-20T16:00Z/2017-08-19T00:01:01.721Z",
        "conversionMetricLocalIds": [
            32767
        ]
    },
"activity": {
        "id": 167169,
        "thirdPartyId": "6116ec53-5a2b-4f5d-9268-41e4c153e494",
        "type": "xt",
        "state": "approved",
        "name": "Master - Serverside - XT",
        "priority": 0,
        "modifiedAt": "2017-07-31T18:23:44Z",
        "metrics": [
            {
                "name": "Entry",
                "metricLocalId": 0
            },
            {
                "name": "Display mboxes",
                "metricLocalId": 2
            },
            {
                "name": "metric_placeholder",
                "metricLocalId": 32767
            }
        ],
        "experiences": [
            {
                "name": "USA Experience",
                "experienceLocalId": 0
            },
            {
                "name": "UK Experience",
                "experienceLocalId": 1
            },
            {
                "name": "France Experience",
                "experienceLocalId": 2
            },
            {
                "name": "Australia Experience",
                "experienceLocalId": 3
            }
        ]
    },
    "orders": [
          {
            "time": "2015-12-04T00:00:00.000-05:00",
            "experienceLocalId": 0,
            "id": "order ID 4444",
            "total": 7.4,
            "duplicate": true,
            "outlier": true,
            "productPurchasedIds": ["laptop3", "book3"]
          },
          {
            "time": "2015-12-02T10:03:00.000-05:00",
            "experienceLocalId": 1,
            "id": "order REF ID#123",
            "total": 23.01
          },

          ...
  ]
}

````

> Sample Response for AP Audit Reports.

````json

  "orders": [
    {
      "time": "2017-01-11T00:00:00.000-05:00",
      "decisionStackId": 0,
      "id": "1452535235728",
      "total": 325,
      "productIds": [
        "5"
      ]
    },
    {
      "time": "2017-01-11T00:00:00.000-05:00",
      "decisionStackId": 1,
      "id": "1452535342214",
      "total": 325,
      "productIds": [
        "5"
      ]
    },
    {
      "time": "2017-01-11T00:00:00.000-05:00",
      "decisionStackId": 2,
      "id": "1452535371489",
      "total": 429,
      "productIds": [
        "9"
      ]
    }
  ]
}

````


`GET /{tenant}/target/activities/ab/{id}/report/orders`

Retrieve the orders/audit report data for an AB, XT or Autotmated Personalization Activity

<aside class="notice">
Change /ab to /xt or /abt in the request url for XT and AP activities. <b>abt</b> is the request paramater for Automated Personalization activities.
</aside>

# Mboxes and Environments

APIs to retrive mboxes, mbox paramaters, profile parmeters and environments.

## List Mboxes

> Sample Request for List Mboxes

````shell

curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/mboxes \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for List Mboxes

````
{
    "total": 12,
    "offset": 0,
    "limit": 5,
    "mboxes": [
        {
            "name": "a1-mobile-aam",
            "status": "active",
            "lastRequestedAt": "2017-07-09T20:41:18.000Z"
        },
        {
            "name": "a1-mobile-ab",
            "status": "active",
            "lastRequestedAt": "2017-07-04T10:22:59.000Z"
        },
        {
            "name": "a1-mobile-mboxparams",
            "status": "active",
            "lastRequestedAt": "2017-07-09T21:13:36.000Z"
        },
        {
            "name": "a1-mobile-profileparams",
            "status": "active",
            "lastRequestedAt": "2017-06-29T17:24:54.000Z"
        },
        {
            "name": "a1-mobile-xt",
            "status": "active",
            "lastRequestedAt": "2017-07-04T10:19:21.000Z"
        }
    ]
}


````

<aside class="notice">
The limit, offset and Sortby paramaters described in List Offers and List Audiences can be used for this API as well.
</aside>


### `GET /{tenant}/target/mboxes`

List all available mboxes for a specific client with the options to filter and sort.

## List Mbox Parameters

> Sample Request for List Mbox Parameters

````shell
curl -X GET \
  'https://mc.adobe.io/adobetargetmobile/target/mbox/a1-mobile-mboxparams?limit=5' \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'


````

> Sample Response for List Mbox Parameters

````
{
    "name": "a1-mobile-mboxparams",
    "mboxParameters": [
        {
            "name": "a.AppID",
            "parameterType": "MBOX"
        },
        {
            "name": "a.CarrierName",
            "parameterType": "MBOX"
        },
        {
            "name": "a.CrashEvent",
            "parameterType": "MBOX"
        },
        {
            "name": "a.DailyEngUserEvent",
            "parameterType": "MBOX"
        },
        {
            "name": "a.DayOfWeek",
            "parameterType": "MBOX"
        },
        {
            "name": "a.DaysSinceFirstUse",
            "parameterType": "MBOX"
        },
        {
            "name": "a.DaysSinceLastUse",
            "parameterType": "MBOX"
        },
        {
            "name": "a.DeviceName",
            "parameterType": "MBOX"
        },
        {
            "name": "a.HourOfDay",
            "parameterType": "MBOX"
        },
        {
            "name": "a.LaunchEvent",
            "parameterType": "MBOX"
        },
        {
            "name": "a.Launches",
            "parameterType": "MBOX"
        },
        {
            "name": "a.MonthlyEngUserEvent",
            "parameterType": "MBOX"
        },
        {
            "name": "a.OSVersion",
            "parameterType": "MBOX"
        },
        {
            "name": "a.PrevSessionLength",
            "parameterType": "MBOX"
        },
        {
            "name": "a.Resolution",
            "parameterType": "MBOX"
        },
        {
            "name": "a.locale",
            "parameterType": "MBOX"
        },
        {
            "name": "a.ltv.amount",
            "parameterType": "MBOX"
        },
        {
            "name": "currentCategory",
            "parameterType": "MBOX"
        },
        {
            "name": "isloggedin",
            "parameterType": "MBOX"
        },
        {
            "name": "mboxAAMB",
            "parameterType": "MBOX"
        },
        {
            "name": "mboxMCGLH",
            "parameterType": "MBOX"
        },
        {
            "name": "mboxMCGVID",
            "parameterType": "MBOX"
        },
        {
            "name": "vst.member_guid.authState",
            "parameterType": "MBOX"
        },
        {
            "name": "vst.member_guid.id",
            "parameterType": "MBOX"
        },
        {
            "name": "vst.mycustomerid.authState",
            "parameterType": "MBOX"
        },
        {
            "name": "vst.mycustomerid.id",
            "parameterType": "MBOX"
        },
        {
            "name": "page.domain",
            "parameterType": "MBOX"
        },
        {
            "name": "page.param",
            "parameterType": "MBOX"
        },
        {
            "name": "page.protocol",
            "parameterType": "MBOX"
        },
        {
            "name": "page.query",
            "parameterType": "MBOX"
        },
        {
            "name": "page.url",
            "parameterType": "MBOX"
        },
        {
            "name": "page.path",
            "parameterType": "MBOX"
        },
        {
            "name": "page.fragment",
            "parameterType": "MBOX"
        },
        {
            "name": "landing.domain",
            "parameterType": "MBOX"
        },
        {
            "name": "landing.param",
            "parameterType": "MBOX"
        },
        {
            "name": "landing.protocol",
            "parameterType": "MBOX"
        },
        {
            "name": "landing.query",
            "parameterType": "MBOX"
        },
        {
            "name": "landing.url",
            "parameterType": "MBOX"
        },
        {
            "name": "landing.path",
            "parameterType": "MBOX"
        },
        {
            "name": "landing.fragment",
            "parameterType": "MBOX"
        },
        {
            "name": "referrer.domain",
            "parameterType": "MBOX"
        },
        {
            "name": "referrer.param",
            "parameterType": "MBOX"
        },
        {
            "name": "referrer.protocol",
            "parameterType": "MBOX"
        },
        {
            "name": "referrer.query",
            "parameterType": "MBOX"
        },
        {
            "name": "referrer.url",
            "parameterType": "MBOX"
        },
        {
            "name": "referrer.path",
            "parameterType": "MBOX"
        }
    ]
}

````


### `GET /{tenant}/target/mbox/{mboxName}`


Get the list of mbox parameters.



## List Profile Parameters

> Sample Request for List Profile Parameters

````shell

curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/profileattributes/mbox \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for List Profile Parameters

````
{
    "mboxProfileAttributes": [
        "activeAccounts",
        "country",
        "entity.id",
        "entity.name",
        "gotlastname",
        "hasChecking",
        "hasMortgage",
        "hasRetirement",
        "house",
        "mbox3rdPartyId",
        "memberLevel",
        "nbalastname",
        "param1",
        "param2",
        "playerName",
        "qaExperience",
        "transformerType"
    ]
}

````


### `GET /{tenant}/target/profileattributes/mbox`


Retrieve the list of available profile attributes and mbox parameters of type profile

<aside class="notice">
Profile attributes and Profile Parameters mean the same thing. Both versions are used in the UI and the documentation.
</aside>


## List Environments

> Sample Request for List Environments

````shell

curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/environments \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````
> Sample Response for List Environments

````
{
    "total": 3,
    "offset": 0,
    "limit": 2147483647,
    "environments": [
        {
            "id": 8820,
            "name": "Development"
        },
        {
            "id": 8818,
            "name": "Production"
        },
        {
            "id": 8819,
            "name": "Staging"
        }
    ]
}

````


### `GET : /{tenant}/target/environments`


List all available environments with the options to filter and sort. Use the Environments API to retrieve the environment IDs corresponding to the various host groups set for the client.

<aside class="notice">
If you are looking to retrieve "Host Groups", use this API.
</aside>


# Batch Updates

Execute multiple API calls as a single batch request.


## Execute Calls in Batch

> Sample Request Object

````shell
{
  "operations": [
    {
      "operationId": 1,
      "dependsOnOperationIds~": [0],
      "method": "POST",
      "relativeUrl": "/v1/offers",
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ],
      "body~": {
        "key": "value"
      }
    }
  ]
}

````

> Sample Response Object

````
{
  "results": [
    {
      "operationId": 1,
      "skipped~": false,
      "statusCode~": 200,
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json; charset=UTF-8"
        }
      ],
      "body~": {
        "id": 5
      }
    }
  ]
}


````




### `POST /{tenant}/target/batch`


Stack multiple API calls together and execute them in a single batch.

Batching allows you to pass instructions for several operations in a single HTTP request. You can also specify dependencies between related operations (described in a section below). TNT will process each of your independent operations (possibly in parallel) and will process your dependent operations sequentially. Once all operations have been completed, a consolidated response will be passed back and the HTTP connection will be closed.

The batch API takes in an array of logical HTTP requests represented as JSON arrays - each request has a method (corresponding to HTTP method GET/PUT/POST/DELETE etc.), a relativeUrl (the portion of the URL after admin/rest/), optional headers array (corresponding to HTTP headers) and an optional body (for POST and PUT requests). The Batch API returns an array of logical HTTP responses represented as JSON arrays - each response has a status code, an optional headers array and an optional body (which is a JSON encoded string). To make batched requests build a JSON object which describes each individual operation to perform. The number of maximum allowed operations are 256 (from 0 to 255).

Specifying dependencies between operations in the request
By default, the operations specified in the batch API request are independent - they can be executed in arbitrary order on the server and an error in one operation does not affect execution of other operations.

Often, the operations in the request are dependent - for example, the output of one operation may be used in the input of the next operation. For example offer created in operationId=0 needs to be used in campaign creation operationId=1.

In order to link two batch operations together specify in the dependent operation the id of the required operation, for instance: "dependsOnOperationId" : 5. Also IDs of created resources via POST requests of batch operations can be used in dependent operations both in "relativeUrl" and "body".

**Permissions & Throttling**
In order to execute batch API actions the underlying user has to have at least "editor" rights (for each individual operation in case additional rights are required than user has then the individual operation will fail). Usual throttling strategies are applied on batch API actions as if every operation has been performed individually.

Batch processing finishes when all operations have been completed, an operation could either be successful (2xx statusCode), failure (4xx, 5xx status code) or skipped because a dependency operation has failed or has been skipped.

### Request Object Parameter


<table>
    <thead>
        <tr>
            <th>Attribute</th>
            <th>Description</th>
            <th>Limits</th>
            <th>Default</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p>body</p>
            </td>
            <td>body for HTTP batch operation. will be ignored for all actions but POST and PUT. can refer to IDs from previous batch actions, for instance: "offerId": "{operationIdResponse:0}", "segmentId": "{operationIdResponse:1}"</td>
            <td>
                <ul>
                    <li>should be a valid JSON</li>
                    <li>in case referencing an operationIdResponse, the operationId response referred should be a valid ID and the method on that action should be POST</li>
                </ul>
            </td>
            <td>empty object {}</td>
        </tr>
        <tr>
            <td>
                <p>dependsOnOperationIds</p>
            </td>
            <td>list of constraint IDs that will assure that current operation will execute only if specified operations have completed successfully. Can be used to achieve chaining of operations.</td>
            <td>
                <ul>
                    <li>maximum 255 operations are allowed</li>
                    <li>unique values are only allowed</li>
                    <li>should point to a valid operationId in the array</li>
                    <li>cyclical dependencies are not allowed</li>
                </ul>
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                <p>headers</p>
            </td>
            <td>array of key-value headers to be sent with particular operation. In case authentication for batch API has been performed via Authorization header, it will be copied for individual operations as well.</td>
            <td>
                <ul>
                    <li>max number of headers in array allowed is 50</li>
                </ul>
            </td>
            <td>Content-Type: application/json</td>
        </tr>
        <tr>
            <td>
                <p>headers-&gt;name</p>
            </td>
            <td>header name</td>
            <td>
                <ul>
                    <li>should be unique among other header names. headers are case insensitive by rfc, otherwise the values will override each other.</li>
                </ul>
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                <p>headers-&gt;value</p>
            </td>
            <td>header value</td>
            <td>
                <ul>
                    <li>-</li>
                </ul>
            </td>
            <td>empty string</td>
        </tr>
        <tr>
            <td>
                <p>method</p>
            </td>
            <td>HTTP method to use. Available options: GET, POST, PUT, PATCH, DELETE</td>
            <td>
                <ul>
                    <li>only GET, POST, PUT, PATCH, DELETE methods are allowed</li>
                </ul>
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                <p>operationId</p>
            </td>
            <td>operation ID used to identify an operation among other operations for responses and referencing results.</td>
            <td>
                <ul>
                    <li>unique among other operations</li>
                    <li>values from 0-255</li>
                </ul>
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                <p>operations</p>
            </td>
            <td>list of operations to perform in a batch. order is not relevant.</td>
            <td>
                <ul>
                    <li>maximum 256 operations are allowed</li>
                </ul>
            </td>
            <td>-</td>
        </tr>
        <tr>
            <td>
                <p>relativeUrl</p>
            </td>
            <td>relative URL for admin rest API, the part after "/admin/rest/". Can contain query string parameters like: "/v2/campaigns?limit=10&amp;offset=10". can refer to URLs with contain IDs from previous batch actions, for instance: "/v1/offers/{operationIdResponse:0}". In case query parameters are sent they have to be URL encoded.</td>
            <td>
                <ul>
                    <li>should start with / (be relative)</li>
                    <li>only new valid JSON APIs are supported</li>
                    <li>in case of invalid relativeURL a 404 response for particular operation will be returned</li>
                    <li>in case referencing an operationIdResponse, the operationId response referred should be a valid ID and the method on that action should be POST</li>
                </ul>
            <td>-</td>
            </td>
        </tr>
    </tbody>
</table>


### Response Object Parameter


<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Description</th>
        </tr>
    </thead><tbody>
        <tr>
            <td>
                <p>operationId</p>
            </td>
            <td>operation ID used to identify an operation among other operations, same ID as it has been sent in POST request.</td>
        </tr>
        <tr>
            <td>
                <p>skipped</p>
            </td>
            <td>boolen flag to mark if operation has been executed or skipped. Will be true in case that current operation depends on a operation which has failed (returned a statusCode value different than 2xx).</td>
        </tr>
        <tr>
            <td>
                <p>statusCode</p>
            </td>
            <td>HTTP status code of operation identified by operationId. In case a different value than 2xx is returned then all depending operations will be skipped (not executed).</td>
        </tr>
        <tr>
            <td>
                <p>headers</p>
            </td>
            <td>array of key-value headers to be sent as a response for particular operation.</td>
        </tr>
        <tr>
            <td>
                <p>headers-&gt;name</p>
            </td>
            <td>header name</td>
        </tr>
        <tr>
            <td>
                <p>headers-&gt;value</p>
            </td>
            <td>header value</td>
        </tr>
        <tr>
            <td>
                <p>body</p>
            </td>
            <td>body for HTTP batch response operation</td>
        </tr>
    </tbody>
</table>



# Recommendations

Recommendations activities automatically display products or content that might interest your customers based on previous user activity or other algorithms. Recommendations help direct customers to relevant items they might otherwise not know about.

Note: Recommendations activities are available as part of the Target Premium solution. They are not available in Target Standard without a Target Premium license.

## Collections

A collection is a set of products or items that are eligible for a recommendation.

Commonly, a collection is a set of similar or related items, such as a single product collection.

### List Collections

> Sample Request for List Collections

````shell

curl -X GET
https://mc.adobe.io/recspm1/target/recs/collections \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for List Collections

````
{
    "offset": 0,
    "limit": 2147483647,
    "total": 21,
    "list": [
        {
            "id": 7257,
            "name": "All Articles"
        },
        {
            "id": 4418,
            "name": "Catalog Y"
        },
        {
            "id": 4044,
            "name": "Empty Collection"
        },
        {
            "id": 5128,
            "name": "Female Products"
        },
        {
            "id": 7491,
            "name": "Generic"
        },
        {
            "id": 7029,
            "name": "Hotels"
        },
        {
            "id": 6765,
            "name": "Macbook"
        },
        {
            "id": 6591,
            "name": "Mens Nike Hats"
        },
        {
            "id": 6605,
            "name": "Mens Nike Hats, Shirts, Shorts"
        },
        {
            "id": 6589,
            "name": "Mens Nike Shirts"
        },
        {
            "id": 6590,
            "name": "Mens Nike Shorts"
        },
        {
            "id": 4316,
            "name": "Product Collection"
        },
        {
            "id": 6892,
            "name": "Retail 4000-4010"
        },
        {
            "id": 5213,
            "name": "Running Shoes"
        },
        {
            "id": 5447,
            "name": "Sample collection name"
        }
    ]
}
````

Get the list of collections available in your account. 

#### GET: /{tenant}/target/recs/collections



### Get Collection by ID

> Sample Request for Get Collection by ID

````shell

curl -X GET
https://mc.adobe.io/recspm1/target/recs/collections/5213 \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````

> Sample Response for Get Collection by ID

````
{
    "id": 5213,
    "name": "Running Shoes",
    "rules": [
        {
            "category": {
                "contains": [
                    "Running Shoes"
                ]
            }
        }
    ]
}
````


Get the collection for a given ID. 

#### GET: /{tenant}/target/recs/collections/{id}


### Create Collection

> Sample Request for Create Collection

````shell
curl -X POST \
  https://mc.adobe.io/recspm1/target/recs/collections/ \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'
  -d '{
 "name":"Smartphones",
 "rules":[
   {"category": {"equals":["smartphone"]}}, 
   {"name": {"contains": ["android", "Android"]}},
   {"value": {"greaterOrEquals": ["600"] }},
   {"message": {"doesNotContain": ["ios"]}}
  ]
}'
````

> Sample Response for Create Collection

````
{
    "id": 8886,
    "name": "Smartphones",
    "rules": [
        {
            "category": {
                "equals": [
                    "smartphone"
                ]
            }
        },
        {
            "name": {
                "contains": [
                    "android",
                    "Android"
                ]
            }
        },
        {
            "value": {
                "greaterOrEquals": [
                    "600"
                ]
            }
        },
        {
            "message": {
                "doesNotContain": [
                    "ios"
                ]
            }
        }
    ]
}
````



### Update Collection

### Delete Collection

## Feeds

### List Feeds

### Get Feed by ID

### Create Feed (HTTP)

### Create Feed (FTP)

### Update Feed (HTTP)

### Update Feed (FTP)

### Delete Feed






