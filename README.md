# AcornHDMI
This is a design for a DVI/HDMI buffer, for use with the SQRL Acorn, an Artix-7 FPGA board originally intended for mining.

## Why
The SQRL Acorn CLE-215+ consists of the largest Artix-7 FPGA, some DDR memory, and associated support circuitry. Since it was designed as an accelerator board in M.2 format, it does not have much in the way of user I/O, merely 4 LVDS pairs on a 2.5V bank, and 2 pairs on a 3.3V bank.

Four pairs is not much, but it is just enough for a DVI or HDMI interface to an external monitor. The remaining issue is the physical layer: while Xilinx does support a TMDS I/O standard on this FPGA, it's only on 3.3V banks and the four pairs are on 2.5V. So while one could engage in some educated guesswork about I/O structures and do some seat-of-the-pants engineering, the more boring approach is to use a chip designed for the purpose.

For this board the PTN3381B fits the bill. Besides buffering into TMDS outputs, it handles level shifting for the Display Data Channel interface and hotplug detect, and generates 5V for the downstream device. Plus it does some other things that are probably unnecessary.

## Chips Used
- **PTN3381B** (NXP): 
NXP makes a number of video interface translation chips, including this one which seems to be intended to take DisplayPort (electrical-wise) and output TMDS. Each input is capacitively coupled and terminated into 50 ohms, so in theory an LVDS diff pair will "see" the 100 ohms it expects. The B version of the part supports up to 1.65 Gbit/s operation, and the D version supports 3 Gbit/s; however a -3 speed grade Artix-7 only goes up to 1250 Mbit/s, so the D is overkill. From a cursory examination, the only difference in the pinout is how the pre-emphasis is configured, so it should be possible to support both models. (Note that the D version is going EOL.)
- **PCA9534** (NXP, TI): 
This is an I2C expander with 8 bits of real FET drive output, as opposed to the weird weak drive that other models use. The I/O bits are used to configure the PTN3381 for the most part. CEC is a stretch goal...

## Connectivity
The Acorn has the relevant I/O on a Hirose DF52 connector.

## Links

## License
CERN OHL v2 Permissive
