# 🏠 SmartRelay 8CH

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Smart Relay Controller</span>

> **The clean way to automate your home.** The SmartRelay 8CH fits in your distribution board on a DIN rail, giving you 8 smart switches for lights, fans, and appliances — all controlled via Zigbee from your ZigHub or Home Assistant.

---

## Quick Start

<div class="quick-start">
<h4>⚡ Smart lighting in 15 minutes</h4>

1. Mount on DIN rail in your distribution board
2. Wire live, neutral, and your load to the relay terminals
3. Pair to your ZigHub Pro (hold PAIR button 5s)
4. Control from dashboard or automation

</div>

!!! danger "Safety first"
    This product handles **230V AC mains voltage**. If you're not a qualified electrician, have a professional handle the wiring.

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Relay Outputs</th></tr>
<tr><td>Number of Channels</td><td><strong>8 independent relays</strong></td></tr>
<tr><td>Max Load per Channel</td><td>10A / 2300W (resistive)</td></tr>
<tr><td>Switching Voltage</td><td>AC 100–250V / DC 30V</td></tr>
<tr><td>Contact Type</td><td>SPDT (NO + NC + COM)</td></tr>
<tr><th colspan="2">Wireless</th></tr>
<tr><td>Protocol</td><td>Zigbee 3.0</td></tr>
<tr><td>Hub Required</td><td>Yes (ZigHub Pro or any Zigbee coordinator)</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Mounting</td><td>DIN Rail (35mm)</td></tr>
<tr><td>Width</td><td>8 DIN modules (144mm)</td></tr>
<tr><td>Power Supply</td><td>Internal 230V AC → 5V DC</td></tr>
</table>

---

## Wiring

Each channel has three terminals: **COM**, **NO** (Normally Open), **NC** (Normally Closed).

For standard light switch replacement:

```
Live In   ──→  COM 1
Light     ──→  NO  1
Neutral   ──→  Neutral Bus
Earth     ──→  Earth Bus
```

Repeat for channels 2–8 as needed.

---

## Pairing

1. Ensure ZigHub Pro is in pairing mode
2. Hold the **PAIR** button on the SmartRelay for 5 seconds until the LED flashes rapidly
3. Within 30 seconds, the relay appears in the ZigHub dashboard as `relay_8ch_XXXX`
4. Rename channels in the dashboard (e.g. "Living Room Light", "Kitchen Fan")

---

## Automations (Home Assistant Example)

```yaml
automation:
  - alias: "Turn off all lights at midnight"
    trigger:
      platform: time
      at: "00:00:00"
    action:
      - service: switch.turn_off
        target:
          entity_id:
            - switch.living_room_light
            - switch.kitchen_light
            - switch.bedroom_light
```
