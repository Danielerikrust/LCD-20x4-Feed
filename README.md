# LCD-20x4-Feed

![LCD Feed](/images/LCD_Feed.jpg#center)

Scrolling 20x4 LCD Feed for Micropython and Rpi Pico

This is written for the Freenove I2C LCD 2004 & I2C LCD 1602 modules. It utilizes the code provided by Freenove, except condensed into a single file with the addition of my LCD Feed functions.

https://freenove.com/fnk0079/

## Installation

Copy *LCD_Display.py* into your Pico */lib* directory.

Add the following lines to main.py:

    import time
    from machine import I2C, Pin, UART
    from LCD_Display import LcdApi, I2CLcd

    """LCD Section"""
    i2c = I2C(0, sda=Pin(20), scl=Pin(21), freq=400000) #GPIO 20 & 21 have no other function but I2C
    devices = i2c.scan()
    if devices != []:
        lcd = I2CLcd(i2c, devices[0], 4, 20)

    lcd.topdata("THIS REMAINS STATIC")
    time.sleep(1)
    lcd.feed("^ These")
    time.sleep(1)
    lcd.feed("^^ Lines")
    time.sleep(1)
    lcd.feed("^^^ Feed")
    time.sleep(1)
    lcd.feed("^^^^ Up")
    time.sleep(1)
    lcd.feed("as you add new ones")

For the Rpi Pico I have found that GPIO 20 & 21 are ideal for I2C devices because these pins are not otherwise used for functions such as UART, ADC or SPIO. Match the Pico & LCD SDA pins together. And match the SCL pins together. 

![Rpi Pico Pinout](/images/Pico_Pinout.png#center)

## lcd.topdata

To feed the full 4 lines of text simply disable the *lcd.topdata* function with:

    lcd.topdataline = False

To start or resume a static top data line use:

    lcd.topdata("  Your new string   ")
