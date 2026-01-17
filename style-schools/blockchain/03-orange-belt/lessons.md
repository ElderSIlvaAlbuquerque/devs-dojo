# ⛓️ Blockchain Systems: Orange Belt Lessons

## Module 1: Blockchain Fundamentals

### 1.1 What is a Blockchain?

A blockchain is:
- **Distributed Ledger**: Copy of transaction history on every node
- **Immutable**: Once recorded, data cannot be changed
- **Decentralized**: No single authority controls it
- **Consensus-Based**: Nodes agree on what's valid

### 1.2 Key Components

**Blocks**:
- Timestamp
- Transactions (data)
- Hash (fingerprint of this block)
- Previous hash (link to previous block)

**Chain**:
- If someone modifies an old block, its hash changes
- This breaks all subsequent blocks (obvious tampering)

**Nodes**:
- Every participant keeps a full copy
- Verify all transactions and blocks
- Consensus mechanism determines what's valid

### 1.3 Consensus Mechanisms

**Proof-of-Work (PoW)** - Bitcoin, Ethereum (pre-merge):
- Solve hard math puzzle to create block
- First one to solve gets reward
- Puzzle ensures work = security cost

**Proof-of-Stake (PoS)** - Ethereum (post-merge), Solana:
- Validators deposit coins as "stake"
- If they validate correctly, they earn rewards
- If they validate incorrectly, they lose stake
- Security comes from economic incentive, not computational work

### 1.4 Transactions

Anatomy of a transaction:
- **From**: Sender's address
- **To**: Recipient's address
- **Value**: Amount to send
- **Data**: Additional instructions (for smart contracts)
- **Gas**: Cost to execute
- **Signature**: Proof sender authorized it

---

## Module 2: Cryptography in Blockchain

### 2.1 Hashing

Hash function: Input → Fixed-size fingerprint

Properties:
- Deterministic: Same input always gives same hash
- Avalanche: Tiny input change = completely different hash
- One-way: Can't reverse hash to get input

Bitcoin uses SHA-256:
```
sha256("hello") = 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
sha256("hallo") = d3751713b7e34c5f5e8e5d9c5e8e5d9c5e8e5d9c5e8e5d9c5e8e5d9c5e8e5d9c
```

### 2.2 Merkle Trees

Efficiently hash large amounts of data:

```
        Root Hash
       /          \
    Hash AB       Hash CD
    /    \        /    \
Hash A  Hash B  Hash C  Hash D
  |       |       |       |
  A       B       C       D
```

To verify transaction C:
- Only need Hash C, Hash D, Hash AB, Root
- Other transactions can be pruned

### 2.3 Public Key Cryptography

- **Private Key**: Secret (like password), signs transactions
- **Public Key**: Derived from private key, proves you own account
- **Signature**: Proof that private key holder authorized transaction

```
Private Key: 0x1a2b3c...
Public Key: 0x9f8e7d...
Address: 0x123abc... (derived from public key)

Signature = Sign(message, private_key)
Verify(message, signature, public_key) = true/false
```

---

## Module 3: Smart Contracts

### 3.1 What Are Smart Contracts?

Programs that run on blockchain:
- Written in Solidity (Ethereum), Rust (Solana), Move (Aptos)
- Executed by every node (full state replication)
- State changes are transactions (cost gas)
- Cannot be changed once deployed

### 3.2 Contract State

Data stored on blockchain (persistent):

```solidity
contract BankAccount {
    mapping(address => uint256) balances;
    
    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }
    
    function withdraw(uint256 amount) public {
        require(balances[msg.sender] >= amount);
        balances[msg.sender] -= amount;
        payable(msg.sender).transfer(amount);
    }
}
```

### 3.3 Gas Costs

Every operation costs gas (in ETH):

```solidity
function expensiveOperation() public {
    uint256[] memory data = new uint256[](1000000);
    // Allocating large array = lots of gas
    
    for(uint i = 0; i < 1000000; i++) {
        data[i] = i;  // Each assignment costs gas
    }
    // This might cost more than available gas!
}
```

Gas optimization is critical (directly affects user cost).

---

## Module 4: Transaction Models

### 4.1 UTXO Model (Bitcoin)

- Like cash: Each bill (UTXO) can be spent once
- Transaction spends one or more UTXOs, creates new UTXOs
- Account balance = sum of your UTXOs

```
Me: Have UTXO A ($5), UTXO B ($3)
Send $6 to Alice:
  Spend UTXO A ($5) + UTXO B ($3)
  Create new UTXO for Alice ($6)
  Create new UTXO for me ($2 change)
```

### 4.2 Account Model (Ethereum)

- Like bank account: Single balance per address
- State is explicit (balance field)
- Transaction updates state

```
Me: Balance = $8
Send $6 to Alice:
  Me: Balance = $2
  Alice: Balance += $6
```

---

## Module 5: Introduction to DeFi

### 5.1 Decentralized Finance

Financial services without intermediaries:
- **Lending**: Lend crypto, earn interest
- **DEX (Decentralized Exchange)**: Trade tokens peer-to-peer
- **Staking**: Lock up tokens, earn yield
- **Derivatives**: Futures, options on blockchain

### 5.2 Automated Market Maker (AMM)

Simple way to trade without order book:

```
Pool has: 100 ETH, 200,000 USDC

Want to swap 10 ETH for USDC:
Formula: ETH * USDC = constant
(100 + 10) * (200,000 - X) = 100 * 200,000
110 * (200,000 - X) = 20,000,000
X = 18,181.82 USDC
```

Result: 10 ETH → 18,181 USDC (price changes with pool balance)

### 5.3 Smart Contract Risks

- **Reentrancy**: Calling function before updating state (classic exploit)
- **Integer Overflow**: Unexpected wrapping behavior
- **Front-Running**: Someone sees your transaction, does theirs first
- **Oracle Manipulation**: Bad price data leads to bad trades

---

## Key Principles

1. **Code is Law**: Once deployed, contract executes exactly as written (no fixes)
2. **Transparency**: All transactions visible (privacy requires ZK proofs)
3. **Immutability**: Security through cryptography, not access control
4. **Incentive Alignment**: Participants follow rules because it's economically beneficial
5. **Efficiency Over Trust**: Optimize for gas and throughput, not centralization

See [03-orange-belt/daily-exercises.md](daily-exercises.md) for hands-on practice.
