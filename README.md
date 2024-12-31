## Playstation 1 In-Game Reset (IGR)
### QSBs for One-wire Controller-PCB installs
<br/>
<br/>

These boards are variations on [PyroESP's](https://github.com/pyroesp) Playstation 1 Reset Mod project.

The original project and code can be found at https://github.com/pyroesp/PlayStation-1-Reset-Mod

To simplify the goal of this project: When installed into a Playstation 1 system, it facilitates a reset of the system using a button combination on controller 1, by tapping into the controller signals and toggling the system reset line. This is useful for those that have ODEs installed, as you can reset back to the menu of the ODE from the controller instead of getting up to hold the reset button down.

Originally I had posted a variation that was more or less a shrink of their original PCB (which used a SOIC package for the microcontroller), instead using the TSSOP version - to get the board as small as it could be for S&Gs and more of a "hardmode" install. This version of the project (while deprecated, unless you REALLY need to avoid installing to the controller PCB) is still hosted in the repository.

A while back (2002? Yes it has taken me that long to publish the final versions here) a member of the [Consolemods.org](https://www.consolemods.org) discord observed a variation on OSHpark that installed to the back of the controller PCB behind the player 1 port. However the project was not laid out correctly, thus the wrong (higher) voltage was applied to the microcontroller. This style of board is a "Quick Solder Board" (QSB), where the board is designed to sit on top of another PCB and solder directly to signal points (versus running a wire for each signal). Such a solution allows for a "one-wire" install of this project. All but one of the signals needed are available from the solder points of the controller ports themselves. The only wire that must be run is for the reset signal.
While these controller-PCB-mounted solutions were not uncommon at the time, the project on OSHpark appeared to the only published gerbers for folks that prefer to fabricate their own PCBs.
I decided to revisit the project to produce a correctly-wired version, using my own consoles for measurement. Some earlier versions of the gerbers were posted to the discord for members to use. This respository has three variations depending on your soldering preferences.
  
Code, details of the solution, original PCB design, and instructions for programming and installation are available at [pyroesp's Github](https://github.com/pyroesp). Programming-ready hex file in the [releases section](https://github.com/pyroesp/PlayStation-1-Reset-Mod/releases)


#### Controller-port (Port 1) install, SOIC Package (Normal difficulty)

<p align="center">
  <img src="images/PS1 IGR pyroesp JFT CTRLR SOIC Normal (20230212) ds.png">
</p>

This variant more or less aimed to substitute the faulty one on OSHpark. Installs over the solder points for controller port 1 and uses the SOIC package of the microcontroller (MCU). This should be fairly easy to assemble for anyone with decent soldering skills.

[Oshpark link](https://oshpark.com/shared_projects/fwJTyytg)

#### Controller-port (Port 1) install, TSSOP Package (Hard difficulty)

<p align="center">
  <img src="images/PS1 IGR pyroesp JFT CTRLR TSSOP Hard (20230212) top ds.png">
</p>

This is almost identical to the above variant, and installs the exact same way. The only difference is the use of the TSSOP package for the MCU. This requires slightly tighter soldering skills.

[Oshpark link](https://oshpark.com/shared_projects/G71d1amG)

#### Controller-ribbon connector (Center of controller PCB) install, UQFN Package (Ultrahard difficulty)

<p align="center">
  <img src="images/PS1 IGR pyroesp JFT CTRLR UQFN Ultra Hard (20241219) ds.png">
</p>

Staying in the same spirit as my original visit to the project, this board aims to be as small is it can be. I realized that another spot on the controller PCB contained all the same signals as the controller port: The connector for the ribbon cable that connects the controller assembly to the main system board. This PCB installs to the back of that connector instead of the controller port. Continuing with that same spirit, I figured go all out and use the UQFN package of the MCU - which is the smallest package it comes in. However this means this board is significantly more difficult to assemble by hand. Not impossible - I hand assembled the one installed in my main console - but takes very good soldering skills and tools. I imagine this is the smallest "one-wire" install of this solution available. All that said, the actual installation of the board into the console should not be much more difficult than the other two options.

[Oshpark link](https://oshpark.com/shared_projects/B2ZQAGCg)


### BOM:

Only two components are needed:

**U1**<br/> Depending on which board you which to assemble, the part number for the MCU will differ slightly (only the last two characters of the part number matter in this case)
- SOIC: Microchip PIC16F18325-I/SL. [Digikey](https://www.digikey.com/en/products/detail/microchip-technology/PIC16F18325-I-SL/5323625)
- TSSOP: Microchip PIC16F18325-I/ST. [Digikey](https://www.digikey.com/en/products/detail/microchip-technology/PIC16F18325-I-ST/5323626)
- UQFN: Microchip PIC16F18325-I/JQ. [Digikey](https://www.digikey.com/en/products/detail/microchip-technology/PIC16F18325-I-JQ/5639473)

**C1**:<br/>You really don't need to be picky about this part. Any 100nf to 1000nf/1uf 0603-sized Ceramic capacitor rated at 16v or above will work. <br />
    Examples:<br />
        [Samsung CL10B104KB8NNNL](https://www.digikey.com/en/products/detail/samsung-electro-mechanics/CL10B104KB8NNNL/3894274)<br />
        [Murata GCJ188R71E104KA12D](https://www.digikey.com/en/products/detail/murata-electronics/GCJ188R71E104KA12D/7363221)

### Notes:
- These have not been designed with the PSone in mind, and are only tested on the original "phat" models. While the PSones have no good ODE option (where this mod is most useful), I may take a quick look the next time I have a PSone open (maybe requires another board revision). 
- There are other variants of the MCU you can use, depending on whether you have trouble sourcing the above (I did when I built my prototypes) but they may be a few cents more expensive as they have extra features or tolerances. In this project, they will all function identically:
  - The "I/" in the part number can be swapped with the "E/" variant. The latter is just "Extended Tempurature range"
  - This project uses the PIC16F18325 MCU, however the the PIC16F18**326** can also be used. It's the exact same MCU with a little bit more memory and storage. Same HEX file can be used to program either. The board I installed in my main console uses the PIC16F18326-E/JQ part. I haven't researched whether the **324** can be used (less memory/storage than the 325). 
- You will of course need a programmer to flash the code to the microcontroller, such as a PICkit3. This can be done in several ways:
  - The ICSP pads on board by soldering some temporary wiring to connect it to the programmer.
  - The ICSP pads by using a 2mm pitch pogo-pin PCB clamp such as this one on [Aliexpress](https://www.aliexpress.com/i/3256806664884457.html)
  - An alternative would be a DIP socket adapter ([an example of such on Aliexpress](https://www.aliexpress.com/item/32868905130.html)) to house the chip for programming before it is soldered to the board.
- The text in the bottom copper layer *may* cause some fabs to complain about the size of the text. OSHpark doesnt have an issue (they seem to fab whatever you throw at them, regardless if it comes out well in the final product), but I have experienced cases in the past where JLCPCB will remove any text from the board that they deem too small.

### Tools used for this project:
- Tracespace View (SVG conversions of gerbers for the above images) https://tracespace.io/view/
- KiCad 8.0.6 https://www.kicad.org/
- GIMP for some of the image edits.

### To-do
- Post more detailed installation instructions
- Post or link to reset line points for various motherboard revisions.

### License:
This derivative work maintains the same source license as the original board and project:  
Attribution-ShareAlike 4.0 International. See license file for more info



<p align="center">
  <img width="300" src="images/PS1-IGR JFT CTRLR Center 3D Transparent.png">
</p>
