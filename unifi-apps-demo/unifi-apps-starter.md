---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-apps-demo/unifi-apps-starter
---

# Unifi Apps Starter

Starting Mini App development can be challenging. The Unifi Apps Starter provides a solid foundation to kickstart your project.

This template includes the essential features needed for building a Mini App, allowing you to customize and build your own application efficiently. This guide covers:

* [What is the Unifi Apps Starter?](unifi-apps-starter.md#what-is-the-unifi-apps-starter)
* [Getting Started](unifi-apps-starter.md#how-to-get-started-with-the-unifi-apps-starter) (Environment setup, Source code, Deployment)
* [Key features](unifi-apps-starter.md#key-features-of-the-unifi-apps-starter) (Wallet connection, Payments, LIFF integration)

## What is the Unifi Apps Starter?

The **Unifi Apps Starter** is a template project designed to help you easily integrate the `dapp-portal-sdk`. While you can always start your Mini App project from scratch, using this starter allows for a faster and smoother development experience.

It also follows a predefined design guide, which can help maintain consistency in UI/UX.

The project is built with **Next.js**. Even if you're planning to use a different framework, this repository can still serve as a useful reference for integrating the `dapp-portal-sdk`.<br>

## How to get started with the Unifi Apps Starter Environment

The Unifi Apps Starter requires **Node.js** to run. It uses `pnpm` as the package manager (compatible with `npm`).

* Recommended Node.js version: **>= 20.0.0**
* The version specified in `.nvmrc`: **v20.18.0**
* Older versions may work partially, but for compatibility with Netlify deployment tools, Node.js >= 20.0.0 is required.

\*Tip: Use [`nvm`](https://github.com/nvm-sh/nvm) to manage Node versions easily.

### Downloading and running the source code&#x20;

You can clone or fork the repository from GitHub:\
[ https://github.com/techreadiness/unifi-apps-starter](https://github.com/techreadiness/unifi-apps-starter)

To run the project locally, follow the instructions in the repository’s `README.md`.

### Deploying to a server

Once you’ve run the Unifi Apps Starter locally and verified that it's working, you can deploy it to a live server using **Netlify**:

<details>

<summary>A netlify account is required </summary>

[Netlify (opens new window)](https://www.netlify.com/)is a hosting service for static sites, open an account before deploying to Netlify. The content on this page can be run on Netlify's free plan.

</details>

```bash
# Go to the root directory
cd ./
# Build the project
pnpm build 
# Deploy to a draft (preview) environment
netlify deploy
# Once verified, deploy to production
netlify deploy --prod 
```

The official published version is available at [https://unifi-apps-starter.netlify.app.](https://unifi-apps-starter.netlify.app/)

## Key features of the Unifi Apps starter

The Unifi Apps Starter comes with several basic features implemented out of the box.\
These demonstrate how to use core functionalities from `dapp-portal-sdk`, but should be treated as **reference code**, not a final solution.

### Connect/Disconnect wallet

Connecting and disconnecting a wallet is the most fundamental feature when using the SDK.\
In the code, you’ll find how to use `walletProvider` and its methods.

**reference code**\
[functions related to wallet connect and disconnect](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Wallet/Sdk/walletSdk.hooks.ts#L58)

### Wallet Session Persistence

You can first check whether a login session exists by calling\
`walletProvider.request({ method: 'kaia_accounts' })`, so that the wallet session remains active after a user logs in once for convenience.<br>

**reference code**\
[maintaining session using kaia\_accounts](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/app/page.tsx#L15)

### Crypto/Fiat payment

The template shows how to handle both **crypto** and **fiat** payments using `paymentProvider`.

You can see examples of:

* Creating paymentId
* Checking the payment status
* Finalizing the payment

**reference code**

[functions related to payment](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Store/Sdk/paymentSdk.hooks.ts#L39)

### KAIA/STRIPE ratio

To support payments, your Mini App needs to apply proper price conversion logic between **crypto (KAIA)** and **fiat (STRIPE)**.\
The starter includes a `usd-to-kaia` function as a reference.\
\
**reference code**\
[usd to kaia conversion](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/app/api/usd-to-kaia/route.ts#L3)

### KAIA/USDT balance

The template shows how to get balance of both kaia and erc20 based token.\
\
**reference code**\
[kaia balance](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Wallet/Sdk/walletSdk.hooks.ts#L87)\
[USDT balance](https://github.com/techreadiness/unifi-apps-starter/blob/012e7939a9971df38ff07eb7f2ef9b7621ad81f2/src/app/store/page.tsx#L28) \
[erc20token balance](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Wallet/Sdk/walletSdk.hooks.ts#L100)

### Smart Contract based USDT transfer

&#x20;The USDT transfer via smart contract is implemented.&#x20;

**reference code**

[transfer parameter ](https://github.com/techreadiness/unifi-apps-starter/blob/70542b9430b34bfdbce35683c7d896d57007d704/src/components/Wallet/Sdk/walletSdk.hooks.ts#L51)\
[USDT smart contract](https://github.com/techreadiness/unifi-apps-starter/blob/main/src/utils/smartContract.ts)

### LIFF integration

If you're planning to integrate with **LINE Front-end Framework (LIFF)**, this project includes useful examples such as:

* When to initialize LIFF
* How to use methods like `shareTargetPicker`

**reference code**

[liff initialization](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Wallet/Sdk/walletSdk.hooks.ts#L38)\
[shareTargetPicker method](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Invitation/Invitation.hooks.ts#L4)
