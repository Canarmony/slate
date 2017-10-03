---
title: MESH API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

> API endpoint

```shell
http://api.mesh-scheduler.com
```


The MESH API is organized around REST. JSON is returned by all API responses, including errors.
The website is [MESHAI](http://www.meshai.io). Feel free to sign up and check it out.
if you need to tak to us please email at **canarmony@gmail.com**



# Resources

## User

A User object is created when signup is completed. A user can be an employee of multiple pools.
The API allows for updating user settings and returning employee accounts that belong to the user. 

### The user object


### Create a user
```shell
curl POST "http://mesh-scheduler.com/api/users"

```


For the scheduler to take employee requests into consideration, employees need to make requests.

Arguments | Name | Description
--------- | ------- | -----------
fname | String | First name 
lname | String | Last name
email | String |
password | String |
password_confirmation | String | 
disclaimer | boolean | In order to create a user you must accept the disclaimer


### Update a user
```shell
curl POST "http://mesh-scheduler.com/api/users/1"

```


For the scheduler to take employee requests into consideration, employees need to make requests.

Arguments | Name | Description
--------- | ------- | -----------
fname | String | First name 
lname | String | Last name
email | String |
is_searchable_by_name | boolean |
is_searchable_by_email | boolean | 
get_email_news | boolean | 
get_email_notifications | boolean |

### Memberships

```shell
curl "http://mesh-scheduler.com/api/users/1/memberships.json -u 'admin:secret'"

```


> The above command returns JSON structured like this:

```json

[
    {
        "user_id":1,
        "id":6,
        "name":"Hassan Nouri",
        "activated":true,
        "created_at":"2016-09-02T17:46:40.023Z",
        "updated_at":"2016-09-02T17:47:05.045Z",
        "pool_id":7,
        "in_schedule":true,
        "invite_digest":null,
        "invited_user_id":null,
        "show_email":true,
        "weight_modifier":1.0
    },
    {
        "user_id":1,
        "id":7,
        "name":"Mohawk Nouri",
        "activated":true,
        "created_at":"2016-09-04T21:49:31.367Z",
        "updated_at":"2016-09-04T21:49:31.400Z",
        "pool_id":8,
        "in_schedule":true,
        "invite_digest":null,
        "invited_user_id":null,
        "show_email":true,
        "weight_modifier":1.0
    }
]
```
Returns a list of employee objects that represents the list of pools that the employee is a member of.

### Assignments
```shell
curl "http://mesh-scheduler.com/api/users/1/assignments.json?start=start_date&end=end_date"

```


> The above command returns JSON structured like this:

```json

[
  {
    "pool_id":8,
    "id":26,
    "employee_alt_name":"Mohawk Nouri",
    "position":"r2",
    "solution_id":0,
    "employee_id":7,
    "published":true,
    "start":"2016-10-28T00:00:00.000Z",
    "end":"2016-10-29T00:00:00.000Z",
    "allDay":true,
    "weight_modifier":1.0,
    "color":null,
    "approved":true,
    "actualstart":null,
    "actualend":null
  },
  {
    "pool_id":9,
    "id":25,
    "employee_alt_name":"Mohawk Nouri",
    "position":"r2",
    "created_at":"2016-10-26T17:13:44.757Z",
    "updated_at":"2016-10-26T17:25:30.029Z",
    "solution_id":0,
    "employee_id":11,
    "published":true,
    "start":"2016-10-28T00:00:00.000Z",
    "end":"2016-10-29T00:00:00.000Z",
    "allDay":true,
    "weight_modifier":1.0,
    "color":null,
    "approved":true,
    "actualstart":null,
    "actualend":null
  }
]
```


Returns the list of assignments that have been created and published for the current user.


Arguments | Name | Description
--------- | ------- | -----------
start | Timestamp | Assignments after the start date 
end | Timestamp | Assignments before the end date


## Pools

A Pool is created when a user requests to create a pool.
The API returns an Assignment given its id as well as a list of assignments for the pool the employee is a member of. 

### the pool object

Attribute | Type | Description
--------- | ------- | -----------
id | Integer | 
name | String | Pool name
activated | Boolean | 

### retrieve an pool
```shell
curl "http://mesh-scheduler.com/api/pools/25.json -u 'admin:secret'"

```


> The above command returns JSON structured like this:

```json

[
  {
    "id":25,
    "name":"Demo_Pool",
    "activated":"true"
  }
]
```
Retrieves the details of an assignement that has been created and published for the employee. By 
providing the ID of the assignment, it is returned.

### list all pools for the user
```shell
curl "http://mesh-scheduler.com/api/pools.json"

```


> The above command returns JSON structured like this:

```json

[
  {
      "id":25,
      "name":"Demo_Pool",
      "activated":"true"
    },
  {
      "id":26,
      "name":"Another_Pool",
      "activated":"true"
    }
]
```




## Employee
An Employee object is created after a User searches for a pool, makes a request to join that pool and is accepted by the pool administrator.
The API returns an individual object given its id as well as other members in the pool. 


### the employee object

```json
[
  {
          "user_id":1,
          "id":7,
          "name":"Mohawk Nouri",
          "activated":true,
          "created_at":"2016-09-04T21:49:31.367Z",
          "updated_at":"2016-09-04T21:49:31.400Z",
          "pool_id":8,
          "in_schedule":true,
          "invite_digest":null,
          "invited_user_id":null,
          "show_email":true,
          "weight_modifier":1.0
  }
]
```

Attribute | Type | Description
--------- | ------- | -----------
id | Integer | Employee object id
name | String | Employees name
activated | Boolean: default false | If set to true, the employee has been activated by the pool administrator
user_id | Integer | The user account that the employee belongs to
pool_id | Integer | The pool that the employee is a member of
in_schedule | Boolean: default false | If set to true, the employee is being scheduled


### Retrieve employee
```shell
curl "http://mesh-scheduler.com/api/employees/7  -u 'admin:secret'"

```


> The above command returns JSON structured like this:

```json
{
        "user_id":1,
        "id":7,
        "name":"Mohawk Nouri",
        "activated":true,
        "created_at":"2016-09-04T21:49:31.367Z",
        "updated_at":"2016-09-04T21:49:31.400Z",
        "pool_id":8,
        "in_schedule":true,
        "invite_digest":null,
        "invited_user_id":null,
        "show_email":true,
        "weight_modifier":1.0
    }
```

Retrieves an employee with a given ID.
If the ID is invalid or the current user does not have the priviledge to retrieve the employee an error is raised.



### List colleagues 
```shell
curl "http://mesh-scheduler.com/api/employees/8/coworkers.json -u 'admin:secret'"

```


> The above command returns JSON structured like this:

```json

[
  {
    "id": 11,
    "name": "Mowhawk Nouri",
    "activated": "true",
    "user_id": nil,
    "pool_id": 8,
    "in_schedule": true
    ...
  },
  {
    "id": 13,
    "name": "Mowhawk Nouri",
    "activated": "true",
    "user_id": 1,
    "pool_id": 8,
    "in_schedule": true
    ...
  }
]
```
List of all the employees colleagues given the employees ID.

## Assignments


An Assignment is created when an employee of the pool is assigned to a empty timeslot within the schedule.
The API returns an Assignment give its id as well as a list of assignments for the pool the employee is a member of. 

### the assignment object

Attribute | Type | Description
--------- | ------- | -----------
id | Integer | 
position | String | The role of the assignment
pool_id | Integer | The pool that the assignment belongs to
employee_id | Integer | The employee that the assignment belongs to
employee_name | String | The name of the employee that the assignment belongs to
start | Timestamp | The starting time of the assignment
end | Timestamp | The ending time of the assignment
allDay | Boolean | If set to true, the assignment is all day (should not show time info).
color | String | If set, the assignment should be shown with this particular custom color.

### retrieve an assignment
```shell
curl "http://mesh-scheduler.com/api/assignments/25.json -u 'admin:secret'"
```

> The above command returns JSON structured like this:

```json
[
  {
    "pool_id":8,
    "id":25,
    "employee_alt_name":"Fahim",
    "position":"r2",
    "created_at":"2016-10-26T17:13:44.757Z",
    "updated_at":"2016-10-26T17:25:30.029Z",
    "solution_id":0,
    "employee_id":11,
    "published":true,
    "start":"2016-10-28T00:00:00.000Z",
    "end":"2016-10-29T00:00:00.000Z",
    "allDay":true,
    "weight_modifier":1.0,
    "color":null,
    "approved":true,
    "actualstart":null,
    "actualend":null,
    "employee_name":"Fahim"
  }
]
```

Using a get request with an ID retrieves the details of the assignment with that ID.




### list assignments
```shell
curl "http://mesh-scheduler.com/api/assignments.json?pool_id=8&start=start_date&end=end_date&empid=employee_id&not_eid=true -u 'admin:secret'"
```


> The above command returns JSON structured like this:

```json
[
  {
    "pool_id":8,
    "id":26,
    "employee_alt_name":"Mohawk Nouri",
    "position":"r2",
    "solution_id":0,
    "employee_id":7,
    "published":true,
    "start":"2016-10-28T00:00:00.000Z",
    "end":"2016-10-29T00:00:00.000Z",
    "allDay":true,
    "weight_modifier":1.0,
    "color":null,
    "approved":true,
    "actualstart":null,
    "actualend":null,
    "employee_name":"Mohawk Nouri"
  },
  {
    "pool_id":8,
    "id":25,
    "employee_alt_name":"Fahim",
    "position":"r2",
    "created_at":"2016-10-26T17:13:44.757Z",
    "updated_at":"2016-10-26T17:25:30.029Z",
    "solution_id":0,
    "employee_id":11,
    "published":true,
    "start":"2016-10-28T00:00:00.000Z",
    "end":"2016-10-29T00:00:00.000Z",
    "allDay":true,
    "weight_modifier":1.0,
    "color":null,
    "approved":true,
    "actualstart":null,
    "actualend":null,
    "employee_name":"Fahim"
  }
]
```
A GET request on the assignments resource will return a list of assignments. Without any parameters, this will default
to returning all the assignments associated with the user (from all pools). If an employee_id, not_employee_id, or
pool_id are included, the list will default to all assignments associated with a pool.


Arguments | Name | Description
--------- | ------- | -----------
pool_id | Integer | Include only assignments from the associated pool
start | Timestamp | Include only assignments whose 'end' timestamp is after this value
end | Timestamp | Include only assignments whose 'start' timestamp is before this value
employee_id | Integer | Include only assignments associated with this employee id
not_employee_id | Integer | Exclude assignments with this employee id


## Requests

A request is made by the employee asking for a vacation, day off, day on, prefer on or prefer off. The API allows for showing 
a single request given the id, showing the list of requests an employee has made, creating, updating and deleting a request. 

### the request object

Attribute | Type | Description
--------- | ------- | -----------
id | Integer | Request object id
start_date | Timestamp | Requests start date 
end_date | Timestamp | Requests end date
request_type | String | vacation, request-off, request-on, prefer-off, prefer-on
employee_id | Integer | The employees id
pool_id | Integer | The pool that the employee is a member of
approved | Boolean | If true, the request will be considered for schedule creation


### create a request
```shell
curl POST "http://mesh-scheduler.com/api/requests?employee_id=8&start_date=date&end_date=end&request_type=type -u 'admin:secret'"

```


For the scheduler to take employee requests into consideration, employees need to make requests.

Arguments | Name | Description
--------- | ------- | -----------
start_date | Timestamp | Requests start date 
end_date | Timestamp | Requests end date
request_type | String | Vacation, request-off, request-on, prefer-off, prefer-on


### show a request
```shell
curl "http://mesh-scheduler.com/api/requests/9.json -u 'admin:secret'"

```


> The above command returns JSON structured like this:

```json

{
    "id":9,
    "employee_id":6,
    "start_date":"2016-09-13",
    "end_date":"2016-09-16",
    "request_type":"vacation",
    "pool_id":7,
    "created_at":"2016-09-04T21:06:01.855Z",
    "updated_at":"2016-09-04T21:06:01.855Z",
    "approved":0
}
```


Returns a request given its ID

### update a request
```shell
curl POST "http://mesh-scheduler.com/api/requests/9.json -u 'admin:secret'"

```
Update a requests start_date, end_date and request_type

### delete a request
```shell
curl DELETE "http://mesh-scheduler.com/api/requests/9.json -u 'admin:secret'"

```
Delete a request given the ID

### list all requests for the employee
```shell
curl "http://mesh-scheduler.com/api/requests.json?employee_id=8&start=start_date&end=end_date&approved=true -u 'admin:secret'"

```


> The above command returns JSON structured like this:

```json

[
    {
        "employee_id":7,
        "id":17,
        "start_date":"2016-10-28",
        "end_date":"2016-10-30",
        "request_type":"vacation",
        "pool_id":8,
        "created_at":"2016-10-26T17:01:40.211Z",
        "updated_at":"2016-10-26T17:01:40.230Z",
        "approved":1
    },
    {
        "employee_id":7,
        "id":19,
        "start_date":"2016-11-15",
        "end_date":"2016-11-18",
        "request_type":"vacation",
        "pool_id":8,
        "created_at":"2016-11-01T17:51:54.279Z",
        "updated_at":"2016-11-01T17:51:54.301Z",
        "approved":1
    }
]
```

Returns the list of requests of the employee provided the employee_id

Arguments | Name | Description
--------- | ------- | -----------
start | Timestamp | Requests after the start date 
end | Timestamp | Requests before the end date
approved | Boolean | If true, the requests that were approved will be shown

## Swaps

A swap is initited when an employee offers an assignment to other members of the pool or requests to take another members assignment.
The API allows to create a swap, list all swaps relevant to the employee, delete and update a swap

## Conversations

Conversations allow for communication between members of a pool. The API allows to create, show and reply to a conversation

## Notifications







# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: auth_token that is saved in the user object"
```


