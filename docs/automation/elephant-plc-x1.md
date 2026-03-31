# ⚙️ ElephantPLC X1

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Programmable Logic Controller</span>&nbsp;
<span class="badge badge-orange">24 I/O</span>

> **Industrial reliability, compact footprint.** The ElephantPLC X1 is a 24 I/O PLC supporting all IEC 61131-3 programming languages, DIN-rail mounting, and communication via Modbus RTU/TCP and EtherNet/IP — ready for your production line on day one.

---

## Quick Start

<div class="quick-start">
<h4>⚡ First program in 4 steps</h4>

1. Mount on DIN rail and connect 24V DC power
2. Wire your inputs (sensors) and outputs (actuators)
3. Install **ElephantStudio IDE** on your PC
4. Write a ladder logic program and upload via Ethernet

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">I/O</th></tr>
<tr><td>Digital Inputs</td><td><strong>14 × 24V DC</strong></td></tr>
<tr><td>Digital Outputs</td><td>10 × Relay (5A / 250V AC)</td></tr>
<tr><td>Analog Inputs</td><td>4 × 0–10V / 4–20mA (selectable)</td></tr>
<tr><td>Analog Outputs</td><td>2 × 0–10V</td></tr>
<tr><th colspan="2">Processor</th></tr>
<tr><td>CPU</td><td>ARM Cortex-M4 @ 168 MHz</td></tr>
<tr><td>Program Memory</td><td>512 KB Flash</td></tr>
<tr><td>Data Memory</td><td>64 KB SRAM</td></tr>
<tr><th colspan="2">Communication</th></tr>
<tr><td>Ethernet</td><td>1 × 10/100 Mbps (Modbus TCP, EtherNet/IP)</td></tr>
<tr><td>Serial</td><td>2 × RS485 (Modbus RTU)</td></tr>
<tr><td>USB</td><td>1 × USB-B (programming)</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Mounting</td><td>DIN Rail (EN 60715)</td></tr>
<tr><td>Power Supply</td><td>24V DC (±15%), 3W</td></tr>
<tr><td>Protection</td><td>IP20</td></tr>
<tr><td>Operating Temperature</td><td>-10°C to +55°C</td></tr>
</table>

---

## I/O Wiring

=== "Digital Inputs"

    ```
    Sensor COM  ──→  DI Common (0V)
    Sensor NO   ──→  DI0 … DI13
    ```

    All digital inputs are optically isolated. Pull-up resistors are built in.

=== "Digital Outputs"

    ```
    Load (+)  ──→  DO0 Common
    Load (-)  ──→  DO0 … DO9
    ```

    !!! warning "Relay ratings"
        Max 5A per relay output. Use external contactors for motors and large loads.

=== "Analog Inputs"

    ```
    Sensor signal  ──→  AI0 … AI3
    Sensor GND     ──→  AI GND
    ```

    Select 0–10V or 4–20mA via DIP switch SW1–SW4 on the module.

---

## Programming

ElephantPLC X1 supports all IEC 61131-3 languages:

| Language | Best for |
|---|---|
| **Ladder Diagram (LD)** | Simple relay-logic replacements |
| **Structured Text (ST)** | Mathematical calculations, loops |
| **Function Block Diagram (FBD)** | Signal processing, PID loops |
| **Sequential Function Chart (SFC)** | State machines, step sequences |

### Install ElephantStudio IDE

```bash
# Windows installer
https://downloads.elephantronics.com/studio/latest

# Minimum requirements
OS: Windows 10 / 11
RAM: 4 GB
Disk: 500 MB
```

### Upload your first program

1. Open ElephantStudio → **New Project** → select *X1*
2. Write your ladder logic in the **Main POU**
3. Go to **Online → Connect** (enter PLC IP: `192.168.1.100`)
4. Click **Download** then **Run**

---

## Modbus

### Modbus RTU (RS485)

Configure in: **System Settings → Communication → COM1**

```
Baud Rate:    9600 (default)
Data Bits:    8
Parity:       None
Stop Bits:    1
Device ID:    1 (adjustable 1–247)
```

### Modbus TCP

The PLC listens on **port 502** by default. Register map:

| Address | Type | Description |
|---|---|---|
| `0x0000–0x000D` | Coils | Digital Outputs DO0–DO13 |
| `0x0100–0x010D` | Discrete | Digital Inputs DI0–DI13 |
| `0x0200–0x0203` | Holding | Analog Inputs AI0–AI3 |

---

## Troubleshooting

| Issue | Fix |
|---|---|
| Can't connect via Ethernet | Check IP address; default is `192.168.1.100` |
| Output relay not switching | Verify load wiring and relay common connection |
| Analog reading incorrect | Check DIP switch position for V/mA mode |
