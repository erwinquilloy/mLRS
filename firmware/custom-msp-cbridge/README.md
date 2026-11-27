# mLRS v1.5.00 + MSP over the CRSF bridge (custom Tx builds)

mLRS v1.5 (release) plus the one change on this branch (`tx, msp`: MSP over the crsf bridge,
proposed upstream as [olliw42/mLRS#560](https://github.com/olliw42/mLRS/pull/560)).

| File | Tx module |
|---|---|
| `tx-radiomaster-nomad-v1.5.00-msp-cbridge.bin` | RadioMaster Nomad |
| `tx-matek-mr24-30-g431kb-v1.5.00-msp-cbridge.hex` | Matek MR24-30 (2.4 GHz) |

With **Tx Ser Port = cbridge** and **Rx Ser Link Mode = mspX**, radio Lua tools (OmniDeck's PARAMS
page, the OmniDeck Param Editor) can read and change INAV settings and download the INAV mission
over mLRS. ArduPilot over the bridge (MAVLink) works as before.

- Tx module only. Receivers stay on the official v1.5.00 release; the version is still v1.5.00,
  so they pair as before.
- Nomad: flashed and confirmed (2026-11-27) with a Matek receiver on official v1.5.00 and INAV:
  telemetry, INAV parameter editing and mission download.
- MR24-30: built from the same branch (2026-11-27), not yet flashed.

## Flashing

- **Nomad** (ESP32): in the mLRS Web Flasher, Local file, set the flash method to **ESPTool (UART)**.
  The default (SystemBoot) uses the STM32 protocol and fails. Or build this branch and run
  `pio run -e tx-radiomaster-nomad -t upload --upload-port COMx`. The .bin is the app image
  (offset 0x10000).
- **MR24-30** (STM32G431): in the mLRS Web Flasher, Local file, flash method **USB (DFU)**, or
  STM32CubeProgrammer over DFU.

Built with PlatformIO (espressif32 6.13.0) for the Nomad and arm-none-eabi gcc 13.2.1
(`tools/run_make_firmwares.py -t tx-matek-mr24-30-g431kb`) for the MR24-30.
