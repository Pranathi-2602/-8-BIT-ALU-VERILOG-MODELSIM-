// alu.v - 8-bit ALU
module alu (
    input  [7:0] A, B,        // Two 8-bit inputs
    input  [2:0] opcode,      // Operation selector (3 bits)
    output reg [7:0] result,  // Result of operation
    output reg carry          // Carry/borrow/shift-out
);

always @(*) begin
    result = 8'd0; carry = 1'b0;  // default values

    case(opcode)
      3'b000: {carry, result} = A + B;   // ADD
      3'b001: {carry, result} = A - B;   // SUB
      3'b010: result = A & B;            // AND
      3'b011: result = A | B;            // OR
      3'b100: result = A ^ B;            // XOR
      3'b101: result = ~A;               // NOT
      3'b110: begin result = A << 1; carry = A[7]; end // SHL
      3'b111: begin result = A >> 1; carry = A[0]; end // SHR
    endcase
end

endmodule

//testbench

`timescale 1ns/1ps
module tb_alu;
  reg  [7:0] A, B;
  reg  [2:0] opcode;
  wire [7:0] result;
  wire carry;

  alu dut(A, B, opcode, result, carry); // instantiate ALU

  initial begin
    A = 8'd10; B = 8'd5; // Example values: A=10 (00001010), B=5 (00000101)

    // Try all operations one by one
    opcode=3'b000; #10; // ADD
    opcode=3'b001; #10; // SUB
    opcode=3'b010; #10; // AND
    opcode=3'b011; #10; // OR
    opcode=3'b100; #10; // XOR
    opcode=3'b101; #10; // NOT
    opcode=3'b110; #10; // SHL
    opcode=3'b111; #10; // SHR

    $stop;
  end
endmodule

<img width="1411" height="596" alt="Screenshot 2025-08-25 112636" src="https://github.com/user-attachments/assets/b4c1a20e-c83c-47cc-a007-8cabd1b23bc8" />
![alu_8bit_samop](https://github.com/user-attachments/assets/01d8edcc-b761-412b-ac6c-f7207b474924)
<img width="1920" height="1080" alt="Screenshot 2025-08-25 112515" src="https://github.com/user-attachments/assets/050deff1-2537-4b62-84db-60d36be9aaec" />


# 8-Bit ALU (Verilog, ModelSim)

## 📌 Project Overview
This project implements an **8-bit Arithmetic Logic Unit (ALU)** in Verilog.  
It performs basic arithmetic and logic operations with **flag registers**.  
The design is verified using **testbenches in ModelSim**.

## 🛠️ Tools & Technologies
- Verilog HDL
- ModelSim (Simulation)

## ⚙️ Features
- Supports arithmetic (Add, Subtract, Increment, Decrement)  
- Logic operations (AND, OR, XOR, NOT)  
- Flags: Zero, Carry, Overflow

## 🚀 How to Run
1. Open the ALU project in ModelSim.  
2. Compile the Verilog files (`alu.v` and `alu_tb.v`).  
3. Run simulation and verify results.  


