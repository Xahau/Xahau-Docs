# L2 Distribution Hook

These are the instructions to install a distribution hook on your L2 table.

{% hint style="danger" %}
PLEASE REVIEW THE HOOK CODE FIRST BEFORE INSTALLING.
{% endhint %}

{% hint style="danger" %}
DO NOT INSTALL THIS HOOK ON IF YOU ARE AN L1 SEAT
{% endhint %}

## Using Governance XApp

Prerequisites:

* Validator Running
* Validator Rekeyed (SetRegularKey)
* Validator Account as "ReadOnly" in Xumm
* Rekeyed Account as "Full" in Xumm

Open the Governance Xapp.&#x20;

1. Select "Add Topic"
2. Enter the Hook Position #1
3. Copy the distribution hook hash below and paste as "Hash" `78CA3F5BD3D4F7B32A6BEBB3844380A9345C9BA496EFEB30314BDDF405D7B4B3`
4. &#x20;The `Destination` should be the genesis account `rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh`

[`https://github.com/Xahau/xahaud/blob/dev/hook/mint.c`](https://github.com/Xahau/xahaud/blob/dev/hook/mint.c)

