# ☀️ SunPower Elite 8K

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Hybrid Inverter</span>&nbsp;
<span class="badge badge-orange">8000W</span>

> **Solar + Storage in one unit.** The SunPower Elite 8K is an 8kW hybrid inverter with integrated battery management system (BMS), dual MPPT, and seamless grid/battery switching — giving you energy independence day and night.

---

## Quick Start

<div class="quick-start">
<h4>⚡ You'll be live in 5 steps</h4>

1. Mount inverter on solid wall, ventilated area
2. Wire DC inputs from solar panels to Dual MPPT
3. Connect your battery bank to the BAT terminals
4. Connect AC grid and backup load outputs
5. Commission via the LCD touchscreen

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Power Output</th></tr>
<tr><td>Rated Solar Power</td><td><strong>8000 W</strong></td></tr>
<tr><td>Battery Discharge Power</td><td>8000 W</td></tr>
<tr><td>Efficiency (Solar → AC)</td><td>98.6%</td></tr>
<tr><th colspan="2">Battery Input</th></tr>
<tr><td>Battery Voltage Range</td><td>40 – 60 V DC</td></tr>
<tr><td>Max Charge / Discharge Current</td><td>100 A</td></tr>
<tr><td>Compatible Battery Types</td><td>LiFePO4, Lead-Acid, Gel</td></tr>
<tr><th colspan="2">DC Solar Input</th></tr>
<tr><td>Number of MPPT</td><td>2 (independent)</td></tr>
<tr><td>Max DC Voltage</td><td>900 V</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Dimensions</td><td>590 × 420 × 210 mm</td></tr>
<tr><td>Weight</td><td>24 kg</td></tr>
<tr><td>Protection Rating</td><td>IP65</td></tr>
</table>

---

## Battery Setup

=== "LiFePO4 (Recommended)"

    ```
    BAT+  ──→  Battery Positive (fused)
    BAT-  ──→  Battery Negative
    CAN   ──→  Battery BMS CAN Bus
    ```

    Enable BMS communication in the LCD menu:  
    **Settings → Battery → Type → LiFePO4 → CAN BMS**

=== "Lead-Acid / Gel"

    Connect BAT+ and BAT- directly. Set capacity (Ah) in Settings.

    !!! note
        Lead-acid batteries do not support BMS communication. Set charge parameters manually.

---

## Operating Modes

| Mode | Description |
|---|---|
| **Solar Priority** | Use solar first, then battery, then grid |
| **Battery Priority** | Discharge battery, use grid only when battery low |
| **Grid Priority** | Grid powers load, solar charges battery |
| **Off-Grid** | Fully isolated from grid — UPS mode |

Configure via: **LCD → Settings → Working Mode**

---

## Troubleshooting

| Error | Cause | Fix |
|---|---|---|
| `BMS Fault` | Battery BMS communication error | Check CAN cable and BMS firmware |
| `Overload` | Load exceeds inverter capacity | Reduce connected loads |
| `Low Battery` | Battery SOC below cutoff | Check battery health |
