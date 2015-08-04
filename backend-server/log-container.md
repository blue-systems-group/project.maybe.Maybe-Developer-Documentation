## Log

The logs api will let developers store logs from device. Each record represents a log entry. Currently, you are only allowed to use POST method.

### POST
This is the only thing you can do with the ```logs``` api.

    $ curl http://localhost:3000/maybe-api-v1/logs/deviceid/packagename -d '[logJSONObject, logJSONObject, ..., logJSONObject]'

The `logJSONObject` should be a JSONObject to represent a log entry, it must have such fields:

fields    | meaning
:-------- | :--------------------------------------
timestamp | timestamp when log received from client
label     | the maybe label of the log
logObject | the actual log received from client

Example of valid `logJSONObject`:

    {"timestamp": 1, "label": 1, "logObject": {"a" : 1, "b": 2}}

If everything good (I hope that),  it will return an empty JSONObject with status code ```201```:

    {}

If any `logJSONObject` is invalid, it will return status code `403` and an error message like:

    {"error": "{\"timestamp\":1,\"label\":1,\"logOxbject\":{\"a\":1,\"b\":2}} is not valid!"}

Note that, the backend will process the array one by one. If any `logJSONObject` is invalid. It'll stop immediately. The `logJSONObject`s before the invalid one will be processed, but others wouldn't be processed.

You should pass your real `deviceid` instead of the `deviceid` in url above.
