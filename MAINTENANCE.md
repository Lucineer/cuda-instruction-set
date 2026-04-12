# cuda-instruction-set — Maintenance Notes

## Purpose
Defines all 200 FLUX opcodes as Rust types. This is the SINGLE SOURCE OF TRUTH for the ISA.
If flux-runtime-c and cuda-instruction-set disagree, cuda-instruction-set is canonical.

## Architecture
- Opcode enum with all 200 values
- Format enum: A (rr), B (ri8), C (ri16), D (rro), E (rio), F (ri16o), G (addr)
- Each opcode has: hex code, name, format, category, description
- ISA reference table in README.md

## Key Invariants
- Opcode values must match flux-runtime-c exactly
- Format types determine encoding size: A=2, B=3, C=4, D=3, E=4, F=5, G=4 bytes
- Confidence opcodes (0x70-0x79) are OPT-IN (StripConf pattern) — not default
- Instinct opcodes (0xB0-0xBF) connect to cuda-instinct-cortex
- Trust opcodes (0xC0-0xCF) connect to cuda-trust

## Adding New Opcodes
1. Add variant to Opcode enum
2. Add entry to format_size() function  
3. Update ISA table in README.md
4. Add to cuda-assembler mnemonics
5. Add test in flux-runtime-c
6. Update this MAINTENANCE.md

## Related Crates
- flux-runtime-c: C implementation (authoritative execution)
- cuda-assembler: Text-to-bytecode compiler
- flux-disasm: Bytecode-to-text decompiler
- cuda-confidence-math: Confidence formula library
- cuda-instinct-cortex: Instinct processing layer
- cuda-atp-market: Energy economy
- cuda-capability-ports: Memory-mapped I/O

## The Deeper Connection
Every opcode is a word in the fleet vocabulary. The 200 opcodes define the BOUNDS of what a FLUX agent can think. The HAV (Higher Abstraction Vocabulary) project maps 2000+ human concepts to these 200 root words — a 10:1 ratio that mirrors natural language. An agent that knows all 200 opcodes can express anything, but an agent that UNDERSTANDS the relationships between them can reason. This crate is the dictionary. cuda-confidence-math is the grammar. cuda-ethics is the conscience. Together they form a mind.
