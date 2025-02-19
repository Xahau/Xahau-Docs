---
description: Compute an sha512-half over some data
---

# util\_sha512h

### Behaviour

{% tabs %}
{% tab title="C" %}
* Compute an `SHA512` hash over the data pointed to by `read_ptr`
* Write the first half of the hash to `write_ptr`
{% endtab %}

{% tab title="Javascript" %}
* Compute an `SHA512` hash over the data pointed to by `data`
* Return the first half of the hash
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t util_sha512h (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t read_ptr,
    uint32_t read_len
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function util_sha512h(data: ByteArray | HexString): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}

### Example

C

{% tabs %}
{% tab title="C" %}
```c
uint8_t hash_out[32];
if (util_sha512h(hash_out, 32, data_in_ptr, data_in_len) < 0)
	rollback("Could not generate Hash", 23, 1);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
util_sha512h(data)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th>Name</th><th width="114">Type</th><th>Description</th></tr></thead><tbody><tr><td>write_ptr</td><td>uint32_t</td><td>Pointer to a buffer the hash will be written to</td></tr><tr><td>write_len</td><td>uint32_t</td><td>Length of output buffer, should be at least 32.</td></tr><tr><td>read_ptr</td><td>uint32_t</td><td>Pointer to the buffer data will be read from (to compute the hash over)</td></tr><tr><td>read_len</td><td>uint32_t</td><td>Length of input data</td></tr></tbody></table>


{% endtab %}

{% tab title="Javascript" %}


<table><thead><tr><th>Name</th><th width="114">Type</th><th>Description</th></tr></thead><tbody><tr><td>data</td><td>ByteArray or HexString</td><td>The data to compute the hash over, can be provided as an array of numbers or a string.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th width="137">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>The number of bytes written, should always be 32.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- Output buffer isn't large enough</td></tr></tbody></table>


{% endtab %}

{% tab title="Javascript" %}
<table><thead><tr><th width="137">Type</th><th>Description</th></tr></thead><tbody><tr><td>ByteArray</td><td>ErrorCode if there is an error in computing the hash, otherwise returns the SHA512-half hash as an array of numbers.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

