# Chip 8 Assembler 

## What is it?

This project is a Chip 8 assembler written in Python 2.7. The assembler will 
take valid Chip 8 assembly statements and generate a binary file containing
the correct machine instructions.


## Requirements

The only requirements for this project is:

* [Python 2.7](http://www.python.org)


## Installation

To install the source files, simply clone the repository in the directory
of your choice:

    git clone https://github.com/craigthomas/Chip8Assembler.git


## Usage

To run the assembler:

    python chip8asm/chip8asm.py input_file -o output_file

This will assemble the instructions found in file `input_file` and will generate
the associated Chip 8 machine instructions in binary format in `output_file`.
Additional options include printing the symbol table:

    python chip8asm/chip8asm.py test.asm -s

Which will have the following output:

    -- Symbol Table --
    start 0x200
    data1 0x209
    data 0x208

Print out the assembled version of the input:

    python chip8asm/chip8asm.py test.asm -p

Which will have the following output:

    -- Assembled Statements --
    0x0200 6100      start  LOAD           r1,$0  # Clear contents of register 1            
    0x0202 7101              ADD           r1,$1  # Add 1 to the register                   
    0x0204 310A              SKE           r1,$A  # Check to see if we are at 10            
    0x0206 1200             JUMP           start  # Jump back to the start                  
    0x0208 1208        end  JUMP             end  # Loop forever                  


## Format

The input file needs to follow the format below:

    LABEL    MNEMONIC    OPERANDS    COMMENT

Where:

* `LABEL` is a 15 character label for the statement
* `MNEMONIC` is a Chip 8 operation mnemonic from the table below
* `OPERANDS` are registers, values or labels, as described in detail below
* `COMMENT` is a 30 character comment describing the statement

### Mnemonic Table

The assembler supports the following Mnemonics:

| Mnemonic | Opcode | Operands | Description |
| -------- | ------ | :------: | ----------- |
| `SYS`    | `0nnn` | 1 | System call (ignored)                                        |
| `CLR`    | `00E0` | 0 | Clear the screen                                             |
| `RTS`    | `00EE` | 0 | Return from subroutine                                       |
| `JUMP`   | `1nnn` | 1 | Jump to address `nnn`                                        |
| `CALL`   | `2nnn` | 1 | Call routine at address `nnn`                                |
| `SKE`    | `3snn` | 2 | Skip next instruction if register `s` equals `nn`            |
| `SKNE`   | `4snn` | 2 | Do not skip next instruction if register `s` equals `nn`     |
| `SKRE`   | `5st0` | 2 | Skip if register `s` equals register `t`                     |
| `LOAD`   | `6snn` | 2 | Load register `s` with value `nn`                            |
| `ADD`    | `7snn` | 2 | Add value `nn` to register `s`                               |
| `MOVE`   | `8st0` | 2 | Move value from register `s` to register `t`                 |
| `OR`     | `8st1` | 2 | Perform logical OR on register `s` and `t` and store in `t`  |
| `AND`    | `8st2` | 2 | Perform logical AND on register `s` and `t` and store in `t` |
| `XOR`    | `8st3` | 2 | Perform logical XOR on register `s` and `t` and store in `t` |
| `ADDR`   | `8st4` | 2 | Add `s` to `t` and store in `s` - register `F` set on carry  |
| `SUB`    | `8st5` | 2 | Subtract `s` from `t` and store in `s` - register `F` set on !borrow         |
| `SHR`    | `8s06` | 1 | Shift bits in register `s` 1 bit to the right - bit 0 shifts to register `F` |
| `SHL`    | `8s0E` | 1 | Shift bits in register `s` 1 bit to the left - bit 7 shifts to register `F`  |
| `SKRNE`  | `9st0` | 2 | Skip next instruction if register `s` not equal register `t` |
| `LOADI`  | `Annn` | 1 | Load index with value `nnn`                                  |
| `JUMPI`  | `Bnnn` | 1 | Jump to address `nnn` + index                                |
| `RAND`   | `Ctnn` | 2 | Generate random number between 0 and `nn` and store in `t`   |
| `DRAW`   | `Dstn` | 3 | Draw `n` bit sprite at x location reg `s`, y location reg `t` |

## License

Please see the file called LICENSE.


## Further Documentation

The best documentation is in the code itself. Please feel free to examine the
code and experiment with it. 
