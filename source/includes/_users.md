
# User

## login()


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

Fields | Required | Meaning |
---------- | ------- | -------
__username__ | yes | A user's username or email.
__password__ | yes | A user's password.

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