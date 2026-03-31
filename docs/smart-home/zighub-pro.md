# 🏠 ZigHub Pro

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Zigbee Gateway</span>

> **Your home, your data.** The ZigHub Pro is a local-first Zigbee 3.0 gateway that runs entirely on your network — no cloud, no subscription, no privacy concerns. Pair up to 200 Zigbee devices and control them from Home Assistant or the built-in web dashboard.

---

## Quick Start

<div class="quick-start">
<h4>⚡ First device paired in 5 minutes</h4>

1. Plug ZigHub Pro into your router via Ethernet
2. Power via USB-C (adapter included)
3. Open `http://zighub.local` in your browser
4. Click **Pair Device** and put your Zigbee device into pairing mode
5. Done — device appears in the dashboard instantly

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Wireless</th></tr>
<tr><td>Zigbee Standard</td><td><strong>Zigbee 3.0 (IEEE 802.15.4)</strong></td></tr>
<tr><td>Max Devices</td><td>200 (with mesh routing)</td></tr>
<tr><td>Range (open)</td><td>~80m direct, unlimited via mesh</td></tr>
<tr><th colspan="2">Processing</th></tr>
<tr><td>CPU</td><td>Quad-core 1.5 GHz</td></tr>
<tr><td>RAM</td><td>512 MB</td></tr>
<tr><td>Storage</td><td>4 GB eMMC</td></tr>
<tr><th colspan="2">Connectivity</th></tr>
<tr><td>Ethernet</td><td>1 × Gigabit LAN</td></tr>
<tr><td>Power</td><td>USB-C 5V/2A</td></tr>
</table>

---

## First Setup

### 1. Network connection

Connect via Ethernet for best reliability. WiFi is available but not recommended for a hub.

### 2. Access the dashboard

Navigate to `http://zighub.local` (or the IP shown on your router's device list).

Default credentials:
```
Username: admin
Password: elephant123   ← change this immediately!
```

### 3. Pair your first device

1. In the dashboard, click **Devices → Add Device**
2. The hub enters pairing mode (60-second window)
3. Trigger pairing mode on your Zigbee device (usually hold button 5s)
4. Device appears with auto-detected capabilities

---

## Home Assistant

The ZigHub Pro exposes all devices via **MQTT** and the **Zigbee2MQTT** protocol, which Home Assistant supports natively.

=== "MQTT Integration"

    In Home Assistant → **Settings → Integrations → MQTT**:

    ```yaml
    broker: 192.168.1.x   # ZigHub IP
    port: 1883
    username: mqtt
    password: mqtt123
    ```

=== "Zigbee2MQTT Add-on"

    If running HA OS, install the **Zigbee2MQTT** add-on and point it to the ZigHub's MQTT broker. All devices appear automatically in HA.

---

## Supported Devices

ZigHub Pro works with **all Zigbee 3.0 certified devices** plus legacy Zigbee HA 1.2 devices. Tested brands include:

Philips Hue · IKEA Tradfri · Aqara · Sonoff · Tuya · Xiaomi · SmartThings · Legrand
