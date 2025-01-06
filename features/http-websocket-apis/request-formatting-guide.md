# Request Formatting Guide

### Public Servers

* wss://xahau.network or https://xahau.network (Mainnet)
* wss://xahau-test.net or https://xahau-test.net (Testnet)

### Sample Requests

To send a sample request to the API, use the following commands.

### Websocket

```
{
  "id": 3,
  "command": "account_info",
  "account": "rhBDFMmr3jSjgsWMqBAYaATLy3PuXy395y",
  "strict": true,
  "ledger_index": "validated",
  "api_version": 1
}
```

### WebSocket Request Structure

Once you establish a WebSocket connection to the `xahaud` server, you can send commands as JSON objects with these fields:

<table><thead><tr><th>Field</th><th width="220">Type</th><th>Description</th></tr></thead><tbody><tr><td>command</td><td>String</td><td>The name of the API method</td></tr><tr><td>id</td><td>(Multiple)</td><td><em>(Optional)</em> Unique identifier for the request. </td></tr><tr><td>api_version</td><td>Number</td><td><em>(Optional)</em> Specifies the API version.</td></tr></tbody></table>

### JSON-RPC

```
POST https://xahau.network/
Content-Type: application/json

{
    "method": "account_info",
    "params": [
        {
            "account": "rhBDFMmr3jSjgsWMqBAYaATLy3PuXy395y",
            "strict": true,
            "ledger_index": "validated",
            "api_version": 1
        }
    ]
}
```

### JSON-RPC Request Structure

<table><thead><tr><th>Field</th><th width="220">Type</th><th>Description</th></tr></thead><tbody><tr><td>method</td><td>String</td><td>The name of the API method</td></tr><tr><td>params</td><td>Array</td><td><em>(Optional)</em> A one-item array containing a JSON object with the parameters of the method.</td></tr></tbody></table>

### Comandline

```
xahaud account_info rhBDFMmr3jSjgsWMqBAYaATLy3PuXy395y validated strict
```

### Commandline Request Structure

<table><thead><tr><th>Field</th><th width="220">Description</th></tr></thead><tbody><tr><td>xahaud</td><td>Start calling the service xahaud</td></tr><tr><td>method</td><td>The name of the API method</td></tr><tr><td>params</td><td>(Optional)</td></tr></tbody></table>
