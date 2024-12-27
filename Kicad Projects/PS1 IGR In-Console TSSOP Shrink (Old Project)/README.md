# Playstation 1 In-Game Reset (IGR) - TSSOP Version

This is a shrink of the PCB for [pyroesp's](https://github.com/pyroesp) Playstation 1 Reset Mod code, found at https://github.com/pyroesp/PlayStation-1-Reset-Mod

Quick overview: The project, when installed into a Playstation 1 system, allows an in-game reset based on a combination of controller buttons. This is most handy when paired with an ODE to reset back to a disc selection menu.

The original board uses the SOIC package of the PIC16F18325 Microcontroller. This one uses the TSSOP package and the board itself is a good amount smaller (12.1x7.7mm). No code changes necessary as the microcontroller itself is the same regardless of package size.  
Code, details of the solution, original PCB design, and instructions for programming and installation are available at [pyroesp's Github](https://github.com/pyroesp). Programming-ready hex file in the [releases section](https://github.com/pyroesp/PlayStation-1-Reset-Mod/releases)


<p align="center">
  <img width="300" src="Images/PS1-IGR TSSOP Version (20210109) svg top.png">
</p>

<p align="center">
  <img width="300" src="Images/PS1-IGR TSSOP Version Top.jpg"> <img width="300" src="Images/PS1-IGR TSSOP Version Bottom.jpg">
</p>

### Why?

Sometimes I like to see how small I can get simple PCBs while maintaining function and hand-solderability. This not only reduces the space required for installation, but proves to be a nice soldering challenge.  
While the original 14.5x12mm board through a fab like OSHpark was already pretty cheap ($1.35 for three), the smaller board is only $0.70 for three.  
The gerber is shared on Oshpark for convenience: https://oshpark.com/shared_projects/F4ubwE2n

Size comparison to the original board:

<p align="center">
  <img width="640" src="Images/PS1-IGR TSSOP Size comparison.png">
</p>

### BOM:

Only two components are needed:
- **U1**: Microchip PIC16F18325-I/ST (TSSOP-14 Package). [Digikey](https://www.digikey.com/en/products/detail/microchip-technology/PIC16F18325-I-ST/5323626)
- **C1**: Any 100nf 0603 =>16v Ceramic capacitor.<br />
    Examples:<br />
        [Samsung CL10B104KB8NNNL](https://www.digikey.com/en/products/detail/samsung-electro-mechanics/CL10B104KB8NNNL/3894274)<br />
        [Murata GCJ188R71E104KA12D](https://www.digikey.com/en/products/detail/murata-electronics/GCJ188R71E104KA12D/7363221)

### Notes:

- You will of course need a programmer to flash the code to the microcontroller, such as a PICkit3. This can be done via the ICSP pads on the bottom of the board by soldering some temporary wiring to connect it to the programmer. An alternative would be a TSSOP to DIP socket adapter ([an example of such on Aliexpress](https://www.aliexpress.com/item/32868905130.html)) to house the chip for programming before it is soldered to the board.
- The text in the bottom copper layer *may* cause some fabs to complain about the size of the text. OSHpark doesnt have an issue (they seem to fab whatever you throw at them, regardless if it comes out well in the final product), but I have experienced cases in the past where JLCPCB will remove any text from the board that they deem too small.

### Tools used for this project:
- Tracespace View (SVG conversions of gerbers for the above images) https://tracespace.io/view/
- KiCad 5.1.8 https://www.kicad.org/
- Inkscape https://inkscape.org/

### License:
This derivative work maintains the same source license as the original board and project:  
Attribution-ShareAlike 4.0 International. See license file for more info