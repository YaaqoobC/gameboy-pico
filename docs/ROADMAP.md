# Game Boy Emulator — Pico 2 W Roadmap

Embedded Game Boy emulator firmware in **C**, with **Pico SDK** and **FreeRTOS**, reusing the portable core from [gameboy-emulator](https://github.com/YaaqoobC/gameboy-emulator).

## Fundamental design
Only one FreeRTOS task owns/mutates emulated CPU, PPU, APU, bus, timers and cartridge state. All devices advance using the same *emulated* clock. Peripheral-host tasks may handle LCD transfers, physical buttons and host audio through bounded queues, task notifications or double buffers.

## Epic / milestone tracking
| Roadmap | Epic | Completion gate |
|---|---|---|
| M8 | #1 RP2350 Bring-up & Core Integration | UF2 and headless test ROM running on hardware |
| M9 | #2 Display, Input & Sound Hardware | On-device display, controls and audio |
| M10 | #3 FreeRTOS Port | Safe task ownership, deterministic core, jitter measurements |
| M11 | #4 Optimization & Storage | Sustained real-time speed and persistent save handling |
| M12 | #5 Standalone Console v1.0 | Documented, reproducible handheld prototype |

## Dependencies
- Begin M8 with a pinned revision of the tested desktop core, after desktop M7 release.
- M8 → M9 → M10 → M11 → M12 is the recommended delivery sequence.
- Hardware selection and pin-map can be explored independently before M8 completes.

## Definition of done
- Run release acceptance tests on an actual Pico 2 W.
- Measure emulator cycles, frame rate, frame transfer, RTOS stack usage and audio underruns.
- Document wiring, power budget, loading approach and reproduction steps.
- Never include copyrighted commercial ROM images.

## Related repository
[Game Boy desktop / reusable C core](https://github.com/YaaqoobC/gameboy-emulator).
