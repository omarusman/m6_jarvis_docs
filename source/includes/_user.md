# User

Here are the endpoints you can use in regards to managing users.

## User Type

The GraphQL type for user. You can use this as a reference for your returned fields in your queries or mutations.

> GraphQL Type:

```graphql
type User {
    id: ID!
    uuid: String!
    name: String!
    email: String!
    role: String
    company_id: String
    company: Company @belongsTo
    parent_id: String
    admin_token: String
    profile_picture: String
    first_login: DateTime
    last_login: DateTime
    tfa_secret: String
    created_at: DateTime
    updated_at: DateTime
}
```

## Create User

Allows to create new user.



> GraphQL Query:

```graphql 
mutation {
  createUser(input: {uuid: "912a6cd0-3f84-4703-972f-76380105a415", name: "John Doe", email: "john@doe.com", password: "secret", role: "subscriber", company_id: "912a6cd0-3f84-4703-972f-76380105a413"}) {
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

__Input Parameters:__

Fields | Required
---------- | ------- 
__uuid__ | yes
__email__ | yes
__password__ | yes
__role__ | no, defaults to *subscriber*
__company_id__ | no
__parent_id__ | no
__admin_token__ | no
__admin_token__ | no
__profile_picture__ | no
__first_login__ | no
__last_login__ | no
__tfa_secret__ | no
    
<aside class="notice">
This requires an <a href="#authentication">authentication</a>.
</aside>

<aside class="notice">
This returns a <a href="#user-type">User Type</a>.
</aside>


> Request:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'content-type: application/json' \
  --data '{"query":"mutation {\n  createUser(input: {uuid: \"912a6cd0-3f84-4703-972f-76380105a415\", name: \"John Doe\", email: \"john@doe.com\", password: \"secret\", role: \"subscriber\", company_id: \"912a6cd0-3f84-4703-972f-76380105a413\"}) {\n    id\n    uuid\n    name\n    email\n    role\n    company_id\n    parent_id\n    admin_token\n    profile_picture\n    first_login\n    last_login\n    tfa_secret\n    created_at\n    updated_at\n  }\n}\n"}'
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
  "data": "{\"query\":\"mutation {\\n  createUser(input: {uuid: \\\"912a6cd0-3f84-4703-972f-76380105a415\\\", name: \\\"John Doe\\\", email: \\\"john@doe.com\\\", password: \\\"secret\\\", role: \\\"subscriber\\\", company_id: \\\"912a6cd0-3f84-4703-972f-76380105a413\\\"}) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}"
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
$body->append('{"query":"mutation {\\n  createUser(input: {uuid: \\"912a6cd0-3f84-4703-972f-76380105a415\\", name: \\"John Doe\\", email: \\"john@doe.com\\", password: \\"secret\\", role: \\"subscriber\\", company_id: \\"912a6cd0-3f84-4703-972f-76380105a413\\"}) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n"}');

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
  .body("{\"query\":\"mutation {\\n  createUser(input: {uuid: \\\"912a6cd0-3f84-4703-972f-76380105a415\\\", name: \\\"John Doe\\\", email: \\\"john@doe.com\\\", password: \\\"secret\\\", role: \\\"subscriber\\\", company_id: \\\"912a6cd0-3f84-4703-972f-76380105a413\\\"}) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = ["content-type": "application/json"]

let postData = NSData(data: "{"query":"mutation {\n  createUser(input: {uuid: \"912a6cd0-3f84-4703-972f-76380105a415\", name: \"John Doe\", email: \"john@doe.com\", password: \"secret\", role: \"subscriber\", company_id: \"912a6cd0-3f84-4703-972f-76380105a413\"}) {\n    id\n    uuid\n    name\n    email\n    role\n    company_id\n    parent_id\n    admin_token\n    profile_picture\n    first_login\n    last_login\n    tfa_secret\n    created_at\n    updated_at\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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
    "createUser": {
      "id": "436",
      "uuid": "912a6cd0-3f84-4703-972f-76380105a415",
      "name": "John Doe",
      "email": "john@doe.com",
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

## View User

Allows to view a user.

> GraphQL Query:

```graphql 
query {
  viewUser(id: 435) {
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

> Request:

```shell
curl --request POST \
  --url http://localhost:8000/graphql \
  --header 'content-type: application/json' \
  --data '{"query":"query {\n  viewUser(id: 435) {\n    id\n    uuid\n    name\n    email\n    role\n    company_id\n    parent_id\n    admin_token\n    profile_picture\n    first_login\n    last_login\n    tfa_secret\n    created_at\n    updated_at\n  }\n}\n"}'
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
  "data": "{\"query\":\"query {\\n  viewUser(id: 435) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}"
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
$body->append('{"query":"query {\\n  viewUser(id: 435) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n"}');

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
  .body("{\"query\":\"query {\\n  viewUser(id: 435) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = ["content-type": "application/json"]

let postData = NSData(data: "{"query":"query {\n  viewUser(id: 435) {\n    id\n    uuid\n    name\n    email\n    role\n    company_id\n    parent_id\n    admin_token\n    profile_picture\n    first_login\n    last_login\n    tfa_secret\n    created_at\n    updated_at\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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
    "viewUser": {
      "id": "435",
      "uuid": "912a6cd0-3f84-4703-972f-76380105a414",
      "name": "John Doe",
      "email": "john@doe.com",
      "role": "subscriber",
      "company_id": "912a6cd0-3f84-4703-972f-76380105a413",
      "parent_id": null,
      "admin_token": null,
      "profile_picture": null,
      "first_login": null,
      "last_login": null,
      "tfa_secret": null,
      "created_at": "2019-05-31 16:57:36",
      "updated_at": "2019-05-31 16:57:36"
    }
  }
}
```

## Update User

Allows to update an existing user.

> GraphQL Query:

```graphql 
mutation {
  updateUser(id: 435, input: {name: "Will Smith", password: "secret"}) {
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

__Input Parameters:__

Fields | Required
---------- | ------- 
__email__ | yes

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
  --header 'content-type: application/json' \
  --data '{"query":"mutation {\n  updateUser(id: 435, input: {name: \"Will Smith\", password: \"secret\"}) {\n    id\n    uuid\n    name\n    email\n    role\n    company_id\n    parent_id\n    admin_token\n    profile_picture\n    first_login\n    last_login\n    tfa_secret\n    created_at\n    updated_at\n  }\n}\n"}'
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
  "data": "{\"query\":\"mutation {\\n  updateUser(id: 435, input: {name: \\\"Will Smith\\\", password: \\\"secret\\\"}) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}"
}

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_PORT => "8000",
  CURLOPT_URL => "http://localhost:8000/graphql",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "{\"query\":\"mutation {\\n  updateUser(id: 435, input: {name: \\\"Will Smith\\\", password: \\\"secret\\\"}) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}",
  CURLOPT_HTTPHEADER => array(
    "content-type: application/json"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```java 
HttpResponse<String> response = Unirest.post("http://localhost:8000/graphql")
  .header("content-type", "application/json")
  .body("{\"query\":\"mutation {\\n  updateUser(id: 435, input: {name: \\\"Will Smith\\\", password: \\\"secret\\\"}) {\\n    id\\n    uuid\\n    name\\n    email\\n    role\\n    company_id\\n    parent_id\\n    admin_token\\n    profile_picture\\n    first_login\\n    last_login\\n    tfa_secret\\n    created_at\\n    updated_at\\n  }\\n}\\n\"}")
  .asString();
```

```swift 
import Foundation

let headers = ["content-type": "application/json"]

let postData = NSData(data: "{"query":"mutation {\n  updateUser(id: 435, input: {name: \"Will Smith\", password: \"secret\"}) {\n    id\n    uuid\n    name\n    email\n    role\n    company_id\n    parent_id\n    admin_token\n    profile_picture\n    first_login\n    last_login\n    tfa_secret\n    created_at\n    updated_at\n  }\n}\n"}".data(using: String.Encoding.utf8)!)

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
    "updateUser": {
      "id": "435",
      "uuid": "912a6cd0-3f84-4703-972f-76380105a414",
      "name": "Will Smith",
      "email": "john@doe.com",
      "role": "subscriber",
      "company_id": "912a6cd0-3f84-4703-972f-76380105a413",
      "parent_id": null,
      "admin_token": null,
      "profile_picture": null,
      "first_login": null,
      "last_login": null,
      "tfa_secret": null,
      "created_at": "2019-05-31 16:57:36",
      "updated_at": "2019-05-31 17:27:25"
    }
  }
}
```

