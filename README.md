# nn-app-camera-esp32p4module-sdio-imx708

nn camera firmware for the **Waveshare ESP32-P4-Module-DEV-KIT** (pre-3.0
silicon, rev v1.3) with the Raspberry Pi **Camera Module 3 Wide NoIR**
(IMX708) — deployed as cam1.

This repo is configuration + glue only:

- `sdkconfig.board` — everything that differs on this board: the pre-3.0
  silicon selects (`ESP32P4_SELECTS_REV_LESS_V3`, 200 MHz PSRAM), esp-hosted
  moved to PSRAM (internal RAM starves otherwise), and the wide-NoIR white
  balance trims.
- `main/` — registers nn-app-media's `app_main.c` verbatim; no app-code copy.
- Shared code arrives via submodules: `nn-app-media` (app + nn_* component
  wrappers + shared sdkconfig) and `nn-modules` (libraries + the esp_video/
  esp_cam_sensor/esp_ipa/esp_sccb_intf forks).

## Build

    git submodule update --init --recursive
    idf.py set-target esp32p4 build

Flash port is the board's own USB (CH343); the C6 radio flashes separately
(see nn-app-media-network).
