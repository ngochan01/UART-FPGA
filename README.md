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

- **Simulation only** – This project is focused on functional simulation, not hardware deployment.
- Intended for learning and academic research purposes.

## Credits

This project is inspired by and partially based on resources and code examples from **Xiaomeige Electronics**, particularly the document:

> 高云开发板FPGA逻辑设计与验证教程 V1.2

## UART Waveform 
UART RX

<img width="1144" height="427" alt="image" src="https://github.com/user-attachments/assets/fd445823-bf91-4ed0-a890-38604ba563d5" />

UART TX

<img width="1144" height="425" alt="image" src="https://github.com/user-attachments/assets/50711dd9-5f90-40d2-896c-74a7f4b1eb09" />


