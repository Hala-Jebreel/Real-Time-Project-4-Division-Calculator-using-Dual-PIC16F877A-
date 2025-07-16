# ⚙️ Real-Time Dual-PIC Division Calculator (Project 4)

## 📌 Overview

This project implements a **floating-point division calculator** using **two PIC16F877A microcontrollers** connected via `PORTC`. The calculator supports digit-by-digit input via a single push button, displays output on a 16x2 LCD, and performs the actual division on the co-processor PIC.

Developed for **ENCS4330: Real-Time Applications & Embedded Systems** at **Birzeit University** using **Assembly language in MPLAB IDE** and simulated in **Proteus 8 Professional**.

---

## 🧩 Key Features

- 🔢 Input two float numbers (up to `999999.999999`) using one push button `P`
- ⏱️ Digit auto-lock after 1 second of inactivity
- 📄 Auto-fill all digits based on the first digit value
- 🔁 Manual override of any digit
- 🧮 Division computed by a **co-processor** PIC and result sent back to master
- 📺 LCD displays:
  - Welcome message blinking 3 times
  - Real-time digit entry with cursor
  - Final result with cycle views (Number 1 → Number 2 → Result)
- 🎯 Double-click to skip stages or restart the process

---

## 🔗 System Architecture

- `Master PIC` (handles LCD, input, communication)
- `Auxiliary PIC` (co-processor that does the math)
- 16x2 **LCD** (connected to PortD in 4-bit mode)
- **Push Button P** (connected to PortB.0, with 10kΩ pull-up)
- **PortC** (8-bit data bus for communication)
- 4 MHz crystal oscillator with 2x15pF capacitors

---

## 🖥️ Hardware Setup

| Component     | Connection               |
|---------------|---------------------------|
| LCD           | PortD (4-bit mode)        |
| Push Button P | PortB.0 (with pull-up)    |
| Data Bus      | PortC (for both PICs)     |
| Crystal       | 4 MHz + 2 × 15pF caps     |
| RS Resistor   | 4.7kΩ to RS of LCD        |
| MCLR Pull-up  | 10kΩ                      |

---

## 🧠 Software Behavior

### Power-On Sequence

1. Blink “Welcome to” / “Division” on LCD 3 times (0.5s delay)
2. Wait 2 seconds

### Number Entry (Digit-by-Digit)

- Show **“Number 1”** → input integer + decimal
- Lock digits after 1s inactivity
- Auto-fill remaining digits with first digit
- Double-click to skip part or proceed

### After Input

- Send both numbers to the **co-processor**
- Master waits for **interrupt-based acknowledgment** after each byte
- Co-processor returns division **result byte-by-byte**
- Display **“Result”** on LCD with value

### Post-Result Navigation

- Button click cycles: `Number 1` → `Number 2` → `Result`
- Double-click restarts input sequence

---

## 📂 Files Structure

.
├── master_code.asm # Assembly code for master PIC
├── auxiliary_code.asm # Assembly code for co-processor PIC
├── RealProject4.pdsprj # MPLAB project file
├── RealProject4.pdsbak # MPLAB project backup
├── Proteus schematic # Schematic with 2 PICs, LCD, button, and wiring
├── Checklist.pdf # Project checklist
├── project4_hard_202502.pdf # Full project description
└── README.md # This file

yaml
Copy
Edit

---

## 🧪 Checklist Summary ✅

✔ Welcome & Division blinking  
✔ Digit auto-lock, wrap from 9→0  
✔ Auto-fill digits & manual override  
✔ Double-click to skip input stages  
✔ PortC communication with ACK interrupts  
✔ Result display logic  
✔ Button cycles between values  
✔ Fully working Proteus schematic

(See full checklist in `Checklist.pdf`)

---

## 👩‍💻 Authors

- **Hala Jebreel** 
- **Talin Abuzulof** 
- **Mays Ajaleen** 
- **Mayar Jafar**
- Instructor: **Dr. Hanna Bullata**  
- Course: **ENCS4330 – Real-Time Applications & Embedded Systems**  
- University: **Birzeit University**  
- Semester: **Spring 2024/2025**

---

## 📸 Screenshots (optional)

Include screenshots of:

- Welcome screen  
- Number entry  
- Final result screen  
- Proteus schematic

---

## 📄 License

This project is intended for academic purposes only.  
All rights reserved © 2025.
