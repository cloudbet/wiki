---
title: 'Depositing Funds: Payments & Networks'
linkTitle: Depositing Funds
description: This guide explains the key concepts to help you manage your funds and deposits.
type: docs
weight: 2
---

When making cryptocurrency deposits on Cloudbet, it's useful to understand the terminology and processes to ensure smooth and secure transactions.

Start by choosing the currency you wish to deposit from the available list (e.g., USDT). Next, select the appropriate network, such as Ethereum, to match the currency. You will receive a deposit address specific to your choices. Use the provided address or QR code in your wallet to send the assets. Ensure that the network in your wallet matches the network of the deposit address. Your funds will be credited to your Cloudbet account as soon as the transaction is verified.

![Deposit with Cloudbet](/wiki/images/cloudbet-deposit.png)

### Currency

A "currency" is the cryptocurrency or token you are transacting, such as BTC, USDT, ETH, and others. Each asset can exist on multiple networks, and choosing the correct network is a requirement for successful transactions.

### Network

The "network" denotes the blockchain network used for your transactions. Popular networks include Ethereum, BNB Smart Chain, Avalanche, Solana, Polygon, and TRON, each with unique characteristics and supported assets.

### Deposit Address

The "deposit address" is the specific address on a blockchain network where transactions are directed. Each network and asset type has a distinct address, and using the correct one ensures your funds reach their intended destination.

## Common Mishaps and How to Avoid Them

### Sending Assets to the Wrong Network

A common error during the deposit or withdrawal process occurs when cryptocurrency is sent to a technically correct address that belongs to a different blockchain network than intended. For instance, if you deposit USDT (ERC-20), which is native to the Ethereum network, into an address on the BNB Smart Chain that supports the same token format, the transaction will process, but the funds will not appear in your Ethereum-based wallet. This issue arises from network incompatibility, despite the address's validity. To prevent such errors, always ensure that both the token and the network selected for your transaction are exactly supported by and correspond to the specifications of the receiving wallet. Avoid losing your assets due to network discrepancies.

### Wrong Address Format

Using an incorrect address format for the selected network can lead to lost funds. For instance, sending Wrapped Bitcoin (WBTC), which operates on the Ethereum network, to a native Bitcoin (BTC) address is a mistake with irreversible consequences. Despite similar address styles between BTC and WBTC, they are fundamentally incompatible for direct transfers. For example, any Ethereum-based asset sent to an address like `0x3aD7NdddXXjsbYh8bC4xjnpUXqqdXHKSHy`, mistaken for a Bitcoin P2SH address  `3aD7NdddXXjsbYh8bC4xjnpUXqqdXHKSHy`, will result in the irretrievable loss of tokens.

### Human Error

Errors such as copying and pasting incorrect addresses or selecting the wrong options can lead to the irreversible loss of funds. To prevent this, always double-check all transaction details before confirming.
