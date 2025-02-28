---
description: Write a XFL float to the Xahaud trace log
---

# trace\_float

### Behaviour

* Write a XFL floating point to the trace log along with a message (if any)

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t trace_float (
    uint32_t mread_ptr,
    uint32_t mread_len,
    int64_t float1 
);
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
#define SBUF(str) (uint32_t)(str), sizeof(str)
trace_float(SBUF("This is a float"), float_one());
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                                               |
| ---------- | --------- | --------------------------------------------------------------------------------------------------------- |
| rmead\_ptr | uint32\_t | Pointer to a message to output before the hex-encoded serialized object found in the slot. _May be null._ |
| mread\_len | uint32\_t | Length of the message. _May be null._                                                                     |
| float1     | int64\_t  | The enclosing XFL integer.                                                                                |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>0</code> if successful<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
{% endtab %}
{% endtabs %}

