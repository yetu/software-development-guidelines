# REST API design guidelines

This document covers the best practices on designing a RESTful API (with the exception for *versioning*).


## General ideas behind REST endpoints

1. A URL (Uniform Resource Locator) identifies a single resource.
1. A URL represents a *hierarchical relationship* between resource's data.
1. REST is based on HTTP heavily, using all it's features (verbs, status codes)
1. In general, you should not go deep in resource description. `/resource/identifier/related_resource` is enough in general
1. Default format should be JSON. It may be overriden, though.
1. Ideally, the API server should be stateless (and then your endpoints are *RESTful*)

## Practices

1. Use HTTP-verbs to denote actions:

`GET` - read/retrieve a resource
`POST` - create a new resource
`PUT` - update an existing resource
`DELETE` - delete an existing resource


| HTTP METHOD | GET | POST | PUT | DELETE |
| ----------- | --- | ---- | --- | ------ |
| /orders     | show all orders | create new order | **bulk update** | delete all orders |
| /orders/123 | show order 123 | BAD REQUEST | if exist - update order, if not - BAD REQUEST | delete order 123|



Good:
```
DELETE /cars/1234
```

Bad:
```
POST /cars/1234/delete
```


1. Use nouns, not verbs

Good:
```
/cars/711
```

Bad:
```
/getCars?id=711
```


1. Use **plural** nouns (and do not mix with singular)

Good:
```
/users/1234
/users/1234/cars
```

Bad:
```
/user/1234
/users/1234/car
```



1. GET method should be idempotent (should not change state)

Good:
```
GET /orders/1234
POST /orders/1234/activate
```

Bad:
```
GET /orders/1234?activate=1
GET /orders/1234/activate
```



1. Make a version **mandatory**. **NEVER** release unversioned api for public usage. Avoid dot-notation:

GOOD:
```
/api/v1/communities
```

BAD:
```
/api/communities
/api/v21.01.2014/communities
```



1. Use HTTP status codes for errors:

| Code | Status | Meaning | 
| ---- | ------ | ------- |
| 200  | OK | Everything is working as intended |
| 201  | OK | New resource have been created | 
| 204  | OK | Resource was successfully deleted |
| 400  | BAD REQUEST | The request was invalid or cannot be served. The exact error should be explained in the error payload. E.g. „The JSON is not valid“ |
| 401  | UNAUTHORIZED | The request requires an user authentication |
| 403  | FORBIDDEN | The server understood the request, but is refusing it or the access is not allowed. |
| 404  | NOT FOUND | There is no resource under the specified URL |
| 422  | UNPROCESSABLE ENTITY | Should be used if the server cannot process the payload, e.g. if required fields are missing |
| 500  | INTERNAL SERVER ERROR | **Avoid using this code directly**. Should be used when server has encountered a crash condition. **Note**: the stracktrace should be logged and not returned as response. |




1. Use JSON-wrapper for any kind of return messages:

Good:
```
{
  "success" : {
    "data" : { // payload },
    "message" : ""
  }
}

{
  "errors" : [
    {
      "developerMessage" : "Request payload cannot be parsed",
      "userMessage" : "The data you have provided cannot be parsed",
      "more_info": "http://devdocs.myhost.com/payload"
    }]
}
```



1. Use parameters for filtering/sorting/limiting. Delimit the *multivalue* parameters with comma. 

Good:
```
/orders/1234?sort=+customer,-price
/orders/1234?fields=customer,price,vat
/orders?limit=25&offset=50
```

Bad:
```
/orders/1234/sorted/asc
/orders/limit/25/offset/50
```


1. Use subresources to denote relations. Do not make deep nesting:

Good:
```
/users/1234/orders
/orders/321
```

Bad:
```
/users/1234/orders/321
```





1. It is a good idea to have different formats for endpoint responses:
  1. JSON `/orders`
  2. XML `/orders.xml`
  3. JSONP `/orders?callback=jsonp_callback`


## Kudos

This guidelines is based on these resources:

1. https://github.com/WhiteHouse/api-standards
1. http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api
1. http://blog.mwaysolutions.com/2014/06/05/10-best-practices-for-better-restful-api/
1. http://www.slideshare.net/mario_cardinal/best-practices-for-designing-pragmatic-restful-api