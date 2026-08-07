# Codex implementation status

## HANDOFF #001 - KiCad 10 hierarchy

Status: completed on 2026-08-07 with stable KiCad 10.0.5.

### Completed

- Created `hardware/kicad/OpenSolarNode-RevA/OpenSolarNode.kicad_pro` and `OpenSolarNode.kicad_sch`.
- Created top-level sheets `01_Power`, `02_MCU`, `03_Measurements`, `04_IO`, and `05_Connectors`.
- Created the seven approved empty subsheets under `01_Power`.
- Added graphical placeholders for `SOLAR`, `BATTERY`, `BACKUP`, `CAM1`, `CAM2`, `AUX12`, `AUX5`, and `USB-C` without assigning symbols, pins, or nets.
- Added `hardware/symbols`, `hardware/footprints`, and `hardware/3d`; retained the existing libraries, production, and mechanical directories.
- Documented project settings and reference conventions in `PROJECT-CONVENTIONS.md`.
- Validated the complete hierarchy with KiCad netlist export.
- Ran KiCad ERC with no project exclusions: 0 errors and 0 warnings.

### Deviations

- Connector placeholders are graphical text only. Electrical connector symbols and pin/net assignments remain intentionally deferred.
- Only the neutral KiCad `Default` net class is configured. Electrical net-class constraints remain deferred until approved PCB/current/clearance rules are provided.

### Unresolved questions

- The hardware license was not specified. The title-block license field is `TBD - requires project owner approval` to avoid making a legal/project decision in Codex.

### Commit

- Implementation commit: `ce1ef5f` (`feat(kicad): create RevA hierarchical project structure`).

## HANDOFF #001A - hardware-adjustable charge current

Status: implemented as an unpopulated schematic reservation on 2026-08-07.

### Frozen requirement recorded

- RevA charge current is selected in hardware by `SW_CHG_CURRENT`, a 4-position DIP switch, and a programming resistor network.
- The charger must operate without the MCU; DIP contacts must never carry charge-path current.
- DIP hardware is THT/easy to hand solder; programming resistors are 0805 preferred and 0603 minimum.
- PCB/silkscreen space is reserved for `CHARGE CURRENT`, the future mapping table, accessible switch orientation, and a future RevB digital-potentiometer option.

### Schematic reservation completed

- Added a labeled graphical configuration block to `01B_BQ24650.kicad_sch`.
- Reserved the DIP-switch area, resistor-network area, `TP_CHG_PROGRAM` location, silkscreen intent, and RevB allowance.
- No electrical symbols, connections, resistor values, current mapping, or digital potentiometer were added.

### Deferred to DP-001 / HANDOFF #002

- Exact resistor values and programming topology.
- DIP truth table and treatment of unused combinations.
- Final programming-node test-point connection.
- Final silkscreen mapping.
