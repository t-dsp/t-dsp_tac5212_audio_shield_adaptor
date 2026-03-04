# T-DSP TAC5212 Audio Shield Adaptor for Teensy 4.1

**Part of the [T-DSP](https://t-dsp.com) open modular audio platform.**

A compact carrier board (60.93mm × 26.46mm) that connects a [T-DSP TAC5212 audio module](https://github.com/t-dsp) and a [Teensy 4.1](https://www.pjrc.com/teensy/) together into a simple, USB-powered Teensy audio shield — with stereo line in/out, two onboard PDM MEMS microphones, USB Host, and SD card access.

[![T-DSP TAC5212 Audio Shield Adaptor - Top Isometric](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/renders/t-dsp_tac5212_audio_shield_adaptor-3D_blender_th_top_iso.png)](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/gallery.html)

| | |
|:---:|:---:|
| [![Top](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/renders/t-dsp_tac5212_audio_shield_adaptor-3D_blender_th_top.png)](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/gallery.html) | [![Bottom](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/renders/t-dsp_tac5212_audio_shield_adaptor-3D_blender_th_bottom.png)](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/gallery.html) |
| [![Front](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/renders/t-dsp_tac5212_audio_shield_adaptor-3D_blender_th_front.png)](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/gallery.html) | [![Rear](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/renders/t-dsp_tac5212_audio_shield_adaptor-3D_blender_th_rear.png)](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/gallery.html) |

**[View 3D Render Gallery](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/gallery.html)** -- interactive slideshow of all board views

## What It Is

This is the simplest board in the T-DSP ecosystem. It is an **adaptor** — a small carrier PCB that brings together two modules:

- **[T-DSP TAC5212 module](https://github.com/t-dsp)** — the pro audio codec daughter board (plugs into the adaptor via headers)
- **[Teensy 4.1](https://www.pjrc.com/teensy/)** — ARM Cortex-M7 running the [Teensy Audio Library](https://www.pjrc.com/teensy/td_libs_Audio.html)

The result is a compact, bus-powered audio shield with stereo line I/O, two MEMS microphones, USB Host, and SD card access — no external power supply required.

## What You Need

| Item | Notes |
|------|-------|
| T-DSP TAC5212 audio module | Plugs into the adaptor's module connector |
| Teensy 4.1 | Socketed onto the adaptor's Teensy headers |
| This adaptor PCB | The carrier board documented here |

Power comes from the Teensy 4.1's USB connector — no external supply needed.

## Features

### Audio I/O
- **Stereo line input** -- via the TAC5212 module's ADC
- **Stereo line output** -- via the TAC5212 module's DAC
- **2× PDM MEMS microphones** -- Knowles SPK0641HT4H-1, speakerphone-grade, for voice capture or stereo room mics

### Connectivity
- **USB Host** -- USB-A host port for MIDI controllers, USB storage, and USB audio devices
- **SD card** -- Accessible via the Teensy 4.1's built-in SD slot

### Power
- **USB-C via Teensy 4.1** -- Bus-powered from the Teensy's USB-C port; no additional power input on this board

## Board Design

- **60.93mm × 26.46mm** PCB
- Designed around the T-DSP audio module board outline standard
- The TAC5212 module handles the entire analog signal path
- KiCad source files, full BOM, and CI-generated manufacturing outputs included
- Open source under CC BY-NC-SA 4.0

## Getting Started

### Hardware

1. Solder pin headers on your **Teensy 4.1** (if not already done)
2. Socket the Teensy 4.1 into the adaptor board headers
3. Plug the **TAC5212 module** into its connector on the adaptor
4. Connect your line-level audio source and output to the TAC5212 module's jacks
5. Connect USB-C to the Teensy 4.1 for power and optionally USB Audio

### Firmware

Use the [Teensy Audio Library](https://www.pjrc.com/teensy/td_libs_Audio.html) with the TAC5212 codec driver. Design your audio graph using PJRC's [Audio System Design Tool](https://www.pjrc.com/teensy/gui/).

```cpp
#include <Audio.h>
#include <Wire.h>

AudioInputI2S         audioIn;
AudioOutputI2S        audioOut;
AudioControlTAC5212   codec;

void setup() {
  AudioMemory(12);
  codec.enable();
  codec.inputSelect(AUDIO_INPUT_LINEIN);
  codec.volume(0.8);
}
```

View the design files in your browser with KiCanvas: [Schematic](https://kicanvas.org/?github=https://github.com/t-dsp/t-dsp_tac5212_audio_shield_adaptor/blob/main/t-dsp_tac5212_audio_shield_adaptor.kicad_sch) | [PCB](https://kicanvas.org/?github=https://github.com/t-dsp/t-dsp_tac5212_audio_shield_adaptor/blob/main/t-dsp_tac5212_audio_shield_adaptor.kicad_pcb)

## Project Files

| Directory | Contents |
|-----------|----------|
| `/3d_models/` | 3D models for PCB components |
| `/lib_fp/` | Custom KiCad footprint libraries |
| `/lib_sch/` | Custom KiCad schematic symbol libraries |
| `/manufacturing/` | CI-generated manufacturing outputs (gerbers, BOM, pick & place, PDFs) |
| `/pages/` | [3D Render Gallery](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/gallery.html), [Interactive BOM](https://t-dsp.github.io/t-dsp_tac5212_audio_shield_adaptor/ibom.html) |

## Manufacturing

Manufacturing files are generated automatically by [KiBot](https://github.com/INTI-CMNB/KiBot) on every push to `main` and on tagged releases via GitHub Actions.

To order:
1. Download the latest `t-dsp_tac5212_audio_shield_adaptor-manufacturing-vX.X.X.zip` from [Releases](https://github.com/t-dsp/t-dsp_tac5212_audio_shield_adaptor/releases)
2. Upload gerbers and drill files to your PCB fab (JLCPCB, PCBWay, etc.)
3. Use the BOM and CPL files for JLCPCB SMT assembly

## About T-DSP

T-DSP is an open modular audio platform built around the Teensy microcontroller and the [Teensy Audio Library](https://www.pjrc.com/teensy/td_libs_Audio.html). This adaptor is the simplest entry point — a small carrier that turns a Teensy 4.1 and a TAC5212 module into a working audio shield.

For a full desktop audio development platform with ESP32 UI, MIDI I/O, S/PDIF, RCA I/O, and multi-module TDM expansion, see the [T-DSP Desktop Pro](https://github.com/t-dsp/t-dsp_desktop_pro).

Learn more at [t-dsp.com](https://t-dsp.com).

## Status

Active development. If you build one, please open an issue or reach out.

## Contact

For consulting, custom audio hardware design, or commercial licensing, reach out via [LinkedIn](https://linkedin.com/in/jayshoe).

## License

[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Free to share and adapt for non-commercial purposes with attribution and same license on derivatives.
