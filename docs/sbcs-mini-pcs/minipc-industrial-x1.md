# 🖥️ MiniPC Industrial X1

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Industrial Mini PC</span>

> **Full x86 power, built for the factory floor.** The MiniPC Industrial X1 is a fanless Intel Core i5 mini PC engineered to run 24/7 in harsh environments — vibration, dust, heat, and wide voltage swings. Run Windows 11, Ubuntu, or your SCADA/HMI software without compromise.

---

## Quick Start

<div class="quick-start">
<h4>⚡ Live in 5 minutes</h4>

1. Mount on DIN rail or VESA bracket
2. Connect 9–48V DC power
3. Connect HDMI display, USB keyboard/mouse
4. Boot from pre-installed Windows 11 IoT Enterprise or Ubuntu 22.04

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Compute</th></tr>
<tr><td>CPU</td><td><strong>Intel Core i5-1235U (12th Gen, 10 cores)</strong></td></tr>
<tr><td>RAM</td><td>16 GB DDR4 SO-DIMM (1 slot, max 32 GB)</td></tr>
<tr><td>Storage</td><td>256 GB NVMe SSD (M.2 2280) + 2.5" SATA bay</td></tr>
<tr><td>Graphics</td><td>Intel Iris Xe (96 EU)</td></tr>
<tr><th colspan="2">Industrial I/O</th></tr>
<tr><td>Serial Ports</td><td>4 × COM (2× RS232, 2× RS485, software selectable)</td></tr>
<tr><td>Digital I/O</td><td>8 × isolated DI, 4 × isolated DO</td></tr>
<tr><td>CAN Bus</td><td>1 × CAN 2.0B (isolated)</td></tr>
<tr><th colspan="2">Standard I/O</th></tr>
<tr><td>USB</td><td>4 × USB 3.2, 2 × USB 2.0</td></tr>
<tr><td>Ethernet</td><td>2 × Intel i225 2.5GbE</td></tr>
<tr><td>Display</td><td>2 × HDMI 2.0 (dual monitor)</td></tr>
<tr><td>Audio</td><td>3.5mm line out (alarm/speaker)</td></tr>
<tr><th colspan="2">Power & Environment</th></tr>
<tr><td>Input Voltage</td><td><strong>9–48V DC</strong> (wide range, reverse-polarity protected)</td></tr>
<tr><td>Typical Power</td><td>18–45W</td></tr>
<tr><td>Operating Temperature</td><td><strong>-20°C to +70°C</strong></td></tr>
<tr><td>Storage Temperature</td><td>-40°C to +85°C</td></tr>
<tr><td>Vibration</td><td>5G, IEC 60068-2-64</td></tr>
<tr><td>Shock</td><td>50G, IEC 60068-2-27</td></tr>
<tr><td>Cooling</td><td>Fully fanless aluminium chassis</td></tr>
<tr><td>Protection</td><td>IP40</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Dimensions</td><td>195 × 135 × 50 mm</td></tr>
<tr><td>Mounting</td><td>DIN rail / VESA 75×75 / desktop</td></tr>
<tr><td>Weight</td><td>1.4 kg</td></tr>
</table>

---

## OS Setup

=== "Windows 11 IoT Enterprise (pre-installed)"

    The unit ships with Windows 11 IoT Enterprise pre-activated. On first boot:

    1. Complete the Windows OOBE (region, language, account)
    2. Run **Windows Update** to get latest drivers
    3. Install your SCADA/HMI software (WinCC, Ignition, Inductive Automation, etc.)

=== "Ubuntu 22.04 LTS"

    ```bash
    # Download Ubuntu 22.04 Desktop ISO
    https://releases.ubuntu.com/22.04/

    # Flash to USB with Rufus (Windows) or dd (Linux)
    sudo dd if=ubuntu-22.04-desktop-amd64.iso of=/dev/sdX bs=4M status=progress

    # Boot from USB and run installer
    # Select NVMe SSD as installation target
    ```

    !!! tip
        Install `linux-modules-extra-$(uname -r)` after first boot to get all Intel NIC and GPU drivers.

---

## Serial Ports (COM)

The 4 COM ports are software-configurable between RS232 and RS485 mode:

```
COM1 → RS232 (DB9 Male)   default
COM2 → RS232 (DB9 Male)   default
COM3 → RS485 (terminal)   default
COM4 → RS485 (terminal)   default
```

Switch mode via jumper JP1–JP4 (see motherboard label) or via the **Elephant Port Manager** utility (Windows).

### Linux device names

```bash
COM1 → /dev/ttyS0
COM2 → /dev/ttyS1
COM3 → /dev/ttyS2
COM4 → /dev/ttyS3
```

---

## Watchdog Timer

Enable the hardware watchdog to automatically recover from software hangs:

=== "Windows"

    The **Elephant Watchdog Service** is pre-installed. Enable it:

    ```
    Services → ElephantWatchdog → Start
    Set timeout: 60 seconds (recommended)
    ```

=== "Linux"

    ```bash
    # Install watchdog daemon
    sudo apt install watchdog

    # Configure /etc/watchdog.conf
    watchdog-device = /dev/watchdog
    watchdog-timeout = 60
    interval = 10

    sudo systemctl enable --now watchdog
    ```

---

## Troubleshooting

| Issue | Fix |
|---|---|
| No display output | Check HDMI cable; try second HDMI port |
| High CPU temperature | Check ambient temperature; ensure ventilation slots are clear |
| COM port not detected | Verify jumper mode setting; check Device Manager (Windows) |
| System won't boot | Hold power button 10s to force off; check SSD seating |
