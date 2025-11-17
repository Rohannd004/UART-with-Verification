# UART Protocol (Verilog HDL)
## 9600 Baud • 8 Data Bits • No Parity (8N1) • Fully Synthesizable

------------------------------------------------------------
Project: UART TX + RX + Baud Rate Generator  
Author : Rohan N D  
Language: Verilog HDL  
Tool   : Xilinx Vivado  
------------------------------------------------------------

# 📘 Project Overview
This project implements a complete UART communication system that includes:
- UART Transmitter (TX)
- UART Receiver (RX)
- Baud Rate Generator
- Top-level Integration Module
- Full Loopback Testbench

The UART follows the **8N1 Frame Format**:
- 8 Data bits
- No Parity
- 1 Stop bit

Baud Rate: **9600**  
Clock: **100 MHz**

------------------------------------------------------------

# 🧱 Block Diagram (Insert Image Here)

TODO: Insert your schematic/block diagram  
Example:
![Block Diagram](images/uart_block_diagram.png)

------------------------------------------------------------

# 📂 Module Descriptions

------------------------------------------------------------
## 1. baud_rate_generator.v
Generates:
- tx_clk_en (baud pulse for transmitter)
- rx_clk_en (16× oversampling pulse for receiver)

Key Parameters:
- clk_freq = 100_000_000
- baud_rate = 9600

------------------------------------------------------------
## 2. sender.v (UART Transmitter)
Transmitter FSM:
- STATE_IDLE
- STATE_START
- STATE_DATA (8-bit shift)
- STATE_STOP

Frame Format:
Start(0) → d0 → d1 → d2 → d3 → d4 → d5 → d6 → d7 → Stop(1)

Parity: NOT INCLUDED (8N1)

------------------------------------------------------------
## 3. rx.v (UART Receiver)
Receiver uses **16× oversampling**.

Receiver FSM:
- RX_STATE_START
- RX_STATE_DATA
- RX_STATE_STOP

Outputs:
- data_out : received byte
- rdy      : data valid flag

Parity Check: NOT INCLUDED

------------------------------------------------------------
## 4. top.v (Integration Module)
Connects:
- Baud rate generator
- TX module
- RX module

Acts as complete UART system for FPGA implementation.

------------------------------------------------------------
## 5. uart_tb.v (Testbench)
Includes:
- send_byte() task
- clear_ready() task
- Displays received data on console
- Full loopback (TX → RX)

Testbench sends:
- 0x41 ('A')
- 0x55 (01010101 pattern)

------------------------------------------------------------

# 📈 Simulation Waveform (Insert Image Here)

TODO: Insert your simulation waveform  
Example:
![Waveform](images/uart_waveform.png)

------------------------------------------------------------

# ▶️ Running Simulation (Vivado)

1. Open Vivado → New Project  
2. Add all `.v` files  
3. Set **uart_top_tb** as simulation top  
4. Run Behavioral Simulation  
5. Observe:
   - TX waveform
   - RX reception
   - rdy = 1 after each byte

------------------------------------------------------------

# ▶️ FPGA Implementation Guide

Pin Mapping Example (Basys 3):

| Signal | Pin | Description      |
|--------|-----|------------------|
| clk    | W5  | 100 MHz clock    |
| rst    | BTN0| Reset input      |
| tx     | JA1 | UART TX output   |
| rx     | JA2 | UART RX input    |

------------------------------------------------------------

# 🧪 Test Results
Simulation Output:
received data is 41  
received data is 55  

------------------------------------------------------------

# 🔮 Future Improvements
- Add parity (even/odd)
- Parity error detection
- Framing error detection
- Configurable baud rate
- FIFO for TX/RX

------------------------------------------------------------

# 👤 Author
**Rohan N D**  
Electronics and VLSI Engineering  

------------------------------------------------------------
# 📁 Repository Structure

UART/
│── src/
│   ├── baud_rate_generator.v
│   ├── sender.v
│   ├── rx.v
│   ├── top.v
│── tb/
│   ├── uart_tb.v
│── images/
│   ├── uart_waveform.png
│   ├── uart_block_diagram.png
│── README.md

------------------------------------------------------------
