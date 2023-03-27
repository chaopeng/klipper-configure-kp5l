# My KP5L Klipper Configure

I have a [Kingroon KP5L](https://kingroon.com/products/official-kingroon-kp5l-3d-printer) 3D printer, I prefer to use klipper instead marlin. I have follow the [official klipper configure](https://github.com/nehilo/Klipper-KingRoon-Printers) but got some issue.

After a lot of upgrade I have totally different KP5L. I hope this repo is useful for your setup and your decision of purchase KP5L.

## Dirs

### kp3s-v1.3

My KP5L came with KP3S v1.3 Motherboard. I also purchased 3D Touch from Kingroon.

I did get my KP5L on Klipper works OK. There is some step and some changes to the offical repo.

1. I did not use TMC UART mode, so I commented out the tmc in `printer.cfg`.
1. My extruder motor direction is not reversed, I removed `!` -> `dir_pin: PD3`.
1. The first setup I did not use bltouch I needed to comment out `[include bltouch.cfg]` in `printer.cfg` and `[gcode_macro PROBE_CALIBRATE]` section in `marcos/marcos.cfg`.
1. I connected the 3d touch to z+ port on the motherboard. The sensor pin should be `sensor_pin: ^PC4`. I found the pinout on [MKS-Robin-Nano](https://github.com/makerbase-mks/MKS-Robin-Nano-V1.X/blob/master/hardware/MKS%20Robin%20Nano-S%20V1.3_001/MKS%20Robin%20Nano-S%20V1.3_001%20PIN.pdf)
1. The 3d touch sensor from kingroon store also always report open no matter pin_down or pin_up. so `pin_up_touch_mode_reports_triggered: False`.
1. I designed a mount for the 3d touch sensor: https://www.thingiverse.com/thing:5745607
1. Messure sensor x, y, z offset follow this [video](https://youtu.be/5vmjBXvY6BA?t=379), then we can generate the bed mesh
1. It is nice to do resonance compensation, the easy way is to print the test tower, follow this [doc](https://www.klipper3d.org/Resonance_Compensation.html).

This setup is pretty good. But I found the CH341 (usb-uart) chip somehow disconnect randomly. So I change the motherboard to M8P.

### m8p-v1.1

My [M8P](https://github.com/bigtreetech/Manta-M8P) is version 1.1. I also upgrade hot end to [E3D Revo Six](https://e3d-online.com/products/revo-six) and use a 5v PWM fan from Noctua.

## Pros & Cons of KP5L

### Pros

- large print area
- frame is solid, better than v wheel

### Cons

- Y axis can move is a huge range, it is not easy to enclosure the print.
- mother board is not reliable, at least for my printer
- hot end is easy to stuck
