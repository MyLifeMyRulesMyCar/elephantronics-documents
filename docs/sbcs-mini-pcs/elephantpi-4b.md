# 🖥️ ElephantPi 4B

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Single Board Computer</span>

> **Industrial brains in a compact box.** The ElephantPi 4B is built around the Raspberry Pi Compute Module 4, housed in a rugged aluminium carrier board with dual Gigabit Ethernet, M.2 NVMe, wide-voltage DC input, and isolated RS485/RS232 — ready for real-world industrial deployment.

---

## Quick Start

<div class="quick-start">
<h4>⚡ Running Linux in 10 minutes</h4>

1. Flash the ElephantPi OS image to an M.2 SSD or eMMC
2. Insert SSD / CM4 module into the carrier board
3. Connect 9–36V DC power
4. SSH in or connect HDMI + USB keyboard

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Compute Module (CM4)</th></tr>
<tr><td>CPU</td><td><strong>Broadcom BCM2711 Quad-core Cortex-A72 @ 1.8 GHz</strong></td></tr>
<tr><td>RAM Options</td><td>2 GB / 4 GB / 8 GB LPDDR4X</td></tr>
<tr><td>eMMC Options</td><td>0 GB (Lite) / 8 GB / 16 GB / 32 GB</td></tr>
<tr><th colspan="2">Carrier Board I/O</th></tr>
<tr><td>Ethernet</td><td>2 × Gigabit (one isolated for fieldbus)</td></tr>
<tr><td>USB</td><td>2 × USB-A 3.0, 1 × USB-C OTG</td></tr>
<tr><td>Serial</td><td>1 × RS485 (isolated), 1 × RS232</td></tr>
<tr><td>Storage</td><td>1 × M.2 2280 NVMe (PCIe Gen 2)</td></tr>
<tr><td>Display</td><td>1 × HDMI 2.0 (4K@30fps)</td></tr>
<tr><td>GPIO</td><td>40-pin HAT-compatible header</td></tr>
<tr><th colspan="2">Power</th></tr>
<tr><td>Input Voltage</td><td><strong>9–36V DC</strong> (terminal block)</td></tr>
<tr><td>Power Consumption</td><td>5–12W typical</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Dimensions</td><td>130 × 90 × 40 mm</td></tr>
<tr><td>Mounting</td><td>DIN rail clip or 4× M3 standoffs</td></tr>
<tr><td>Operating Temperature</td><td>-20°C to +60°C</td></tr>
<tr><td>Protection</td><td>IP20</td></tr>
</table>

---

## OS Setup

### Download the image

```bash
# ElephantPi OS (Debian 12 Bookworm based)
https://downloads.elephantronics.com/elephantpi/os/latest.img.xz

# Verify checksum
sha256sum latest.img.xz
```

### Flash to M.2 SSD

Use **Raspberry Pi Imager** or `dd`:

```bash
# Using dd (Linux/macOS)
xz -d latest.img.xz
sudo dd if=latest.img of=/dev/sdX bs=4M status=progress
```

!!! tip "Headless SSH"
    Create an empty file called `ssh` in the `/boot` partition after flashing to enable SSH on first boot.

### First boot

Default credentials:
```
Username: elephant
Password: elephant123
```

---

## Serial Ports

### RS485 (isolated)

The RS485 port is isolated from the main board — safe for connecting to PLCs and industrial sensors without ground loops.

```bash
# Device node
/dev/ttyRS485   # or /dev/ttyAMA2 depending on OS version

# Test with minicom
sudo apt install minicom
minicom -D /dev/ttyRS485 -b 9600
```

Python example — read Modbus register from PLC:

```python
from pymodbus.client import ModbusSerialClient

client = ModbusSerialClient(
    port='/dev/ttyRS485',
    baudrate=9600,
    parity='N',
    stopbits=1,
    bytesize=8
)
client.connect()
result = client.read_holding_registers(address=0, count=4, slave=1)
print(result.registers)
```

---

## GPIO

The 40-pin GPIO header is fully compatible with Raspberry Pi HATs. Use `gpiozero` or `RPi.GPIO`:

```python
from gpiozero import LED, Button

led = LED(17)
btn = Button(27)

btn.when_pressed = led.on
btn.when_released = led.off
```

---

## Watchdog

Enable the hardware watchdog for reliable unattended operation:

```bash
# Enable on boot
echo 'dtparam=watchdog=on' | sudo tee -a /boot/config.txt
sudo reboot

# Configure watchdog daemon
sudo apt install watchdog
sudo systemctl enable watchdog
```
