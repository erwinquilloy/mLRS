# mLRS v1.5.00 + MSP over the CRSF bridge (custom Tx build)

`tx-radiomaster-nomad-v1.5.00-msp-cbridge.bin`: RadioMaster Nomad Tx, mLRS v1.5 (release) plus
the one change on this branch (`tx, msp`: MSP over the crsf bridge, proposed upstream as
[olliw42/mLRS#560](https://github.com/olliw42/mLRS/pull/560)).

With **Tx Ser Port = cbridge** and **Rx Ser Link Mode = mspX**, radio Lua tools (OmniDeck's PARAMS
page, the OmniDeck Param Editor) can read and change INAV settings and download the INAV mission
over mLRS. ArduPilot over the bridge (MAVLink) works as before.

- Tx module only. Receivers stay on the official v1.5.00 release; the version is still v1.5.00,
  so they pair as before.
- Flashed and confirmed on a RadioMaster Nomad (2026-11-27) with a Matek receiver on official
  v1.5.00 and INAV: telemetry, INAV parameter editing and mission download.
- Flashing: the mLRS Web Flasher's custom-file option used the STM32 protocol and failed on the
  Nomad. What worked: build this branch and `pio run -e tx-radiomaster-nomad -t upload
  --upload-port COMx` over the Nomad's USB port. This .bin is the app image (offset 0x10000).
- Built with PlatformIO (espressif32 6.13.0) from this branch.
