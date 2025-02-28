---
description: Skip a hook that appears later in the hook chain on the hook account
---

# hook\_skip

### Behaviour

{% tabs %}
{% tab title="C" %}
* Search the hook chain for a hook identified by the hook hash at `read_ptr`
* Mark it as disabled for this chain execution
{% endtab %}

{% tab title="Javascript" %}
* Skip the execution of a hook based on the provided hash and flag.
* Returns a status code indicating the result of the operation.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t hook_skip (
    uint32_t read_ptr,
    uint32_t read_len,
    uint32_t flags
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function hook_skip(
    hash: ByteArray | HexString,
    flag: number
  ): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t phash[] = { 0x19U, 0xFEU, 0x69U, 0xF1U, 0x53U, 0x66U, 0x4EU, 0x8CU, 
                    0x97U, 0xF4U, 0x4CU, 0x5CU, 0x3CU, 0x65U, 0x63U, 0x79U, 
                    0xC2U, 0xD0U, 0x26U, 0xE7U, 0x90U, 0xEFU, 0x38U, 0xF7U, 
                    0xEDU, 0x73U, 0xE9U, 0xCEU, 0x9CU, 0x9DU, 0xBFU, 0x03U };
int64_t result = 
  	hook_skip(phash, 32, 0);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const phash = [ 0x19, 0xFE, 0x69, 0xF1, 0x53, 0x66, 0x4E, 0x8C, 
                0x97, 0xF4, 0x4C, 0x5C, 0x3C, 0x65, 0x63, 0x79, 
                0xC2, 0xD0, 0x26, 0xE7, 0x90, 0xEF, 0x38, 0xF7, 
                0xED, 0x73, 0xE9, 0xCE, 0x9C, 0x9D, 0xBF, 0x03 ]
const result = hook_skip(phash, 0);
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}


| Name      | Type      | Description                                                                                                   |
| --------- | --------- | ------------------------------------------------------------------------------------------------------------- |
| read\_ptr | uint32\_t | Pointer to a buffer containing the hook hash                                                                  |
| read\_len | uint32\_t | Length of the hook hash (always 32)                                                                           |
| flags     | uint32\_t | <p>If 0:<br>- add the hash to the hook skip list<br><br>If 1<br>- remove the hash from the hook skip list</p> |
{% endtab %}

{% tab title="Javascript" %}


| Name | Type                   | Description                                         |
| ---- | ---------------------- | --------------------------------------------------- |
| hash | ByteArray or HexString | The hash of the hook to skip.                       |
| flag | number                 | A flag indicating the reason for skipping the hook. |
{% endtab %}
{% endtabs %}

### Return Code

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th width="163">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>If successful <code>1</code><br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>DOESNT_EXIST</code><br>- The specified paramater doesn't exist or is null<br><br><code>INVALID_ARGUMENT</code><br>- Hash is not 32 bytes</td></tr></tbody></table>
{% endtab %}

{% tab title="Javascript" %}
<table><thead><tr><th width="163">Type</th><th>Description</th></tr></thead><tbody><tr><td>number or ErrorCode</td><td>Returns a status code indicating the result of the operation.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

