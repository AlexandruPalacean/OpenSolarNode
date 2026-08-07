# OpenSolarNode Handoff

## Context

This repository is being designed collaboratively. The browser ChatGPT instance is leading architecture/design review; the VS Code Codex instance should handle local repository implementation, file creation, KiCad scaffolding, and Git operations.

GitHub repository:
https://github.com/AlexandruPalacean/OpenSolarNode

Local workspace expected by Codex:
`E:\OpenSolarNode`

## Frozen RevA requirements

### Power
- Solar input for nominal 18 V panel, target up to ~100 W.
- AGM 12 V battery initially; SLA/GEL compatibility desired.
- Solar charger IC: **TI BQ24650**.
- Main system bus: **12 V / 5 A continuous, 8 A peak**.
- Backup input: external **12 V AC-DC supply**, automatically selected by hardware power-path logic.
- Auxiliary output: **5 V / 3 A**.
- Critical charging, protection, and backup behavior must work with the MCU absent or crashed.

### Monitoring
Use **3 x INA228**:
1. Solar input power/current/voltage.
2. Battery bidirectional current/voltage/power.
3. Load/system output current/voltage/power.

Battery current sign convention to be decided in firmware, but hardware must support bidirectional measurement.

### MCU variants
Common PCB if practical, with alternative population:
- **ESP32-C3-MINI-1** for Wi-Fi / ESPHome native API.
- **ESP32-H2-MINI-1** for Zigbee / ESPHome Zigbee.

### User I/O
- 2 x opto-isolated digital inputs, nominally 12 V control; wider 6-30 VDC compatibility is desirable if it does not complicate/cost much.
- 2 x digital output channels, each supporting alternative population:
  - mechanical relay, or
  - MOSFET/high-side solid-state output.
- RESET button.
- BOOT button.
- USER button, usable for Zigbee pairing / factory reset / identify.
- USB-C programming connector, specifically chosen to be easy to hand solder (hybrid THT/SMT preferred).

### LEDs
Status LEDs for main rails / source states are desired, but must be disable-able to reduce idle consumption.
Use jumper(s), preferably:
- one jumper for nonessential status LEDs,
- optional separate POWER LED jumper if useful.

### Protection / serviceability
- **5x20 mm THT fuse holders**, not automotive or SMD fuses.
- Battery connected through screw terminal.
- Screw terminals generally preferred for field wiring.
- PCB mounting holes: M3.

### PCB / assembly rules
- 4-layer PCB.
- Hand-assembly friendly by a hobbyist with soldering iron + hot air.
- Passives minimum **0603**, **0805 preferred**.
- No 0402/0201.
- No BGA/CSP/WLCSP.
- Avoid QFN unless there is no reasonable alternative.
- No via-in-pad, blind/buried vias, or microvias.
- Prefer THT or large-pitch connectors and serviceable components.
- Components should be active/current and reasonably available from Mouser, DigiKey, and/or TME.

## Architecture decisions already accepted

- MPPT/solar charger: BQ24650.
- 4-layer PCB.
- ESP32-C3-MINI-1 / ESP32-H2-MINI-1 variants.
- Three INA228 monitors.
- Hardware-only critical power path.
- 5x20 mm THT fuses.
- Screw-terminal battery connection.
- Disable-able status LEDs.

## Immediate tasks for Codex

1. Initialize Git repository in `E:\OpenSolarNode` if not already initialized.
2. Set remote to `https://github.com/AlexandruPalacean/OpenSolarNode`.
3. Create the repository folder structure matching this handoff package.
4. Commit this initial scaffold.
5. Create an empty KiCad RevA project under `hardware/kicad/OpenSolarNode-RevA/` using the locally installed KiCad version.
6. Do **not** invent the detailed schematic yet.
7. Prepare KiCad hierarchical sheets/placeholders for:
   - Solar Charger
   - Battery / Monitoring
   - Power Path / Backup
   - 12V / 5V / 3V3 Power
   - MCU / USB
   - Digital Inputs
   - Digital Outputs
   - Connectors / Protection
8. Leave a short local note with exact KiCad version and any created filenames.
9. Commit and push the scaffold to GitHub.

## Next design work expected from browser ChatGPT

The browser instance will continue with concrete component selection and calculations for the power block, starting with:
- BQ24650 charger implementation and setpoints.
- Power-path controller/topology for primary solar/battery source + 12 V backup.
- 5 V / 3 A converter.
- 3.3 V MCU rail.
- protection parts, fuses, TVS, MOSFETs.
- exact orderable parts from Mouser/DigiKey/TME.

Codex should avoid independently changing frozen architectural decisions unless it identifies a hard KiCad/tooling conflict; in that case record the issue in `HANDOFF-CODEX.md` rather than silently changing the design.
