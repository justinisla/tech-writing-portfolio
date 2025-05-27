## Get alarms

`GET /alarms` \
Get a page of alarms.

### Query Parameters

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

### Example
#### Request
```
curl -X GET "https://your-subdomain.alienvault.cloud/api/2.0/alarms?page=1&size=50&sort=timestamp_occurred,asc&status=open&suppressed=true&rule_intent=Environmental Awareness&rule_method=AWS EC2 Security Group Modified&rule_strategy=Network Access Control Modification&priority_label=medium&alarm_sensor_sources=308ba880-2518-44bb-9ada-07b158d11713&timestamp_occurred_gte=1517933139670&timestamp_occurred_lte=1517933149670" \
	-H "Authorization: Bearer string"
```
#### Response Body
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
        "...",
        {
            "id": "b6df9d3b-7bcc-4360-bef1-e3049ab52619",
            "suppressed": false,
            "status": "open",
            "priority_label": "medium",
            "timestamp_occurred": "1735983981756",
            "...": "..."
        }
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