# Computational Theory - SHA-256 Implementation

A complete implementation of the SHA-256 cryptographic hash algorithm built entirely from first principles, following the [FIPS PUB 180-4 specification](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf).

---

## Overview

This repository contains a ground-up implementation of SHA-256 (Secure Hash Algorithm 256-bit), one of the most widely used cryptographic hash functions. The implementation is divided into five progressive problems that build from basic cryptographic primitives to a complete, working SHA-256 algorithm.

### What is SHA-256?

SHA-256 is a cryptographic hash function that:
- Takes an input of any size
- Produces a fixed 256-bit (32-byte) output
- Is deterministic (same input always gives same output)
- Is one-way (computationally infeasible to reverse)
- Is collision-resistant (hard to find two inputs with same output)

### Purpose of This Repository

This implementation serves as:
- **Educational resource**: Learn how SHA-256 works internally
- **Specification compliance**: Follows FIPS PUB 180-4 exactly
- **Reference implementation**: Pure Python, easy to understand
- **Security demonstration**: Shows proper and improper use of hashing

---

## Prerequisites

### Required Software

- **Python**: 3.8 or higher
- **Jupyter Notebook** or **JupyterLab**: For running the main notebook
- **NumPy**: For efficient numerical operations

### Recommended

- **VS Code** with Python extension (for editing)
- **Git**: For version control

---

## Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/sha256-implementation.git
cd sha256-implementation
```

### Step 2: Create Virtual Environment (Recommended)

**On Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**On macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

**Requirements file (`requirements.txt`):**
```
numpy>=1.21.0
jupyter>=1.0.0
notebook>=6.4.0
```

### Step 4: Verify Installation
```bash
python -c "import numpy; import jupyter; print('Installation successful!')"
```

---

## Run the Jupyter Notebook

1. **Start Jupyter**:
```bash
   jupyter notebook problems.ipynb
```

2. **In your browser**: 
   - Navigate to the opened notebook
   - Select `Cell` → `Run All` from the menu
   - Or press `Shift + Enter` to run cells individually

---

## Problem Descriptions

### Problem 1: Cryptographic Primitive Functions

**Purpose**: Implement the basic bitwise operations used throughout SHA-256.

**Functions**:
- `u_32(x)` - Type conversion to 32-bit unsigned integers
- `rotr(x, n)` - Right rotation operation
- `Ch(x, y, z)` - Choose function (conditional selection)
- `Maj(x, y, z)` - Majority function (voting)
- `Parity(x, y, z)` - XOR parity (used in SHA-1)
- `Sigma0(x)`, `Sigma1(x)` - Sigma functions for compression (uppercase Σ)
- `sigma0(x)`, `sigma1(x)` - sigma functions for message schedule (lowercase σ)

---

### Problem 2: Round Constants Generation

**Purpose**: Generate the 64 round constants (K₀–K₆₃) from cube roots of first 64 primes.

**Functions**:
- `primes(n)` - Generate first n prime numbers
- `cube_root(primes)` - Compute cube roots
- `frac_32()` - Extract first 32 bits of fractional parts
- `hex_conversion(constants)` - Format as hexadecimal

---

### Problem 3: Message Preprocessing

**Purpose**: Pad and parse messages into 512-bit blocks.

**Functions**:
- `file_to_msg(filepath)` - Read file as bytes
- `create_padded_blocks(partial_block, length)` - Apply SHA-256 padding
- `block_parse(msg)` - Generator yielding 512-bit blocks

---

### Problem 4: Hash Computation

**Purpose**: Implement the core SHA-256 hash algorithm.

**Functions**:
- `expand_message_schedule(block)` - Expand 16 words to 64
- `initialize_working_variables(hash)` - Set up a–h variables
- `compress(vars, W, K)` - Perform 64 compression rounds
- `sha256_hash_block(hash, block)` - Process one block
- `sha256(message)` - Complete SHA-256 implementation

---

### Problem 5: Password Security Analysis

**Purpose**: Demonstrate vulnerabilities of unsalted password hashing.

**Functions**:
- `crack_password_hash(target, wordlist)` - Dictionary attack implementation
- `crack_all_passwords()` - Crack all three hashes
- Security analysis and recommendations
