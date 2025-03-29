# Open Heart
"Open Heart" is a simple Sega Genesis/Mega Drive multi-mod using a bare Raspberry Pi Pico or compatible board. Now Is Time To The 68000 Heart On Fire.

## Features
- Switchless region changing with automatic PAL/NTSC switching
- Dual Frequency Oscillator for correct speed in both modes
- In-game reset function
- In-game switchable overclocking
- TMSS bypass

## Generic install instructions

This mod is very similar to other extant mods so adapting it to your particular console should not be difficult. Schematics or references for other similar mods might prove helpful.
Remove the oscillator and mount the Pico as closely to its board location as is feasible. **5V** and **ground** are easily connected to the through-holes left from removing the oscillator. It is recommended to use a diode (I used a 1n4001) on the 5V point if you plan on updating firmware with the mod installed. **MCLK** should be connected to the oscillator clock output. **VCLK** is connected to the clock in pin of the 68000 (the VDP is also connected to this and should be disconnected from it). These wires should be kept as short as possible. **Jpn/Export** and **NTSC/PAL** should be connected to the points on your board where +5V and Ground determine region and 50/60Hz respectively. **VRES** and **HALT** are connected to the corresponding pins on the 68000. **Pins 6, 7 and 9** correspond to those pins on the first controller port, counting 1 through 9 starting with the top left pin from the front of the console. **Cart Enable** corresponds to pin B17 of the cartridge port, pin B1 is the leftmost pin at the front, facing the console. This is used for the TMSS bypass, if you are installing this on a non TMSS console, this should probably be connected to ground. The **VCLK** and **HALT** connections are optional if for some reason you do not wish to use the overclocking feature. If you want to have an LED that shows you what state the mod is in, get a "common cathode" bi-color LED. Attach the cathode to ground somewhere, and the two anodes to LED1 and LED2. Region is indicated by changing color: LED1's color indicates Japan, LED2's color indicates US/Americas, and the mix of the two colors indicates Europe. Overclock is indicated by pulsing the LED at 3Hz when it's enabled. See the MD2 VA0 install below for a suggested mounting for Model 2 MDs.

![pico-pins](https://github.com/user-attachments/assets/30e0a15a-6264-401b-8ba3-f9aff79de867)

## Genesis/MD2 VA0 install
![image](https://github.com/user-attachments/assets/e98d79b8-494d-4cbd-8726-a24f79ac75f8)

The LED can be mounted this way with its cathode leg in the left hole of the original LED mount:
![20250328_175125](https://github.com/user-attachments/assets/477e97ee-7fe8-4cce-ab1f-0cc4175103df)

## Setting up the Pi Pico
Download the [openheart.uf2 firmware image](https://github.com/DUSTINODELLOFFICIAL/openheart/raw/refs/heads/main/build/openheart.uf2) from /build and flash it to the Pico by connecting it to your computer while holding down the BOOTSEL button. It will show up as a storage device, just drag the UF2 file onto it. It's good to go when the storage device disconnects.

## How to use
- To reset game, hold A+B+C+Start for 1 second
- To toggle overclock on and off, hold A+Start for 1 second
- To change region, press Reset button 3 times within 3 seconds. The last used region is saved until it is changed again.

## Notes & considerations
- Use at your own risk: I don't have the means to test this on all of the different versions of MD/Genesis motherboards. There is nothing that should prevent it from working on any MD/Genesis, but for now, you're on your own
- The clocks generated by the Pi Pico are specced at exactly 53.7 and 53.2 MHz for NTSC and PAL. This is imperceptibly slightly faster and slower (1/100ths of a % either way) than the original oscillator ratings respectively. In reality, it is likely within tolerance and not different than the difference between any two consoles. For what it's worth, the service manual also refers to the oscillator as 53.7 and 53.2MHz.
- Overclocking sets the CPU to the master clock/5 (stock is MCLK/7). This is about 10.74MHz on NTSC. Most games work well with this with a few exceptions of mild graphical glitching, but since this is out of spec for an 8MHz rated 68000, your results can of course vary.
- The phase relationship of the Pico-generated VCLK and MCLK haven't been looked at at all or compared to stock in any way.
- Some (few?) NTSC Model 1 VA7's and Model 2 VA0's [have a broken 50Hz mode.](https://consolemods.org/wiki/Genesis:Motherboard_Differences#VA0_(1993,_All_Regions) "have a broken 50Hz mode.")
- PAL mode composite video is not tested on NTSC consoles and vice versa--I don't have the equipment. It should work; however, the service manual calls for different parts for the video encoder in each case so it may not function as intended. This doesn't apply to RGB output, which is known to work.
