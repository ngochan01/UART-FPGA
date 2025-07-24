Link youtube: 
https://youtu.be/fD2b4xtbNiw?si=n9lRd3FgZIARJVv7 ( uart transmitter)
https://youtu.be/PrWgCfWXQog?si=6nKUGdaXlZfS4y0V ( uart receiver )
# UART Module on FPGA – Simulation with Xilinx ISE

This project implements a UART (Universal Asynchronous Receiver/Transmitter) module using Verilog HDL, designed and simulated entirely in the Xilinx environment. The system includes both transmission (TX) and reception (RX) modules, featuring multi-sampling and noise-resilient techniques suitable for industrial applications.

## Features

- UART TX and RX modules with 1 start bit, 8 data bits, 1 stop bit
- Baud rate support: 9600, 19200, 38400, 57600, 115200 bps
- Oversampling and majority voting for noise reduction
- Testbench with loopback functionality
- Written in Verilog HDL
- Simulated using Xilinx tools

## Project Scope

- Simulation only – This project is focused on functional simulation, not hardware deployment.
- Intended for learning and academic research purposes.

## Credits

This project is inspired by and partially based on resources and code examples from Xiaomeige Electronics, particularly the document:

> 高云开发板FPGA逻辑设计与验证教程 V1.2

## UART Waveform 
UART RX

<img width="1144" height="427" alt="image" src="https://github.com/user-attachments/assets/fd445823-bf91-4ed0-a890-38604ba563d5" />
## Signal Analysis: 0 – 3000ns

### Initial Configuration
- `baud_set[2:0] = 000` (baud rate 9600 – the slowest)
- `reset_n = 1` (system is reset and operates normally)
- `clk` runs continuously with a 20ns cycle (50MHz)

### First Byte Transmission (`0b10101010`)
At around **1400ns**:
- `data_byte_tx[7:0] = 10101010` is loaded
- `send_en` triggers with a short pulse to start transmission
- `uart_state = 1` (TX module becomes active)
- `uart_tx_rx`: initially HIGH (idle), then pulled LOW to send the Start bit (bit 0)

### Data Reception
- RX module receives data from `uart_tx_rx`
- Initial `data_byte_rx[7:0] = 00000000`
- After reception: `data_byte_rx[7:0] = 10101010` (`0xAA`)
- `rx_done` signal will pulse to indicate reception is complete (not visible in this time window)

### Timing Characteristics
- At `baud_set = 0`, each UART bit ≈ 104.16μs (for 9600 baud)
- However, waveform only covers up to 3000ns → not enough to show full byte transmission

### System State at 3000ns
- `tx_done = 0` (transmission not yet complete)
- System is still in the Start bit phase of transmission


UART TX

<img width="1144" height="425" alt="image" src="https://github.com/user-attachments/assets/50711dd9-5f90-40d2-896c-74a7f4b1eb09" />

## Waveform Progress

### Initial State
- `reset_n = 1` → System active
- `send_en = 0`
- `uart_tx = 1` (idle state)

### First Transmission (~35 μs)
- `send_en = 1` → 1 pulse to start transmission
- `data_byte = 0b10101010`
- `uart_tx` behavior:
  - Drops to `0` (Start bit)
  - Sends 8 bits, LSB first
  - Rises to `1` (Stop bit)

### Second Transmission (~200 μs)
- `send_en = 1` → 1 pulse to start transmission
- `data_byte = 0b01010101`
- `uart_tx` repeats the same transmission process

### Other Notes
- `baud_set = 100` → High baud rate (faster transmission)
- `tx_done = 1` when the full stop bit is transmitted

