# DisplayWrapper

This is a small wrapper to map ThingPulse OLED library calls to LovyanGFX. It contains LovyanGFX configurations for SSD1306, ST7789 and ILI9341 based displays. This just maps the Thingpulse library calls used by the Morserino32 project so that larger ST7789 & ILI9341 displays can be used. Hence it's probably not fit for any other purpose.

# Fonts
The font support is very limited and only supports mapping of the fonts used by the Morserino32 project (DialogInput bold & plain in 12 and 15) to AdafruitGFX fonts as those are supported by LovyanGFX. A more sophisticated font mapping might be very usable, but due to the limited amount of fonts being used in M32 this does the trick so far. Original thingpulse and GFX fonts were generated via http://oleddisplay.squix.ch/ . The Adafruit `fontconvert` utility can be used to generate GFX fonts from ttf. Example to generate an 8-bit font at 15p including special chars like umlauts: `fontconvert IntelOneMono-Bold.ttf 15 32 255`

The header defines:
~~~
#define DialogInput_plain_12 0
#define DialogInput_bold_12 1
#define DialogInput_plain_15 2
#define DialogInput_bold_15 3
~~~

Instead of including those thingpulse font files from squix the numeric defines will let `setFont()` chose the right AdafruitGFX font variant as per specified index. When `ST7789_DRIVER` is defined, this will map to the same font with size 24 and 30.

## SSD1306 usage

The library defaults to SSD1306. Example pio build flags:
~~~
build_flags=
  -D OLED_SDA=17
  -D OLED_SCL=18
~~~

## ST7789 usage

`ST7789_DRIVER` has to be defined. Example pio build flags for a Heltec VM-T190:
~~~
build_flags=
    -DST7789_DRIVER
    -DTFT_WIDTH=170
    -DTFT_HEIGHT=320
    -DTFT_MISO=-1
    -DTFT_MOSI=48
    -DTFT_SCLK=38
    -DTFT_CS=39
    -DTFT_DC=47
    -DTFT_RST=40
    -DTFT_BL=17
    -DTFT_OFFSET_X=35 ; Heltec T190 & CYD 1.9
~~~

## ILI9341 usage

Same as for the sst7789.

# color
It is possible to use color "themes". To do this, you need to enable themes by setTheme(uint16_t forground_color, uint16_t background_color). The arguments are 16bit RGB values. You can turn color support off by calling that function with two equal arguments (foreground_color == background_color).