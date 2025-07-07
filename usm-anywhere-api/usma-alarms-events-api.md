# USM Anywhere APIs

This document describes the Alarms and Events APIs, which allow you to query and filter alarms and events data within the USM Anywhere platform.

## Alarms
- [Get alarms](#get-alarms)
- [Get alarm details](#get-alarm-details)
### Get alarms
`GET /alarms` \
Get a page of alarms.

#### Parameters
| Parameter                | Type    | Required | Description                                                                 | Example                                |
| ------------------------ | ------- | -------- | --------------------------------------------------------------------------- | -------------------------------------- |
| `page`                   | integer | No       | The number of results to return (zero-based).                               | `2`                                    |
| `size`                   | integer | No       | The number of results to return for each page.                              | `10`                                   |
| `sort`                   | string  | No       | The field and direction (ascending or descending) used to sort the results. | `timestamp_occurred, desc`             |
| `status`                 | string  | No       | The status of the alarm.                                                    | `open`                                 |
| `suppressed`             | boolean | No       | Filters alarms by the `suppressed` flag.                                    | `false`                                |
| `rule_intent`            | string  | No       | The intent of the rule that triggered the alarm.                            | `Environmental Awareness`              |
| `rule_method`            | string  | No       | The method of the rule that triggered the alarm.                            | `AWS EC2 Security Group Modified`      |
| `rule_strategy`          | string  | No       | The method of the rule that triggered the alarm.                            | `Network Access Control Modification`  |
| `priority_label`         | array   | No       | Filters alarms by one or more priority labels.                              | `medium, high`                         |
| `alarm_sensor_sources`   | string  | No       | The uuid of the sensor.                                                     | `085dff4e-8256-40ca-8ed8-cfd3bd56f505` |
| `timestamp_occurred_gte` | string  | No       | Returns alarms that occurred on or after the specified timestamp.           | `1737990884154`                        |
| `timestamp_occurred_lte` | string  | No       | Returns alarms that occurred on or before the specified timestamp.          | `1748358884320`                        |

#### Response Codes
* **200 OK**: The request succeeded and a list of alarms is returned.
* **400 Bad Request**: The request was malformed or included invalid query parameters.
* **401 Unauthorized**: Authentication failed. The bearer token is missing or invalid.
* **500 Internal Server Error**: Something went wrong on the server.

#### Example
##### Request
```
curl -X GET "https://your-subdomain.alienvault.cloud/api/2.0/alarms?page=1&size=50&sort=timestamp_occurred,asc&status=open&suppressed=true&rule_intent=Environmental Awareness&rule_method=AWS EC2 Security Group Modified&rule_strategy=Network Access Control Modification&priority_label=medium&alarm_sensor_sources=308ba880-2518-44bb-9ada-07b158d11713&timestamp_occurred_gte=1517933139670&timestamp_occurred_lte=1517933149670" \
	-H "Authorization: Bearer string"
```
##### Response Body
```
{
    "_links": {
      "first": {
        "href": "https://mysubdomain.alienvault.cloud/api/2.0/alarms?page=0&size=20&sort=timestamp_occurred,desc",
        "templated": false
      },
      "self": {
        "href": "https://mysubdomain.alienvault.cloud/api/2.0/alarms",
        "templated": false
      },
      "next": {
        "href": "https://mysubdomain.alienvault.cloud/api/2.0/alarms?page=1&size=20&sort=timestamp_occurred,desc",
        "templated": false
      },
      "last": {
        "href": "https://mysubdomain.alienvault.cloud/api/2.0/alarms?page=175&size=20&sort=timestamp_occurred,desc",
        "templated": false
      }
    },
    "_embedded": {
      "alarms": [
        {
            "id": "971918fd-a569-548a-5a80-1ffcda2a8365",
            "suppressed": false,
            "status": "open",
            "priority_label": "medium",
            "timestamp_occurred": "1748359996332",
            "...": "..."
        },
        {
            "id": "fb01cd15-4a9d-4c3b-9f20-b6489e5f5ecb",
            "suppressed": false,
            "status": "open",
            "priority_label": "high",
            "timestamp_occurred": "1738632982727",
            "...": "..."
        },
        "..."
      ]
    },
    "page": {
      "size": 20,
      "totalElements": 3506,
      "totalPages": 176,
      "number": 0
    }
}
```

### Get alarm details
`GET /alarms/{alarm_id}` \
Get the details of an alarm.

#### Parameters
| Parameter  | Type   | Required | Description          | Example                                |
| ---------- | ------ | -------- | -------------------- | -------------------------------------- |
| `alarm_id` | string | Yes      | The ID of the alarm. | `1036671a-764d-485c-a100-ec8ab695e9c8` |

#### Response Codes
* **200 OK**: The request succeeded and an alarm is returned.
* **400 Bad Request**: The request was malformed or included invalid query parameters.
* **401 Unauthorized**: Authentication failed. The bearer token is missing or invalid.
* **404 Not Found**: The alarm was not found.
* **500 Internal Server Error**: Something went wrong on the server.

#### Example
##### Request
```
curl -X GET "https://your-subdomain.alienvault.cloud/api/2.0/alarms/1036671a-764d-485c-a100-ec8ab695e9c8" \
	-H "Authorization: Bearer string"
```
##### Response Body
```
{
  "uuid": "1036671a-764d-485c-a100-ec8ab695e9c8",
  "has_alarm": false,
  "needs_enrichment": true,
  "priority": 20,
  "suppressed": false,
  "events": [
    { "uuid" : "..." }
  ],
  "rule_intent": "Environmental Awareness",
  "app_type": "amazon-aws",
  "source_username": "user@alienvault.com",
  "security_group_id": "sg-xxxxx",
  "destination_name": "ec2.amazonaws.com",
  "timestamp_occured": "1517932134000",
  "authentication_type": "IAMUser",
  "event_type": "Alarm",
  "rule_method": "AWS EC2 Security Group Modified",
  "priority_label": "low",
  "app_id": "amazon-aws",
  "source_name": "x.xx.xx.xxxx",
  "timestamp_received": "1517933139670",
  "rule_strategy": "Network Access Control Modification",
  "request_user_agent": "signin.amazonaws.com",
  "rule_id": "AWSEC2SecurityGroupMod",
  "sensor_uuid": "433152d2-10ee-4645-8c04-9f8269a447e7",
  "transient": false,
  "event_name": "Add inbound network traffic rule to security group",
  "packet_type": "alarm",
  "status": "open",
  "_links": {
    "self": {
      "href": "https://mysubdomain.aveng.us/api/2.0/alarms/971918fd-a569-548a-5a80-1ffcda2a8365",
      "templated": false
    }
  }
}
```


## Events
- [Get events](#get-events)
- [Get event details](#get-event-details)
### Get events
`GET /events` \
Get a page of events.

#### Parameters
| Parameter                | Type    | Required | Description                                                                 | Example                                |
| ------------------------ | ------- | -------- | --------------------------------------------------------------------------- | -------------------------------------- |
| `page`                   | integer | No       | The number of results to return (zero-based).                               | `2`                                    |
| `size`                   | integer | No       | The number of results to return for each page.                              | `10`                                   |
| `sort`                   | string  | No       | The field and direction (ascending or descending) used to sort the results. | `timestamp_occurred, desc`             |
| `account_name`           | string  | No       | The account name associated with the event.                                 | `my_account`                           |
| `plugin`                 | string  | No       | The name of the plugin associated with the event.                           | `windows_security`                     |
| `event_name`             | string  | No       | The name of the event.                                                      | `User Login Failure`                   |
| `source_name`            | string  | No       | The source name associated with the event.                                  | `Windows Security Log`                 |
| `source_username`        | string  | No       | The username of the user that triggered the event.                          | `my_user`                              |
| `suppressed`             | boolean | No       | Filters events by the `suppressed` flag.                                    | `false`                                |
| `sensor_uuid`            | string  | No       | The uuid of the sensor.                                                     | `085dff4e-8256-40ca-8ed8-cfd3bd56f505` |
| `timestamp_occurred_gte` | string  | No       | Returns events that occurred on or after the specified timestamp.           | `1737990884154`                        |
| `timestamp_occurred_lte` | string  | No       | Returns events that occurred on or before the specified timestamp.          | `1748358884320`                        |

#### Response Codes
* **200 OK**: The request succeeded and a list of events is returned.
* **400 Bad Request**: The request was malformed or included invalid query parameters.
* **401 Unauthorized**: Authentication failed. The bearer token is missing or invalid.
* **500 Internal Server Error**: Something went wrong on the server.

#### Example
##### Request
```
curl -X GET "https://your-subdomain.alienvault.cloud/api/2.0/events?page=1&size=50&sort=timestamp_occured,asc&account_name=account&suppressed=true&plugin=plugin&event_name=name&source_name=name&sensor_uuid=308ba880-2518-44bb-9ada-07b158d11713&source_username=user@email.com&timestamp_occured_gte=1517933139670&timestamp_occured_lte=1517933149670" \
	-H "Authorization: Bearer string"
```
##### Response Body
```
{
  "_links": {
    "first": {
      "href": "https://mysubdomain.alienvault.cloud/api/2.0/events?page=0&size=20&sort=timestamp_occured,desc",
      "templated": false
    },
    "self": {
      "href": "https://mysubdomain.alienvault.cloud/api/2.0/events",
      "templated": false
    },
    "next": {
      "href": "https://mysubdomain.alienvault.cloud/api/2.0/events?page=1&size=20&sort=timestamp_occured,desc",
      "templated": false
    },
    "last": {
      "href": "https://mysubdomain.alienvault.cloud/api/2.0/events?page=175&size=20&sort=timestamp_occured,desc",
      "templated": false
    }
  },
  "_embedded": {
    "events": [
      {
          "id": "971918fd-a569-548a-5a80-1ffcda2a8365",
          "event_name": "User Login Failure",
          "suppressed": false,
          "timestamp_occurred": "1748359996332",
          "...": "..."
      },
      {
          "id": "fb01cd15-4a9d-4c3b-9f20-b6489e5f5ecb",
          "event_name": "Port Scan Detected",
          "suppressed": false,
          "timestamp_occurred": "1738632982727",
          "...": "..."
      },
      "..."
    ]
  },
  "page": {
    "size": 20,
    "totalElements": 3506,
    "totalPages": 176,
    "number": 0
  }
}
```

### Get event details
`GET /event/{event_id}` \
Get the details of an event

#### Parameters
| Parameter  | Type   | Required | Description          | Example                                |
| ---------- | ------ | -------- | -------------------- | -------------------------------------- |
| `event_id` | string | Yes      | The ID of the event. | `1036671a-764d-485c-a100-ec8ab695e9c8` |

#### Response Codes
* **200 OK**: The request succeeded and an event is returned.
* **400 Bad Request**: The request was malformed or included invalid query parameters.
* **401 Unauthorized**: Authentication failed. The bearer token is missing or invalid.
* **404 Not Found**: The event was not found.
* **500 Internal Server Error**: Something went wrong on the server.

#### Example
##### Request
```
curl -X GET "https://your-subdomain.alienvault.cloud/api/2.0/events/{eventId}" \
	-H "Authorization: Bearer string"
```
##### Response Body
```
{
  "id": "39a6918f-33f2-ec9b-0fcc-42bb90f10a1f",
  "account_name": "generic-account",
  "plugin_device_type": "Cloud Infrastructure",
  "destination_canonical": "s3.amazonaws.com",
  "destination_name": "s3.amazonaws.com",
  "has_alarm": false,
  "request_user_agent": "s3.amazonaws.com",
  "packet_type": "log",
  "source_canonical": "s3.amazonaws.com",
  "event_name": "PutObject",
  "timestamp_occured": "1528817037000",
  "source_service_name": "s3.amazonaws.com",
  "event_type": "AwsApiCall",
  "app_name": "amazon-aws",
  "timestamp_received": "1528817107938",
  "destination_hostname": "s3.amazonaws.com",
  "source_infrastructure_name": "Amazon Global",
  "plugin": "Amazon AWS CloudTrail",
  "app_type": "amazon-aws",
  "authentication_type": "AWSService",
  "access_control_outcome": "Allow",
  "suppressed": "false",
  "plugin_device": "CloudTrail",
  "destination_infrastructure_type": "Cloud Service",
  "source_infrastructure_type": "Cloud Service",
  "destination_zone": "us-east-1",
  "needs_enrichment": true,
  "source_hostname": "s3.amazonaws.com",
  "app_id": "amazon-aws",
  "plugin_family": "Amazon",
  "plugin_version": "0.24",
  "destination_userid": "101720206348",
  "event_action": "Create",
  "destination_infrastructure_name": "Amazon Global",
  "source_name": "s3.amazonaws.com",
  "received_from": "s3.amazonaws.com",
  "event_description": "Action for uploading an object (PUT or POST).",
  "_links": {
    "self": {
      "href": "https://mysubdomain.aveng.us/api/2.0/events/39a6918f-33f2-ec9b-0fcc-42bb90f10a1f",
      "templated": false
    }
  }
}
```