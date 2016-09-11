# python-sidecarclient version 2

## Install


```shell
python setup.py install
```

## obj = sidecarclient.client.Client(**args)

Function to get the instance of sidecarclient

|SL.NO.| Argument nAME | Required                                     | Default Value | Description                   |
|:-----|:--------------|:---------------------------------------------|:--------------|:------------------------------|
|1     | username      |True, if user_id or auth_token is not given   | None          | Keystone admin username       |
|2     | user_id       |True, if user_name or auth_token is not given | None          | Keystone admin user id        |
|3     | password      |True, if auth_token is not given              | None          | Keystone admin password       |
|4     | tenant_id     |True, if auth_version is 2 and tenant_name is None,  and user credential is provided. | None     | Keystone admin tenant id      |
|5     | tenant_name   |True, if auth_version is 2 and tenant_id   is None,  and user credential is provided. | None     | Keystone admin tenant name    |
|6     | auth_url      |True                                          | None          | Keystone authentication url   |
|7     | auth_version  |Optional                                      | 2             | Keystone auth version, value must be either 2 or 3     |
|8     | project_id    |True, if auth_version is 3 and project_name is None | None    | Keystone admin project id      |
|9     | project_name  |True, if auth_version is 3 and project_id is None   | None    | Keystone admin project name    |
|10    | project_domain_id    |True, if auth_version is 3 and project_domain_name is None | None    | Keystone admin project's domain id      |
|11    | project_domain_name  |True, if auth_version is 3 and project_domain_id is None,    | None    | Keystone admin project's domain name    |
|12    | user_domain_id    |True, if auth_version is 3 and user_domain_name is None,  and user credential is provided. | None    | Keystone admin user's domain id      |
|13    | user_domain_name  |True, if auth_version is 3 and user_domain_id is None, and user credential is provided.   | None    | Keystone admin user's domain name    |
|14    | aith_token    |True, if no user credential is there                         | None    | Keystone admin user's token id      |
|15    | user_domain_name  |True, if auth_version is 3 and user_domain_id is None   | None    | Keystone admin user's domain name    |
|16    | endpoint  |True  | None    | sidecar endpoint. After user got token from keystone, if user has this endpoint, with given endpint_type and region_name    |
|17    | endpoint_type    |Optional | 'publicURL'    | against which ednpoint type we need to check. In version 3, its `internal`, `admin`, `public`, in version 2.0 it is `publicURL`, `adminURL`, `internalURL`|
|18    | region_name     |True      | None  | Against which region, the endpoint should b echecked.    |
|19    | timeout         |Optional  | 300   | Maximum seconds to wait for the result      |
|20    | insecure        |Optional  | False | wheather HTTPS should be verified or not |


## Listing events
> obj.events.list(**arg)

>> Diffrent filtering options are:

|SL.NO.| Argument Name         | Required     | Default Value | Description                                             |
|:-----|:----------------------|:-------------|:--------------|:--------------------------------------------------------|
|1     | id                    | optional     | None          | id of the event to be filtered                          |
|2     | name                  | optional     | None          | name of the event to be filtered                        |
|3     | node_uuid             | optional     | None          | filter the events on the basis of node_uuid             |
|4     | event_create_time     | optional     | None          | filter the events on the basis of event_create_time in (yyyy-mm-dd HH:ii:ss format)    |
|5     | min_event_create_time | optional     | None          | filter the events on the basis of min event_create_time in (yyyy-mm-dd HH:ii:ss format)     |
|6     | max_event_create_time | optional     | None          | filter the events on the basis of max event_create_time in (yyyy-mm-dd HH:ii:ss format)     |
|7     | marker                | optional     | None          | last event id                                           |
|8     | limit                 | optional     | None          | maximum number of events to be displayed                |

> It outputs a resultGenerator object.
> len(ticket_list) = Number of results fetched
> On looping the ResultGenerator object, it provides an event object. The Event object has following properties.

|SL.NO.| Argument Name         | Data Type     | Default Value | Description                                            |
|:-----|:----------------------|:-------------|:--------------|:--------------------------------------------------------|
|1     | id                    | string       | None          | id of the event                                         |
|2     | name                  | string       | None          | name of the event                                       |
|3     | node_uuid             | string       | None          | HOST id on which the event is occuring                  |
|4     | event_create_time     | string (yyyy-mm-dd HH:ii::ss format) | None |  event create time                       |
|5     | event_complete_time   | string (yyyy-mm-dd HH:ii::ss format) | None |  event complete time                     |
|6     | event_status          | string ('created', 'running', 'completed') | None |  event status                      |
|7     | vm_uuid_list          | list conating, instance ids  | empty list  |  the instances, which took part in the evacuation   |
|8     | extra                 | json                         | None |  any meta data                                  |


## Creating a new event
> obj.events.create(**arg)

>> Diffrent parameters required:

|SL.NO.| Argument Name         | Data Type    | Default Value | Description                                            |
|:-----|:----------------------|:-------------|:--------------|:--------------------------------------------------------| 
|1     | name                  | string       | None          | name of the event                                       |
|2     | node_uuid             | string       | None          | HOST id on which the event is occuring                  | 
|3     | vm_uuid_list (optional) | list conating, instance ids  | empty list  |  the instances, which took part in the evacuation   | 

It returns an *Event* object of newly created event.

## Getting detail of an event
> obj.events.detail(id)

For getting detail of an event only event id need to be passed.

It returns an *Event* Object.

## Editing an event
> obj.events.detail(id, **args)

Diffrent arguments:

|SL.NO.| Argument Name         | Data Type     | Required     | Description                                            |
|:-----|:----------------------|:-------------|:--------------|:--------------------------------------------------------|
|1     | id                    | string       | True          | id of the event  to be edited                           |
|2     | name                  | string       | optional      | name of the event                                       |
|3     | node_uuid             | string       | optional      | HOST id on which the event is occuring                  | 
|4     | event_status          | string ('created', 'running', 'completed') | optional |  event status                  |
|5     | vm_uuid_list          | list conating, instance ids  | optional  |  the instances, which took part in the evacuation   |



>> Diffrent parameters required:

|SL.NO.| Argument Name         | Data Type    | Default Value | Description                                            |
|:-----|:----------------------|:-------------|:--------------|:--------------------------------------------------------| 
|1     | name                  | string       | None          | name of the event                                       |
|2     | node_uuid             | string       | None          | HOST id on which the event is occuring                  | 
|3     | vm_uuid_list (optional) | list conating, instance ids  | empty list  |  the instances, which took part in the evacuation   | 

It returns an *Event* object of newly created event.
