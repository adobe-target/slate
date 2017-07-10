---
title: Target API v1.0
toc_footers: []
includes: []
search: true
highlight_theme: Xcode
---

# Introduction 

Welcome to the Adobe Target API. Adobe Target is a part of the Adobe Experience Cloud that helps you to optimize and personalize your customers' experience.

You can use the Target REST APIs to list, create and modify Target Activities, Audiences and Offers, retreive reports, update profiles etc.

# Before you begin

In all the code examples, you must replace the {tenant} variable with your tenant value. You must replace <ACCESS_TOKEN> with your personal API key.
 
You will need an account on Adobe I/O to get the access token and the API key. See the Authentication section for more information.
 
# Postman Collection

Postman is a application that makes it easy to fire API calls. We have created a Postman collection with all the common API calls. Just click on the 'Run in Postman' button to import the Target API collection.

<aside class="notice">
Don't forget to replace the {{tenant}}, {{access_token}} and {{api_key}} values with your own in the API calls.
</aside>

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/8df29390f5e380f44a7c)

# Response Codes

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


## Get Environments

> Sample Request for Get Environments

````shell

curl -X GET \
  https://mc.adobe.io/adobetargetmobile/target/environments \
  -H 'authorization: Bearer <your-bearer-token>' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/vnd.adobe.target.v1+json' \
  -H 'x-api-key: <your-api-token>'

````
> Sample Response for Get Environments

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



