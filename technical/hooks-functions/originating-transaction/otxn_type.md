---
description: Get the Transaction Type of the originating transaction
---

# otxn\_type

### Behaviour

* Return the Transaction Type of the originating transaction

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t otxn_type (
    void
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function otxn_type(): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t tt = 
  otxn_type();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const tt = txn_type()
```
{% endtab %}
{% endtabs %}

### Parameters

None

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                         |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | The Transaction Type of the originating transaction. Check the table below for a list of known Transaction Types at time of writing |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                                                       |
| ------------------- | --------------------------------------------------------------------------------- |
| ErrorCode \| number | Returns the Transaction Type as a number, or an ErrorCode if the retrieval fails. |
{% endtab %}
{% endtabs %}



### Known Transaction Types

| Name                            | Value |
| ------------------------------- | ----- |
| ttPAYMENT                       | 0     |
| ttESCROW\_CREATE                | 1     |
| ttESCROW\_FINISH                | 2     |
| ttACCOUNT\_SET                  | 3     |
| ttESCROW\_CANCEL                | 4     |
| ttREGULAR\_KEY\_SET             | 5     |
| ttOFFER\_CREATE                 | 7     |
| ttOFFER\_CANCEL                 | 8     |
| ttTICKET\_CREATE                | 10    |
| ttTICKET\_CANCEL                | 11    |
| ttSIGNER\_LIST\_SET             | 12    |
| ttPAYCHAN\_CREATE               | 13    |
| ttPAYCHAN\_FUND                 | 14    |
| ttPAYCHAN\_CLAIM                | 15    |
| ttCHECK\_CREATE                 | 16    |
| ttCHECK\_CASH                   | 17    |
| ttCHECK\_CANCEL                 | 18    |
| ttDEPOSIT\_PREAUTH              | 19    |
| ttTRUST\_SET                    | 20    |
| ttACCOUNT\_DELETE               | 21    |
| ttHOOK\_SET                     | 22    |
| ttURITOKEN\_MINT                | 45    |
| ttURITOKEN\_BURN                | 46    |
| ttURITOKEN\_BUY                 | 47    |
| ttURITOKEN\_CREATE\_SELL\_OFFER | 48    |
| ttURITOKEN\_CANCEL\_SELL\_OFFER | 49    |
| ttGENESIS\_MINT                 | 96    |
| ttIMPORT                        | 97    |
| ttCLAIM\_REWARD                 | 98    |
| ttINVOKE                        | 99    |
| ttAMENDMENT                     | 100   |
| ttFEE                           | 101   |
| ttUNL\_MODIFY                   | 102   |
| ttEMIT\_FAILURE                 | 103   |
| ttUNL\_REPORT                   | 104   |
