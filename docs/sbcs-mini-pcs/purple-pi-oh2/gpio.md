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