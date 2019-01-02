# MicroPython-ST7735 multiple displays

This is a fork of [boochow's library](https://github.com/boochow/MicroPython-ST7735) which is a modified version of [GuyCarver's ST7735.py](https://github.com/GuyCarver/MicroPython/blob/master/lib/ST7735.py) ST7735 TFT LCD driver for MicroPython.

It differs in that you can connect multiple diplays on the same bus and use the library to control all of them. Instead of supplying a single chip-select pin, you give an array of the chip-select pins of all displays. All other pins are shared. I added a method to instruct the library which display to use, i.e. which chip-select to activate.

```python

# Initialize SPI Bus
spi = SPI(2, baudrate=20000000, polarity=0, phase=0, sck=Pin(14), mosi=Pin(13), miso=Pin(12))

# CS pins for all screens in use
screens = [5, 18, 19]
# Initialize the TFT with the screens array
# DC = 16, Reset = 17, CS = [5,18,19]
tft=TFT(spi,16,17,screens)

tft.use(0)
tft.fill(TFT.BLACK)
tft.use(1)
tft.fill(TFT.WHITE)

```

