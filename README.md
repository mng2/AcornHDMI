# AcornHDMI
This is a design for a DVI/HDMI buffer, for use with the SQRL Acorn, an Artix-7 FPGA board originally intended for mining.

## Why
The SQRL Acorn CLE-215+ consists of the largest Artix-7 FPGA, some DDR memory, and associated support circuitry. Since it was designed as an accelerator board in M.2 format, it does not have much in the way of user I/O, merely 4 LVDS pairs on a 2.5V bank, and 2 pairs on a 3.3V bank.

Four pairs is not much, but it is just enough for a DVI or HDMI interface to an external monitor. The remaining issue is the physical layer: while Xilinx does support a TMDS I/O standard on this FPGA, it's only on 3.3V banks and the four pairs are on 2.5V. So while one could engage in some educated guesswork about I/O structures and do some seat-of-the-pants engineering, the more boring approach is to use a chip designed for the purpose.

For this board the PTN3381D (or B?) fits the bill. Besides buffering into TMDS outputs, it handles level shifting for the Display Data Channel interface and hotplug detect, and generates 5V for the downstream device. Plus it does some other things that are probably unnecessary.

## Details

## License
CERN OHL v2 Permissive
