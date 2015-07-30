# Log Collection
Developers can use a function to upload a log entry to Maybe backend.

In our current implementation, the log must be a `JSONObject` and should associated with a Maybe `label`.

So the api like:

```Java
    JSONObject logObject = new JSONObject();
    logObject.put("length", input.length());
    maybe.log("algorithms", logObject);
```

## Implementation
The library will cache logs, and batch upload them on appropriate time.

When is appropriate time? It depends:

* cache file size
* battery level
* available of Internet

This is a good use case for Maybe itself.

TODO: implement log upload logic by Maybe itself.
