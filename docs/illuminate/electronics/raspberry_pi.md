# Raspberry Pi Pico

## Overview
The Raspberry Pi Pico is a small, low-cost micro-controller board that can be used for various projects.

## Getting Started
To get started we want to create a circuit that will blink an LED. We will make use of the built in LED on the board. We need the following components:

![Pico](./images/pico-wh-hero.jpg)

- Raspberry Pi Pico
- A computer (Mac or Windows)
- A micro USB cable

### About the Raspberry Pi Pico

Most micro-controllers have a set of pins that are used for input and output. The diagram below is a reference for the pins on the Raspberry Pi Pico:

![Pins](./images/pico-pins.png)

The GPIO pins are used for input and output. The GND pin is used to ground the circuit. The VSYS pin is used to power the circuit when not connected to a USB cable.

### Managing the Code
1. We need to install software called Thonny to write and upload code to the Raspberry Pi Pico. 

    !!! Note
        Thonny is a Python IDE (Integrated Development Environment) that can connect to the Raspberry Pi Pico.

2. In a web browser navigate to [thonny.org](https://thonny.org/) and download the software. Once downloaded double click to install but do not open it yet.
    ![Thonny Site](./images/thonny-site.png)

3. We need to flash MicroPython onto the Raspberry Pi Pico. To do this download the latest [Pico W](https://micropython.org/download/rp2-pico-w/rp2-pico-w-latest.uf2) UF2 file.
4. Holding down the BOOTSEL button on the Raspberry Pi Pico, plug in a USB cable to your computer. A new drive should appear on your computer. 
    ![Pico W BOOTSEL](./images/Pico-bootsel.png)
5. Copy the UF2 file to this drive. The drive should then disappear and the flashing process will begin.
6. You can now open the Thonny IDE and configure it to connect to the Raspberry Pi Pico.
7. Select `Run` -> `Configure interpreter`.
8. Select `MicroPython (Raspberry Pi Pico)` from the list of devices.
9. Click on the `Port or WebREPL` drop-down menu and select the port that corresponds to your Raspberry Pi Pico. Use `Try to detect port automatically` if you are unsure which port to select.
    ![Pico W Thonny Configuration](./images/thonny_configure.png)

### Running the code
To run the code, simply click on the `Run current script (F5)` button in Thonny IDE. The code will be uploaded to the Raspberry Pi Pico and executed.

The code to make the onboard LED blink is as follows:
```python
from machine import Pin
from utime import sleep

# Use the onboard LED
led = Pin("LED", Pin.OUT)

# loop continuously and turn the LED on and off every half second.
while True:
  led.toggle()
  sleep(0.5)
```

## Components for the Illuminate Project

### Per Class
| Component | Quantity | Description |
| ---- | ---- | ---- |
| USB-A to Micro USB | 3 | Connect Laptops to the Raspberry Pi Pico |
| USB-C to Micro USB | 3 | Connect MacBooks to the Raspberry Pi Pico |

### Per Student
| Component | Quantity | Description | Image |
| ---- | ---- | ---- | ---- |
| Raspberry Pi Pico | 1 | Single board micro-controller | ![Raspberry Pi Pico WH](./images/pico-wh-hero.jpg) |
| Breadboard | 1 | Prototyping board for electronic circuits | ![Breadboard](./images/breadboard.jpg) |
| Jumper wires M-F | 24 (max) | Wires to connect components together. 2 per LED |
| Jumper wires F-F | 1 | Wires to connect components together, used to connect ground (GND) on the board to the breadboard |
| Resistors | 1 | 220ohm resistor, not strictly required but does prevent long term damage to the LEDs | ![Resistor](./images/220_ohm_resistor.jpg) |
| Button switch | 1 | Used to turn on/off the lights | ![Button Switch](./images/push_button.jpg) |
| 5mm LEDs | 4-12 | Light emitting diode (various colours)|
| 5mm Flat LED Holder | 4-12 | Holder for the flat 5mm LEDs | ![5mm LED Holder](./images/led_holder.jpg) |
| 2 x 1.5V AA or AAA battery holder | 1 | Holder for AA or AAA batteries | ![AA Battery Holder](./images/battery_holder.jpg) |


### Student Supplied
| Component | Quantity | Description | Image |
| ---- | ---- | ---- | ---- |
| AA or AAA Batteries | 2 | Power supply for the Raspberry Pi Pico | 
| Paints | Various | Students should take their lid and box if required and decorate it with paints at home. |

## Software
- Students and teachers will need to install [Thonny](https://thonny.org/) on their laptop to program their Raspberry Pi Pico.
- [Wokwi](https://www.wokwi.com){_target="_blank"} will be used for prototyping and testing the circuits. 

## Circuit

### Wiring Diagram
Prototyping for the wiring should be completed in [Wokwi](https://www.wokwi.com){_target="_blank"}. 

### Single LED
The following is an example of a single LED circuit:
[![Single LED](./images/blinking_led.png)](https://wokwi.com/projects/300504213470839309){_target="_blank"}

**Key Points:**

- When using Python you need to use indentation to define the body of a function or loop.

### Multiple LEDs
The following is an example of a multiple LED circuit that demonstrates traffic lights:
[![Traffic Lights](./images/traffic_light_leds.png)](https://wokwi.com/projects/431541307875514369){_target="_blank"}

=== "Advanced"

    - Replace the code in the traffic light demonstration above with the code in the `Looping` tab. 
    - Notice the result is the same but the code is more efficient. 
    - We use a second loop inside the first loop to reduce the amount of code written and to make the code more readable.

=== "Looping"

    ``` python
    from machine import Pin
    from utime import sleep

    print('hello')

    sleep(0.01) # Wait for USB to become ready in seconds

    red_led = Pin(5, Pin.OUT)
    amber_led = Pin(9, Pin.OUT)
    green_led = Pin(13, Pin.OUT)

    led = Pin(5, Pin.OUT)
    while True:          # Continuously loop over the code indented
        red_led.high()
        sleep(2)
        amber_led.high()
        sleep(0.5)

        # flash red and amber twice
        count = 0
        while count < 2:
            red_led.low()
            amber_led.low()
            sleep(0.2)
            red_led.high()
            amber_led.high()
            count = count + 1
            sleep(0.2)

        red_led.low()
        amber_led.low()
        sleep(0.2)

        # turn off red and amber and turn on green for 2 seconds
        red_led.low()
        amber_led.low()
        green_led.high()
        sleep(2)

        # turn off green, turn on amber
        green_led.low()
        amber_led.high()
        sleep(1)
        # ensure amber off before starting loop again
        amber_led.low()
    ```
