# ⛓️ Blockchain Systems: Getting Started

## Prerequisites

- ✅ Completed **04-green-belt** from core belts
- ✅ Comfortable with cryptography concepts
- ✅ Understanding of distributed systems
- ✅ Basic knowledge of cryptocurrency (Bitcoin, Ethereum)

## What You'll Build

### Orange Belt Projects

1. **Smart Contract**: Write and deploy a simple smart contract (token, NFT, or basic DeFi)
2. **Blockchain Interaction**: Query blockchain data, send transactions
3. **Transaction Analysis**: Understand how transactions work
4. **Consensus Simulation**: Simulate PoW or PoS consensus mechanism

### Green Belt Projects

1. **DeFi Protocol**: Build a simple lending or AMM protocol
2. **Cross-Chain Bridge**: Enable asset transfer between chains
3. **Smart Contract Security**: Audit and fix vulnerable contracts
4. **L2 Integration**: Work with Layer 2 scaling solutions

## Tech Stack Setup

### Minimal (to start)

- **Blockchain**: Ethereum testnet (free ETH for testing)
- **Language**: Solidity (most popular)
- **Tools**: Remix IDE (browser-based)
- **Interaction**: Ethers.js (JavaScript library)

### Full (production)

- **Blockchain**: Ethereum mainnet or Layer 2 (Arbitrum, Optimism)
- **Language**: Solidity + Rust (Solana) for comparison
- **Tools**: Foundry (smart contract dev toolkit)
- **Interaction**: web3.py or ethers.js
- **Testing**: pytest, Foundry tests
- **Deployment**: Hardhat, Safe (for multi-sig)

## Getting Started

### Step 1: Set Up a Testnet Account

1. Install MetaMask browser extension
2. Create a new wallet (or import existing)
3. Switch to Sepolia testnet
4. Get free testnet ETH from faucet (https://sepoliafaucet.com)

### Step 2: Deploy Your First Smart Contract

Use Remix IDE (no setup needed):

1. Go to https://remix.ethereum.org
2. Create new file `HelloWorld.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract HelloWorld {
    string public message = "Hello, Blockchain!";
    
    function getMessage() public view returns (string memory) {
        return message;
    }
    
    function setMessage(string memory newMessage) public {
        message = newMessage;
    }
}
```

3. Compile and deploy to Sepolia testnet
4. Interact with contract via Remix

### Step 3: Understand What Just Happened

- Your contract is now on the blockchain (forever)
- Every state change costs gas (ETH)
- Anyone can call `getMessage()` (reads are free)
- Calling `setMessage()` costs gas (state change)

### Step 4: Start Orange Belt

Begin with [03-orange-belt/lessons.md](03-orange-belt/lessons.md).

You now have:
- [ ] A testnet wallet
- [ ] Deployed your first smart contract
- [ ] Understand blockchain basics
- [ ] Ready to learn blockchain systems engineering
