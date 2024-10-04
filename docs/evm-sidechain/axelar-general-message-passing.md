---
html: axelar-general-message-passing.html
blurb: Learn more about Axelar general message passing.
labels:
  - Interoperability
status: not_enabled
---
# Axelar General Message Passing (GMP)

## Feature Overview

Axelar General Message Passing (GMP) is a cross-chain communication protocol that allows arbitrary data and function calls to be transmitted securely across different blockchain networks. Through GMP, smart contract execution on one chain can be triggered from another, enabling interoperability beyond simple token transfers.

For the XRPL Ledger, this integration unlocks smart contract functionality by bridging it to the XRPL EVM Sidechain. Specifically, when a transaction on XRPL needs to initiate a smart contract on the EVM Sidechain, Axelar acts as the relay layer, verifying the message, ensuring consensus, and executing the command on the EVM side. This seamless interaction empowers XRPL with access to EVM-compatible DeFi protocols, automated workflows, and complex dApps, expanding its utility and ecosystem capabilities.

## How It Works

The Axelar GMP protocol operates as follows:

![xrpl-evm-sidechain-axelar-gmp](../img/evm-sidechain-axelar-gmp.png)

1. **Message Construction**: On XRPL, a message is constructed with the destination chain, contract address, and the function call to be executed. This message is submitted as a XRPL Payment transaction to the Axelar Multisig account.
2. **Message Submission and Verification**: The message is submitted to the Axelar network, where it is verified and relayed to the destination chain, which corresponds to the XRPL EVM Sidechain. Once relayed, the Axelar amplifier gateway approves the message.
3. **Call smart contract function**: The Axelar relayer executes the message on the desired smart contract on the XRPL EVM Sidechain.

## Key Components


- **Axelar Multisig Account**: The Axelar Multisig account is the account that is responsible for submitting the message to the Axelar network (from XRPL Ledger).
- **Axelar Amplifier Gateway**: The Axelar Amplifier Gateway is the smart contract which communicates with the Axelar network, enabling the message passing functionality.
- **XRPL EVM Sidechain**: The XRPL EVM Sidechain is the destination for the message, which corresponds to the XRPL EVM Sidechain.
- **XRPL Ledger**: The XRPL Ledger is the source of the message, which corresponds to the XRPL Ledger.

## Example

