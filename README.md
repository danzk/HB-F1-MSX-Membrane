# MSX Hit Bit Keyboard Membranes

Replacement keyboard membranes for Sony MSX "Hit Bit" home computers.

This repository hosts one design per machine, each in its own directory, all
sharing a common KiCad footprint library.

## Variants

| Machine | Directory | Notes |
| --- | --- | --- |
| Sony HB-F1 | [hb-f1/](hb-f1/) | Original design |
| Sony HB-F1II | [hb-f1ii/](hb-f1ii/) | Reworked PCB with revised switch footprint |

Each variant directory contains its own `pcb/` (KiCad project), `gerber/`
(fabrication outputs) and `mech/` (mechanical drawings), plus a `doc/`
folder for any variant-specific images. Reference material and renders
shared across variants live in the top-level [doc/](doc/) directory.

## Shared footprint library

Both projects reference the same footprints in
[footprints/Sony_Hit_Bit.pretty/](footprints/Sony_Hit_Bit.pretty/) via each
project's `fp-lib-table` (`${KIPRJMOD}/../../footprints/Sony_Hit_Bit.pretty`).

## Manufacturing

See [doc/MANUFACTURING.md](doc/MANUFACTURING.md) for how to order the membrane
from JLCPCB as a 2-layer flexible PCB (stackup, order settings and stiffener
details).

## Other projects

Related keyboard membrane / replacement projects for other Sony MSX models:

- [RBSC/KeyboardMembrane_SonyF1Xx](https://github.com/RBSC/KeyboardMembrane_SonyF1Xx)
  — replacement membrane PCB and gerbers for the Sony HB-F1XV, HB-F1XD and
  HB-F1XDJ.
- [S0urceror/HB-F1XD-keyboard](https://github.com/S0urceror/HB-F1XD-keyboard)
  — KiCad PCB replacement for the Sony HB-F1XD MSX2 keyboard membrane.

## Tooling

2D mechanical drawings were performed with QCAD v3.31.2.7 — https://www.qcad.org/

Electronics were designed with KiCad v8.0.7 — https://www.kicad.org/

The PCB layout uses the font IBM Plex Sans — https://www.ibm.com/plex/

## Licence

Copyright Alexander Knapik 2025.

This source describes Open Hardware and is licensed under the CERN-OHL-W v2 or later.

You may redistribute and modify this documentation and make products
using it under the terms of the CERN-OHL-W v2 (https://cern.ch/cern-ohl).
This documentation is distributed WITHOUT ANY EXPRESS OR IMPLIED
WARRANTY, INCLUDING OF MERCHANTABILITY, SATISFACTORY QUALITY
AND FITNESS FOR A PARTICULAR PURPOSE. Please see the CERN-OHL-W v2
for applicable conditions.
