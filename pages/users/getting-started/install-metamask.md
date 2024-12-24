# Install MetaMask

MetaMask is a browser extension and wallet for accessing decentralized applications (dApps) on EVM-compatible chains. It allows users to interact with blockchain networks directly from their browser, making it an essential tool for interacting with the XRPL EVM sidechain.

## Attention

The XRPL EVM-compatible sidechain implementation is a **proof of concept** extension to the XRP Ledger protocol and is intended for development purposes only. It is currently connected to the **XRPL Devnet** and not the production mainnet. **Do not send transactions in Mainnet.**

This guide explains how to install MetaMask. For configuring it for XRPL EVM, refer to the "Connect MetaMask to the XRPL EVM Sidechain" guide.

---

## 1. Installing MetaMask

To begin, download and install the MetaMask extension for your browser:

1. Visit [metamask.io](https://metamask.io/download/).
2. Select your preferred browser (Chrome, Firefox, Brave, or Edge) and follow the installation instructions.

<Insert Screenshot of the MetaMask Download Page>

Once installed, a MetaMask icon will appear in your browser's toolbar.

---

## 2. Create an Account on MetaMask

Follow these steps to create a new MetaMask wallet:

1. Click the MetaMask icon in your browser.
2. Click **"Create a Wallet."**
3. Secure your wallet:
   - Save the **seed phrase** provided by MetaMask in a safe location. This is the only way to recover your wallet if you lose access to it.
   - **Never share your seed phrase with anyone.**
   <Insert Screenshot Showing the Seed Phrase and Warning>
4. Set a password and click **"Create."**

Your MetaMask wallet is now ready to use.

<Insert Screenshot of the Wallet Interface after Creation>

---

## 3. Import an Existing Account (Optional)

If you already have an XRPL EVM-compatible account, you can import it into MetaMask using its private key:

1. Open MetaMask and click the account icon in the top-right corner.
2. Select **"Import Account."**
3. Enter your private key and click **"Import."**

Your existing account will now be accessible in MetaMask.

<Insert Screenshot of Import Account Screen>

---

## Notes for Developers

MetaMask injects the XRPL EVM sidechain Web3 API into every website's JavaScript context. This allows dApps to interact seamlessly with the XRPL EVM blockchain.

If you encounter any issues, ensure that you are on the latest version of MetaMask. Additionally, remember that this is a **Devnet environment**, so it should only be used for testing and development purposes.

For configuring MetaMask to connect to XRPL EVM, see the "Connect MetaMask to the XRPL EVM Sidechain" documentation.
