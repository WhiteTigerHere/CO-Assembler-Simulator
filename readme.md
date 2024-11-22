
# **RISC-V Assembler and Simulator Framework**

This project involves implementing a subset of the RV32I (RISC-V 32-bit integer) instruction set architecture (ISA). RISC-V is an open-source, load-store ISA increasingly used in open-source hardware development.

---

## **Project Overview**

### **1. Instruction Set Architecture (ISA)**
RISC-V is a load-store architecture where data is first loaded into registers before processing. This ISA supports various instruction formats:
- **R-type:** Register-register arithmetic/logic operations (e.g., `add`, `sub`, `xor`).
- **I-type:** Immediate arithmetic/logic, load operations (e.g., `addi`, `lw`, `jalr`).
- **S-type:** Store operations (e.g., `sw`).
- **U-type:** Upper immediate operations (e.g., `lui`).
- **B-type:** Branch operations (e.g., `beq`, `bne`).
- **J-type:** Jump operations (e.g., `jal`).

### **2. Key Definitions**
- **`rs`:** Source register
- **`rd`:** Destination register
- **`rt`:** Temporary register
- **`imm`:** Immediate value
- **`PC`:** Program Counter
- **`sp`:** Stack Pointer
- **`x0`:** Zero register (always contains `0` and is immutable)

### **3. Instruction and Register Encoding**
Each RISC-V instruction is uniquely encoded in 32 bits. Registers (`x0` to `x31`) are also represented in binary, with `x0` being hardwired to the value `0`. It is recommended to use saved registers for maintaining program state.

---

## **Project Components**

### **1. Assembler**
The assembler translates RISC-V assembly code into 32-bit binary machine code. 

#### **Features:**
- **Input:** Assembly code file (`.txt`)
- **Output:** Machine code file (`.txt`)
- **Error Handling:** 
  - Syntax errors.
  - Invalid registers or immediate values.
  - Unsupported instructions.
- **Location:** `SimpleAssembler/Assembler.py`

#### **Workflow:**
1. Reads assembly instructions.
2. Encodes instructions into binary based on the RISC-V ISA rules.
3. Outputs a machine code file for the simulator.

---

### **2. Simulator**
The simulator executes the binary machine code and generates a trace of executed instructions.

#### **Features:**
- **Input:** Machine code file (`.txt`)
- **Output:** Trace file (`.txt`) showing:
  - **Program Counter (PC):** Updated after each instruction.
  - **Register Values:** State after each operation.
  - **Memory Modifications:** For load/store instructions.
- **Error Handling:**
  - Invalid memory accesses.
  - Division by zero.
  - Unrecognized machine code.
- **Location:** `SimpleSimulator/Simulator.py`

#### **Workflow:**
1. Reads the machine code file.
2. Executes instructions step-by-step, updating registers and memory.
3. Outputs an execution trace showing the state at each step.

---

## **How the Assembler and Simulator Work Together**

### **Workflow:**
1. **Assembler** translates human-readable assembly code into machine-readable binary.
2. **Simulator** executes the machine code and outputs a trace of the program's behavior.

### **End-to-End Process:**
1. Write RISC-V assembly code in a `.txt` file.
2. Run the assembler to generate machine code.
3. Use the simulator to execute the machine code and observe the output trace.

Our project implements the entire ISA architecture and the instruction types.

---

## **Testing Framework**

### **Test Organization**
- **Assembler Tests** (in `tests/assembly/`):
  - **Simple Tests:** Basic functionality (`simpleBin/`).
  - **Hard Tests:** Complex scenarios (`hardBin/`).
  - **Error Generation Tests:** Syntax and edge-case errors (`errorGen/`).
  - **Expected Output:**
    - `bin_s/`: Correct machine code for simple tests.
    - `bin_h/`: Correct machine code for hard tests.
    - `user_bin_s/` & `user_bin_h/`: Student-generated outputs.
  
- **Simulator Tests** (in `tests/bin/` and `tests/traces/`):
  - **Simple Tests:** Basic execution cases.
  - **Hard Tests:** Complex control flow and memory usage.
  - **Expected Output:**
    - `traces/`: Correct execution traces.
    - `bin/`: Student-generated execution traces.

---

## **How to Use the Framework**

### **Assembler**
1. Rename your assembler script to `Assembler.py`.
2. Place it in the `SimpleAssembler/` folder.
3. Use the following command:
   - **Linux:**
     ```bash
     python3 src/main.py --no-sim --linux
     ```
   - **Windows:**
     ```bash
     python3 src\main.py --no-sim --windows
     ```
4. Example:
   ```bash
   python3 Assembler.py tests/assembly/simpleBin/test1.txt tests/assembly/user_bin_s/test1.txt
   ```

### **Simulator**
1. Rename your simulator script to `Simulator.py`.
2. Place it in the `SimpleSimulator/` folder.
3. Use the following command:
   - **Linux:**
     ```bash
     python3 src/main.py --no-asm --linux
     ```
   - **Windows:**
     ```bash
     python3 src\main.py --no-asm --windows
     ```
4. Example:
   ```bash
   python3 Simulator.py tests/assembly/user_bin_s/test1.txt tests/bin/test1_trace.txt
   ```

---

## **Troubleshooting**

### **Common Errors**
1. **General Syntax Error at Line 0:**
   - Verify assembly file format.
   - Ensure correct syntax for registers, instructions, and immediates.
2. **File Not Found:**
   - Ensure all required files are present in the expected directories.
3. **Python Not Found:**
   - Ensure Python 3 is installed and added to the system PATH.

---


## **Resources**
- [RISC-V Official Documentation](https://riscv.org/)
- [RV32I Instruction Reference](https://msyksphinz-self.github.io/riscv-isadoc/html/rvi.html)
- [RISC-V Simulator Demo](https://ascslab.org/research/briscv/simulator/simulator.html)

--- 
