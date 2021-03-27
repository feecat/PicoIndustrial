# PicoIndustrial
Industrial Control Module Based on RPI PICO  
----------  
![](/Docs/PicoIndustrial.png)  
You can [buy it at here](https://item.taobao.com/item.htm?id=641338698393), for now im in small batch production. Also you can manufactory it by yourself.  
There have 8 digital input, 8 relay output, 2 analog input, 2 analog output and 4 pico pin output.  
Digital IO is DC 24v PNP/NPN compatible, Analog IO is 0-10v or 0-20mA selectable.  
It was a simple plc or simple controller, Like some they called "arduino plc" controller but more powerfull.  
Here is product images, Actually its first that one-shoot successful product for me:  
![](/Docs/image_0.jpg)![](/Docs/image_1.jpg)  

## Example MicroPython Code  
```python
# Example of PicoIndustrial
from machine import Pin, PWM, ADC
from utime import sleep_ms
# Digital I/O Mapping
DI = [Pin(26, Pin.IN, Pin.PULL_DOWN), Pin(22, Pin.IN, Pin.PULL_DOWN), Pin(21, Pin.IN, Pin.PULL_DOWN), Pin(20, Pin.IN, Pin.PULL_DOWN), Pin(19, Pin.IN, Pin.PULL_DOWN), Pin(18, Pin.IN, Pin.PULL_DOWN), Pin(17, Pin.IN, Pin.PULL_DOWN), Pin(16, Pin.IN, Pin.PULL_DOWN)]
DO = [Pin(7, Pin.OUT), Pin(9, Pin.OUT), Pin(10, Pin.OUT), Pin(11, Pin.OUT), Pin(12, Pin.OUT), Pin(13, Pin.OUT), Pin(14, Pin.OUT), Pin(15, Pin.OUT)]
LED = [Pin(25, Pin.OUT), Pin(8, Pin.OUT), Pin(4, Pin.OUT)]
# ADC + DAC, DAC Use PWM to control voltage
AI = [ADC(Pin(28)), ADC(Pin(27))]
AO = [PWM(Pin(5)), PWM(Pin(6))]
AO[0].freq(500000)
AO[1].freq(500000)
# Write Init code here
LED[0].value(1)
# Write Loop code here
while True:
    # Analog IO
    AO[0].duty_u16(32767)
    print(AI[0].read_u16())
    # LED Toggle
    LED[2].value(not LED[2].value())
    # Digital IO
    DO[0].value(DI[0].value())
    DO[1].value(not DI[1].value())
    DO[2].value(DI[2].value())
    # Sleep
    sleep_ms(100)
    
```
