````markdown
# Blockchain - Green Belt Lessons

## Lesson 1: Upgradeable Smart Contracts

### Core Concepts
- Proxy patterns (transparent, UUPS, diamond)
- Storage layout stability and gaps
- Initializers vs constructors
- Access control for upgrades

### Implementation (Solidity)
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import {UUPSUpgradeable} from "@openzeppelin/contracts/proxy/utils/UUPSUpgradeable.sol";
import {OwnableUpgradeable} from "@openzeppelin/contracts-upgradeable/access/OwnableUpgradeable.sol";

contract Vault is UUPSUpgradeable, OwnableUpgradeable {
    uint256 public totalAssets;
    uint256[49] private __gap; // storage gap for future upgrades

    function initialize() public initializer {
        __Ownable_init();
        totalAssets = 0;
    }

    function deposit(uint256 amount) external {
        totalAssets += amount;
    }

    function _authorizeUpgrade(address) internal override onlyOwner {}
}
```

---

## Lesson 2: Security and Invariants

### Core Concepts
- Reentrancy, checks-effects-interactions
- Access control and circuit breakers
- Fuzzing and invariants
- Static analysis (Slither) and audit checklists

### Invariant Example (Foundry)
```solidity
function invariant_totalAssetsNonNegative() public {
    assert(vault.totalAssets() >= 0);
}
```

### Threat Modeling
- Identify assets, roles, and trust boundaries
- Enumerate threats (spoofing, tampering, reentrancy)
- Document mitigations and assumptions

---

## Lesson 3: DeFi Mechanics

### Core Concepts
- AMM math (constant product), fees, slippage
- Oracle design (median, TWAP) and manipulation risks
- Liquidations and health factors

### AMM Snippet
```solidity
function getAmountOut(uint256 amountIn, uint256 reserveIn, uint256 reserveOut) public pure returns (uint256) {
    uint256 amountInWithFee = amountIn * 997; // 0.3% fee
    uint256 numerator = amountInWithFee * reserveOut;
    uint256 denominator = reserveIn * 1000 + amountInWithFee;
    return numerator / denominator;
}
```

### Liquidation Check (TypeScript)
```ts
function isLiquidatable(healthFactor: number): boolean {
  return healthFactor < 1.0;
}
```

---

## Lesson 4: Scalability and L2

### Core Concepts
- Rollups (optimistic vs zk), finality, fraud proofs
- Bridge risks: replay, message ordering, censorship
- Gas optimization patterns and calldata efficiency

### L2 Deployment Checklist
- Verify compiler and opcode support
- Estimate calldata and storage costs
- Add retry/backoff for L2 RPC providers
- Monitor bridge message status

---

## Lesson 5: Observability and Operations

### Core Concepts
- Event design for analytics and alerts
- Node health, reorg detection, fork choice
- MEV awareness and mitigation

### Monitoring Snippet (TypeScript)
```ts
import { JsonRpcProvider } from "ethers";

const provider = new JsonRpcProvider(process.env.RPC_URL!);

async function watchReorgs() {
  let lastHash = await provider.send("eth_blockNumber", []);
  provider.on("block", async (blockNumber) => {
    const block = await provider.getBlock(blockNumber);
    if (block.parentHash !== lastHash) {
      console.warn("Potential reorg detected", { blockNumber, parent: block.parentHash, expected: lastHash });
    }
    lastHash = block.hash;
  });
}
```

---

These lessons prepare you to ship secure, scalable blockchain systems.
````