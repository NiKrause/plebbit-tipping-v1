# Plebbit Tipping v1

This is a Solidity smart contract project using Hardhat for a decentralized tipping system called `PlebbitTippingV1`.

## Deployed Contracts

| Network      | Contract Address                                                                 |
|--------------|----------------------------------------------------------------------------------|
| Sepolia      | [0x49753cB4ff375e04D2BC2A64971F60cD1a091381](https://sepolia.etherscan.io/address/0x49753cB4ff375e04D2BC2A64971F60cD1a091381#code) |
| Amoy         | [0x49753cB4ff375e04D2BC2A64971F60cD1a091381](https://amoy.polygonscan.com/address/0x49753cB4ff375e04D2BC2A64971F60cD1a091381#code) |
| Base Sepolia | [0x49753cB4ff375e04D2BC2A64971F60cD1a091381](https://amoy.polygonscan.com/address/0x49753cB4ff375e04D2BC2A64971F60cD1a091381#code) | 


## Features
- **tip**: Allows users to send tips to other users with an optional comment.
- **getTipsTotalAmount**: Gets the total tip amount for a particular comment and fee recipients.
- **getTips**: Retrieves the list of tips for a comment.
- Access control with admin and moderator roles using OpenZeppelin's AccessControl.
- Deterministic contract address deployment across different chains.

## Prerequisites
- Node.js (preferably LTS)
- npm

## Getting Started

### Installation

1. Clone the repository:
   ```bash
   git clone <your-repo-url>
   cd plebbit-tipping-v1
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Compile the contract:
   ```bash
   npm run compile
   ```

### Running Tests

Execute the following command to run the tests:
```bash
npm test
```

### Deployment

Start a local Hardhat node:
```bash
npm run node
```

Deploy the contract locally:
```bash
npm run deploy:localhost
```

For general deployment:
```bash
npm run deploy
```

#### Running Tests on a Mainnet Fork (Ethereum)

You can run tests against a fork of the current Ethereum mainnet using Hardhat.  
You'll need an RPC URL from a provider like Alchemy or Infura.

1. Set your mainnet RPC URL as an environment variable:
   ```bash
   export MAINNET_RPC_URL="https://eth-mainnet.g.alchemy.com/v2/your-api-key"
   ```

2. Start a Hardhat node forked from mainnet:
   ```bash
   npx hardhat node --fork $MAINNET_RPC_URL
   ```

3. In a new terminal, run the tests:
   ```bash
   npm test
   ```

#### Deploying on Testnets
   ```bash
   npx hardhat deploy --network sepolia
   ```
   ```bash
   npx hardhat deploy --network amoy
   ```
   ```bash
   npx hardhat deploy --network baseSepolia
   ```

After deploying to a testnet, you can verify your contract on the relevant block explorer (Etherscan for Sepolia, Polygonscan for Amoy) using the following scripts:

```
npm run verify:sepolia -- <DEPLOYED_CONTRACT_ADDRESS> <CONSTRUCTOR_ARGS>
```

or

```
npm run verify:amoy -- <DEPLOYED_CONTRACT_ADDRESS> <CONSTRUCTOR_ARGS>
```

Replace `<DEPLOYED_CONTRACT_ADDRESS>` with your contract's address and `<CONSTRUCTOR_ARGS>` with any constructor arguments (if any).

## Contract API

### Main Functions

- `tip(address recipient, uint256 amount, address feeRecipient, bytes32 senderCommentCid, bytes32 recipientCommentCid)`
- `getTipsTotalAmount(bytes32 recipientCommentCid, address[] calldata feeRecipients)`
- `getTipsTotalAmounts(bytes32[] calldata recipientCommentCids, address[][] calldata feeRecipients)`
- `getTipsTotalAmountsSameFeeRecipients(bytes32[] calldata recipientCommentCids, address[] calldata feeRecipients)`
- `getTipsAmounts(bytes32 recipientCommentCid, address[] calldata feeRecipients, uint256 offset, uint256 limit)`
- `getTips(bytes32 recipientCommentCid, address[] calldata feeRecipients, uint256 offset, uint256 limit)`
- `getSenderTipsTotalAmount(bytes32 senderCommentCid, address sender, bytes32 recipientCommentCid, address[] calldata feeRecipients)`
- `getSenderTipsTotalAmounts(bytes32 senderCommentCid, address sender, bytes32[] calldata recipientCommentCids, address[][] calldata feeRecipients)`
- `getSenderTipsTotalAmountsSameFeeRecipients(bytes32 senderCommentCid, address sender, bytes32[] calldata recipientCommentCids, address[] calldata feeRecipients)`

### Admin Functions

- `setMinimumTipAmount(uint256 _minimumTipAmount)` - Only moderators
- `setFeePercent(uint256 _feePercent)` - Only moderators (1-20%)

## License

This project is licensed under the MIT License.
