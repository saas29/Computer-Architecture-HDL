# Computer Architecture — HDL Projects

Hardware Description Language (HDL) implementations for the
[Nand2Tetris](https://www.nand2tetris.org/) course
(*The Elements of Computing Systems* by Nisan & Schocken, MIT Press).

This repository contains working HDL chips built from the ground up — from
basic memory elements (Bit, Register) all the way to a fully functional
16-bit Hack CPU, plus custom sequential counter designs (Johnson & Ring
counters).

## Project Structure

```
Computer-Architecture-HDL/
├── project-03/                # Project 3 — Sequential Logic (Memory)
│   ├── a/
│   │   ├── Bit.hdl            # 1-bit register
│   │   ├── Register.hdl       # 16-bit register (16 Bit chips)
│   │   ├── RAM8.hdl           # 8-register memory
│   │   ├── RAM64.hdl          # 64-register memory
│   │   ├── PC.hdl             # 16-bit program counter
│   │   ├── DMux8Way16.hdl     # 8-way 16-bit demultiplexer
│   │   └── *.tst / *.cmp      # Test scripts and compare files
│   └── b/
│       ├── RAM512.hdl         # 512-register memory
│       ├── RAM4K.hdl          # 4K-register memory
│       ├── RAM16K.hdl         # 16K-register memory
│       └── *.tst / *.cmp      # Test scripts and compare files
│
├── project-05-cpu/            # Project 5 — Computer Architecture
│   └── CPU.hdl                # The Hack CPU (16-bit processor)
│
├── project-counters/          # Custom Sequential Circuits
│   ├── JohnsonCounter.hdl     # 4-bit Johnson (twisted-ring) counter
│   └── RingCounter.hdl        # 4-bit Ring counter with reset
│
├── docs/                      # Reports and documentation
│   ├── EOC_Report_Part_B.docx
│   └── EOC_Report_Part_B.pdf
│
├── LICENSE
└── README.md
```

## Chips Implemented

### Project 3 — Sequential Logic (Memory Hierarchy)

The memory chips are built hierarchically — each larger memory is composed
of eight copies of the next smaller one, addressed by a demultiplexer.

| Chip | Description | Key Idea |
|------|-------------|----------|
| **Bit** | 1-bit register | DFF + Mux feedback loop |
| **Register** | 16-bit register | 16 parallel Bit chips |
| **RAM8** | 8 × 16-bit memory | 8 Registers + DMux8Way / Mux8Way16 |
| **RAM64** | 64 × 16-bit memory | 8 RAM8 chips |
| **RAM512** | 512 × 16-bit memory | 8 RAM64 chips |
| **RAM4K** | 4K × 16-bit memory | 8 RAM512 chips |
| **RAM16K** | 16K × 16-bit memory | 8 RAM4K chips |
| **PC** | 16-bit program counter | Register + Inc16 + three Mux16 layers (inc / load / reset) |

### Project 5 — The Hack CPU

A complete 16-bit processor that executes the Hack machine language:

- Decodes A-instructions and C-instructions from the 16-bit instruction word.
- Routes data between the A-register, D-register, ALU, and memory.
- Implements all eight jump conditions using the ALU's `zr` and `ng` flags.
- Drives the program counter for sequential execution, jumps, and reset.

### Custom Counters

| Chip | Type | Sequence |
|------|------|----------|
| **JohnsonCounter** | Twisted-ring counter | `0000 → 1000 → 1100 → 1110 → 1111 → 0111 → 0011 → 0001 → repeat` (8 states) |
| **RingCounter** | One-hot ring counter | `1000 → 0100 → 0010 → 0001 → repeat` (4 states, after reset) |

## How to Run

1. Download the [Nand2Tetris Software Suite](https://www.nand2tetris.org/software).
2. Open the **Hardware Simulator**.
3. Load any `.hdl` file from this repository.
4. Load the matching `.tst` test script (for Project 3 chips).
5. Click **Run** — the simulator compares output against the `.cmp` file.

## Tools Used

- **HDL** — Nand2Tetris Hardware Description Language
- **Hardware Simulator** — from the Nand2Tetris software suite

## References

- Nisan, N. & Schocken, S. (2005). *The Elements of Computing Systems*.
  MIT Press. [nand2tetris.org](https://www.nand2tetris.org/)

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file.
