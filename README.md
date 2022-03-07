[:fr:](LISEZMOI.md) [:uk:](README.md)

# Pi400RGB
Scart/VGA interface for Raspberry Pi 400

Evolution of VGA_Zero (https://github.com/llegoff/VGA_Zero) and Pi400VGA (https://github.com/llegoff/Pi400VGA)

buy on [ebay](https://www.ebay.fr/itm/403514313069) :package: :credit_card:

![](img/Pi400RGB1.jpg)

![](img/Pi400RGB2.jpg)

### DPI (Display parallel Interface)
Like [VGA666](https://github.com/fenlogic/vga666), this pcb uses dpi interface (in mode 6 to free gpio 18 & 19)

![](img/dpi-packing.png)

see https://www.raspberrypi.org/documentation/hardware/raspberrypi/dpi/README.md

only the necessary bits of the dpi are redirected to the 40-pin GPIO port, with the 'gpio=2-9,12-17,20-25=a2' line on config.txt

/boot/config.txt

    # disable i2c, pin use by h-sync & v-sync
    dtparam=i2c_arm=off
    # remplace dtoverlay=vc4-kms-v3d by
    dtoverlay=vc4-fkms-v3d
    #configuration DPI
    gpio=2-9,12-17,20-24=a2
    dpi_output_format=0x6
    enable_dpi_lcd=1
    display_default_lcd=1
    dpi_group=2
    dpi_mode=16
    #---------------- dpi_mode line VGA ---------------------
    #---> 640x480 60hz    dpi_mode=4
    #---> 800x600 60hz    dpi_mode=9
    #---> 1024x768 60hz   dpi_mode=16
    #---> 1280x768 60hz   dpi_mode=23
    #---> 1280x800 60hz   dpi_mode=28
    #---> 1280x960 60hz   dpi_mode=32
    #---> 1280x1024 60hz  dpi_mode=35
    #---> 1360x768 60hz   dpi_mode=39
    #---> 1366x768 60hz   dpi_mode=81
    #---> 1400x1050 60hz  dpi_mode=42
    #---> 1440x900 60hz   dpi_mode=47
    #---> 1600x1200 60hz  dpi_mode=51
    #---> 1680x1050 60hz  dpi_mode=58
    #---> 1920x1080 60hz  dpi_mode=82
    #---> 1920x1200 60hz  dpi_mode=69
    #---> 1920x1440 60hz  dpi_mode=73    
    #--------------- dpi_mode line SCART ------------------
    dpi_mode=87
    hdmi_timings=506 1 8 44 52 240 1 6 10 6 0 0 0 60 0 9600000 1
    #hdmi_timings=320 1 17 33 34 224 1 14 8 18 0 0 0 60 0 6400000 1

### Audio Interface
audio interface is connected to gpio 18 & 19 (PWM)

/boot/config.txt

    # Enable audio for PiZero(loads snd_bcm2835)
    dtoverlay=audremap,pins_18_19
    dtparam=audio=on

### Recalbox

edit the config file /crt/recalbox-crt-options.cfg in the [RECALBOX] partition mounted when you plug the SD card in your computer:

    # Pour rgbpi
    adapter.type = rgbpi

https://wiki.recalbox.com/fr/tutorials/video/crt/recalbox-on-crt-with-scart-dac

![](img/recalbox-config.png)

## Schematic
![sch](img/sch.PNG)

## PCB
![pcb](img/3D.PNG)
![pcb](img/3D2.PNG)

## Installation
copy content of [config-example.txt](img/config-example.txt?raw=true) to /boot/config.txt


## Révision
rev1 : initial version

rev2 : add DDC on VGA connector and dip switch, coming soon
