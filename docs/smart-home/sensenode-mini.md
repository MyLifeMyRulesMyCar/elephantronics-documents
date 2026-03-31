# 🏠 SenseNode Mini

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">IoT Sensor Node</span>

> **Know what's happening in every room.** The SenseNode Mini is a coin-sized wireless sensor that measures temperature, humidity, motion, and door/window state — reporting everything to your ZigHub in real time, for 2 years on a single battery.

---

## Quick Start

<div class="quick-start">
<h4>⚡ Sensing in 2 minutes</h4>

1. Pull the battery tab to activate
2. Hold the button once to enter pairing mode (LED flashes)
3. Pair to ZigHub Pro — it auto-detects all sensors
4. Mount anywhere with the included double-sided tape

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Sensors</th></tr>
<tr><td>Temperature</td><td>±0.3°C accuracy, -10°C to +60°C</td></tr>
<tr><td>Humidity</td><td>±2% RH, 0–100%</td></tr>
<tr><td>Motion (PIR)</td><td>5m range, 120° field of view</td></tr>
<tr><td>Door/Window</td><td>Reed contact (magnetic)</td></tr>
<tr><td>Light Level</td><td>0–65,000 lux</td></tr>
<tr><th colspan="2">Power</th></tr>
<tr><td>Battery</td><td>2 × AAA (included)</td></tr>
<tr><td>Battery Life</td><td>~2 years (5-min reporting interval)</td></tr>
<tr><td>Low Battery Alert</td><td>Yes — notified via ZigHub</td></tr>
<tr><th colspan="2">Wireless</th></tr>
<tr><td>Protocol</td><td>Zigbee 3.0</td></tr>
<tr><td>Range</td><td>30m indoor</td></tr>
<tr><th colspan="2">Physical</th></tr>
<tr><td>Dimensions</td><td>58 × 38 × 16 mm</td></tr>
<tr><td>Weight</td><td>28g (with batteries)</td></tr>
<tr><td>Mounting</td><td>Adhesive pad or 2 × M3 screws</td></tr>
</table>

---

## Pairing

1. Pull plastic battery activation tab (first use only)
2. Press the small button **once** — LED flashes blue rapidly
3. In ZigHub dashboard, click **Devices → Add Device**
4. SenseNode appears within 10 seconds as `sensenode_XXXX`
5. Rename it (e.g. "Bedroom Sensor")

---

## Sensor Use Cases

| Sensor | What you can automate |
|---|---|
| Temperature | Turn on heater when temp < 18°C |
| Humidity | Turn on exhaust fan when humidity > 70% |
| Motion | Turn lights on when motion detected |
| Door/Window | Alert when door opens while away |
| Light Level | Lower blinds when lux > 50,000 |

---

## Reporting Interval

Default reporting interval is **5 minutes** to maximise battery life. For faster updates (e.g. security use), adjust in ZigHub dashboard:

```
Device Settings → SenseNode Mini → Report Interval → 30s
```

!!! warning "Battery impact"
    Setting the interval below 1 minute significantly reduces battery life. For motion triggers, the sensor always reports instantly regardless of interval setting.
