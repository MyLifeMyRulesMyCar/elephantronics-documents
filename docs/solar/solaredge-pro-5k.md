# ☀️ SolarEdge Pro 5K

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Grid-Tie Inverter</span>&nbsp;
<span class="badge badge-orange">5000W</span>

> **The reliable workhorse for residential solar.** The SolarEdge Pro 5K delivers 5kW of clean grid-tied power with 99.2% efficiency, built-in WiFi monitoring, and a rugged IP65 enclosure that handles harsh outdoor conditions.

---

## Quick Start

<div class="quick-start">
<h4>⚡ You'll be live in 4 steps</h4>

1. Mount the inverter on a shaded wall (see [Mounting](#mounting))
2. Connect DC strings from panels (see [Wiring](#wiring))
3. Connect AC output to your distribution board
4. Power on and scan the QR code for the monitoring app

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Power Output</th></tr>
<tr><td>Rated Power</td><td><strong>5000 W</strong></td></tr>
<tr><td>Max AC Output Current</td><td>22.7 A</td></tr>
<tr><td>Efficiency (Peak)</td><td>99.2%</td></tr>
<tr><td>Power Factor</td><td>> 0.99</td></tr>
<tr><th colspan="2">DC Input</th></tr>
<tr><td>Max DC Input Voltage</td><td>1000 V</td></tr>
<tr><td>MPPT Voltage Range</td><td>200 – 800 V</td></tr>
<tr><td>Max Input Current per MPPT</td><td>13.5 A</td></tr>
<tr><td>Number of MPPT Inputs</td><td>2</td></tr>
<tr><th colspan="2">Communication</th></tr>
<tr><td>Connectivity</td><td>WiFi 2.4GHz, RS485, USB</td></tr>
<tr><td>Monitoring App</td><td>Elephantronics Cloud (iOS & Android)</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Dimensions</td><td>540 × 315 × 184 mm</td></tr>
<tr><td>Weight</td><td>14.5 kg</td></tr>
<tr><td>Protection Rating</td><td>IP65</td></tr>
<tr><td>Operating Temperature</td><td>-25°C to +60°C</td></tr>
</table>

---

## Mounting

Mount the inverter vertically on a solid wall in a shaded location. Avoid direct sunlight on the enclosure.

```
Clearance requirements:
  Top:    ≥ 300 mm
  Bottom: ≥ 300 mm
  Sides:  ≥ 200 mm
  Front:  ≥ 700 mm (service access)
```

!!! warning "Heat dissipation"
    Never install inside a sealed cabinet. The inverter requires airflow for cooling.

---

## Wiring

=== "DC Wiring (Panels → Inverter)"

    ```
    Panel String 1+  ──→  DC+ Input 1
    Panel String 1-  ──→  DC- Input 1
    Panel String 2+  ──→  DC+ Input 2
    Panel String 2-  ──→  DC- Input 2
    ```

    !!! danger "Before wiring"
        Ensure the AC breaker and DC disconnect are **OFF** before making any connections.

=== "AC Wiring (Inverter → Grid)"

    | Inverter Terminal | Connect to |
    |---|---|
    | L (Line) | Phase from DB |
    | N (Neutral) | Neutral from DB |
    | PE (Ground) | Earth from DB |

=== "Communication Wiring"

    ```
    RS485 A  →  Pin 1 of monitoring device
    RS485 B  →  Pin 2 of monitoring device
    GND      →  Ground
    ```

---

## Monitoring

After wiring, connect to the inverter's WiFi hotspot (`SE-PRO5K-XXXX`) using the Elephantronics app to configure your home WiFi credentials.

Once connected, the dashboard shows:

- Real-time power output (W)
- Daily / monthly / yearly energy yield (kWh)
- Grid export / import values
- Fault code history

---

## Troubleshooting

| Error Code | Meaning | Action |
|---|---|---|
| `E001` | Grid voltage out of range | Check utility voltage; may be a grid issue |
| `E003` | Isolation fault | Inspect panel wiring for ground fault |
| `E012` | Over temperature | Check ventilation clearances |
| `E025` | Communication lost | Check WiFi credentials and router |

!!! tip "Factory Reset"
    Hold the reset button for 10 seconds to restore factory settings. WiFi credentials will need to be re-entered.
