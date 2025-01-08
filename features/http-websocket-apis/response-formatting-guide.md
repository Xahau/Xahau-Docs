# Response Formatting Guide

Responses are structured differently based on whether the request is made through the WebSocket, JSON-RPC, or Commandline interfaces. The JSON-RPC and Commandline interfaces share the same format, as the Commandline interface internally uses JSON-RPC.

### Fields

| Field         | Type     | Description                                                                                                                                                            |
| ------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id            | (Varies) | (For WebSocket) The ID from the original request.                                                                                                                      |
| status        | String   | (For WebSocket) Indicates `success` when the request was received and processed correctly.                                                                             |
| result.status | String   | (For JSON-RPC and Commandline) Indicates `success` when the request was successfully processed.                                                                        |
| type          | String   | (For WebSocket) The value `response` is used for direct replies to API requests. Asynchronous notifications use other values, such as `ledgerClosed` or `transaction`. |
| result        | Object   | Contains the query result, with content that varies by command.                                                                                                        |
| warning       | String   | _(Optional)_ If present, the value is `load`, indicating the client is nearing the rate limit threshold where the server may disconnect.                               |
| warnings      | Array    | _(Optional)_ A list of **Warning Objects** with important server warnings. For more details, see API Warnings.                                                         |
| forwarded     | Boolean  | _(Optional)_ `true` indicates the request was forwarded from a Reporting Mode server to a P2P server to fulfill the request. Default is `false`.                       |

API Warnings

When a response contains a `warnings` array, each entry represents a specific warning from the server. Each **Warning Object** includes the following fields:



| Field   | Type   | Description                                                                                                                                                                            |
| ------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id      | Number | A unique numeric code identifying this warning message.                                                                                                                                |
| message | String | A human-readable explanation of the warning. Avoid writing code that relies on the content of this field; use the `id` (and `details`, if available) to interpret the warning instead. |
| details | Object | _(Optional)_ Additional context about the warning. The content varies by warning type.                                                                                                 |
