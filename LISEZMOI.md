[:fr:](LISEZMOI.md) [:uk:](README.md)

# Pi400RGB
Interface Péritel/VGA pour le Raspberry Pi 400

Evolution du VGA_Zero (https://github.com/llegoff/VGA_Zero) et du Pi400VGA (https://github.com/llegoff/Pi400VGA)

Achetez la V1 VGA on [ebay  :package: :credit_card:](https://www.ebay.fr/itm/403577489257)

Achetez la V2 sur [ebay  :package: :credit_card:](https://www.ebay.fr/itm/403578324991) (with dip switch for recalbox)

![](img/Pi400RGB1.jpg)

![](img/Pi400RGB2.jpg)

![](img/Pi400RGB3.jpg)


### DPI (Display parallel Interface)
Comme pour l'interface [VGA666](https://github.com/fenlogic/vga666), ce montage utilise le l'interface DPI du Raspberry pi (mode 6), 

![](img/dpi-packing.png)

voir https://www.raspberrypi.org/documentation/hardware/raspberrypi/dpi/README.md

seuls les bits nécessaires du dpi sont redirigées sur le port GPIO 40 broches, avec la ligne 'gpio=2-9,12-17,20-25=a2' dufichier config.txt 

/boot/config.txt

    # disable i2c, pin use by h-sync & v-sync
    dtparam=i2c_arm=off
    # remplacer dtoverlay=vc4-kms-v3d par
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
    #244p@60
    #hdmi_timings=320 1 4 30 46 240 1 4 5 14 0 0 0 60 0 6400000 1
    #288p@50
    #hdmi_timings=384 1 16 32 40 288 1 3 2 19 0 0 0 50 0 7363200 1
    #576i@50
    hdmi_timings=768 1 24 72 88 576 1 6 5 38 0 0 0 50 1 14875000 1
    #480i@60
    #hdmi_timings=640 1 24 64 104 480 1 3 6 34 0 0 0 60 1 13054080 1
    #480p@60
    #hdmi_timings=640 1 24 96 48 480 1 11 2 32 0 0 0 60 0 25452000 1
    
Configuration compatible avec vc4-kms-v3d

    dtoverlay=vc4-kms-dpi-generic,rgb666-padhi
    dtparam=hactive=768,hfp=24,hsync=72,hbp=88
    dtparam=vactive=576,vfp=6,vsync=5,vbp=38
    dtparam=clock-frequency=14875000
    #Resolution          hactive hfp hsync hbp  vactive vfp vsync vbp clock-frequency
    #VGA 640x480 @60     640     16  96    48   480     10  2     33  25175000
    #SVGA 800x600 @60    800     40  128   88   600     1   4     23  40000000
    #XGA 1024x768 @60    1024    24  136   160  768     3   6     29  65000000
    #244p @60            320     4   30    46   240     4   5     14  6400000
    #288p @50            384     16  32    40   288     3   2     19  7363200
    #576i @50            768     24  72    88   576     6   5     38  14875000
    #480i @60            640     24  64    104  480     3   6     34  13054080
    #480p @60            640     24  96    48   480     11  2     32  25452000
    #more timming on http://tinyvga.com/vga-timing
    
    
### Interface audio
le son est généré en MLI (PWM) à partir des broches gpio 18 & 19

/boot/config.txt

    # Enable audio on GPIO for Pi 400
    dtoverlay=audremap,pins_18_19
    dtparam=audio=on
  
### Recalbox

Editez le fichier de configuration /crt/recalbox-crt-options.cfg qui se trouve dans la partition [RECALBOX] lorsque vous placez la carte sd dans votre ordinateur:

Voir le manuel : https://www.recalbox.com/fr/recalbox-rgb-dual/manual/


editez le fichier /crt/recalbox-crt-options.cfg

    # Pour recalboxrgbdual
    adapter.type = recalboxrgbdual

le premier démarrage peut prendre 5 minutes

https://wiki.recalbox.com/fr/tutorials/video/crt/recalbox-on-crt-with-scart-dac

![](img/recalbox-config.png)

Ajouter un cavalier de configuration sur le PCB V1

![](img/config_jumper.jpg)

   
## Schéma & Circuit Imprimé
![sch](img/sch.PNG)

![pcb](img/3D.PNG)
![pcb](img/3D2.PNG)

## Installation
Copier le contenu du fichier [config-example.txt](img/config-example.txt?raw=true) dans le fichier /boot/config.txt

## Révision
rev1

rev2 : ajout du DDC sur le connecteur VGA et dip switch, arrive prochainement
