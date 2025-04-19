# Quantum-Chain

![Quantum-Chain Banner](https://via.placeholder.com/1200x300/001933/FFFFFF?text=Quantum-Chain:+Post-Quantum+Blockchain)

A quantum-resistant blockchain implementation with attack simulation capabilities. This project demonstrates how to build a blockchain that is resistant to attacks from quantum computers through the use of post-quantum cryptography.

<p align="center">
  <img src="https://img.shields.io/badge/version-1.0.0-blue.svg" alt="Version 1.0.0">
  <img src="https://img.shields.io/badge/node-%3E%3D14.0.0-green.svg" alt="Node >= 14.0.0">
  <img src="https://img.shields.io/badge/license-MIT-yellow.svg" alt="License: MIT">
  <img src="https://img.shields.io/badge/purpose-educational-red.svg" alt="Purpose: Educational">
</p>

## 🎯 Features

- **Dual Cryptography System**: Supports both classical (ECDSA) and quantum-resistant (SPHINCS+ and lattice-based) cryptography
- **Quantum Attack Simulation**: Simulates quantum attacks using Shor's algorithm against different cryptographic schemes
- **Security Analysis**: Provides detailed metrics on blockchain security posture
- **Migration Tools**: Allows users to migrate funds from vulnerable to quantum-resistant addresses
- **Educational Purpose**: Demonstrates the vulnerability of classical cryptography and the security of post-quantum cryptography

## 🚀 Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/quantum-chain.git
cd quantum-chain

# Install dependencies
npm install

# Make the CLI executable
chmod +x bin/quantum-chain.js

# Install globally (optional)
npm install -g .
```

## 💻 Usage Guide

### Creating a Wallet

Create a new wallet with classical and quantum-resistant keys:

```bash
quantum-chain wallet create --name "MyWallet" --password "securepassword"
```

This creates a wallet with three types of keys:
- Classical ECDSA keypair (0x... address)
- SPHINCS+ quantum-resistant keypair (qx... address)
- Lattice-based quantum-resistant keypair (lx... address)

Terminal output example:
```
✅ Wallet created successfully!

Wallet ID: 49782947-dacb-4ff0-a8a0-4c21c2fda82f
Name: MyWallet

Classical Address: 0x1279cf32527fd8906144479581fee7b113b585c1
Quantum Address (SPHINCS+): qx991a87528237b49757d0d83be16f1649940375b4
Quantum Address (Lattice): lx9fa56ec6f28a7eb3adf52ac5d271f6e3710e6ba2

Your wallet has been encrypted and saved.
Keep your password and Wallet ID safe!
```

### Listing Wallets

View all wallets in the system:

```bash
quantum-chain wallet list
```

Terminal output example:
```
Found 3 wallet(s)

Available Wallets:
--------------------------------------------------------------------------------
ID                                   | Name                | Classical Address | Quantum Addresses
--------------------------------------------------------------------------------
49782947-dacb-4ff0-a8a0-4c21c2fda82f | MyWallet            | 0x1279cf32... | qx991a8752...
27f26c43-c72c-4f8e-87d3-20021941d9aa | AliceWallet         | 0xbc21f0a5... | qxbd6c5e96...
1b72e688-43f4-4eb6-b03c-3ac9842d37fd | BobWallet           | 0x5e5e61fe... | qx493f1236...
```

### Viewing Wallet Information

Get detailed information about a specific wallet:

```bash
quantum-chain wallet info --id "49782947-dacb-4ff0-a8a0-4c21c2fda82f"
```

Terminal output example:
```
Wallet Information:
----------------------------------------
Wallet ID: 49782947-dacb-4ff0-a8a0-4c21c2fda82f
Name: MyWallet

Addresses:
Classical (ECDSA): 0x1279cf32527fd8906144479581fee7b113b585c1
Quantum (SPHINCS+): qx991a87528237b49757d0d83be16f1649940375b4
Quantum (Lattice): lx9fa56ec6f28a7eb3adf52ac5d271f6e3710e6ba2

Balances:
Classical: 0 tokens
Quantum (SPHINCS+): 100 tokens
Quantum (Lattice): 0 tokens
--------------------
Total: 100 tokens

Recent Transactions:
2025-04-19 14:36:26 | +100 | Confirmed
  From: MINING_REWARD
  Type: SYSTEM
  TX: cf79bc5053...
```

### Checking Wallet Balance

Check the balance for a specific wallet:

```bash
quantum-chain wallet balance --id "49782947-dacb-4ff0-a8a0-4c21c2fda82f"
```

Or check balance for a specific address:

```bash
quantum-chain wallet balance --address "qx991a87528237b49757d0d83be16f1649940375b4"
```

Terminal output example:
```
Balance for wallet "MyWallet" (49782947-dacb-4ff0-a8a0-4c21c2fda82f):
----------------------------------------
Classical (0x1279cf32...): 0 tokens
Quantum SPHINCS+ (qx991a8752...): 100 tokens
Quantum Lattice (lx9fa56ec6...): 0 tokens
----------------------------------------
Total: 100 tokens
```

### Creating Transactions

Create transactions with different signature types:

```bash
# Classical transaction (vulnerable to quantum attacks)
quantum-chain tx create --from "49782947-dacb-4ff0-a8a0-4c21c2fda82f" --to "0x6a4be65a0f453623d77cb817260bd231319394b0" --amount 10 --type classical

# SPHINCS+ quantum-resistant transaction
quantum-chain tx create --from "49782947-dacb-4ff0-a8a0-4c21c2fda82f" --to "qx979401c668dcca51f38b9e2a97ea5ff1c126db72" --amount 15 --type sphincs

# Lattice-based quantum-resistant transaction
quantum-chain tx create --from "49782947-dacb-4ff0-a8a0-4c21c2fda82f" --to "lx1fc391eff8b0ad095698aa61ea41d99bb5d8791b" --amount 20 --type lattice
```

Terminal output example:
```
Transaction Information:
------------------------------------------------------------
From: qx991a87528237b49757d0d83be16f1649940375b4
To: qx979401c668dcca51f38b9e2a97ea5ff1c126db72
Amount: 15 tokens
Signature Type: Quantum-Resistant (SPHINCS+)

Enter wallet password: ********

Transaction created and signed!
Transaction Hash: 5e9829f9dad315f21639250e2b6fbe487e28bd1a03bc1bdd165abb4daed0f1e0
Status: Pending (waiting to be mined)

Type 'quantum-chain tx info --hash 5e9829f9...' to check status.
```

### Viewing Transaction Information

Get detailed information about a specific transaction:

```bash
quantum-chain tx info --hash "5e9829f9dad315f21639250e2b6fbe487e28bd1a03bc1bdd165abb4daed0f1e0"
```

Terminal output example:
```
Transaction Information:
------------------------------------------------------------
Transaction Hash: 5e9829f9dad315f21639250e2b6fbe487e28bd1a03bc1bdd165abb4daed0f1e0
Status: Pending
Timestamp: 2025-04-20 10:15:30

From: qx991a87528237b49757d0d83be16f1649940375b4
To: qx979401c668dcca51f38b9e2a97ea5ff1c126db72
Amount: 15 tokens

Signature Type: Quantum-Resistant (SPHINCS+ hash-based)

Security Information:
------------------------------------------------------------
✅ This transaction uses quantum-resistant SPHINCS+ signatures.
   It is secure against known quantum computing attacks.

Security Level: 256 bits

Vulnerability: Low - SPHINCS+ is designed to be secure against quantum computers.
Algorithm: Hash-based signature scheme, resistant to Shor's algorithm.
```

### Mining Blocks

Mine a new block to process pending transactions and earn rewards:

```bash
quantum-chain mine --reward-address "qx991a87528237b49757d0d83be16f1649940375b4"
```

Terminal output example:
```
⛏️ Mining new block with 1 pending transaction(s)...

Block #2 mined successfully!
Block Hash: 00006af85660afc0208ef4b354c6089bfa4fd11383675ccaa1353253e66fa94e
Transactions: 2 (1 pending + 1 mining reward)
Mining Reward: 100 tokens to qx991a87528237b49757d0d83be16f1649940375b4
Nonce Found: After 3231 attempts
Time Required: 1.35 seconds
Hash Rate: 2393 hashes/second

Block added to the blockchain.
```

### Checking Blockchain Status

View the current status of the blockchain:

```bash
quantum-chain chain status
```

Terminal output example:
```
Blockchain Status:
------------------------------------------------------------
Chain Length: 3 blocks
Latest Block: #2 (00006af856...)
Block Time: 2025-04-20 10:18:45
Pending Transactions: 0
Mining Difficulty: 4 (65536 hashes on average)
Chain Validation: Valid

Security Metrics:
------------------------------------------------------------
Transaction Distribution:
  Classical: 0 (0.0%)
  SPHINCS+: 1 (50.0%)
  Lattice: 0 (0.0%)

Address Distribution:
  Classical: 0
  Quantum-Resistant: 1

Token Security:
  Vulnerable: 0 tokens (0.0%)
  Secure: 215 tokens (100.0%)

Security Assessment:
✅ LOW RISK: Only 0.0% of funds are vulnerable to quantum attacks.
```

### Viewing Block Information

Get detailed information about a specific block:

```bash
quantum-chain block info --index 2
```

Terminal output example:
```
Block #2 Information:
------------------------------------------------------------
Block Hash: 00006af85660afc0208ef4b354c6089bfa4fd11383675ccaa1353253e66fa94e
Previous Block: 00004dafd0b42798a627e1dd984bb5d2f9e9a1b7dc840c3a2f40360117c167063df2
Timestamp: 2025-04-20 10:18:45
Nonce: 3231
Transactions: 2

Block Security Metrics:
------------------------------------------------------------
Classical Transactions: 0 (0.0%)
SPHINCS+ Transactions: 1 (50.0%)
Lattice Transactions: 0 (0.0%)

Transactions:
------------------------------------------------------------
1. [SYSTEM] MINING_REWARD -> qx991a87528237b49757d0d83be16f1649940375b4 (100 tokens)
2. [SPHINCS+] qx991a8752... -> qx979401c6... (15 tokens)
   TX: 5e9829f9dad3...

Block Verification: Valid ✓
```

### Analyzing Security

Check detailed security metrics for the blockchain:

```bash
quantum-chain security metrics
```

Terminal output example:
```
Quantum Security Analysis:
================================================================================

Transaction Metrics:
--------------------------------------------------------------------------------
Total Transactions: 3

By Signature Type:
  Classical (ECDSA): 0 (0.0%)
  Quantum (SPHINCS+): 2 (66.7%)
  Quantum (Lattice): 0 (0.0%)
  Combined Quantum: 2 (66.7%)

Address Metrics:
--------------------------------------------------------------------------------
Total Addresses: 2

By Address Type:
  Classical (0x...): 0 (0.0%)
  Quantum-Resistant (qx/lx...): 2 (100.0%)

Balance Security Metrics:
--------------------------------------------------------------------------------
Total Tokens: 215

By Address Security:
  Vulnerable (Classical): 0 tokens (0.0%)
  Secure (Quantum-Resistant): 215 tokens (100.0%)

Overall Security Assessment:
--------------------------------------------------------------------------------
✅ LOW RISK: Only 0.0% of funds are vulnerable to quantum attacks.
            0 tokens in 0 classical addresses are at risk.

Recommendation: Continue using quantum-resistant addresses for new transactions.

Security Trend Analysis:
--------------------------------------------------------------------------------
Classical Usage: Decreasing ↓
Quantum-Resistant Usage: Increasing ↑

Quantum Attack Mitigation:
--------------------------------------------------------------------------------
1. Use SPHINCS+ or Lattice-based signatures for all new transactions
2. Migrate existing funds from classical to quantum-resistant addresses
3. Monitor the development of quantum computing capabilities
4. Use the attack simulation tool to assess specific vulnerabilities: quantum-chain attack simulate
```

### Quantum Attack Simulation

#### Analyzing Blockchain Vulnerability

```bash
quantum-chain attack analyze
```

Terminal output example:
```
🔍 Blockchain Vulnerability Analysis:
------------------------------------------------------------
Blockchain State:
Total Blocks: 3
Total Transactions: 3

Transaction Security:
Classical (ECDSA) Transactions: 0 (0.0%)
Quantum-Safe (SPHINCS+) Transactions: 2 (66.7%)
Quantum-Safe (Lattice) Transactions: 0 (0.0%)

Address Security:
Vulnerable Addresses: 0
Secure Addresses: 2

Value Security:
Total Value in Vulnerable Addresses: 0 tokens
Total Value in Quantum-Safe Addresses: 215 tokens

RISK ASSESSMENT:
0.0% of funds are vulnerable to quantum attacks
LOW RISK - Maintain quantum-resistant usage

Recommendations:
1. Use quantum-resistant signatures (SPHINCS+ or Lattice) for all new transactions
2. Migrate funds from classical to quantum-resistant addresses
3. Monitor quantum computing advancements

Simulation Options:
Run quantum-chain attack simulate --qubits 4000 --target "0x..." to simulate a quantum attack
Run quantum-chain attack report to generate a comprehensive vulnerability report
```

#### Simulating Attack on Classical Address

```bash
quantum-chain attack simulate --qubits 4000 --target "0x1279cf32527fd8906144479581fee7b113b585c1"
```

Terminal output example:
```
🔬 Initializing quantum attack simulation with 4000 qubits...

Target Address: 0x1279cf32527fd8906144479581fee7b113b585c1
Signature Algorithm: ECDSA (secp256k1)

⚙️ Simulating quantum attack:

Step 1: Initialize quantum circuit
Attempting to initialize a quantum circuit with 4000 qubits for Shor's algorithm.
Shor's algorithm requires approximately 2n qubits for an n-bit discrete logarithm problem. For 256-bit elliptic curve, we need about 512 qubits.

Step 2: Quantum Fourier Transform
Applying quantum Fourier transform to find the period in the elliptic curve discrete logarithm problem.
Converting the ECDLP into a period-finding problem that quantum computers can solve efficiently.

Step 3: Period estimation
Estimating the period using 4000 qubits.
Processing approximately 1,048,576 quantum operations at 7,812,500 operations per second.

Step 4: Period found
Successfully found the period in the elliptic curve discrete logarithm.
Quantum Fourier Transform successfully extracted the private key from the public key.

Step 5: Key extraction
Extracted private key from quantum calculation results.
Private key corresponds to the period of the function representing the discrete logarithm problem.

[██████████████████████████████] 100% Complete

🔓 COMPROMISED: Private key successfully derived!
Time Required: 0.1 seconds (simulated)
Balance at Risk: 0 tokens

RESULT: This address would be compromised by a sufficiently powerful quantum computer.
RECOMMENDATION: Migrate funds to quantum-resistant address immediately.

Mathematical Explanation:
--------------------------------------------------------------------------------
Algorithm: Shor's Algorithm for Elliptic Curve Discrete Logarithm

Steps:
  1. Convert the problem of finding k where Q = kP to finding the period of a function f(x) = P^x
  2. Create a quantum superposition of states |x⟩|f(x)⟩
  3. Apply quantum Fourier transform to obtain period r
  4. Use continued fractions to recover private key k from period r

Computational Complexity:
  classical: O(2^(n/2)) with best algorithms (exponential)
  quantum: O(n^3) with Shor's algorithm (polynomial)
  speedup: Exponential

Security Implications:
  ECDSA is broken when large-scale quantum computers become available. All funds secured only by ECDSA signatures would be at risk.
```

#### Simulating Attack on Quantum-Resistant Address

```bash
quantum-chain attack simulate --qubits 4000 --target "qx991a87528237b49757d0d83be16f1649940375b4"
```

Terminal output example:
```
🔬 Initializing quantum attack simulation with 4000 qubits...

Target Address: qx991a87528237b49757d0d83be16f1649940375b4
Signature Algorithm: SPHINCS+ (hash-based)

⚙️ Simulating quantum attack:

Step 1: Analyzing SPHINCS+ structure
Examining the hash-based signature scheme structure to find attack vectors.
SPHINCS+ uses a hash tree with many one-time signatures, creating a stateless signing mechanism resistant to quantum attacks.

Step 2: Applying Grover's algorithm
Attempting to use Grover's algorithm with 4000 qubits to find hash collisions.
Grover's algorithm provides at most a quadratic speedup for searching, reducing security from n bits to approximately n/2 bits.

Step 3: Security level assessment
SPHINCS+ retains approximately 128 bits of security against quantum attacks.
Even with Grover's algorithm, breaking a 256-bit hash function would require 2^128 quantum operations, which remains computationally infeasible.

Step 4: Computational feasibility analysis
Calculating resources required to break the SPHINCS+ signature.
Would require approximately 340282366920938463463374607431768211456 quantum operations, which is infeasible regardless of quantum computer speed.

Step 5: Attack conclusion
Attack on SPHINCS+ signature is unsuccessful.
The post-quantum security of SPHINCS+ effectively resists even the most powerful quantum algorithms currently known.

[██████████████████████████████] 100% Complete

✅ SECURE: Attack unsuccessful!
Reason: Quantum-resistant algorithm
Estimated time to break: 2^128 quantum operations (infeasible)
Balance Protected: 100 tokens

RESULT: This address is secure against quantum attacks.

SPHINCS+ successfully protects against quantum computing threats.

Mathematical Explanation:
--------------------------------------------------------------------------------
Algorithm: SPHINCS+ Resistance to Quantum Attacks

Steps:
  1. SPHINCS+ security is based on the pre-image resistance of cryptographic hash functions
  2. Best quantum attack is Grover's algorithm, which provides quadratic speedup
  3. For a hash function with n bits of security, Grover reduces it to n/2 bits
  4. With n=256, quantum security is still 128 bits, requiring 2^128 operations

Computational Complexity:
  classical: O(2^n) for finding hash pre-images
  quantum: O(2^(n/2)) with Grover's algorithm
  securityMaintained: Yes, 128-bit quantum security is still beyond computational feasibility

Security Implications:
  SPHINCS+ remains secure against quantum attacks, making it suitable for long-term security.
```

#### Generating Attack Report

```bash
quantum-chain attack report
```

Terminal output example:
```
🛡️ Quantum Attack Impact Report
================================================================================

Blockchain State:
--------------------------------------------------------------------------------
Total Blocks: 3
Total Transactions: 3

Vulnerability Assessment:
--------------------------------------------------------------------------------
Vulnerable Funds: 0 tokens (0.0%)
Secure Funds: 215 tokens (100.0%)
Vulnerable Addresses: 0
Secure Addresses: 2

Attack Projection:
--------------------------------------------------------------------------------
Estimated Time to Compromise All Vulnerable Addresses: 0 seconds
Potential Loss: 0 tokens
Required Quantum Resources: 512 logical qubits

Mitigation Strategy:
--------------------------------------------------------------------------------
Recommended Action: Migrate all funds from classical to quantum-resistant addresses
Estimated Time to Migrate: 0 seconds
Migration Cost: 0 tokens (transaction fees)

Transaction Distribution:
--------------------------------------------------------------------------------
Classical (ECDSA): 0 (0.0%)
Quantum (SPHINCS+): 2 (66.7%)
Quantum (Lattice): 0 (0.0%)

Risk Assessment:
--------------------------------------------------------------------------------
LOW RISK: Only 0.0% of funds are vulnerable
Continue monitoring
```

### Migrating Funds

Migrate funds from a classical address to a quantum-resistant address:

```bash
quantum-chain wallet migrate --id "49782947-dacb-4ff0-a8a0-4c21c2fda82f" --to-quantum sphincs
```

Terminal output example:
```
Migration Information:
------------------------------------------------------------
From: 0x1279cf32527fd8906144479581fee7b113b585c1 (Classical)
To: qx991a87528237b49757d0d83be16f1649940375b4 (Quantum SPHINCS+)
Amount: 10 tokens

Do you want to proceed with the migration? Yes

Enter your wallet password: ********

✅ Migration transaction created!
Transaction Hash: 8b72a49f6de13cd4a5b4e3c7821e3f69d85479a2e18d3a7c821dbf21ae7e54e8
From: 0x1279cf32527fd8906144479581fee7b113b585c1
To: qx991a87528237b49757d0d83be16f1649940375b4
Amount: 10 tokens

The transaction has been added to the mempool and will be mined in the next block.
Check status with: quantum-chain tx info --hash "8b72a49f6de13cd4a5b4e3c7821e3f69d85479a2e18d3a7c821dbf21ae7e54e8"
```

## 📊 Technical Details

### Cryptographic Schemes Comparison

| Feature | Classical (ECDSA) | SPHINCS+ | Lattice-Based |
|---------|------------------|----------|---------------|
| Address prefix | 0x... | qx... | lx... |
| Algorithm type | Elliptic curve | Hash-based | Lattice problems |
| Classical security | 128 bits | 256 bits | 256 bits |
| Quantum security | 0 bits | 128 bits | 128 bits |
| Signature size | ~72 bytes | >7KB | ~2.5KB |
| Private key size | 32 bytes | ~1KB | ~2KB |
| Performance | Very fast | Slow | Moderate |
| Quantum vulnerability | High (Shor's algorithm) | Low (Grover's algorithm) | Low |

### Quantum Attack Mechanisms

#### Shor's Algorithm (Threat to Classical Cryptography)

<p align="center">
  <img src="https://via.placeholder.com/800x400/001933/FFFFFF?text=Shor's+Algorithm+Visualization" alt="Shor's Algorithm Visualization">
</p>

Shor's algorithm can efficiently solve the discrete logarithm problem on which ECDSA is based:

1. The security of ECDSA relies on finding k where Q = kP (P is a generator point, Q is a public key)
2. Shor's algorithm converts this to a hidden period finding problem
3. Quantum Fourier Transform can find this period efficiently
4. The algorithm completes in polynomial time (O(n³)) instead of exponential time (O(2^n))

#### SPHINCS+ Quantum Resistance

<p align="center">
  <img src="https://via.placeholder.com/800x400/001933/FFFFFF?text=SPHINCS++Quantum+Resistance" alt="SPHINCS+ Quantum Resistance">
</p>

SPHINCS+ security is based on the pre-image resistance of cryptographic hash functions:

1. Best quantum attack is Grover's algorithm, providing quadratic speedup
2. For a hash function with n bits of security, Grover reduces it to n/2 bits
3. With n=256, quantum security is still 128 bits, requiring 2^128 operations
4. This remains computationally infeasible even with quantum computers

#### Lattice-Based Cryptography Quantum Resistance

<p align="center">
  <img src="https://via.placeholder.com/800x400/001933/FFFFFF?text=Lattice-Based+Cryptography" alt="Lattice-Based Cryptography">
</p>

Lattice-based security is based on the hardness of finding short vectors in lattices:

1. Security based on the hardness of finding short vectors in lattices (SVP or LWE problems)
2. Best classical algorithms (BKZ) require exponential time
3. Known quantum algorithms provide at most polynomial speedup for specific sub-problems
4. The core lattice problems remain exponentially difficult even for quantum computers

## 🛠️ Project Structure

```
quantum-chain/
├── bin/
│   └── quantum-chain.js       # Main CLI entry point
├── lib/
│   ├── blockchain.js          # Core blockchain implementation
│   ├── wallet.js              # Wallet management functionality
│   ├── transaction.js         # Transaction creation and validation
│   ├── mining.js              # Block mining implementation
│   ├── cryptography/
│   │   ├── classical.js       # ECDSA implementation
│   │   ├── sphincs.js         # SPHINCS+ implementation
│   │   └── lattice.js         # Lattice-based cryptography implementation
│   └── attack/
│       ├── analyzer.js        # Vulnerability analysis
│       └── simulator.js       # Quantum attack simulation
├── utils/
│   ├── config.js              # Configuration settings
│   ├── storage.js             # Data persistence
│   └── formatting.js          # Output formatting
├── data/
│   ├── wallets/               # Encrypted wallet storage
│   └── blockchain/            # Blockchain data
├── package.json
└── README.md
```

## ⚠️ Limitations & Disclaimers

- This is an educational project and not intended for production use
- The SPHINCS+ and lattice-based implementations are simplified simulations
- Real quantum attacks would require large-scale quantum computers that don't exist yet
- For a production system, use established post-quantum cryptography libraries

## 🚧 Future Work

- Implement peer-to-peer networking for a distributed blockchain
- Create a web-based UI for easier interaction
- Add support for quantum-resistant smart contracts
- Optimize SPHINCS+ implementation for better performance
- Use actual post-quantum cryptography libraries
- Add cross-chain migration tools
- Create Docker containerization for easier deployment
- Enhance attack simulation with different models
- Add support for hardware acceleration
- Create a comprehensive test suite

## 📝 License

MIT

---

<p align="center">
  Made with ❤️ for quantum-safe blockchain education
</p>
