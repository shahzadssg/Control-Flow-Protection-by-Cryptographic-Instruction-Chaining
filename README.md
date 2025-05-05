# Control-Flow Protection by Cryptographic Instruction Chaining

A Python proof-of-concept implementation of the secure execution environment described in “Control Flow Protection by Cryptographic Instruction Chaining” 

---

## Overview

This repository contains a standalone Jupyter Notebook (`control_flow_protection.ipynb`) implementing:

- **Instruction encryption & chaining** using per-instruction key derivation  
- **Authenticated encryption** (AES-CFB + HMAC-SHA256) for instructions, registers, and memory  
- **Control-flow handling** (branches, jumps, calls/returns) with cryptographic binding  
- A **benchmark harness** measuring crypto-primitive throughput, memory-encrypt throughput, and per-instruction latency  

---

## Paper Summary

> **Control Flow Protection by Cryptographic Instruction Chaining**  
> by Shahzad Ahmad, Stefan Rass, Maksim Goman, Manfred Schlägl, Daniel Große.
> We present a novel secure execution environment that provides comprehensive protection for program execution through a unified cryptographic approach. Our construction employs authenticated encryption (ensuring confidentiality, integrity, and correct ordering), and introduces a key-chaining mechanism that binds consecutive instructions to prevent reordering and replay attacks. Specialized handling for control-flow operations preserves security guarantees across complex execution paths. A Python proof-of-concept validates practicality, and performance analysis quantifies computational overhead.

Key contributions:

1. **Cryptographic binding of instructions** via fresh per-instruction keys  
2. **Authenticated encryption** for instructions, registers, and memory  
3. **Secure control-flow**: BEQ, JMP, CALL/RET handled with deterministic key derivation  
4. **Performance evaluation** demonstrating feasibility and overhead  

---

## Disclaimer

> **This code is provided “as-is” for research and educational purposes only.**  
> While it demonstrates the core cryptographic chaining concepts, it is **not** hardened for production use.  
> Do **not** run untrusted code under this environment without a full security audit. 

---

## Benchmark Results

Below is a summary of the end-to-end timings observed on a typical Python 3.x setup:

| **Operation**               | **Measured**         | **Derived Metric**                                            |
|-----------------------------|----------------------|---------------------------------------------------------------|
| Encrypt + MAC (1 KiB)       | 0.0321 s total       | Avg = 32.1 µs per 1 KiB<br>Throughput ≈ 31.9 MiB/s            |
| Decrypt + MAC (1 KiB)       | 0.0314 s total       | Avg = 31.4 µs per 1 KiB<br>Throughput ≈ 32.8 MiB/s            |
| Memory encrypt (32 B)       | 0.0002 s total       | Throughput ≈ 1.91 × 10⁵ B/s                                   |
| Instruction execution       | 0.0131 s for 18 instr| Avg = 728 µs per instr<br>Rate ≈ 1 374 instr/s                |

---

## Usage

1. Clone this repo  
2. Open `control_flow_protection.ipynb` in Jupyter or Colab  
3. Run all cells to see the implementation and benchmark output  

---

## License

This work has partially been supported by the LIT Secure and Correct Systems Lab funded by the State of Upper Austria.
