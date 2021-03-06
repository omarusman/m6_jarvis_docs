
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

## Login

Allows a user to be authenticated and returns it's assigned `{access token}` credentials.

> GraphQL Query:

```graphql 
mutation {
  login(data: {username: "john@doe.com", password: "secret"}) {
    access_token
    refresh_token
    expires_in
    token_type
  }
}
```

__Input Parameters:__

Fields | Required
---------- | ------- 
__username__ | yes
__password__ | yes

<aside class="notice">
This <strong>does not</strong> require an <a href="#authentication">authentication</a>.
</aside>

> Request:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'content-type: application/json' \
  --data '{"query":"mutation {\n  login(data: {username: \"john@doe.com\", password: \"secret\"}) {\n    access_token\n    refresh_token\n    expires_in\n    token_type\n  }\n}\n"}'
```

```javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:8000/graphql",
  "method": "POST",
  "headers": {
    "content-type": "application/json"
  },
  "data": "{\"query\":\"mutation {\\n  login(data: {username: \\\"john@doe.com\\\", password: \\\"secret\\\"}) {\\n    access_token\\n    refresh_token\\n    expires_in\\n    token_type\\n  }\\n}\\n\"}"
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
$body->append('{"query":"mutation {\\n  login(data: {username: \\"john@doe.com\\", password: \\"secret\\"}) {\\n    access_token\\n    refresh_token\\n    expires_in\\n    token_type\\n  }\\n}\\n"}');

$request->setRequestUrl('http://localhost:8000/graphql');
$request->setRequestMethod('POST');
$request->setBody($body);

$request->setHeaders(array(
  'content-type' => 'application/json'
));

$client->enqueue($request)->send();
$response = $client->getResponse();

echo $response->getBody();
```

```java 
HttpResponse<String> response = Unirest.post("http://localhost:8000/graphql")
  .header("content-type", "application/json")
  .body("{\"query\":\"mutation {\\n  login(data: {username: \\\"john@doe.com\\\", password: \\\"secret\\\"}) {\\n    access_token\\n    refresh_token\\n    expires_in\\n    token_type\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = ["content-type": "application/json"]

let postData = NSData(data: "{"query":"mutation {\n  login(data: {username: \"john@doe.com\", password: \"secret\"}) {\n    access_token\n    refresh_token\n    expires_in\n    token_type\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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

> Response:

```json
{
  "data": {
    "login": {
      "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjcxYmFmNzNjNGRhZWZlMGEwMmYzMmVmNWQzMjAwMzhiZDAwMzVlMzg4MDNhMjkxOTZhYjQzY2VkNjg4OGQ3OWY0MWZkNmRjNWNjODFmN2EzIn0.eyJhdWQiOiIyIiwianRpIjoiNzFiYWY3M2M0ZGFlZmUwYTAyZjMyZWY1ZDMyMDAzOGJkMDAzNWUzODgwM2EyOTE5NmFiNDNjZWQ2ODg4ZDc5ZjQxZmQ2ZGM1Y2M4MWY3YTMiLCJpYXQiOjE1NTkyMjY1NDEsIm5iZiI6MTU1OTIyNjU0MSwiZXhwIjoxNTkwODQ4OTQxLCJzdWIiOiIzODYiLCJzY29wZXMiOltdfQ.xNcLkJNTG4c0VYRB1MI7ZmW0ZEc_HJBNLJw1AmKedTK0pL5T2Tc7s0feRtbBU731tt2imu5kumssDExf3WNZkTIsumwRRg4PNdatbGhVuruHJ7pcdvc8dTIsEB8ECWoVMVjNrZPLOshEoDVRk5sX5OqbRLCWqdGGVle33D1ozHP7-q_sbL9iv2OUUg4gfl36EYMgAUoVA6OKbWUlVyLba7QZGq9BHf9g4W9Vdd6x5jHMULFPIAVACSGJJDJmTcRoNFH5zdtYAHAwuWgvngbAIHIOiYZGo3P_1nW0stTLq8tFg36iGVLtWU3yUWbKVPiBDwbxI4PQW2iOGBOLSyveOIn7VqCPDZoRnXNdcp_u_Ix51Or8YYbWKc61Vd6CM6zllnM3XgiImE9Mua7yH6TTHtd-l2DV2CX20O6q27ZDlOxJ-WVzziioAWxhioX6GyACiUc5M9YgkC4QswSYSbtPYPgOGh9N3enqUXTrnjHybkPwgxOd9kAfVoPL5f4qoMEHxxr5tpoZAtYU5lhlp12ktEDyP4_Kgzu25qpi6MejdQOVKBA0EkRtYQM3DpIK9Kv7oihG-sb_vLw3shHDF0x1lxQMoZ2rgVL-9zEszKhwmXNXn6VDzGuwh4AksKW74lLkpdTZT27_7-_VYios-JDKOvBkMSWzer8uAWabZMCra1U",
      "refresh_token": "def50200820cae791fb2eccb2ee08c0044d71e38d57ed7eec6c2072a6e5250e6cc28e978c919d26eda47ee5c1165b7969ad8178cae4cecac6c2c39865470f8bda7db7f61e198b78a11691ea9d022103a81ec0757151243283e930361c84935f44f3da2aec5f7e29fea096bb5c5e39cd025adefcc38c2d1f2b78809a5deec74633d60266dffd0d34331d5c80e76be0a7142a4d7c20657f299e0756b09f2ab90a93f6ea9db936fd40e6119973b19d0eb65467372804b19fc8edb4ace09968d03e4b4ccd59f4bb99f15674ba7adff614ee73b6254aa243bf47648bf7c50bf6382b898c6765170cdc373a89e8cb773da408f90251b7616e59d52c82f129c8fd537e453a6ffd7e6c45d04d669509b695e1f62bc2d87a9206805a7d5a29c6a677897912cccd6c236f8dbbe0bdf31cfbb6d6f245d273e047a66886d5705d85e1d45ae08a8f51d9fa62b7335a25f7d320803e4ccb3d8893c4e78df53208211c99794e7ed5d436c",
      "expires_in": 31622400,
      "token_type": "Bearer"
    }
  }
}
```

## Me

Allows to view the current authenticated user.

> GraphQL Query:

```graphql 
{
  me {
    id
    uuid
    name
    email
    role
    company_id
    parent_id
    admin_token
    profile_picture
    first_login
    last_login
    tfa_secret
    created_at
    updated_at
  }
}

```

<aside class="notice">
This requires an <a href="#authentication">authentication</a>.
</aside>

<aside class="success">
This returns a <a href="#user-type">User Type</a>.
</aside>

> Request:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUwOWQ2OGY4MDcwYTQwNjc5YTI5MzdkYTk0NTkyNDNjZGE1ODkwZDAzZGNlZmRjNGY5YzFhOTNlNmE1ZWRiZjZjM2Q1OWVlMjgyZDhiNGU1In0.eyJhdWQiOiIyIiwianRpIjoiZTA5ZDY4ZjgwNzBhNDA2NzlhMjkzN2RhOTQ1OTI0M2NkYTU4OTBkMDNkY2VmZGM0ZjljMWE5M2U2YTVlZGJmNmMzZDU5ZWUyODJkOGI0ZTUiLCJpYXQiOjE1NTkzMjY0MDUsIm5iZiI6MTU1OTMyNjQwNSwiZXhwIjoxNTkwOTQ4ODA1LCJzdWIiOiI0MzYiLCJzY29wZXMiOltdfQ.6miluE4R6POa34N2I23mbApCtRNYI_C2lQrfQksbZ7lswNT7ACtNkqfEkcWkuBKHL4KiLikYTEllqZxQx5FhCSFDmvNbMoKw3yJU1JK0y4g1bG_iZGuqoFC32I-Pqn4Rb7j-xHM_zLAb7PumBJlGQZ9ezBS75dZ6CqZd2u3g-kdMgheCrv0SkxK7ZiXYABXNt0droUY3WadTAi_J7H-fftJ--_GWKQg9Jdue3HKcI5tTP5dLHM2hI0C0IO3axdjpG8Q35JhjOukybEGL1NLOouzNWYSm2lRGKIenvbfFIC7drwn1w_fu19iEcfA370clTbbNZwWMcdgQJbJW9QL4Cxj5AbF06Fyyhu73oYR5LiNE5sDNymg_G3iP5Meyf5RWab5SPPSAgagMmeS2yOCc9rIEw6VqUsuQl0mef_ogWdUJ5Ku3AYpd1bb6I6gt1Kf4Cm0w5BuF-LofJkmLxnk1RRLaXgObDyLrzIYjOfrNcuzmMXiD4eaeNJtiuM2Erh0zG3AsYnognopDnOk2CGACMYqbGSs0OU7v-eUOe7jVMdnwlAN1wh5CI28cdi8VWf2x9AtHpBIGpI4xVC8xCnsEGw41sHG1K3gmejRwU0LYNEzv3AzRyq8mDSQfcQkNVTfJnVGBWHJzfHr8DHLLA-1PiPTR8VtexMKTV1v6mr6cnUs' \
  --header 'content-type: application/json' \
  --data '{"query":"{\n  me {\n    id\n    uuid\n    name\n    email\n    role\n    company_id\n    parent_id\n    admin_token\n    profile_picture\n    first_login\n    last_login\n    tfa_secret\n    created_at\n    updated_at\n  }\n}\n"}'
```

```javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:8000/graphql",
  "method": "POST",
  "headers": {
    "content-type": "application/json",
    "authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUwOWQ2OGY4MDcwYTQwNjc5YTI5MzdkYTk0NTkyNDNjZGE1ODkwZDAzZGNlZmRjNGY5YzFhOTNlNmE1ZWRiZjZjM2Q1OWVlMjgyZDhiNGU1In0.eyJhdWQiOiIyIiwianRpIjoiZTA5ZDY4ZjgwNzBhNDA2NzlhMjkzN2RhOTQ1OTI0M2NkYTU4OTBkMDNkY2VmZGM0ZjljMWE5M2U2YTVlZGJmNmMzZDU5ZWUyODJkOGI0ZTUiLCJpYXQiOjE1NTkzMjY0MDUsIm5iZiI6MTU1OTMyNjQwNSwiZXhwIjoxNTkwOTQ4ODA1LCJzdWIiOiI0MzYiLCJzY29wZXMiOltdfQ.6miluE4R6POa34N2I23mbApCtRNYI_C2lQrfQksbZ7lswNT7ACtNkqfEkcWkuBKHL4KiLikYTEllqZxQx5FhCSFDmvNbMoKw3yJU1JK0y4g1bG_iZGuqoFC32I-Pqn4Rb7j-xHM_zLAb7PumBJlGQZ9ezBS75dZ6CqZd2u3g-kdMgheCrv0SkxK7ZiXYABXNt0droUY3WadTAi_J7H-fftJ--_GWKQg9Jdue3HKcI5tTP5dLHM2hI0C0IO3axdjpG8Q35JhjOukybEGL1NLOouzNWYSm2lRGKIenvbfFIC7drwn1w_fu19iEcfA370clTbbNZwWMcdgQJbJW9QL4Cxj5AbF06Fyyhu73oYR5LiNE5sDNymg_G3iP5Meyf5RWab5SPPSAgagMmeS2yOCc9rIEw6VqUsuQl0mef_ogWdUJ5Ku3AYpd1bb6I6gt1Kf4Cm0w5BuF-LofJkmLxnk1RRLaXgObDyLrzIYjOfrNcuzmMXiD4eaeNJtiuM2Erh0zG3AsYnognopDnOk2CGACMYqbGSs0OU7v-eUOe7jVMdnwlAN1wh5CI28cdi8VWf2x9AtHpBIGpI4xVC8xCnsEGw41sHG1K3gmejRwU0LYNEzv3AzRyq8mDSQfcQkNVTfJnVGBWHJzfHr8DHLLA-1PiPTR8VtexMKTV1v6mr6cnUs"
  },
  "data": "{\"query\":\"{\\n  me {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}"
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
$body->append('{"query":"{\\n  me {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n"}');

$request->setRequestUrl('http://localhost:8000/graphql');
$request->setRequestMethod('POST');
$request->setBody($body);

$request->setHeaders(array(
  'content-type' => 'application/json',
  'authorization' => 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUwOWQ2OGY4MDcwYTQwNjc5YTI5MzdkYTk0NTkyNDNjZGE1ODkwZDAzZGNlZmRjNGY5YzFhOTNlNmE1ZWRiZjZjM2Q1OWVlMjgyZDhiNGU1In0.eyJhdWQiOiIyIiwianRpIjoiZTA5ZDY4ZjgwNzBhNDA2NzlhMjkzN2RhOTQ1OTI0M2NkYTU4OTBkMDNkY2VmZGM0ZjljMWE5M2U2YTVlZGJmNmMzZDU5ZWUyODJkOGI0ZTUiLCJpYXQiOjE1NTkzMjY0MDUsIm5iZiI6MTU1OTMyNjQwNSwiZXhwIjoxNTkwOTQ4ODA1LCJzdWIiOiI0MzYiLCJzY29wZXMiOltdfQ.6miluE4R6POa34N2I23mbApCtRNYI_C2lQrfQksbZ7lswNT7ACtNkqfEkcWkuBKHL4KiLikYTEllqZxQx5FhCSFDmvNbMoKw3yJU1JK0y4g1bG_iZGuqoFC32I-Pqn4Rb7j-xHM_zLAb7PumBJlGQZ9ezBS75dZ6CqZd2u3g-kdMgheCrv0SkxK7ZiXYABXNt0droUY3WadTAi_J7H-fftJ--_GWKQg9Jdue3HKcI5tTP5dLHM2hI0C0IO3axdjpG8Q35JhjOukybEGL1NLOouzNWYSm2lRGKIenvbfFIC7drwn1w_fu19iEcfA370clTbbNZwWMcdgQJbJW9QL4Cxj5AbF06Fyyhu73oYR5LiNE5sDNymg_G3iP5Meyf5RWab5SPPSAgagMmeS2yOCc9rIEw6VqUsuQl0mef_ogWdUJ5Ku3AYpd1bb6I6gt1Kf4Cm0w5BuF-LofJkmLxnk1RRLaXgObDyLrzIYjOfrNcuzmMXiD4eaeNJtiuM2Erh0zG3AsYnognopDnOk2CGACMYqbGSs0OU7v-eUOe7jVMdnwlAN1wh5CI28cdi8VWf2x9AtHpBIGpI4xVC8xCnsEGw41sHG1K3gmejRwU0LYNEzv3AzRyq8mDSQfcQkNVTfJnVGBWHJzfHr8DHLLA-1PiPTR8VtexMKTV1v6mr6cnUs'
));

$client->enqueue($request)->send();
$response = $client->getResponse();

echo $response->getBody();
```

```java 
HttpResponse<String> response = Unirest.post("http://localhost:8000/graphql")
  .header("content-type", "application/json")
  .header("authorization", "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUwOWQ2OGY4MDcwYTQwNjc5YTI5MzdkYTk0NTkyNDNjZGE1ODkwZDAzZGNlZmRjNGY5YzFhOTNlNmE1ZWRiZjZjM2Q1OWVlMjgyZDhiNGU1In0.eyJhdWQiOiIyIiwianRpIjoiZTA5ZDY4ZjgwNzBhNDA2NzlhMjkzN2RhOTQ1OTI0M2NkYTU4OTBkMDNkY2VmZGM0ZjljMWE5M2U2YTVlZGJmNmMzZDU5ZWUyODJkOGI0ZTUiLCJpYXQiOjE1NTkzMjY0MDUsIm5iZiI6MTU1OTMyNjQwNSwiZXhwIjoxNTkwOTQ4ODA1LCJzdWIiOiI0MzYiLCJzY29wZXMiOltdfQ.6miluE4R6POa34N2I23mbApCtRNYI_C2lQrfQksbZ7lswNT7ACtNkqfEkcWkuBKHL4KiLikYTEllqZxQx5FhCSFDmvNbMoKw3yJU1JK0y4g1bG_iZGuqoFC32I-Pqn4Rb7j-xHM_zLAb7PumBJlGQZ9ezBS75dZ6CqZd2u3g-kdMgheCrv0SkxK7ZiXYABXNt0droUY3WadTAi_J7H-fftJ--_GWKQg9Jdue3HKcI5tTP5dLHM2hI0C0IO3axdjpG8Q35JhjOukybEGL1NLOouzNWYSm2lRGKIenvbfFIC7drwn1w_fu19iEcfA370clTbbNZwWMcdgQJbJW9QL4Cxj5AbF06Fyyhu73oYR5LiNE5sDNymg_G3iP5Meyf5RWab5SPPSAgagMmeS2yOCc9rIEw6VqUsuQl0mef_ogWdUJ5Ku3AYpd1bb6I6gt1Kf4Cm0w5BuF-LofJkmLxnk1RRLaXgObDyLrzIYjOfrNcuzmMXiD4eaeNJtiuM2Erh0zG3AsYnognopDnOk2CGACMYqbGSs0OU7v-eUOe7jVMdnwlAN1wh5CI28cdi8VWf2x9AtHpBIGpI4xVC8xCnsEGw41sHG1K3gmejRwU0LYNEzv3AzRyq8mDSQfcQkNVTfJnVGBWHJzfHr8DHLLA-1PiPTR8VtexMKTV1v6mr6cnUs")
  .body("{\"query\":\"{\\n  me {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = [
  "content-type": "application/json",
  "authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUwOWQ2OGY4MDcwYTQwNjc5YTI5MzdkYTk0NTkyNDNjZGE1ODkwZDAzZGNlZmRjNGY5YzFhOTNlNmE1ZWRiZjZjM2Q1OWVlMjgyZDhiNGU1In0.eyJhdWQiOiIyIiwianRpIjoiZTA5ZDY4ZjgwNzBhNDA2NzlhMjkzN2RhOTQ1OTI0M2NkYTU4OTBkMDNkY2VmZGM0ZjljMWE5M2U2YTVlZGJmNmMzZDU5ZWUyODJkOGI0ZTUiLCJpYXQiOjE1NTkzMjY0MDUsIm5iZiI6MTU1OTMyNjQwNSwiZXhwIjoxNTkwOTQ4ODA1LCJzdWIiOiI0MzYiLCJzY29wZXMiOltdfQ.6miluE4R6POa34N2I23mbApCtRNYI_C2lQrfQksbZ7lswNT7ACtNkqfEkcWkuBKHL4KiLikYTEllqZxQx5FhCSFDmvNbMoKw3yJU1JK0y4g1bG_iZGuqoFC32I-Pqn4Rb7j-xHM_zLAb7PumBJlGQZ9ezBS75dZ6CqZd2u3g-kdMgheCrv0SkxK7ZiXYABXNt0droUY3WadTAi_J7H-fftJ--_GWKQg9Jdue3HKcI5tTP5dLHM2hI0C0IO3axdjpG8Q35JhjOukybEGL1NLOouzNWYSm2lRGKIenvbfFIC7drwn1w_fu19iEcfA370clTbbNZwWMcdgQJbJW9QL4Cxj5AbF06Fyyhu73oYR5LiNE5sDNymg_G3iP5Meyf5RWab5SPPSAgagMmeS2yOCc9rIEw6VqUsuQl0mef_ogWdUJ5Ku3AYpd1bb6I6gt1Kf4Cm0w5BuF-LofJkmLxnk1RRLaXgObDyLrzIYjOfrNcuzmMXiD4eaeNJtiuM2Erh0zG3AsYnognopDnOk2CGACMYqbGSs0OU7v-eUOe7jVMdnwlAN1wh5CI28cdi8VWf2x9AtHpBIGpI4xVC8xCnsEGw41sHG1K3gmejRwU0LYNEzv3AzRyq8mDSQfcQkNVTfJnVGBWHJzfHr8DHLLA-1PiPTR8VtexMKTV1v6mr6cnUs"
]

let postData = NSData(data: "{"query":"{\n  me {\n    id\n    uuid\n    name\n    email\n    role\n    company_id\n    parent_id\n    admin_token\n    profile_picture\n    first_login\n    last_login\n    tfa_secret\n    created_at\n    updated_at\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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

> Response:

```json
{
  "data": {
    "me": {
      "id": "436",
      "uuid": "912a6cd0-3f84-4703-972f-76380105a415",
      "name": "John Doe",
      "email": "john15@doe.com",
      "role": "subscriber",
      "company_id": "912a6cd0-3f84-4703-972f-76380105a413",
      "parent_id": null,
      "admin_token": null,
      "profile_picture": null,
      "first_login": null,
      "last_login": null,
      "tfa_secret": null,
      "created_at": "2019-05-31 17:06:00",
      "updated_at": "2019-05-31 17:06:00"
    }
  }
}
```

## Logout

Allows a user to be logged out.

> GraphQL Query:

```graphql 
mutation {
  logout {
    status
    message
  }
}
```

<aside class="notice">
This requires an <a href="#authentication">authentication</a>
</aside>

<aside class="notice">
You must replace <code>{access_token}</code> with your assigned access token.
</aside>

> Request:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'authorization: Bearer {access_token}' \
  --header 'content-type: application/json' \
  --data '{"query":"mutation {\n  logout {\n    status\n    message\n  }\n}\n"}'
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
  "data": "{\"query\":\"mutation {\\n  logout {\\n    status\\n    message\\n  }\\n}\\n\"}"
}

$.ajax(settings).done(function (response) {
  console.log(response);
});
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
$body->append('{"query":"mutation {\\n  logout {\\n    status\\n    message\\n  }\\n}\\n"}');

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
  .body("{\"query\":\"mutation {\\n  logout {\\n    status\\n    message\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = [
  "content-type": "application/json",
  "authorization": "Bearer {access_token}"
]

let postData = NSData(data: "{"query":"mutation {\n  logout {\n    status\n    message\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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

> Response:

```json
{
  "data": {
    "logout": {
      "status": "TOKEN_REVOKED",
      "message": "Your session has been terminated"
    }
  }
}
```

## Refresh Token

For short-lived access tokens, users can refresh access tokens via the refresh token that was provided by [login()](#login).

> GraphQL Query:

```graphql 
mutation {
  refreshToken(data: {
    refresh_token: "{request_token}"}) {
    access_token
    refresh_token
    expires_in
    token_type
  }
}
```

__Input Parameters:__

Fields | Required
---------- | ------- 
__request_token__ | yes

<aside class="notice">
This <strong>does not</strong> require an <a href="#authentication">authentication</a>.
</aside>

<aside class="notice">
You must replace <code>{request_token}</code> with your request token.
</aside>

> Request:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'content-type: application/json' \
  --data '{"query":"mutation {\n  refreshToken(data: {\n    refresh_token: \"{request_token}\"}) {\n    access_token\n    refresh_token\n    expires_in\n    token_type\n  }\n}\n"}'
```

```javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:8000/graphql",
  "method": "POST",
  "headers": {
    "content-type": "application/json"
  },
  "data": "{\"query\":\"mutation {\\n  refreshToken(data: {\\n    refresh_token: \\\"{request_token}\\\"}) {\\n    access_token\\n    refresh_token\\n    expires_in\\n    token_type\\n  }\\n}\\n\"}"
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
$body->append('{"query":"mutation {\\n  refreshToken(data: {\\n    refresh_token: \\"{request_token}\\"}) {\\n    access_token\\n    refresh_token\\n    expires_in\\n    token_type\\n  }\\n}\\n"}');

$request->setRequestUrl('http://localhost:8000/graphql');
$request->setRequestMethod('POST');
$request->setBody($body);

$request->setHeaders(array(
  'content-type' => 'application/json'
));

$client->enqueue($request)->send();
$response = $client->getResponse();

echo $response->getBody();
```

```java 
HttpResponse<String> response = Unirest.post("http://localhost:8000/graphql")
  .header("content-type", "application/json")
  .body("{\"query\":\"mutation {\\n  refreshToken(data: {\\n    refresh_token: \\\"{request_token}\\\"}) {\\n    access_token\\n    refresh_token\\n    expires_in\\n    token_type\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = ["content-type": "application/json"]

let postData = NSData(data: "{"query":"mutation {\n  refreshToken(data: {\n    refresh_token: \"{request_token}\"}) {\n    access_token\n    refresh_token\n    expires_in\n    token_type\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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

> Response:

```json
{
  "data": {
    "refreshToken": {
      "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImM5MTY5ZjM5MTEyMDYyOTc2YjE1ZmU4YjI5ZTk0ZTFmYTFhMmI5YTgyMDUxYjk4YWNkZDVmZmNhZDk5NDYzMDIzNDJiNmU4N2Q4MTMzYzJmIn0.eyJhdWQiOiIyIiwianRpIjoiYzkxNjlmMzkxMTIwNjI5NzZiMTVmZThiMjllOTRlMWZhMWEyYjlhODIwNTFiOThhY2RkNWZmY2FkOTk0NjMwMjM0MmI2ZTg3ZDgxMzNjMmYiLCJpYXQiOjE1NTkyMzA1NTgsIm5iZiI6MTU1OTIzMDU1OCwiZXhwIjoxNTkwODUyOTU4LCJzdWIiOiIzODYiLCJzY29wZXMiOltdfQ.3Bw5AWWn3vNMTvKqxSlCnFWLSjBBAJA76DKY2oVMP1DhFVPBLfiw3RKBY2sFxMWLqVFmOn_x_L43JtEZk4TN3hCIqHvXCecA6XKnN_mX-d5eroIw10VsQlFWuhukZ-IsFtmd-k1--3eYRUDkQw2kOYZqwvBlU_sLdX46HVpQJrLYZNe76lBI1ZQesb3n1pu31WE8egwPkH72BtplT_abjSZlfsejW1XjhYMFQ2FRvzufp0XANa_UlauA-IqwnNDhFz031ukWrtIrqyfC8l3gmi8h2i5Gbce2Q-BtcxGYxNo8VzDJh10zRbwlZ5P5q8jkgfGTe2C7nsVUInU7ofWwN_-WetKCiF6VO6PNVc7KlZJIG7L-KU9FTJp-chwjUOthCn1qSFzldO64X4mdLGjdLiYJnJL--o4FL-xMk2SLb3X38GzlTwN9-PoYVkla5gO3iDaM-ddvQNW_VH3yrc-8WQkMC6sbGfKcF5ZY2T6i6DFgYBWiWtTQCUpBJ3XIR5Pn8yW5xGMr32OINnQbz72E_gwpAX3-V5NuFErBCbOTRHFIzmWuaJah7XZy3bEg6b2gkV_iM87r316UzZ7jG6Z0xBfRxpmhL4HMPySlSSjyAmgI-JC_snrxCpoh90qY7DKuLkO7DhBUgWS-YcLIVRuTXAdoj-8yucbl9oD8GLHuudQ",
      "refresh_token": "{request_token}",
      "expires_in": 31622400,
      "token_type": "Bearer"
    }
  }
}
```

## Forgot Password

Allows to initiate a forgot password request.

> GraphQL Query:

```graphql 
mutation {
  forgotPassword(data: {email: "john@doe.com"}) {
    status
    message
  }
}
```

__Input Parameters:__

Fields | Required
---------- | ------- 
__email__ | yes

<aside class="notice">
This <strong>does not</strong> require an <a href="#authentication">authentication</a>.
</aside>

> Request:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'content-type: application/json' \
  --data '{"query":"mutation {\n  forgotPassword(data: {email: \"john@doe.com\"}) {\n    status\n    message\n  }\n}\n"}'
```

```javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:8000/graphql",
  "method": "POST",
  "headers": {
    "content-type": "application/json"
  },
  "data": "{\"query\":\"mutation {\\n  forgotPassword(data: {email: \\\"john@doe.com\\\"}) {\\n    status\\n    message\\n  }\\n}\\n\"}"
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
$body->append('{"query":"mutation {\\n  forgotPassword(data: {email: \\"john@doe.com\\"}) {\\n    status\\n    message\\n  }\\n}\\n"}');

$request->setRequestUrl('http://localhost:8000/graphql');
$request->setRequestMethod('POST');
$request->setBody($body);

$request->setHeaders(array(
  'content-type' => 'application/json'
));

$client->enqueue($request)->send();
$response = $client->getResponse();

echo $response->getBody();
```

```java 
HttpResponse<String> response = Unirest.post("http://localhost:8000/graphql")
  .header("content-type", "application/json")
  .body("{\"query\":\"mutation {\\n  forgotPassword(data: {email: \\\"john@doe.com\\\"}) {\\n    status\\n    message\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = ["content-type": "application/json"]

let postData = NSData(data: "{"query":"mutation {\n  forgotPassword(data: {email: \"john@doe.com\"}) {\n    status\n    message\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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

> Response:

```json
{
  "data": {
    "forgotPassword": {
      "status": "EMAIL_SENT",
      "message": "We have e-mailed your password reset link!"
    }
  }
}
```

## Update Forgotten Password

Allows to change the password after a forgot password request.

> GraphQL Query:

```graphql 
mutation {
  updateForgottenPassword(data: {email: "john@doe.com", token: "$2y$10$xx", password: "newsecret", password_confirmation: "newsecret"}) {
    status
    message
  }
}
```

__Input Parameters:__

Fields | Required
---------- | ------- 
__email__ | yes
__token__ | yes
__password__ | yes
__password_confirmation__ | yes

<aside class="notice">
This <strong>does not</strong> require an <a href="#authentication">authentication</a>.
</aside>

> Request:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'content-type: application/json' \
  --data '{"query":"mutation {\n  updateForgottenPassword(data: {email: \"john@doe.com\", token: \"$2y$10$xx\", password: \"newsecret\", password_confirmation: \"newsecret\"}) {\n    status\n    message\n  }\n}\n"}'
```

```javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:8000/graphql",
  "method": "POST",
  "headers": {
    "content-type": "application/json"
  },
  "data": "{\"query\":\"mutation {\\n  updateForgottenPassword(data: {email: \\\"john@doe.com\\\", token: \\\"$2y$10$xx\\\", password: \\\"newsecret\\\", password_confirmation: \\\"newsecret\\\"}) {\\n    status\\n    message\\n  }\\n}\\n\"}"
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
$body->append('{"query":"mutation {\\n  updateForgottenPassword(data: {email: \\"john@doe.com\\", token: \\"$2y$10$xx\\", password: \\"newsecret\\", password_confirmation: \\"newsecret\\"}) {\\n    status\\n    message\\n  }\\n}\\n"}');

$request->setRequestUrl('http://localhost:8000/graphql');
$request->setRequestMethod('POST');
$request->setBody($body);

$request->setHeaders(array(
  'content-type' => 'application/json'
));

$client->enqueue($request)->send();
$response = $client->getResponse();

echo $response->getBody();
```

```java 
HttpResponse<String> response = Unirest.post("http://localhost:8000/graphql")
  .header("content-type", "application/json")
  .body("{\"query\":\"mutation {\\n  updateForgottenPassword(data: {email: \\\"john@doe.com\\\", token: \\\"$2y$10$xx\\\", password: \\\"newsecret\\\", password_confirmation: \\\"newsecret\\\"}) {\\n    status\\n    message\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = ["content-type": "application/json"]

let postData = NSData(data: "{"query":"mutation {\n  updateForgottenPassword(data: {email: \"john@doe.com\", token: \"$2y$10$xx\", password: \"newsecret\", password_confirmation: \"newsecret\"}) {\n    status\n    message\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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

> Response:

```json
{
  "data": {
    "updateForgottenPassword": {
      "status": "PASSWORD_UPDATED",
      "message": "Your password has been reset!"
    }
  }
}
```

