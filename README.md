# CD-i Notes
This repository will periodically be updated with my reverse-engineering of the Philips CD-i 220 F2 player's CDIC-related OS code.

The Philips CD-i 220 F2 used a set of five chips to manage audio-related tasks:
- "ATTEX", a GSX38KG307CE46 gate array.
- A pair of FCB61C65 8Kx8 SRAMs to provide 16K of buffer RAM for samples and CD sector data.
- A custom ADPCM decoder IC, IMS66490.
- A custom DSP IC, PCB5010.

These five chips are collectively referred to as the "CDIC", and are what provided audio playback facilities on numerous Philips and Magnavox CD-i players from the early 90's. In later revisions of the hardware, these were replaced by a Motorola DSP56001, and in still-later hardware revisions, they were replaced by an ASIC called "IKAT".

Emulation of the CDIC is currently good enough in MAME that a large number of games run with no audio issues. However, there are nonetheless some games, such as Namco's Pac-Panic, which lack audio due to an incomplete understanding of the CDIC's behavior.

It has been difficult to work out a set of emulated behavior which makes all CD-i games happy based on observing what gets written to the CDIC's registers. This is primarily because all games published on the console were expected to communicate with the hardware through OS calls, rather than by touching the hardware directly as games did in contemporary consoles such as the NES and SNES. This is something which only became en vogue upwards of 15 years later, with the advent of such consoles as the Xbox 360 and PlayStation 3.

As such, I have opted to manually disassemble, and re-write in C-like pseudocode, all of the functions pertaining to audio playback that reside in the CD-i 220 F2 player's BIOS. While this represents a significant amount of work, it is less work than any of the alternatives, which include writing a working Motorola DSP56001 core, adding /DTACK support to MAME's Motorola 68000 core, and low-level emulating the two Motorola 68HC05 MCUs on the player.

This repository will contain only one file, a simple text file containing the current state of my reverse-engineering effort.
