# Circuitpython-Keypad_I2C
A simple test using PCF8574 I2C IO Expander with 3x4 Matrix Keypad in Circuitpython

I am using Seeed XIAO RP2040 in a bunch of new projects, because it's small. 
Matrix Keypads, LCD Displays and other devices use a bunch of pins. So I started to use PCF8574 and PCF8575 in my projects, in order to save a few pins.

```
''' Trying to create a Matrix Keypad with I2C Adapter PCF 8574 '''
import board
import busio
import time
import adafruit_matrixkeypad
import adafruit_pcf8574

i2c = busio.I2C (scl=board.SCL, sda=board.SDA)
pcf = adafruit_pcf8574.PCF8574(i2c)

''' This configuration is for my Matrix Keypad soldered directly in PCF8574'''
rows = [pcf.get_pin(5), pcf.get_pin(0), pcf.get_pin(1), pcf.get_pin(3)]
cols = [pcf.get_pin(4), pcf.get_pin(6), pcf.get_pin(2)]
keys = ((1, 2, 3),
        (4, 5, 6),
        (7, 8, 9),
        ('*', 0, '#'))

keypad = adafruit_matrixkeypad.Matrix_Keypad(rows, cols, keys)

while True:
    keys = keypad.pressed_keys
    if keys:
        print("Pressed: ", keys)
    time.sleep(0.1)
```
