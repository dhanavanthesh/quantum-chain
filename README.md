# Quantum-Chain

A quantum-resistant blockchain implementation with attack simulation capabilities. This project demonstrates how to build a blockchain that is resistant to attacks from quantum computers through the use of post-quantum cryptography.

## Features

- **Dual Cryptography System**: Supports both classical (ECDSA) and quantum-resistant (SPHINCS+ and lattice-based) cryptography
- **Quantum Attack Simulation**: Simulates quantum attacks using Shor's algorithm against different cryptographic schemes
- **Security Analysis**: Provides detailed metrics on blockchain security posture
- **Migration Tools**: Allows users to migrate funds from vulnerable to quantum-resistant addresses
- **Educational Purpose**: Demonstrates the vulnerability of classical cryptography and the security of post-quantum cryptography

## Installation

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

## Usage

### Creating a Wallet

```bash
quantum-chain wallet create --name "MyWallet" --password "securepassword"
```

This creates a wallet with three types of keys:
- Classical ECDSA keypair (0x... address)
- SPHINCS+ quantum-resistant keypair (qx... address)
- Lattice-based quantum-resistant keypair (lx... address)

### Creating Transactions

```bash
# Classical transaction (vulnerable to quantum attacks)
quantum-chain tx create --from "wallet-uuid" --to "0x123..." --amount 10 --type classical

# SPHINCS+ quantum-resistant transaction
quantum-chain tx create --from "wallet-uuid" --to "qx123..." --amount 15 --type sphincs

# Lattice-based quantum-resistant transaction
quantum-chain tx create --from "wallet-uuid" --to "lx123..." --amount 20 --type lattice
```

### Mining Blocks

```bash
quantum-chain mine --reward-address "qx456..."
```

### Blockchain Exploration

```bash
# Check blockchain status
quantum-chain chain status

# View block details
quantum-chain block info --index 5

# Check security metrics
quantum-chain security metrics
```

### Quantum Attack Simulation

```bash
# Analyze blockchain for vulnerabilities
quantum-chain attack analyze

# Simulate attack on a classical address
quantum-chain attack simulate --qubits 4000 --target "0x789..."

# Simulate attack on a quantum-resistant address
quantum-chain attack simulate --qubits 4000 --target "qx789..."

# Generate attack impact report
quantum-chain attack report
```

### Migration

```bash
# Migrate funds from classical to SPHINCS+ address
quantum-chain wallet migrate --id "wallet-uuid" --to-quantum sphincs

# Migrate funds from classical to Lattice address
quantum-chain wallet migrate --id "wallet-uuid" --to-quantum lattice
```

## Technical Details

### Cryptographic Schemes

#### Classical Cryptography (ECDSA)

- Based on the secp256k1 elliptic curve (same as Bitcoin and Ethereum)
- Offers approximately 128 bits of security against classical computers
- Vulnerable to quantum computers through Shor's algorithm
- Generates addresses with "0x" prefix

#### SPHINCS+ (Quantum-Resistant)

- Stateless hash-based signature scheme
- Security based on the one-wayness of cryptographic hash functions
- Resistant to quantum computers including Shor's algorithm
- Larger signatures (>7KB) compared to ECDSA (~72 bytes)
- Generates addresses with "qx" prefix

#### Lattice-Based Cryptography (Quantum-Resistant)

- Based on the hardness of lattice problems like Learning With Errors (LWE)
- Resistant to known quantum attacks
- Medium-sized signatures (~2.5KB)
- Good performance characteristics for a post-quantum scheme
- Generates addresses with "lx" prefix

### Quantum Attack Simulation

The simulation demonstrates:

1. How Shor's algorithm can break ECDSA by solving the discrete logarithm problem
2. Why hash-based signatures like SPHINCS+ resist quantum attacks
3. How lattice-based cryptography maintains security in a post-quantum world
4. The computational requirements for performing quantum attacks

## Project Structure

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

## Limitations & Disclaimers

- This is an educational project and not intended for production use
- The SPHINCS+ and lattice-based implementations are simplified simulations
- Real quantum attacks would require large-scale quantum computers that don't exist yet
- For a production system, use established post-quantum cryptography libraries

## Mathematical Background

### Shor's Algorithm Attack on ECDSA

Shor's algorithm can efficiently solve the discrete logarithm problem on which ECDSA is based:

1. The security of ECDSA relies on finding k where Q = kP (P is a generator point, Q is a public key)
2. Shor's algorithm converts this to a hidden period finding problem
3. Quantum Fourier Transform can find this period efficiently
4. The algorithm completes in polynomial time (O(n³)) instead of exponential time (O(2^n))

### SPHINCS+ Quantum Resistance

SPHINCS+ security is based on the pre-image resistance of cryptographic hash functions:

1. Best quantum attack is Grover's algorithm, providing quadratic speedup
2. For a hash function with n bits of security, Grover reduces it to n/2 bits
3. With n=256, quantum security is still 128 bits, requiring 2^128 operations
4. This remains computationally infeasible even with quantum computers

### Lattice-Based Cryptography Quantum Resistance

Lattice-based security is based on the hardness of finding short vectors in lattices:

1. Security based on the hardness of finding short vectors in lattices (SVP or LWE problems)
2. Best classical algorithms (BKZ) require exponential time
3. Known quantum algorithms provide at most polynomial speedup for specific sub-problems
4. The core lattice problems remain exponentially difficult even for quantum computers

## License

MIT