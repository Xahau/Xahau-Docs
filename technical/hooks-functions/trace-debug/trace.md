---
description: Write the contents of a buffer to the Xahaud trace log
---

# trace

### Behaviour

* Write a buffer from inside the Hook to the trace log along with a message (if any)

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t trace (
    uint32_t mread_ptr,
    uint32_t mread_len,
    uint32_t dread_ptr,
    uint32_t dread_len,
    uint32_t as_hex
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function trace(
    message: string | null,
    data: any,
    hex: boolean | 0 | 1
  ): ErrorCode
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
#define SBUF(str) (uint32_t)(str), sizeof(str)
trace(SBUF("Buffer conatained"), SBUF(some_buffer), 1);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
trace("Buffer conatained", some_buffer, 1);
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                                         |
| ---------- | --------- | --------------------------------------------------------------------------------------------------- |
| mread\_ptr | uint32\_t | Pointer to a message to output before the buffer. _May be null._                                    |
| mread\_len | uint32\_t | Length of the message. _May be null._                                                               |
| dread\_ptr | uint32\_t | Pointer to the buffer to output.                                                                    |
| dread\_len | uint32\_t | Length of the buffer to output.                                                                     |
| as\_hex    | uint32\_t | <p>If <code>1</code> output the buffer as hex.<br>If <code>0</code> output the buffer as utf-8.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Name    | Type    | Description                                                          |
| ------- | ------- | -------------------------------------------------------------------- |
| message | string  | The 'logging key', message to output before the buffer (can be null) |
| data    | any     | The data to log                                                      |
| hex     | boolean | <p>Should it log formatted in HEX?<br><br>0 - NO<br>1 - YES</p>      |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>0</code> if successful<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type      | Description                                                                                 |
| --------- | ------------------------------------------------------------------------------------------- |
| ErrorCode | <p>int64_t, value is 0 if successful</p><p></p><p> If negative, an error: OUT_OF_BOUNDS</p> |
{% endtab %}
{% endtabs %}

