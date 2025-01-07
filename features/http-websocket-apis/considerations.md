# Considerations

## Markers

Some methods return more data than can fit efficiently into a single response. When the results exceed the response limit, a `marker` field is included in the response. This field allows you to retrieve additional pages of data through subsequent requests. To continue fetching data, include the `marker` value from the previous response in your next request. If a response does not include a `marker`, it means you have reached the end of the data set.

The format of the `marker` field is intentionally unspecified. Each server can define the `marker` as needed, meaning it could be a string, a nested object, or another type. The `marker` format may vary between servers and even between methods on the same server. Each `marker` is temporary and may become invalid after approximately 10 minutes.

## Rate Limit

The `xahaud` server enforces rate limits on API clients using public APIs to prevent excessive requests. Rate limiting is applied based on the client’s IP address, meaning multiple clients sharing a [network address translation (NAT)](https://en.wikipedia.org/wiki/Network_address_translation) will share the same rate limit associated with their public IP.

When a client is nearing the rate limit, the server includes a `"warning": "load"` field at the top level of an API response. This warning does not appear on every response but may be sent several times before the server disconnects the client. Clients connected as an admin are exempt from rate limiting.

If a client exceeds the rate limit, the server disconnects the client and temporarily blocks further requests from that IP address. The WebSocket and JSON-RPC APIs handle disconnects differently, as described below.
