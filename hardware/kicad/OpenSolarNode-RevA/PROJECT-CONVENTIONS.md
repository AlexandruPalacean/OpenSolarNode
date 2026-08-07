# OpenSolarNode RevA KiCad conventions

- Toolchain: stable KiCad 10 (created and validated with 10.0.5).
- Project: `OpenSolarNode`; revision: `RevA`.
- Sheet size: A4 throughout; page numbers follow hierarchy order.
- Schematic connection grid: 50 mil.
- Default schematic text and labels: 50 mil with consistent KiCad defaults.
- Annotation starts at 1 and uses conventional prefixes: `U`, `R`, `C`, `L`, `D`, `Q`, `F`, `TP`, `J`, `K`, and `SW`.
- ERC exclusions: none. Legitimate findings must be resolved, not suppressed.
- Net classes: only KiCad's neutral `Default` class exists until electrical and PCB constraints are approved.
- License field: `TBD - requires project owner approval`; no license has been selected by Codex.
- Official KiCad symbols and footprints are preferred. Custom libraries remain empty until required by an approved implementation handoff.
