# Manufacturing the Membrane at JLCPCB (Flexible PCB)

This guide explains how to order the Hit Bit keyboard membrane from
[JLCPCB](https://jlcpcb.com/) as a **2-layer Flexible PCB (FPC)**. It applies to
both variants — substitute the variant's `gerber/` folder accordingly:

| Variant | Gerber folder |
| --- | --- |
| Sony HB-F1 | [hb-f1/gerber/](../hb-f1/gerber/) |
| Sony HB-F1II | [hb-f1ii/gerber/](../hb-f1ii/gerber/) |

> **Note (HB-F1II):** this variant has not yet been verified on real hardware.
> See [hb-f1ii/README.md](../hb-f1ii/README.md) before ordering.

All values below are taken from the **Board Characteristics** and **Stiffener
Characteristics** tables and the layer stackup embedded in the KiCad PCB (the
`User.Comments` layer). They are reproduced here so they can be matched against
the JLCPCB order form.

---

## 1. Files to upload

JLCPCB accepts a single ZIP of the Gerber/drill set. Zip the contents of the
variant's `gerber/` folder. The required files are:

| File | Purpose |
| --- | --- |
| `pcb-F_Cu.gbr` | Top copper |
| `pcb-B_Cu.gbr` | Bottom copper |
| `pcb-F_Mask.gbr` | Top coverlay opening |
| `pcb-B_Mask.gbr` | Bottom coverlay opening |
| `pcb-F_Silkscreen.gbr` | Top legend (direct print) |
| `pcb-B_Silkscreen.gbr` | Bottom legend (direct print) |
| `pcb-Edge_Cuts.gbr` | Board outline **and internal cut-outs** |
| `pcb-PTH.drl` | Plated holes |
| `pcb-NPTH.drl` | Non-plated holes |
| `pcb-User_1.gbr` | **Stiffener outline** (65 × 15 mm PI stiffener) |
| `pcb-job.gbrjob` | Gerber job metadata (optional but helpful) |

You can omit the paste layers (`pcb-F_Paste.gbr`, `pcb-B_Paste.gbr`) and
`pcb-User_Comments.gbr` — there is no SMT assembly, and the comments layer is
documentation only.

> If you need to regenerate these, open the project in KiCad 10, then
> **File → Plot** (select the layers above, Gerber format) and
> **File → Fabrication Outputs → Drill Files** (Excellon, PTH/NPTH separated).

---

## 2. JLCPCB order configuration

Set **Base Material** to **`Flex`** first — the flex-specific fields (polyimide
thickness, coverlay, flex copper weight, stiffener) only appear after that.
Field labels and option strings below are quoted verbatim from the JLCPCB quote
form (<https://cart.jlcpcb.com/quote>); the right-hand column is the value
encoded in the PCB.

| JLCPCB field | Selection | Source |
| --- | --- | --- |
| Base Material | **`Flex`** | Polyimide stackup |
| Layers | **`2`** | Copper Layer Count |
| Dimensions (single piece) | **350 × 170 mm** | Board overall dimensions |
| Different Design | `1` | — |
| Delivery Format | `Single PCB` | — |
| PCB Thickness (flex) | **≈ 0.1 mm** (nearest flex option) | Board Thickness 0.1034 mm |
| Coverlay colour | **`Yellow`** | F.Mask / B.Mask colour |
| Outer Copper Weight | **`1/3 oz`** (≈12 µm; lightest flex option) | "12 µm finish copper (1/3 Oz.)" |
| Surface Finish | **`ENIG`** | Copper Finish |
| Gold Fingers | `No` | see note below |
| Castellated Holes | `No` | Castellated pads |
| Stiffener | **`Polyimide`** — see section 3 | Stiffener required |
| EMI Shielding Film | (leave off) | — |

> The `PCB Thickness` and `Outer Copper Weight` option lists change once
> `Flex` is selected (the form's default lists are for FR-4). Pick the flex
> value closest to the spec — ~0.1 mm thickness and the lightest copper
> (1/3 oz / 12 µm).

For reference, the design rules are well inside JLCPCB's FPC limits:
min track/spacing **0.25 mm / 0.25 mm**, min hole **0.5 mm**, and vias are
tented.

**Gold Fingers:** the design marks the cable tail as an edge connector, but the
exposed contacts there are simply coverlay openings plated by the **ENIG**
finish — leave `Gold Fingers` set to `No` (that option adds bevelled, thick
gold edge fingers, which the FFC/ZIF connector does not need).

---

## 3. Stiffener

The tail that inserts into the keyboard connector needs a stiffener so it has
enough thickness and rigidity for the connector.

| Property | Value |
| --- | --- |
| Required | Yes |
| Material | **Polyimide (PI)** |
| Stiffener thickness | **0.225 mm** (use the nearest available, e.g. 0.20–0.25 mm) |
| Overall size | 65 × 15 mm |
| Side | **Bottom** (B.Stiffener) — copper on stiffener side: No |
| Total thickness at tail | ≈ 0.289 mm (0.1034 mm flex + stiffener) |
| Gerber layer defining region | **`User.1`** (`pcb-User_1.gbr`) |

When ordering, set **`Stiffener`** to **`Polyimide`** (the other options are
`Without`, `FR4`, `Stainless Steel` and `3M Tape`). In the order remarks,
instruct JLCPCB that the stiffener location/outline is defined by the `User.1`
gerber layer (`pcb-User_1.gbr`) and goes on the bottom side. The target total
thickness at the contact tail is ~0.3 mm to suit the MSX keyboard FFC connector.

---

## 4. Layer stackup (reference)

| # | Layer | Type | Material | Thickness | Colour |
| --- | --- | --- | --- | --- | --- |
| 1 | F.Silkscreen | Top Silk Screen | Direct Printing | — | White |
| 2 | F.Paste | Top Solder Paste | — | — | — |
| 3 | F.Mask | Top Solder Mask (coverlay) | Coverlay + Adhesive | 0.0275 mm | Yellow |
| 4 | F.Cu | Copper | — | 0.012 mm (1/3 oz) | — |
| 5 | Dielectric 1 | Core | Polyimide | 0.025 mm | — |
| 6 | B.Cu | Copper | — | 0.012 mm (1/3 oz) | — |
| 7 | B.Mask | Bottom Solder Mask (coverlay) | Coverlay + Adhesive | 0.0275 mm | Yellow |
| 8 | B.Paste | Bottom Solder Paste | — | — | — |
| 9 | B.Silkscreen | Bottom Silk Screen | Direct Printing | — | White |
| 10 | B.Stiffener | Bottom Stiffener | Polyimide | 0.225 mm | — |

Base flex thickness (layers 3–7): **≈ 0.1034 mm**.

---

## 5. Things to check before paying

- **Board size.** The 350 × 170 mm HB-F1 board has already been manufactured at
  JLCPCB, so the size is within their single-piece FPC limit. The HB-F1II board
  shares the same outline dimensions.
- **Cut-outs.** The design contains internal cut-outs ("Cut-out in design:
  Yes"); confirm they are read from `pcb-Edge_Cuts.gbr` in JLCPCB's Gerber
  viewer.
- **Stiffener placement.** Verify in the Gerber viewer that the stiffener
  region (`User.1`) lands on the connector tail, on the bottom side.
- **Coverlay openings.** Check that the contact fingers and any test points are
  exposed (coverlay opened) and everything else is covered.
- If anything is ambiguous, raise it in the JLCPCB order remarks or via their
  review chat before production.
