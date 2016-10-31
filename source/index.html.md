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
The website is [MESH](http://www.mesh-scheduler.com). Feel free to sign up and check it out.
if you need to tak to us please email at **canarmony@gmail.com**



# Resources

## User

A User object is created when signup is completed. A user can be an employee of multiple pools.
The API allows for updating user settings and returning employee accounts that belong to the user. 

### The user object

### Create a user

### Retrieve a user

### Update a user

## Employees

An Employee object is created after a User searches for a pool, makes a request to join that pool and is accepted by the pool administrator.
The API returns an individual object given its id as well as other members in the pool. 


### the employee object

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
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

Retrieves an employee with a given ID.
If the ID is invalid or the current user does not have the priviledge to retrieve the employee an error is raised.

### List colleagues 

List of all the employees colleagues given the employees ID.

## Assignments

An Assignment is created when an employee of the pool is assigned to a empty timeslot within the schedule.
The API returns an Assignment give its id as well as a list of assignments for the pool the employee is a member of. 

### the assignment object

Attribute | Type | Description
--------- | ------- | -----------
id | Integer | 
position | String | Employees name
pool_id | Integer | The pool that the assignment belongs to
employee_id | Integer | The employee that the assignment belongs to
start | Timestamp | The starting time of the assignment
end | Timestamp | The ending time of the assignment
allDay | Boolean | If set to true, the assignment is all day.

### retrieve an assignment

Retrieves the details of an assignement that has been created and published for the employee. By 
providing the ID of the assignment, it is returned.

### list all assignments for the employee

Returns the list of assignments provided the pool_id that have been created and published for the employee.


Arguments | Name | Description
--------- | ------- | -----------
start | Timestamp | Assignments after the start date 
end | Timestamp | Assignments before the end date
eid | Integer | the employee id 
not_eid | Boolean | All assignments belonging to employees in the pool that are not the employee is returned
          
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

For the scheduler to take employee requests into consideration, employees need to make requests.

Arguments | Name | Description
--------- | ------- | -----------
start_date | Timestamp | Requests start date 
end_date | Timestamp | Requests end date
request_type | String | Vacation, request-off, request-on, prefer-off, prefer-on


### show a request

Returns a request given its ID

### update a request

Update a requests start_date, end_date and request_type

### delete a request

Delete a request given the ID

### list all requests for the employee

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
  -H "Authorization: meowmeowmeow"
```


> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens


```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten


```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```


> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

