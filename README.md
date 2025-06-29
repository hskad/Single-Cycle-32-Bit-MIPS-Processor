# Single-Cycle 32-bit MIPS Processor in Verilog

![Verilog](https://img.shields.io/badge/Language-Verilog-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg) <!--- Suggesting MIT, you can change this --->

A complete 32-bit single-cycle MIPS processor implemented in Verilog. This project was developed as part of a computer architecture course, demonstrating the fundamental concepts of processor design, including datapath and control unit implementation.

## 📋 Table of Contents
- [Features](#-features)
- [Processor Architecture](#-processor-architecture)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Simulation](#simulation)
- [Implemented Instructions](#-implemented-instructions)
- [Project Report](#-project-report)

## ✨ Features
- **32-bit MIPS Architecture**: Implements a subset of the MIPS instruction set.
- **Single-Cycle Datapath**: Every instruction is executed in a single clock cycle.
- **Modular Design**: The processor is built from interconnected modules like the ALU, Control Unit, Register File, and Memories.
- **Testbenched**: Includes a comprehensive testbench (`mips_processor_tb.v`) for functional verification.

## 🏛️ Processor Architecture
The datapath is designed according to the single-cycle MIPS architecture. It consists of the following core components:

| Module              | File (`/rtl`)         | Description                                                      |
| ------------------- | --------------------- | ---------------------------------------------------------------- |
| **Top Module**      | `mips_processor.v`    | Integrates all components to form the complete processor.        |
| **Control Unit**    | `control_unit.v`      | Generates control signals based on the instruction's opcode.     |
| **ALU**             | `alu.v`               | Performs arithmetic and logical operations.                      |
| **ALU Control**     | `alu_control.v`       | Decodes the `funct` field to generate specific ALU control signals. |
| **Register File**   | `register_file.v`     | Manages 32 general-purpose registers (`$0` - `$31`).               |
| **Instruction Memory**| `instruction_memory.v`| Stores and fetches instructions.                               |
| **Data Memory**     | `data_memory.v`       | Handles `load` and `store` operations.                           |
| **Program Counter** | `pc.v`                | Holds the address of the current instruction.                    |
| **Sign Extend**     | `sign_extend.v`       | Extends a 16-bit immediate value to 32 bits.                     |
| **Multiplexers**    | `mux2.v`              | Used throughout the datapath to select between inputs.           |

A detailed diagram of the datapath can be found in the [Project Report](doc/Project%20Report.pdf).

## 📁 Project Structure
The project is organized into the following directories for clarity and maintainability:

```
.
├── .gitignore
├── README.md
├── doc/
│   └── Project Report.pdf
├── rtl/
│   ├── alu.v
│   ├── alu_control.v
│   ├── control_unit.v
│   ├── data_memory.v
│   ├── instruction_memory.v
│   ├── mips_processor.v
│   ├── mux2.v
│   ├── pc.v
│   ├── register_file.v
│   └── sign_extend.v
└── sim/
    └── mips_processor_tb.v
```

- **/rtl**: Contains all the synthesizable Verilog source files (Register-Transfer Level).
- **/sim**: Contains the testbench file(s) for simulation.
- **/doc**: Contains the project documentation.

## 🚀 Getting Started

### Prerequisites
- A Verilog simulator (e.g., [Icarus Verilog](http://iverilog.icarus.com/), ModelSim, Vivado).
- A waveform viewer (e.g., [GTKWave](http://gtkwave.sourceforge.net/)).

### Simulation
Follow these steps to run the simulation using Icarus Verilog and GTKWave.

1.  **Clone the repository:**
    ```sh
    git clone <your-repository-url>
    cd <your-repository-name>
    ```

2.  **Compile the Verilog files:**
    The command below compiles all Verilog files in the `rtl` and `sim` directories and creates a simulation executable named `mips_sim`.
    ```sh
    iverilog -o mips_sim sim/mips_processor_tb.v rtl/*.v
    ```

3.  **Run the simulation:**
    This will execute the testbench and generate a waveform file (`mips_processor_tb.vcd`).
    ```sh
    vvp mips_sim
    ```

4.  **View the waveform:**
    Open the generated `.vcd` file with GTKWave to analyze the signals and verify the processor's behavior.
    ```sh
    gtkwave mips_processor_tb.vcd
    ```

## 💻 Implemented Instructions

The processor supports the following MIPS instructions:

**R-Type (Register)**
- `add`
- `sub`
- `and`
- `or`
- `slt` (Set on Less Than)
- *(add other R-types you implemented)*

**I-Type (Immediate)**
- `lw` (Load Word)
- `sw` (Store Word)
- `beq` (Branch on Equal)
- *(add other I-types you implemented)*

**J-Type (Jump)**
- `j` (Jump)
- *(add other J-types you implemented)*

> **Note**: You may need to pre-load the instruction memory file (`instruction_memory.v`) with machine code to test specific programs.

## 📄 Project Report
A detailed technical report is available in the `/doc` directory. It covers:
- In-depth architectural design and datapath diagrams.
- Implementation details of each module.
- Simulation results and verification strategy.

[**View the Project Report**](doc/Project%20Report.pdf)
