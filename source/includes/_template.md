## TITLE

Some description

> GraphQL Query:

```graphql 
mutation {
  someFunction(data: {email: "john@doe.com"}) {
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
```

```javascript
```

```php
```

```java 
```

```swift 
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