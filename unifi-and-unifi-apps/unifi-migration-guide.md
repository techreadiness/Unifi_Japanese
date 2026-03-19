---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-and-unifi-apps/unifi-migration-guide
---

# Unifi Migration Guide

## Wallet Function Updates

#### Effective Date: February 12, 2026, 11:00 AM (UTC+0)

Dear Developers,

This notice is to inform you that Dapp Portal will be rebranded as Unifi.

Along with the rebranding, the Wallet functionality will be updated and certain actions are required to ensure your Apps continue operating smoothly.

#### Concept of Unifi Rebranding

<table><thead><tr><th width="166.141357421875">AS-IS</th><th width="166.203857421875">TO-BE</th><th>NOTE</th></tr></thead><tbody><tr><td>Dapp Portal</td><td>Unifi</td><td></td></tr><tr><td>Mini Dapp</td><td>Unifi Apps</td><td></td></tr><tr><td>Mini Dapp SDK</td><td>Unifi Apps SDK</td><td>No change in the SDK Library name<br>(~/@linenext/dapp-portal-sdk)</td></tr><tr><td>Dapp Portal Wallet</td><td>Unifi Wallet</td><td></td></tr></tbody></table>

## Overview of Unifi

Unifi is a stablecoin wallet built on the Kaia blockchain.

After user registration and Approve authorization, it provides an automatic deposit service.

* Auto-deposit target at launch: USDT
* Other assets (e.g., KAIA, BORA) remain supported but are not eligible for auto-deposit.

Once a Dapp Portal user migrates to Unifi:

* The user's on-chain USDT balance may appear as zero
* All USDT will be automatically deposited into Unifi's account pool

Developers must query the Unifi account balance, not only the on-chain balance. Therefore, Developers using USDT must follow the steps below.

## SDK Version Update Required

The new SDK version that supports Unifi is **v1.5.2**. Please update your SDK to this version.

If not updated:

* USDT Payments via PaymentProvider will fail due to insufficient balance
* Auto-deposited USDT will not be detected

Please update to the Unifi-compatible SDK as soon as it becomes available.

#### Note

By using the PaymentProvider, USDT payments can be executed using the balance automatically deposited in the Unifi account simply by updating the SDK version without modification.

Other functionalities guarantee compatibility with the Unifi Apps SDK, so no changes are required.

## Updated USDT Balance Query Method

* AS-IS: Queries on-chain USDT only

`getErc20TokenBalance()`

* TO-BE: Queries on-chain + Unifi deposit balance

`getErc20TokenBalanceWithDepositedBalance()`

## Smart Contract-Based USDT Transfer Changes

<figure><img src="../.gitbook/assets/USDT_Transfer (2).png" alt=""><figcaption></figcaption></figure>

For USDT transfers implemented via smart contract including Swap, Developers must include `depositTokenAddress` and `depositAmount` in the `kaia_sendTransaction` request.

Changes are required when the walletType is WEB or LIFF. If the walletType is OKX, BITGET, Extension or Mobile developers can use the AS-IS parameters.

* AS-IS

```
params = {
typeInt: 48,
from: "walletAddress",
to: "contractAddress",
value: "0x0",
input: "0xabcd..."
}
```

* TO-BE

```
params = {
typeInt: 48,
from: "walletAddress",
to: "contractAddress",
value: "0x0", // Kaia Amount
input: "0xabcd...",
depositTokenAddress: "0xd077a400968890eacc75cdc901f0356c943e4fdb", // USDT contract address
depositAmount: "1000000", // Amount of USDT to transfer as token decial. 1 USDT = 1000000
gas: "0x30D40" // We recommend hard-coding the gas limit to approximately 200,000
}
```

* Ref.&#x20;
  * Contract Address of USDT on Kaia: `0xd077a400968890eacc75cdc901f0356c943e4fdb`&#x20;
  * Gas: Gas estimation is not possible due to an 'execution revert' error because USDT in Unifi Wallet is fully deposited into interest vault.&#x20;

## Modify Browser Tab Name

* AS-IS: {dapp\_name} | Mini Dapp
* TO-BE: {dapp\_name} | Unifi Apps

## Modify Connect Button for Unifi

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

{% file src="../.gitbook/assets/Unifi_Symbol_400x400.svg" %}

{% file src="../.gitbook/assets/Unifi_Symbol_400x400.png" %}

## Update OA Rich Menu for Unifi

<figure><img src="../.gitbook/assets/OA_Richmenu_Unifi (1).png" alt="" width="563"><figcaption></figcaption></figure>

* Replace the **Dapp Portal logo** in the OA Rich Menu with the **Unifi logo**.
* The LIFF URL remains unchanged: [https://liff.line.me/2006533014-8gD06D64](https://liff.line.me/2006533014-8gD06D64)

{% file src="../.gitbook/assets/Unifi_Logo_Primary_512_512 (2).png" %}

{% file src="../.gitbook/assets/Unifi_Logo_Primary_1024_1024.svg" %}
