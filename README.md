# RISC-V Assembler & Simulator (RV32I)

A Python-based toolchain designed to assemble RISC-V assembly code into machine language and simulate its execution on a virtualized 32-bit processor. This project supports the **RV32I Base Integer Instruction Set** along with custom extended instructions.

##  Features

### 1. The Assembler
* **Function:** Converts assembly code (from `ip.txt`) into 32-bit binary machine code.
* **Capabilities:**
    * Handles all standard Instruction Types: **R, I, S, B, U, J**.
    * **Symbol Resolution:** Supports labels (e.g., `loop:`, `start:`) and calculates PC-relative offsets automatically.
    * **Error Handling:** Validates register names and immediate values.

### 2. The Simulator
* **Function:** Executes binary machine code (from `op.txt`) and simulates the processor state.
* **Architecture:**
    * Simulates 32 General Purpose Registers (`x0`-`x31`).
    * Implements a Program Counter (PC) that updates based on execution flow.
    * **Virtual Halt:** Detects `beq zero, zero, 0` as a termination signal.
* **Trace Output:** Generates a trace file (`Op_regs.txt`) showing register states after every instruction.

### 3. Extended (Bonus) Instructions
The simulator supports custom operations beyond standard RV32I:
* **`mul`**: Performs integer multiplication.
* **`rst`**: Resets all registers/state.
* **`rvrs`**: Bitwise reverse operation.

##  Project Structure
```text
RISC-V-Assembler-Simulator/
├── src/
│   ├── assembler.py   # The Assembler logic (reads ip.txt -> writes op.txt)
│   └── simulator.py   # The Execution engine (reads op.txt -> writes Op_regs.txt)
├── tests/
│   ├── assembly/      # Source .txt files (Input test cases)
│   └── bin_s/         # Expected binary outputs (Verification)
└── README.md
```
##  How to Run

### Prerequisite
* Python 3.x installed.

### Step 1: Create Input File
In the root directory of the project, create a text file named **`ip.txt`**.
Paste your RISC-V assembly code into it.
*Example content for `ip.txt`:*
```asm
addi x1, x0, 10
addi x2, x0, 20
add x3, x1, x2
beq x0, x0, 0
```
### Step 2: Run Assembler
Run the assembler to convert your ip.txt into machine code.
```bash
python3 src/assembler.py
Result: A file named op.txt will be automatically generated containing the binary code.
```
* **Result:** A file named op.txt will be automatically generated containing the binary code.

###Step 3: Run Simulator
Run the simulator to execute the binary code from op.txt.
```bash
python3 src/simulator.py
```
* **Result:** The execution trace will be saved to Op_regs.txt (or printed to console depending on configuration).

##  Test Suite
The repository includes a comprehensive test suite in the `tests/` folder.
* **`tests/assembly/`**: Source Assembly files.
* **`tests/bin_s/`**: Expected Binary outputs.

**To run a test case:**
1. Copy the content of a file from `tests/assembly/` (e.g., `Ex_test_0.txt`).
2. Paste it into your local `ip.txt`.
3. Run the Assembler and Simulator as shown above.

##  Technical Details
* **Addressing:** Implements Little Endian memory addressing.
* **Register File:** `x0` is hardwired to 0. All other registers are initialized to 0.
* **ISA subset:** RV32I (Base Integer) + Custom Extensions.
