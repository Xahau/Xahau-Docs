---
description: Write an integer to the Xahaud trace log
---

# trace\_num

### Behaviour

* Write an integer to the trace log along with a message (if any)

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t trace_num (
    uint32_t mread_ptr,
    uint32_t mread_len,
    int64_t number 
);
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
#define SBUF(str) (uint32_t)(str), sizeof(str)
trace_num(SBUF("This is an integer"), 10);
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
| number     | int64\_t  | The number.                                                                                               |
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

