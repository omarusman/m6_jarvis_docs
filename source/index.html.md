---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript
  - php
  - java
  - swift

toc_footers:
  - <a href='https://mesasix.com' target='_blank'>To learn more about Jarvis</a>
  - <a href='https://mesasix.com' target='_blank'>Service Provided by Mesasix</a>

includes:
  - users
  - errors

search: true
---

# Introduction

Welcome to Jarvis Analytics API/GraphQL documentation. Here you can find useful API endpoints for this product/service.

Jarvis Analytics is designed from the ground up, a HIPAA compliant, web based solution, that can seamlessly interface to leading Practice Management Software/EHR and supercharge your practice performance.

Accessible, anytime, anywhere and on any device.

# GraphQL

The API is based on GraphQL pattern. 

GraphQL is an open-source data query and manipulation language for APIs, and a runtime for fulfilling queries with existing data. GraphQL is a query language for your API, and a server-side runtime for executing queries by using a type system you define for your data. 

To learn more, see [GraphQL](http://graphql.org/learn/)

# Authentication

> To authorize, use this code:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'authorization: Bearer {access_token}' \
  --header 'content-type: application/json' \
  --data '{"query":""}'
```

```javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:8000/graphql",
  "method": "POST",
  "headers": {
    "content-type": "application/json",
    "authorization": "Bearer {access_token}"
  },
  "data": "{\"query\":\"\"}"
}

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

```php
<?php

$client = new http\Client;
$request = new http\Client\Request;

$body = new http\Message\Body;
$body->append('{"query":""}');

$request->setRequestUrl('http://localhost:8000/graphql');
$request->setRequestMethod('POST');
$request->setBody($body);

$request->setHeaders(array(
  'content-type' => 'application/json',
  'authorization' => 'Bearer {access_token}'
));

$client->enqueue($request)->send();
$response = $client->getResponse();

echo $response->getBody();
```

```java
HttpResponse<String> response = Unirest.post("http://localhost:8000/graphql")
  .header("content-type", "application/json")
  .header("authorization", "Bearer {access_token}")
  .body("{\"query\":\"\"}")
  .asString();
```

```swift
import Foundation

let headers = [
  "content-type": "application/json",
  "authorization": "Bearer {access_token}"
]

let postData = NSData(data: "{"query":""}".data(using: String.Encoding.utf8)!)

let request = NSMutableURLRequest(url: NSURL(string: "http://localhost:8000/graphql")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```
> Make sure to replace `{access_token}` with your assigned access token.

The API needs an access token. To get your access token, you can login with your email and password using the `login()` endpoint.

The API expects that you have a Authorization Bearer header attached to your request, see following:

`Authorization: Bearer {access_token}`

<aside class="notice">
You must replace <code>{access_token}</code> with your assigned access token.
</aside>