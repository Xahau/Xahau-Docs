---
description: Convert a 20 byte Account ID to an r-address
---

# util\_raddr

### Behaviour

{% tabs %}
{% tab title="C" %}
* Read a 20 byte  Account ID from the `read_ptr`
* Write the equivalent r-address for that Account ID to `write_ptr`
{% endtab %}

{% tab title="Javascript" %}
* Read a 20 byte Account ID from the `accountid`
* Return the equivalent r-address for that Account ID
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t util_raddr (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t read_ptr,
    uint32_t read_len
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function util_raddr(accountid: ByteArray | HexString): ErrorCode | string
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t raddr_out[40];
uint8_t acc_id[20] =
{
    0x2dU, 0xd8U, 0xaaU, 0xdbU, 0x4eU, 0x15U,               
    0xebU, 0xeaU,  0xeU, 0xfdU, 0x78U, 0xd1U, 0xb0U,
    0x35U, 0x91U,  0x4U, 0x7bU, 0xfaU, 0x1eU,  0xeU
};
int64_t bytes_written = 
    util_raddr(raddr_out, sizeof(raddr_out), acc_id, 20);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const raddr = util_raddr('8D329C03074A98EF0488AB6ABBF5883F68CCFD4E')
// or
const raddr = util_raddr([
    0x8D, 0x32, 0x9C, 0x03, 0x07, 0x4A, 0x98, 0xEF, 0x04, 0x88,
    0xAB, 0x6A, 0xBB, 0xF5, 0x88, 0x3F, 0x68, 0xCC, 0xFD, 0x4E
])
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}


<table><thead><tr><th>Name</th><th width="82">Type</th><th>Description</th></tr></thead><tbody><tr><td>write_ptr</td><td>uint32_t</td><td>Pointer to a buffer of a suitable size to store the output r-address. Recommend at least 35 bytes.</td></tr><tr><td>write_len</td><td>uint32_t</td><td>Length of the output buffer.</td></tr><tr><td>read_ptr</td><td>uint32_t</td><td>Pointer to the Account ID.</td></tr><tr><td>read_len</td><td>uint32_t</td><td>The length of the input. Always 20.</td></tr></tbody></table>
{% endtab %}

{% tab title="Javascript" %}
<table><thead><tr><th>Name</th><th width="82">Type</th><th>Description</th></tr></thead><tbody><tr><td>accountid</td><td>number[]/string</td><td>The HEX account ID to return as r-address, can be provided as an array of numbers or a string.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                             |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written (the length of the output r-address).<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>INVALID_ARGUMENT</code><br>- <code>read_len</code> was not 20.<br><br><code>TOO_SMALL</code><br>- <code>write_len</code> was not large enough to store produced r-address in.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type          | Description                                                                               |
| ------------- | ----------------------------------------------------------------------------------------- |
| string/number | ErrorCode if there is an error in formatting, otherwise returns the r-address as a string |
{% endtab %}
{% endtabs %}

