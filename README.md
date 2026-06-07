# Mediapad

a custom USB media controller I designed from scratch. three mechanical switches for playback, a rotary encoder for volume, and a little OLED screen I'm still adding. built as part of [Hack Club's Hackpad program](https://stardance.hackclub.com/missions/hackpad/guide).

> **status:** PCB design done, case WIP in Onshape, OLED coming next

---

## what it does

plug it in over USB-C and it shows up as a keyboard. no drivers, no software. just works.

| control | action |
|---|---|
| key 1 | play / pause |
| key 2 | previous track |
| key 3 | next track |
| encoder (rotate) | volume up / down |
| encoder (click) | mute |

---

## what's in it

| part | details |
|---|---|
| Seeed Studio XIAO RP2040 | microcontroller, USB-C, runs CircuitPython |
| EC11 rotary encoder | 20 detents, built-in click |
| 3x MX-compatible switches | any MX switch works |
| SSD1306 OLED | 128x32, I2C — footprint on board, wiring it up next |
| custom PCB | 2-layer, designed in KiCad, ordered from JLCPCB |
| 3D printed case | designed in Onshape, v2 redesign in progress |

---

## firmware

running [KMK](https://github.com/KMKfw/kmk_firmware), which is keyboard firmware written in CircuitPython. the XIAO mounts as a USB drive when you plug it in, so changing keybindings is just editing `code.py` and saving. no reflashing needed.

```python
from kmk.kmk_keyboard import KMKKeyboard
from kmk.keys import KC
from kmk.modules.encoder import EncoderHandler

keyboard = KMKKeyboard()
encoder_handler = EncoderHandler()

keyboard.keymap = [[
    KC.MPLY,  # play / pause
    KC.MPRV,  # previous track
    KC.MNXT,  # next track
]]

encoder_handler.map = [[(KC.VOLU, KC.VOLD, KC.MUTE)]]
```

---

## pcb

designed in KiCad 8. two-layer board, all traces routed by hand. schematic and layout files are in the `Mediapad/` folder.

to open it: install KiCad 8, then open `Mediapad/Mediapad.kicad_pro`.

---

## current progress

- [x] PCB schematic + layout (KiCad)
- [ ] case redesign (Onshape v2, the v1 is literally just a box)
- [ ] add OLED to PCB revision
- [ ] solder and test the full build
- [ ] get the OLED showing track info

---

## project page

[mediapad.vercel.app](https://mediapad.vercel.app)

---

built by [arya vora](https://github.com/AryaVora621) as part of [Hack Club Hackpad](https://stardance.hackclub.com/missions/hackpad/guide)
