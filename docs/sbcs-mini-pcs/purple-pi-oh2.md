# 🖥️ Purple Pi OH2

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Single Board Computer</span>&nbsp;
<span class="badge badge-orange">RK3576 · 6 TOPS NPU</span>

> **Industrial-grade edge computing with built-in AI acceleration.** The Purple Pi OH2 is powered by the Rockchip RK3576 octa-core SoC (8nm), delivering up to 16GB LPDDR4 memory, a 6 TOPS NPU, 8K HDMI 2.1 output, triple MIPI CSI cameras, and dual Gigabit Ethernet — all in a compact SBC built for demanding industrial and embedded deployments.

---

## Quick Start

<div class="quick-start">
<h4>⚡ Up and running in 5 steps</h4>

1. Flash Debian, Ubuntu, or Buildroot to eMMC or a microSD card
2. Connect power (DC 9–24V barrel jack)
3. Attach HDMI display and USB keyboard/mouse
4. SSH in or use the desktop — default user: `root`
5. Connect Ethernet — DHCP assigns an IP automatically

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">Processor & Memory</th></tr>
<tr><td>SoC</td><td><strong>Rockchip RK3576</strong> (8nm)</td></tr>
<tr><td>CPU</td><td>4× Cortex-A72 @ 2.2GHz + 4× Cortex-A53</td></tr>
<tr><td>NPU</td><td><strong>6 TOPS</strong> neural processing unit</td></tr>
<tr><td>RAM</td><td>Up to 16GB LPDDR4</td></tr>
<tr><th colspan="2">Storage</th></tr>
<tr><td>eMMC</td><td>Onboard eMMC 5.1 (OS bootable)</td></tr>
<tr><td>microSD</td><td>TF card slot — SDIO 3.0 (J4)</td></tr>
<tr><td>M.2 NVMe</td><td>M-Key 2280, PCIe 2.1 (J6)</td></tr>
<tr><th colspan="2">Display Output</th></tr>
<tr><td>HDMI</td><td>HDMI 2.1 — up to 8K@60fps (J14)</td></tr>
<tr><td>DisplayPort</td><td>DP 1.4 via USB-C — up to 4K@30fps (J7)</td></tr>
<tr><td>MIPI DSI</td><td>40-pin FPC 0.5mm connector (J15)</td></tr>
<tr><th colspan="2">Camera Input</th></tr>
<tr><td>MIPI CSI</td><td>3× independent interfaces (J19, J20, J25)</td></tr>
<tr><th colspan="2">Connectivity</th></tr>
<tr><td>Ethernet</td><td>2× Gigabit RJ45 (eth0: J21, eth1: J22)</td></tr>
<tr><td>WiFi / BT</td><td>AP6256 module (antenna FPC included)</td></tr>
<tr><td>USB 3.2 Gen1</td><td>1× Type-C OTG + DP Alt Mode (J7)</td></tr>
<tr><td>USB 3.0</td><td>2× Type-A stacked (J10)</td></tr>
<tr><td>USB 2.0</td><td>2× PH2.0-4P headers (J8, J9)</td></tr>
<tr><th colspan="2">Expansion (40-pin Header)</th></tr>
<tr><td>GPIO</td><td>16× programmable GPIOs</td></tr>
<tr><td>UART</td><td>3× TTL UART channels</td></tr>
<tr><td>I2C</td><td>2× channels (I2C4: pins 3/5 · I2C7: pins 27/28)</td></tr>
<tr><td>SPI</td><td>1× channel (/dev/spidev0.x)</td></tr>
<tr><td>CAN Bus</td><td>2× CAN channels</td></tr>
<tr><td>ADC</td><td>1× analog input header (J26)</td></tr>
<tr><th colspan="2">Audio</th></tr>
<tr><td>Codec</td><td>ES8388</td></tr>
<tr><td>Speaker</td><td>PH2.0-4P dual channel, 4Ω 3W/ch (J13)</td></tr>
<tr><td>Headphone</td><td>3.5mm 4-pole CTIA jack (J12)</td></tr>
<tr><td>Microphone</td><td>MX1.25T-2P connector (J11)</td></tr>
<tr><th colspan="2">Other</th></tr>
<tr><td>Debug UART</td><td>USB-C (CH340 chip, J5) at 1.5Mbps</td></tr>
<tr><td>RTC</td><td>Battery holder for CR1220 coin cell (J23)</td></tr>
<tr><td>Fan</td><td>PH2.0-2P 5V fan header (J3)</td></tr>
<tr><th colspan="2">Power & OS</th></tr>
<tr><td>Input Voltage</td><td><strong>DC 9–24V</strong> (barrel jack)</td></tr>
<tr><td>Supported OS</td><td>Debian · Ubuntu · Buildroot</td></tr>
</table>

---

## Connectivity

### Ethernet

The Purple Pi OH2 has two native Gigabit Ethernet ports (`eth0` and `eth1`). Both support automatic DHCP — just plug in a cable and the board is network-ready.

```bash
# Check IP address assigned by DHCP
ip addr show eth0

# Set a static IP
nmcli con mod "Wired connection 1" ipv4.addresses 192.168.1.100/24 \
  ipv4.gateway 192.168.1.1 ipv4.dns "8.8.8.8" ipv4.method manual
nmcli con up "Wired connection 1"
```

### WiFi

```bash
# Check interface status
nmcli device

# List available networks
nmcli device wifi list

# Connect to a network
nmcli device wifi connect "YourSSID" password "YourPassword"

# Confirm connection
nmcli connection show --active
ip addr show wlan0
```

!!! note "Antenna required"
    Always connect the included WiFi/BT antenna FPC for reliable wireless reception.

### Bluetooth

```bash
bluetoothctl power on          # Turn on Bluetooth
bluetoothctl scan on           # Scan for devices
bluetoothctl devices           # List found devices
bluetoothctl trust  XX:XX:XX:XX:XX:XX   # Trust a device
bluetoothctl pair   XX:XX:XX:XX:XX:XX   # Pair
bluetoothctl connect XX:XX:XX:XX:XX:XX  # Connect
```

---

## GPIO (40-pin Header)

The 40-pin header is Raspberry Pi HAT-compatible and exposes 16 GPIOs, UART, I2C, SPI, and CAN. All GPIO logic is 3.3V.

```bash
# Install GPIO tools
sudo apt update && sudo apt install -y libgpiod-dev gpiod

# Set pin HIGH (Pin 7 = GPIO2_B4 = gpiochip2 offset 12)
gpioset gpiochip2 12=1

# Set pin LOW
gpioset gpiochip2 12=0

# Read a pin
gpioget gpiochip2 12

# Control multiple pins at once
gpioset gpiochip2 12=1 13=0 14=1
```

### Key pin assignments

| Pin | Function | Device Node |
|-----|----------|-------------|
| 3 / 5 | I2C4 SDA / SCL | /dev/i2c-4 |
| 8 / 10 | UART7 TX / RX | /dev/ttyS7 |
| 19, 21, 23, 24, 26 | SPI0 (MOSI, MISO, CLK, CS0, CS1) | /dev/spidev0.x |
| 27 / 28 | I2C7 SDA / SCL | /dev/i2c-7 |
| 37 | POWER_KEY | /dev/input/event0 |

---

## Storage & Expansion

### M.2 NVMe SSD

Install a 2280 NVMe drive into the M-Key slot (J6), then verify detection:

```bash
fdisk -l    # NVMe shows as /dev/nvme0n1
lsblk       # Confirm mount tree
```

### microSD Card

The TF card slot (J4, back of board) supports SDIO 3.0. List storage after insertion:

```bash
lsblk       # microSD shows as /dev/mmcblk1
```

!!! warning "Manual mount may be needed"
    During boot, eMMC partition changes can affect TF card automounting. Mount manually with `mount /dev/mmcblk1p1 /mnt` if needed.

### USB Power Control

Software control for the two USB 3.0 Type-A ports:

```bash
echo 0 > /sys/class/leds/usb_pwr/brightness   # Power OFF
echo 1 > /sys/class/leds/usb_pwr/brightness   # Power ON
```

---

## Camera (MIPI CSI)

Three independent MIPI CSI interfaces support simultaneous camera input.

| Connector | Device Node | Default Sensor |
|-----------|-------------|----------------|
| J19 | /dev/video42 | OV13855 |
| J20 | /dev/video51 | OV13855 |
| J25 | /dev/video33 | Standard CSI |

```bash
# Live preview from J19 (requires display)
export DISPLAY=:0
gst-launch-1.0 v4l2src device=/dev/video42 \
  ! video/x-raw,format=NV12,width=1920,height=1080,framerate=30/1 \
  ! videoconvert ! autovideosink sync=false

# Capture a still image from J19
v4l2-ctl --verbose -d /dev/video42 \
  --set-fmt-video=width=1920,height=1080,pixelformat='NV12' \
  --stream-mmap=4 --stream-skip=3 \
  --stream-to=./capture.yuv --stream-count=1 --stream-poll

# Play back the captured frame
ffplay -f rawvideo -video_size 1920x1080 -pixel_format nv12 ./capture.yuv
```

!!! note "J20 color tint"
    J20 may show a green tint depending on the sensor module used. Apply a color correction filter in your pipeline if needed.

---

## Audio

The ES8388 codec handles speaker, headphone, and microphone I/O.

```bash
# Enable speaker / headphone output
amixer -c 0 cset name='Speaker Switch' on

# Play audio
aplay -D hw:0,0 audio.wav

# Record from headphone mic (J12)
amixer -c 0 cset numid=67 off               # Disable onboard mic
echo -n "mic1" > /sys/class/es8388_mic/mic_channel
arecord -D hw:0,0 -f S16_LE -r 16000 -c 2 recording.wav

# Set capture volume (0–192)
amixer -c 0 cset numid=50 100

# Enable Automatic Level Control (stereo)
amixer -c 0 cset numid=41 3
```

---

## Troubleshooting

| Issue | Likely Cause | Fix |
|-------|--------------|-----|
| No display on HDMI | Cable or resolution mismatch | Try a different HDMI cable; check OS display settings |
| WiFi weak or disconnects | Antenna not connected | Attach the included antenna FPC to the AP6256 connector |
| microSD not automounted | eMMC partition change on boot | Mount manually: `mount /dev/mmcblk1p1 /mnt` |
| NVMe not detected | Drive not fully seated | Re-seat the M.2 drive and re-tighten the screw |
| Camera shows green tint | Sensor color calibration on J20 | Apply color correction in GStreamer pipeline |
| No audio output | Speaker switch disabled | Run `amixer -c 0 cset name='Speaker Switch' on` |
| USB device not recognized | USB power is off | Run `echo 1 > /sys/class/leds/usb_pwr/brightness` |