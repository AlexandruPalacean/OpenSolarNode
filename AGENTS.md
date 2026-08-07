# OpenSolarNode collaboration rules

These instructions apply to the entire repository.

## Architecture authority

The browser ChatGPT design/review workflow owns hardware architecture, component selection, calculations, schematic and PCB review, EMC, and RF decisions.

Codex may:

- implement approved decisions in KiCad;
- organize and refactor project files without changing electrical intent;
- create and maintain symbol and footprint libraries;
- maintain repository structure, documentation, and Git history;
- identify conflicts, risks, and missing information.

Codex must not independently change these frozen architectural areas:

- MPPT charger architecture or BQ24650 selection;
- INA228 monitoring architecture;
- ESP32-C3-MINI-1 / ESP32-H2-MINI-1 variants;
- supply topology and rail architecture;
- hardware PowerPath / backup topology;
- connector strategy or selected connector requirements;
- PCB construction and design philosophy.

Any major hardware decision or required departure from an approved decision must receive architectural validation before implementation. If implementation exposes a conflict, Codex must stop that affected change, document the issue in `HANDOFF-CODEX.md`, and request review instead of silently choosing an alternative.

## Current implementation sequence

Implement only after reviewed design decisions are handed off, in this order unless the architecture owner changes it:

1. Power stage: solar protection, fuse, reverse protection, BQ24650, battery, PowerPath, 12 V bus, 5 V buck, and 3.3 V rail.
2. ESP subsystem.
3. INA228 monitoring.
4. Digital I/O.
5. PCB layout.
