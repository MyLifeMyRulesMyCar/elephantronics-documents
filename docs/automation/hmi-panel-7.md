# ⚙️ HMI Panel 7"

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">HMI Touchscreen</span>

> **See your process, control your process.** The 7" HMI Panel gives operators a clear, responsive window into any PLC-driven system — from conveyor speeds to tank levels — with drag-and-drop screen design and built-in alarms.

---

## Quick Start

<div class="quick-start">
<h4>⚡ Live display in 3 steps</h4>

1. Connect power and wire RS485 to your PLC
2. Design your screen in **ElephantHMI Designer** on your PC
3. Transfer project via USB stick or Ethernet and go live

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Display</th></tr>
<tr><td>Screen Size</td><td><strong>7.0" IPS LCD</strong></td></tr>
<tr><td>Resolution</td><td>800 × 480 pixels</td></tr>
<tr><td>Brightness</td><td>400 cd/m²</td></tr>
<tr><td>Touch Type</td><td>5-point capacitive</td></tr>
<tr><td>Viewing Angle</td><td>170° H / 170° V</td></tr>
<tr><th colspan="2">Communication</th></tr>
<tr><td>Ethernet</td><td>1 × 10/100 Mbps</td></tr>
<tr><td>Serial</td><td>1 × RS485, 1 × RS232</td></tr>
<tr><td>USB Host</td><td>1 × USB-A (project transfer)</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Panel Cutout</td><td>192 × 138 mm</td></tr>
<tr><td>Front Protection</td><td>IP65</td></tr>
<tr><td>Power</td><td>24V DC, 6W</td></tr>
</table>

---

## PLC Connection

=== "RS485 (Modbus RTU)"

    ```
    HMI A+  ──→  PLC RS485 A
    HMI B-  ──→  PLC RS485 B
    HMI GND ──→  PLC Signal GND
    ```

    In ElephantHMI Designer → **Device Settings**:
    - Protocol: `Modbus RTU`
    - Baud: `9600`
    - Station ID: `1`

=== "Ethernet (Modbus TCP)"

    Connect both HMI and PLC to the same network switch.

    In ElephantHMI Designer → **Device Settings**:
    - Protocol: `Modbus TCP`
    - PLC IP: `192.168.1.100`
    - Port: `502`

---

## Screen Design

The **ElephantHMI Designer** software (free download) provides:

- Drag-and-drop widget library (gauges, buttons, bars, charts)
- Tag browser — link any widget directly to PLC registers
- Alarm management with email/SMS notification
- Recipe management for multi-product lines
- Multi-language support (UTF-8)

### Transfer project to panel

=== "USB Stick"
    1. In Designer: **File → Export → USB Package**
    2. Copy to a FAT32 USB stick
    3. Insert into HMI Panel → it prompts to update automatically

=== "Ethernet"
    1. In Designer: **Online → Download**
    2. Enter HMI IP address (default `192.168.1.200`)
    3. Transfer completes in ~30 seconds
