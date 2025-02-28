# Hook API Conventions

### Naming conventions

All Hook APIs follow a standard naming convention:

|           |                 |              |                 |
| --------- | --------------- | ------------ | --------------- |
| namespace | \[ \_ noun #1 ] | \[ \_ verb ] | \[ \_ noun #2 ] |

This may look confusing at first but is actually quite simple:

* If the first noun is missing then it is implicitly the same as the namespace
* If the verb is missing then it is implicitly `get`

Thus:

* `state()` means: fetch a hook state.
* `state_set()` means: set a hook.
* `state_foreign()` means: fetch a foreign hook state.

### Memory model

Each Hook executes as a singular stack frame. All working memory must exist within this stackframe. There is no heap and no dynamic memory.

When Hooks communicate with `xahaud` they can only pass _integer_ values. Typically these integers are pointers within the Hook's memory. Since the Hook runs within xahaud, these points can then be resolved by xahaud and written to or read from as needed to perform the Hook API function.

### Allowed functions

Only two functions are allowed within a Hook: `hook()` and `cbak()`. Read about this [here](../../../concepts/compiling-hooks.md)

### Parameters

{% tabs %}
{% tab title="C" %}
All parameters passed to a Hook API must be one of: `uint32_t, int32_t, uint64_t, int64_t`. Typically these are pointers and lengths of buffers within the Hook's stack frame. Sometimes they are [Integer Encoded Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md) or other data.

The parameters to a Hook API are always in the following order:

1. Writing pointer _if any_
2. Writing length _if any_
3. Reading pointer _if any_
4. Reading length _if any_
5. Specifics / other fields _if any_

Some Hook APIs may only write or may only read from memory, and some might not do either and return a value only by return code.
{% endtab %}

{% tab title="Javascript" %}
All parameters passed to a Hook API must be one of: `string, number[], bigint(xfl), object(json)`. Typically these are pointers and lengths of buffers within the Hook's stack frame. Sometimes they are [Integer Encoded Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md) or other data.

The parameters to a Hook API are always in the following order:

1. Writing variable _if any_
2. Reading variable _if any_
3. Specifics / other fields _if any_

Some Hook APIs may only write or may only read from memory, and some might not do either and return a value only by return code.
{% endtab %}
{% endtabs %}



### Return codes

All Hook APIs return a _signed integer_. Read about return codes here: [Return codes](return-codes.md)
