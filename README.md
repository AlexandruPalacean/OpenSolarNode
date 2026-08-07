# OpenSolarNode

Open-source solar power and energy-management platform for ESPHome and Home Assistant.

Current phase: hardware architecture and component selection for RevA.

Core frozen requirements:
- 12 V AGM/SLA/GEL battery
- Solar charger based on TI BQ24650
- 12 V system bus, 5 A continuous / 8 A peak
- 5 V auxiliary output, 3 A
- Hardware power-path / backup input at 12 V
- 3 x INA228 for solar, battery, and load monitoring
- ESP32-C3-MINI-1 Wi-Fi variant
- ESP32-H2-MINI-1 Zigbee variant
- ESPHome / Home Assistant integration
- 2 opto-isolated digital inputs, nominal 12 V control (design target 6-30 VDC acceptable)
- 2 configurable digital outputs with alternative relay or MOSFET population
- USB-C for programming, hand-solder friendly connector
- RESET / BOOT / USER buttons
- Status LEDs with jumpers to disable LED consumption
- 5x20 mm THT fuse holders
- Battery connection via screw terminal
- 4-layer PCB
- Hand-assembly friendly: passives >=0603, 0805 preferred; no BGA/CSP/WLCSP; avoid QFN unless unavoidable
- Components must be reasonably available from Mouser, DigiKey, or TME

See HANDOFF.md for the current implementation task list.
