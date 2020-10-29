#### JSend

All AllMyWishrs services implement [the JSend specification](https://github.com/omniti-labs/jsend) for serving API responses. In a nutshell, this middleware attaches a JSend object to each request with `success` and `error` methods that can then be invoked later on. This means our responses usually follow the same general formats.

_Successes_

```json
{
  "status" : "success",
  "data" : {
     "relevant data here : ""
  }
}
```

_Errors_ 

```json
{
  "status" : "error",
  "message" : "relevant message about the error here", //Please send useful error messages not an error occured. Dont let thunder strike you
  "code" : "error code, often just the http status code",
  "error_code": "3-digit-internal-error-code",
  "data" : {
    "any other relevant info about the error here i.e. conditions, stack traces etc" : ""
  }
}
```

The `status` key - a simple key to let you know upfront if the request was successful or not. This is merely an added convenience as the HTTP status code attached to the server response can also be used to determine the result of an API call. This is the only key that is universal across requests.

The `message` key - In the event of an error, the message key will contain a description of the error. This key is only available in error responses

The `data` key - is where you want to look at for the result of your request. It can either be an object, or an array depending on the request made. In the event of an error, this usually filled with additional information on whatever error occurred for help with debugging.

The `code` key - This key is only available in the event of an error. This simply mirrors whatever HTTP status code accompanied the request as another added convenience. This code could also just be read from the request itself.

Also ensure you attach the proper http response codes

```
_Common Codes_
SERVER_ERROR: 500
CONFLICT: 409
NOT_FOUND: 404
BAD_REQUEST: 400
SUCCESS: 200
CREATED: 201
UNAUTHORIZED: 401
```


> Note: because we follow the JSend specification, this means the content type for responses will always be `application/json`!


