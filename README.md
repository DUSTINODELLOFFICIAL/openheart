"Open Heart" is a simple sega genesis/mega drive multi-mod using a bare raspberry pi pico or compatible board.

Generic install instructions

This mod is very similar to other extant mods so adapting it to your particular console should not be difficult. 5V and ground are easily connected to the vias left from removing the oscillator. MCLK should be connected to the oscillator clock output. VCLK is connected to the clock in pin of the 68000 (the VDP is connected to this and should be disconnected from it). Jpn/Export and NTSC/PAL should be connected to the points on your board where +5V and Ground determine region and 50/60Hz respectively. VRES and HALT are connected to the corresponding pins on the 68000. Pins 6, 7 and 9 correspond to those pins on the first controller port, counting 1 through 9 starting with the top left pin from the front of the console. Cart Enable corresponds to pin B17 of the cartridge port, pin B1 is the leftmost pin at the front, facing the console. If you are installing this on a non TMSS console, this should probably be connected to ground.

