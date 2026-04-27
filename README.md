# cuda-instruction-set

Agent-native instruction set unifying FLUX VM, cuda-genepool instincts, and cuda-axiom deliberation into one bytecode format. 80 opcodes with confidence propagation, A2A encoding, and assembler/disassembler.

## Opcode Map

| Range | Category | Count | Description |
|-------|----------|-------|-------------|
| 0x00–0x07 | Control | 8 | NOP, MOV, JMP, CALL, RET, HALT |
| 0x08–0x17 | ArithConf | 16 | Arithmetic with Bayesian confidence propagation |
| 0x18–0x1F | Logic | 8 | Bitwise operations with confidence |
| 0x20–0x27 | Compare | 8 | Confidence-aware comparisons |
| 0x28–0x2F | Stack | 8 | Typed stack push/pop/swap/dup |
| 0x30–0x37 | Perception | 8 | IO, sensor fusion |
| 0x38–0x4F | A2A | 24 | Agent-to-agent communication |
| 0x50–0x57 | Memory | 8 | Capability-based memory regions |
| 0x58–0x5F | Type | 8 | Boxed values, casting |
| 0x60–0x67 | SIMD | 8 | 4-wide vector operations |
| 0x68–0x6F | Instinct | 8 | Biological instinct activation |
| 0x70–0x77 | Energy | 8 | ATP budgets, apoptosis |
| 0x78–0x7F | System | 8 | Debug, barriers, resources |

## Confidence Propagation

Every ArithConf operation propagates uncertainty using Bayesian fusion:

```rust
use cuda_instruction_set::Confidence;

// Bayesian fusion of independent confidences
let fused = Confidence::fuse(Confidence::HIGH, Confidence::MEDIUM);
// fused = 1/(1/0.95 + 1/0.5) ≈ 0.329

// Sequential composition (confidence decreases through chains)
let chained = Confidence::chain(Confidence::HIGH, Confidence::MEDIUM);
// chained = 0.95 * 0.5 = 0.475
```

## Quick Start

```bash
git clone https://github.com/Lucineer/cuda-instruction-set.git
cd cuda-instruction-set
cargo test    # 18 tests
cargo build   # zero external dependencies
```

## Key Types

- **`Confidence(f32)`** — Confidence value in [0.0, 1.0] with Bayesian fusion/chain
- **`Opcode`** — 80 opcodes across 13 categories
- **`ConfValue`** — Value with attached confidence metadata
- **`Instruction`** — Opcode + operands + confidence
- **`Assembler`** — Text → bytecode assembler
- **`Disassembler`** — Bytecode → text disassembler
- **`A2AMessage`** — Agent-to-agent encoded message

## Design

- **Agent-native**: Every instruction carries confidence for uncertain environments
- **80 opcodes**: Covering control flow, arithmetic, perception, inter-agent comms, biology
- **Zero dependencies**: Pure Rust, no external crates
- **Edge-tested**: Compiles and passes all tests on Jetson Orin Nano (ARM64)

---

## Fleet Context

Part of the Lucineer/Cocapn fleet. See [fleet-onboarding](https://github.com/Lucineer/fleet-onboarding) for boarding protocol.

- **Vessel:** JetsonClaw1 (Jetson Orin Nano 8GB)
- **Domain:** Low-level systems, CUDA, edge computing
- **Comms:** Bottles via Forgemaster/Oracle1, Matrix #fleet-ops
