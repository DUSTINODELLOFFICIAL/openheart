# Open Heart
"Open Heart" is a simple Sega Genesis/Mega Drive multi-mod using a bare Raspberry Pi Pico or compatible board. Now Is Time To The 68000 Heart On Fire.

**NOTE THAT THIS MOD IS STILL A WORK IN PROGRESS and that some features and wiring may change, but the info here will stay consistent with the current version of the firmware. Take note of any changes before updating the firmware.**

## Features
- Switchless region changing with automatic PAL/NTSC switching
- Dual Frequency Oscillator for correct speed in both modes
- In-game reset function
- In-game switchable overclocking
- TMSS bypass
- Optional LED to indicate region and overclock status

## Generic install instructions

You may want to look at [this thread](https://github.com/DUSTINODELLOFFICIAL/openheart/issues/4)

This mod is very similar to other extant mods so adapting it to your particular console should not be difficult. Schematics or references for other similar mods might prove helpful.
Remove the oscillator and mount the Pico as closely to its board location as is feasible.
- **5V** and **ground** are easily connected to the through-holes left from removing the oscillator. It is recommended to use a diode (I used a 1n4001) on the 5V point if you plan on updating firmware with the mod installed.
- **MCLK** should be connected to the oscillator clock output. 
- **VCLK** is connected to the clock in pin of the 68000 (the VDP is also connected to this and should be disconnected from it). These wires should be kept as short as possible.
- **Jpn/Export** and **NTSC/PAL** should be connected to the points on your board where +5V and Ground determine region and 50/60Hz respectively.
- **VRES** and **HALT** are connected to the corresponding pins on the 68000. 
- **Pins 6, 7 and 9** correspond to those pins on the first controller port, counting 1 through 9 starting with the top left pin from the front of the console.
- **Cart Enable** corresponds to pin B17 of the cartridge port, pin B1 is the leftmost pin at the front, facing the console. This is used for the TMSS bypass, if you are installing this on a non TMSS console, this should probably be connected to ground.
- **MRES** corresponds to pin B2 of the cartridge port. This is used for the TMSS bypass,when a flashcart gets in and out of special modes such as Master System or Sega CD. If you are installing this on a non TMSS console, this should not be connected.
- **M3** corresponds to pin B30 of the cartridge port, required to detect master system mode.
- The **VCLK** and **HALT** connections are optional if for some reason you do not wish to use the overclocking feature. If you want to have an LED that shows you what state the mod is in, get a "common cathode" bi-color LED. Attach the cathode to ground somewhere, and the two anodes to LED1 and LED2. Region is indicated by changing color: LED1's color indicates Japan, LED2's color indicates US/Americas, and the mix of the two colors indicates Europe. Overclock is indicated by pulsing the LED at 3Hz when it's enabled. See the MD2 VA0 install below for a suggested mounting for Model 2 MDs.

![Screenshot_20250620_130043_Firefox](https://github.com/user-attachments/assets/a3d26eb5-29e0-487f-9045-4d70c442b57f)

## Genesis/MD2 VA0 install
![image](https://github.com/user-attachments/assets/ee34c3cc-4640-4e1c-9d61-5105bb64a103)

The LED can be mounted this way with its cathode leg in the left hole of the original LED mount:
![20250328_175125](https://github.com/user-attachments/assets/477e97ee-7fe8-4cce-ab1f-0cc4175103df)

## Model 2 VA1 install
Note: the MRES wire can be attached to a via (the lower left one next to the B1 marking).
![image](https://github.com/user-attachments/assets/c1c9d5d3-175b-4908-ab80-af9f95baf7d5)

## Model 1 VA6 install
See [this post](https://github.com/DUSTINODELLOFFICIAL/openheart/issues/4#issuecomment-2764840539) from adardar211 or [these pictures (without overclock)](https://imgur.com/a/E07TWUL)  from Zeb-76.

## Model 1 VA4 install
See [these pictures](https://imgur.com/a/BYaBhWR), thanks to Zeb-76

## Setting up the Pi Pico
Download the [openheart.uf2 firmware image](https://github.com/DUSTINODELLOFFICIAL/openheart/raw/refs/heads/main/build/openheart.uf2) from /build and flash it to the Pico by connecting it to your computer while holding down the BOOTSEL button. It will show up as a storage device, just drag the UF2 file onto it. It's good to go when the storage device disconnects.

## How to use
- To reset game, hold A+B+C+Start for 1 second
- To toggle overclock on and off, hold A+Start for 1 second
- To change region, press Reset button 3 times within 3 seconds. The last used region is saved until it is changed again.

## Notes & considerations
- Use at your own risk: The mod seems to work fine in various Model 1 and Model 2 revisions, but not every revision is tested.
- This is primarily a Mega Drive mod. The region and DFO feature works for SMS games in SMS mode, but the other features rely on Mega Drive mode.
- Overclocking sets the CPU to the master clock/5 (stock is MCLK/7). This is about 10.74MHz on NTSC. Most games work well with this, but be aware you can still experience crashes, graphics glitches, or controller malfunctioning.
- The clocks generated by the Pi Pico are imperceptibly slightly different (+0.013% NTSC, -0.006% PAL) than the original oscillator ratings. This isn't noticeable, but may be worth considering if you are a speedrunner.
- Switching between 50 and 60Hz, or toggling overclock on and off often while playing a game, might rarely result in odd behavior. If this happens just cycle power.
- Some (few?) NTSC Model 1 VA7's and Model 2 VA0's [have a broken 50Hz mode.](https://consolemods.org/wiki/Genesis:Motherboard_Differences#VA0_(1993,_All_Regions) "have a broken 50Hz mode.") These consoles still work at 60Hz however.
- PAL mode composite video on NTSC consoles and vice versa may or may not work. RGB output will work. This could depend on your TV or which standard is being used.
