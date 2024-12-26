Services must log into this meilisearch instance from the same server it is installed on.

To create a new key for a service (replacing the values in angle brackets <>), you may
try to follow these steps, but consult your chosen service for their specific steps if it fails.

Create an API key:
```

curl -s -X POST 'http://localhost:__PORT__/keys' -H 'Content-Type: application/json'   -H "Authorization: Bearer __KEY__"   --data-binary '{
    "description": "<description>",
    "actions": ["*"],
    "indexes": ["<index_name>"],
    "expiresAt": "2027-01-01T00:00:00Z"
  }' | jq '.key'

```
> Note: Use `"expiresAt": null` to never expire.
> Also note: the <index_name> will likely have specific requirements (for example it needs
 to end in `---notes` for [Sharkey](https://docs.joinsharkey.org/docs/customisation/meilisearch))

List keys:

```shell
curl -s 'http://localhost:__PORT__/keys'   -H "Authorization: Bearer $MASTER_KEY" | jq .
```

The login details for the service are then:
```
Host: 'localhost:__PORT__' OR Host: 'localhost', port: '__PORT__'
API key: '<key_from_previous_steps>'
index: '<index_name>'
scope: 'global'
```
