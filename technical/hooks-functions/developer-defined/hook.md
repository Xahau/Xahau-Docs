---
description: The main function of your hook
---

# hook

### Concepts

* [Compiling Hooks](../../../concepts/compiling-hooks.md)

### Behaviour

* `hook` is a user defined function called by `xahaud` in order to fire your hook.
* Your `hook` function calls either `accept` or `reject` to pass or reject the originating transaction.
* If execution reaches the end of the function it is implicitly an `accept`.

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t hook (
    uint32_t reserved
)
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
type Hook = (reserved?: number) => number
```


{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t hook(uint32_t reserved)
{
  return 0;
}
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
export const Hook = (reserved: number) => {
    return 0
}
```
{% endtab %}
{% endtabs %}

### Parameters

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th width="183">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>reserved</td><td>uint32_t</td><td>Reserved for future use.</td></tr></tbody></table>


{% endtab %}

{% tab title="Javascript" %}
<table><thead><tr><th width="183">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>reserved</td><td>number</td><td>Reserved for future use.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | An arbitrary return code you wish to return from your hook. This will be present in the metadata of the originating transaction. |


{% endtab %}

{% tab title="Javascript" %}
| Type   | Description                                                                                                                      |
| ------ | -------------------------------------------------------------------------------------------------------------------------------- |
| number | An arbitrary return code you wish to return from your hook. This will be present in the metadata of the originating transaction. |
{% endtab %}
{% endtabs %}

