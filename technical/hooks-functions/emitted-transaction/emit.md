---
description: Prepares a JSON transaction for emission.
---

# prepare

### Concepts

* [Transactions](../../protocol-reference/transactions/)

### Behaviour

{% tabs %}
{% tab title="Javascript" %}
* This function takes a transaction JSON object and prepares it for emission.
* The transaction must be complete except for the Account field, which should always be the Hook account.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="Javascript" %}
```javascript
function prepare(
    txJson: Record<string, any> | Transaction
  ): ErrorCode | Record<string, any> | Transaction
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="Javascript" %}
```javascript
const prepared_txn = prepare({
                TransactionType: "Payment",
                Destination: util_raddr(p1address_ns),
                Amount: parseFloat(drops_sent)*2
            })
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="Javascript" %}


<table><thead><tr><th>Name</th><th width="124">Type</th><th>Description</th></tr></thead><tbody><tr><td>txJson</td><td>Record&#x3C;string, any> | Transaction</td><td>The transaction JSON, must be a complete transaction except for Account (always the Hook account).</td></tr></tbody></table>
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="Javascript" %}


<table><thead><tr><th width="231">Type</th><th>Description</th></tr></thead><tbody><tr><td>ErrorCode | Record&#x3C;string, any> | Transaction</td><td>Returns an ErrorCode if there is an error, or the prepared transaction JSON or Transaction object.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

