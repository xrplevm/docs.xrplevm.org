# Deploy the Smart Contract

Deploying a smart contract on the **XRPL Ethereum Virtual Machine (EVM)** sidechain can be accomplished using two popular tools: **Remix IDE** and **Hardhat**. This guide will provide a complete walkthrough for both methods.

---

## Option 1: Deploy Using Remix IDE

Remix is a web-based development environment for smart contracts, perfect for quick deployments and testing.

### Steps:

### 1. Set Up Your Wallet
- **Install MetaMask**:
  If you haven't already, install the [MetaMask wallet](https://metamask.io/) extension in your browser.
- **Connect to XRPL EVM Sidechain**:
  Add the XRPL EVM network to MetaMask:
  - **Network Name**: XRPL EVM Devnet
  - **RPC URL**: [https://rpc.xrplevm.org](https://rpc.xrplevm.org)
  - **Chain ID**: 1440002
  - **Currency Symbol**: XRP
  - **Block Explorer URL**: [https://explorer.xrplevm.org](https://explorer.xrplevm.org)

### 2. Open Remix IDE
- Navigate to [Remix IDE](https://remix.ethereum.org/).

### 3. Write or Import Your Smart Contract
- Write your Solidity smart contract or import an existing one. Example:
  ```solidity
  // SPDX-License-Identifier: MIT
  pragma solidity ^0.8.0;

  contract HelloWorld {
      string public message;

      constructor(string memory _message) {
          message = _message;
      }

      function setMessage(string memory _message) public {
          message = _message;
      }
  }
  ```

### 4. Compile the Contract
- In Remix, navigate to the **Solidity Compiler** tab.
- Select the appropriate Solidity version and click **Compile**.

### 5. Deploy the Contract
- Go to the **Deploy & Run Transactions** tab.
- Select **Injected Web3** as the environment (this will connect Remix to MetaMask).
- Ensure MetaMask is connected to the XRPL EVM network.
- Click **Deploy**, approve the transaction in MetaMask, and wait for the contract to be deployed.

### 6. Verify Deployment
- After deployment, you can interact with the contract directly in Remix or view the deployed contract on the [XRPL EVM Explorer](https://explorer.xrplevm.org) using the contract address.

---

## Option 2: Deploy Using Hardhat

Hardhat is a development framework for Ethereum-compatible smart contracts, ideal for larger projects and automation.

### Steps:

### 1. Set Up Your Development Environment
- **Install Node.js**:
  Download and install [Node.js](https://nodejs.org/).
- **Install Hardhat**:
  Create a new project folder and install Hardhat:
  ```bash
  mkdir my-hardhat-project
  cd my-hardhat-project
  npm init -y
  npm install --save-dev hardhat
  ```
- **Create a Hardhat Project**:
  ```bash
  npx hardhat
  ```
  Select "Create a basic sample project" and follow the prompts.

### 2. Configure the Network
- Open the `hardhat.config.js` file and add the XRPL EVM network:
  ```javascript
  require("@nomiclabs/hardhat-ethers");

  module.exports = {
    solidity: "0.8.0",
    networks: {
      xrplEVM: {
        url: "https://rpc.xrplevm.org",
        accounts: ["<YOUR_PRIVATE_KEY>"] // Replace with your wallet private key
      }
    }
  };
  ```

> **Warning**: Never share your private key publicly. Use environment variables to manage sensitive information.

### 3. Write Your Smart Contract
- Create a new file in the `contracts` folder, e.g., `HelloWorld.sol`.
- Write or paste your Solidity smart contract (e.g., the `HelloWorld` contract provided earlier).

### 4. Compile the Contract
- Run the following command to compile your contract:
  ```bash
  npx hardhat compile
  ```

### 5. Deploy the Contract
- Create a new script in the `scripts` folder, e.g., `deploy.js`:
  ```javascript
  async function main() {
    const [deployer] = await ethers.getSigners();

    console.log("Deploying contracts with the account:", deployer.address);

    const HelloWorld = await ethers.getContractFactory("HelloWorld");
    const helloWorld = await HelloWorld.deploy("Hello, XRPL!");

    await helloWorld.deployed();

    console.log("HelloWorld deployed to:", helloWorld.address);
  }

  main()
    .then(() => process.exit(0))
    .catch((error) => {
      console.error(error);
      process.exit(1);
    });
  ```
- Deploy the contract:
  ```bash
  npx hardhat run scripts/deploy.js --network xrplEVM
  ```

### 6. Verify Deployment
- Check the contract address in the terminal output.
- View the deployed contract on the [XRPL EVM Explorer](https://explorer.xrplevm.org) using the contract address.

---

## Conclusion

Both **Remix IDE** and **Hardhat** provide powerful tools for deploying smart contracts on the XRPL EVM. Remix is ideal for quick testing and learning, while Hardhat offers a robust framework for complex projects. Choose the method that best suits your needs and start building innovative decentralized applications (dApps) on the XRPL EVM Sidechain.

