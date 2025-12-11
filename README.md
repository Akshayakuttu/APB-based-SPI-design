# APB-based-SPI-design
A modular APB-based SPI Master design implemented in Verilog, featuring baud rate generation, shift register logic, APB slave interface, and slave select control.
# APB-Based SPI Master Design (Verilog HDL)

This project implements a fully synthesizable **SPI Master** that is accessible through an **AMBA APB (Advanced Peripheral Bus)** interface.  
The design is modular, cleanly partitioned, and easy to integrate in SoC designs.

The SPI Master consists of four main RTL blocks:

- **Baud Rate Generator**  
- **Shift Register**  
- **APB Slave Interface**  
- **SPI Slave Select & Control Block**

The top module connects these blocks to form a complete SPI master with APB programmability.

---

## **Project Objective**

To design a Verilog-based SPI Master that communicates over APB and supports:

- Programmable SCLK frequency  
- Interrupt generation  
- Data transfers via shift register  
- Slave select control  
- Full APB read/write operations

1️⃣ Baud Rate Generator
	•	Generates programmable SCLK for SPI transactions
	•	Frequency derived from APB PCLK
	•	Contains counter logic + divider register
2️⃣ Shift Register
	•	Performs serial-to-parallel and parallel-to-serial conversion
	•	Handles MOSI/MISO sequencing
	•	Driven by SCLK from the baud generator
3️⃣ APB Slave Interface
	•	Decodes APB signals: PADDR, PWDATA, PWRITE, PSEL, PENABLE
	•	Generates PRDATA, PREADY, PSLVERR
	•	Writes to configuration registers used by other blocks
4️⃣ Slave Select & Control Block
	•	Drives chip select (ss) for SPI slaves
	•	Controls enable, interrupt generation, and transaction start
	•	Interacts with shift register and baud generator
  
 Top Module

Integrates all four submodules and provides APB + SPI top-level I/O:

APB Inputs:
PCLK, PRESETn, PADDR, PWRITE, PSEL, PENABLE, PWDATA

SPI Outputs:
ss, sclk, mosi, spi_interrupt_request

APB Outputs:
PRDATA, PREADY, PSLVERR
