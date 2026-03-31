# ⚙️ HMI Panel 10"

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">HMI Touchscreen</span>

> **More screen, more clarity.** The 10" HMI Panel gives you a full HD widescreen display for complex dashboards with multiple data streams — perfect for SCADA-style overviews of large production lines.

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Display</th></tr>
<tr><td>Screen Size</td><td><strong>10.1" IPS LCD</strong></td></tr>
<tr><td>Resolution</td><td>1280 × 800 pixels</td></tr>
<tr><td>Brightness</td><td>500 cd/m²</td></tr>
<tr><td>Touch Type</td><td>10-point capacitive multi-touch</td></tr>
<tr><th colspan="2">Processing</th></tr>
<tr><td>CPU</td><td>Quad-core ARM Cortex-A17 @ 1.8 GHz</td></tr>
<tr><td>RAM</td><td>2 GB DDR4</td></tr>
<tr><td>Storage</td><td>8 GB eMMC + MicroSD slot</td></tr>
<tr><th colspan="2">Communication</th></tr>
<tr><td>Ethernet</td><td>2 × 10/100/1000 Mbps</td></tr>
<tr><td>Serial</td><td>2 × RS485, 1 × RS232, 1 × CAN</td></tr>
<tr><td>USB</td><td>2 × USB-A 3.0, 1 × USB-C</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Panel Cutout</td><td>260 × 195 mm</td></tr>
<tr><td>Front Protection</td><td>IP65</td></tr>
<tr><td>Power</td><td>24V DC, 12W</td></tr>
</table>

---

## Key Advantages Over 7" Panel

| Feature | 7" Panel | 10" Panel |
|---|---|---|
| Resolution | 800×480 | **1280×800** |
| Multi-touch points | 5 | **10** |
| Ethernet ports | 1 | **2** |
| USB ports | 1 | **3** |
| CAN Bus | ✗ | **✓** |
| MicroSD | ✗ | **✓** |

!!! tip "When to choose the 10""
    Choose the 10" when you need multiple PLCs connected simultaneously, CAN bus devices (e.g. servo drives), or data logging to MicroSD.

---

## Multi-PLC Setup

The 10" Panel can communicate with **up to 8 PLCs simultaneously** via Ethernet:

```
HMI ETH1  ──→  Switch ──→  PLC-1 (192.168.1.100)
                        ──→  PLC-2 (192.168.1.101)
                        ──→  PLC-3 (192.168.1.102)

HMI ETH2  ──→  Isolated network (safety-critical PLCs)
```

In Designer → **Device List**, add each PLC with its IP and protocol.

---

## Data Logging

The built-in data logger writes to MicroSD at configurable intervals:

```
Log interval:    100ms minimum
File format:     CSV (Excel compatible)
Max file size:   2 GB per file
Auto-rotate:     Daily / weekly / monthly
```

Access logs via USB drive or FTP over Ethernet.
