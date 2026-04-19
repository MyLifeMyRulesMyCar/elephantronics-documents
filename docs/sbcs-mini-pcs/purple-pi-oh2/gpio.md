# 💡 GPIO Usage

<span class="badge badge-blue">Purple Pi OH2</span>&nbsp;
<span class="badge badge-blue">DI-DO</span>&nbsp;
<span class="badge badge-blue">I2C</span>&nbsp;
<span class="badge badge-blue">SPI</span>&nbsp;
<span class="badge badge-orange">Python · gpiod</span>

> Control a GPIO pin from Python to switch an LED on and off — a practical starting point for any digital output application (relays, buzzers, indicators).

---

## Connect via SSH (VS Code)

1. Install the **Remote - SSH** extension in VS Code
2. Press `F1` → **Remote-SSH: Connect to Host**
3. Enter: `ssh industio@<your_device_ip>`

---

## GPIO Map

| Pin # | Function     | Description / Alternate Functions           | Voltage / Type | Device Node / Notes        |
|------:|-------------|--------------------------------------------|----------------|----------------------------|
| 1     | 3.3V        | Power supply output                        | 3.3V DC        | Power output               |
| 2     | 5V          | Power supply output                        | 5V DC          | Power output               |
| 3     | I2C4_SDA    | I2C4 data signal                           | 3.3V logic     | /dev/i2c-4                 |
| 4     | 5V          | Power supply output                        | 5V DC          | Power output               |
| 5     | I2C4_SCL    | I2C4 clock signal                          | 3.3V logic     | /dev/i2c-4                 |
| 6     | GND         | Ground                                     | 0V             | Reference ground           |
| 7     | GPIO76      | GPIO2_B4 - General purpose I/O             | 3.3V logic     | gpiochip2 offset 12        |
| 8     | UART7_TX    | UART7 transmit data                        | TTL 3.3V       | /dev/ttyS7                 |
| 9     | GND         | Ground                                     | 0V             | Reference ground           |
| 10    | UART7_RX    | UART7 receive data                         | TTL 3.3V       | /dev/ttyS7                 |
| 11    | GPIO75      | GPIO2_B3 - General purpose I/O             | 3.3V logic     | gpiochip2 offset 11        |
| 12    | GPIO77      | GPIO2_B5 - General purpose I/O             | 3.3V logic     | gpiochip2 offset 13        |
| 13    | GPIO72      | GPIO2_B0 - General purpose I/O             | 3.3V logic     | gpiochip2 offset 8         |
| 14    | GND         | Ground                                     | 0V             | Reference ground           |
| 15    | GPIO73      | GPIO2_B1 - General purpose I/O             | 3.3V logic     | gpiochip2 offset 9         |
| 16    | GPIO74      | GPIO2_B2 - General purpose I/O             | 3.3V logic     | gpiochip2 offset 10        |
| 17    | 3.3V        | Power supply output                        | 3.3V DC        | Power output               |
| 18    | GPIO136     | GPIO4_B0 - General purpose I/O             | 3.3V logic     | gpiochip4 offset 8         |
| 19    | SPI0_MOSI   | SPI0 master output, slave input            | 3.3V logic     | /dev/spidev0.0             |
| 20    | GND         | Ground                                     | 0V             | Reference ground           |
| 21    | SPI0_MISO   | SPI0 master input, slave output            | 3.3V logic     | /dev/spidev0.0             |
| 22    | GPIO137     | GPIO4_B1 - General purpose I/O             | 3.3V logic     | gpiochip4 offset 9         |
| 23    | SPI0_SCLK   | SPI0 serial clock                          | 3.3V logic     | /dev/spidev0.0             |
| 24    | SPI0_CS0    | SPI0 chip select 0                         | 3.3V logic     | /dev/spidev0.0             |
| 25    | GND         | Ground                                     | 0V             | Reference ground           |
| 26    | SPI0_CS1    | SPI0 chip select 1                         | 3.3V logic     | /dev/spidev0.1             |
| 27    | I2C7_SDA    | I2C7 data signal                           | 3.3V logic     | /dev/i2c-7                 |
| 28    | I2C7_SCL    | I2C7 clock signal                          | 3.3V logic     | /dev/i2c-7                 |
| 29    | GPIO56      | GPIO1_D0 - General purpose I/O             | 3.3V logic     | gpiochip1 offset 24        |
| 30    | GND         | Ground                                     | 0V             | Reference ground           |
| 31    | GPIO57      | GPIO1_D1 - General purpose I/O             | 3.3V logic     | gpiochip1 offset 25        |
| 32    | GPIO132     | GPIO4_A4 - General purpose I/O             | 3.3V logic     | gpiochip4 offset 4         |
| 33    | GPIO58      | GPIO1_D2 - General purpose I/O             | 3.3V logic     | gpiochip1 offset 26        |
| 34    | GND         | Ground                                     | 0V             | Reference ground           |
| 35    | GPIO59      | GPIO1_D3 - General purpose I/O             | 3.3V logic     | gpiochip1 offset 27        |
| 36    | GPIO134     | GPIO4_A6 - General purpose I/O             | 3.3V logic     | gpiochip4 offset 6         |
| 37    | POWER_KEY   | Power key input (system power control)     | 3.3V logic     | /dev/input/event0          |
| 38    | GPIO98      | GPIO3_A2 - General purpose I/O             | 3.3V logic     | gpiochip3 offset 2         |
| 39    | GND         | Ground                                     | 0V             | Reference ground           |
| 40    | GPIO99      | GPIO3_A3 - General purpose I/O             | 3.3V logic     | gpiochip3 offset 3         |


## Project Setup

=== "Create folder & virtual environment"

    ```bash
    mkdir my_project && cd my_project

    sudo apt update
    sudo apt install python3-venv python3-libgpiod libgpiod-dev gpiod -y

    python3 -m venv venv
    source venv/bin/activate
    ```

    Your prompt should change to:
    ```
    (venv) industio@device:~/my_project$
    ```

=== "Create the script file"

    ```bash
    touch led_controller.py
    ```

---
## Digital Output 

### Hardware Wiring

```
Pin 40 (GPIO3_A3)  →  [220Ω resistor]  →  LED (+)
GND (Pin 39)       →  LED (–)
```

!!! warning "Always use a resistor"
    A 220Ω resistor protects both the LED and the GPIO pin from overcurrent. Skipping it can permanently damage the pin.

---

### LED Control Scripts

=== "Single blink"

    ```python
    import gpiod
    import time

    chip = gpiod.Chip("gpiochip3")
    line = chip.get_line(3)          # Pin 40 = gpiochip3 offset 3
    line.request(consumer="LED", type=gpiod.LINE_REQ_DIR_OUT)

    print("LED ON")
    line.set_value(1)
    time.sleep(2)

    print("LED OFF")
    line.set_value(0)
    line.release()
    ```

=== "Continuous blink loop"

    ```python
    import gpiod
    import time

    chip = gpiod.Chip("gpiochip3")
    line = chip.get_line(3)
    line.request(consumer="LED", type=gpiod.LINE_REQ_DIR_OUT)

    try:
        while True:
            line.set_value(1)
            time.sleep(1)
            line.set_value(0)
            time.sleep(1)
    except KeyboardInterrupt:
        print("Stopped")
    finally:
        line.set_value(0)
        line.release()
    ```

---

### Run the Script

!!! warning "sudo required"
    GPIO access requires root privileges on this board.

```bash
sudo python3 led_controller.py
```

Stop the blink loop at any time with `Ctrl + C`.

---

### Manual GPIO Testing (no Python)

Useful for quickly verifying your wiring before running a script:

```bash
gpioinfo                    # List all chips and offsets
gpioset gpiochip3 3=1       # Pin 40 HIGH → LED on
gpioset gpiochip3 3=0       # Pin 40 LOW  → LED off
gpioget gpiochip3 3         # Read current state
```

---

## Digital Input 

### Connection :

* **GPIO7** → Input pin
* **3.3V** → HIGH signal
* **GND** → LOW signal

> It is recommended to use a pull-up resistor to ensure a stable input signal and avoid floating values.

### Method 1 – Polling (Continuous Reading)

```python
import gpiod
import time

chip = gpiod.Chip("gpiochip2")   # GPIO controller
line = chip.get_line(12)         # GPIO76

# Request line as input
line.request(consumer="di_test", type=gpiod.LINE_REQ_DIR_IN)

try:
    while True:
        value = line.get_value()
        print("DI Value:", value)  # 0 or 1
        time.sleep(1)

except KeyboardInterrupt:
    print("Stopped")

finally:
    line.release()
```

#### Save and Run the Script

```bash
sudo python3 di_polling.py
```

### Method 2 – Event-Based (Interrupt Style)

```python
import gpiod

chip = gpiod.Chip("gpiochip2")
line = chip.get_line(12)

line.request(
    consumer="DI_event",
    type=gpiod.LINE_REQ_EV_BOTH_EDGES
)

print("Waiting for input changes...")

try:
    while True:
        if line.event_wait(sec=10):
            event = line.event_read()
            
            if event.type == gpiod.LineEvent.RISING_EDGE:
                print("Signal HIGH (3.3V)")
            elif event.type == gpiod.LineEvent.FALLING_EDGE:
                print("Signal LOW (GND)")

except KeyboardInterrupt:
    print("Stopped")

finally:
    line.release()
```
#### Save and Run the Script

```bash
sudo python3 di_event.py
```

---

## I2C OLED (SSD1306) Complete Guide

!!! warning "Disconnect power first"
    Remove power before connecting the SSD1306 OLED Display to avoid damaging the device.

---

###  Overview

This guide covers:

* Detecting I2C devices
* Communicating via Python
* Displaying text on OLED
* Rendering images + custom graphics

---

### Wiring (SSD1306 OLED)

| OLED Pin | Purple Pi |
| -------- | --------- |
| VCC      | 3.3V      |
| GND      | GND       |
| SDA      | Pin 3     |
| SCL      | Pin 5     |

#### Interpretation

| Item           | Value        |
| -------------- | ------------ |
| I2C Bus        | `/dev/i2c-4` |
| Device Address | `0x3C`       |
| Device Type    | SSD1306 OLED |

---

### Detect I2C Bus

#### List available I2C buses:

```bash
ls /dev/i2c-*
```

**Example output:**

```
/dev/i2c-0 ... /dev/i2c-7
```

---

### Scan for I2C Devices

!!! warning "Root permission required"
    Scanning I2C buses requires sudo access.

```bash
sudo i2cdetect -y 4
```

**Output:**

```
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:                         -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- 3c -- -- -- 
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- -- 
```

**Device found at:**

```
0x3C
```

---

### Install Required Packages

```bash
sudo apt update
sudo apt install i2c-tools -y
pip install python-periphery pillow
```

---

### Basic I2C Test

Create the `i2c_test.py` script:

```python
from periphery import I2C
import time

# Purple Pi OH2 Configuration
I2C_BUS = "/dev/i2c-4"  # Confirmed by your i2cdetect output
I2C_ADDR = 0x3C         # Confirmed by your scan

def main():
    try:
        # Open I2C connection
        i2c = I2C(I2C_BUS)
        print(f"Connected to {I2C_BUS}, device at {hex(I2C_ADDR)}")

        # SSD1306 Initialization Sequence
        init_sequence = [
            0xAE,  # Display off
            0x00, 0x10, 0x40, 0xB0, 0x81, 0xCF, 0xA1, 0xA6,
            0xA8, 0x3F, 0xC8, 0xD3, 0x00, 0xD5, 0x80, 0xD9,
            0xF1, 0xDA, 0x12, 0xDB, 0x40, 0x8D, 0x14, 0xAF  # Display on
        ]

        # Send initialization commands
        for cmd in init_sequence:
            i2c.transfer(I2C_ADDR, [I2C.Message([0x00, cmd])])
        time.sleep(0.1)

        # Clear display function
        def clear_display():
            for page in range(8):
                # Set page address
                i2c.transfer(I2C_ADDR, [I2C.Message([0x00, 0xB0 + page])])
                # Set column address
                i2c.transfer(I2C_ADDR, [I2C.Message([0x00, 0x00])])
                i2c.transfer(I2C_ADDR, [I2C.Message([0x00, 0x10])])
                # Write zeros to all columns
                for _ in range(128):
                    i2c.transfer(I2C_ADDR, [I2C.Message([0x40, 0x00])])

        clear_display()

        # Simple 5x7 font
        font = {
            'H': [0x7F, 0x08, 0x08, 0x08, 0x7F],
            'e': [0x38, 0x54, 0x54, 0x54, 0x18],
            'l': [0x00, 0x41, 0x7F, 0x40, 0x00],
            'o': [0x38, 0x44, 0x44, 0x44, 0x38],
            ' ': [0x00, 0x00, 0x00, 0x00, 0x00],
        }
        
        text = "Hello"

        # Position at page 1
        i2c.transfer(I2C_ADDR, [I2C.Message([0x00, 0xB1])])
        # Set column to 0
        i2c.transfer(I2C_ADDR, [I2C.Message([0x00, 0x00])])
        i2c.transfer(I2C_ADDR, [I2C.Message([0x00, 0x10])])

        # Write each character
        for char in text:
            char_data = font.get(char, [0x00]*5)
            for col in char_data:
                i2c.transfer(I2C_ADDR, [I2C.Message([0x40, col])])
            # Space between characters
            i2c.transfer(I2C_ADDR, [I2C.Message([0x40, 0x00])])

        print("Text sent successfully!")
        i2c.close()

    except Exception as e:
        print(f"Error: {e}")
        print("\nTroubleshooting:")
        print("1. Make sure you're using sudo: sudo python3 i2c_test.py")
        print("2. Check wiring: SDA=Pin3, SCL=Pin5, VCC=Pin1(3.3V), GND=Pin9")

if __name__ == "__main__":
    main()
```

#### Run the Test:

```bash
sudo python3 i2c_test.py
```

**Expected Output:**

```
Connected to /dev/i2c-4, device at 0x3c
Text sent successfully!
```

---

## Display Image (Bitmap)

### Generate Bitmap

First, create a bitmap from your image. Place your graphics file in the project directory, then create `converter.py`:

```python
from PIL import Image

# Load image - replace with yours
img = Image.open("elephant.png").convert("L") 

# Resize smaller (leave space for text)
img = img.resize((128, 48))

# Convert to black/white
img = img.point(lambda x: 0 if x < 128 else 255, '1')

# Create empty OLED buffer
buffer = [0x00] * (128 * 8)

pixels = img.load()

# Center vertically (top area)
y_offset = 0   # top aligned (can change to center if you want)

for x in range(128):
    for y in range(48):
        if pixels[x, y] == 0:
            oled_y = y + y_offset
            page = oled_y // 8
            index = x + (page * 128)
            buffer[index] |= (1 << (oled_y % 8))

# Save buffer
with open("elephant_bitmap.py", "w") as f:
    f.write("elephant_bitmap = [\n")
    for i in range(0, len(buffer), 16):
        line = ", ".join(f"0x{b:02X}" for b in buffer[i:i+16])
        f.write(f"    {line},\n")
    f.write("]\n")

print("Smaller elephant bitmap generated!")
```

#### Run the Converter:

```bash
python3 converter.py
```

**Output:** `elephant_bitmap.py` file is created

---

### Create `oled_image.py`

This script displays the image with text. Adjust positioning and text as needed:

```python
from periphery import I2C
from elephant_bitmap import elephant_bitmap

I2C_BUS = "/dev/i2c-4"
I2C_ADDR = 0x3C

i2c = I2C(I2C_BUS)

def send_cmd(cmd):
    i2c.transfer(I2C_ADDR, [I2C.Message([0x00, cmd])])

def send_data(data):
    i2c.transfer(I2C_ADDR, [I2C.Message([0x40] + data)])

# -------- INIT --------
def init_display():
    cmds = [
        0xAE, 0x20, 0x00, 0xB0, 0xC8, 0x00, 0x10,
        0x40, 0x81, 0xFF, 0xA1, 0xA6, 0xA8, 0x3F,
        0xA4, 0xD3, 0x00, 0xD5, 0xF0, 0xD9, 0x22,
        0xDA, 0x12, 0xDB, 0x20, 0x8D, 0x14, 0xAF
    ]
    for c in cmds:
        send_cmd(c)

# -------- TEXT DRAW --------
def draw_centered_text_on_buffer(buffer, text):
    font = {
        'E':[0x7F,0x49,0x49,0x49,0x41],
        'l':[0x00,0x41,0x7F,0x40,0x00],
        'e':[0x38,0x54,0x54,0x54,0x18],
        'p':[0x7C,0x14,0x14,0x14,0x08],
        'h':[0x7F,0x08,0x08,0x08,0x70],
        'a':[0x20,0x54,0x54,0x54,0x78],
        'n':[0x7C,0x08,0x04,0x04,0x78],
        't':[0x04,0x3F,0x44,0x40,0x20],
        'r':[0x7C,0x08,0x04,0x04,0x08],
        'o':[0x38,0x44,0x44,0x44,0x38],
        'i':[0x00,0x44,0x7D,0x40,0x00],
        'c':[0x38,0x44,0x44,0x44,0x20],
        's':[0x48,0x54,0x54,0x54,0x20],
    }

    char_width = 6
    text_width = len(text) * char_width
    start_x = (128 - text_width) // 2

    page = 7  # bottom page

    for i, char in enumerate(text):
        char_data = font.get(char, [0x00]*5)

        for col in range(5):
            x = start_x + i * char_width + col
            if 0 <= x < 128:
                index = x + (page * 128)
                buffer[index] = char_data[col]

        # spacing column
        x = start_x + i * char_width + 5
        if 0 <= x < 128:
            buffer[x + (page * 128)] = 0x00

# -------- DISPLAY --------
def display_image(buffer):
    for page in range(8):
        send_cmd(0xB0 + page)
        send_cmd(0x00)
        send_cmd(0x10)
        start = page * 128
        send_data(buffer[start:start+128])

# -------- MAIN --------
try:
    init_display()

    # Copy original buffer (important!)
    buffer = elephant_bitmap.copy()

    # Add centered text
    draw_centered_text_on_buffer(buffer, "Elephantronics")

    # Display final image
    display_image(buffer)

    print("🐘 Elephant + Elephantronics displayed!")

except Exception as e:
    print("Error:", e)

finally:
    i2c.close()
```

#### Run Image Display:

```bash
sudo python3 oled_image.py
```