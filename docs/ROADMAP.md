# Embedded — Outcome-based Delivery Roadmap

> **Epics** group work by subsystem; **stories** represent individual changes; **milestones** are demonstrable integration results. The original M1–M12 story prefixes are permanent backlog identifiers, **not** native GitHub milestones. Milestones below intentionally span epics. No dates are committed.

| Checkpoint | Demonstrable outcome | Required verification | Contributing epics |
|---|---|---|---|
| E1 | **Portable core executes on Pico 2 W** | Pinned desktop core compiles for RP2350, loads a licensed diagnostic ROM, executes headlessly, outputs serial test results. | #1 |
| E2 | **First game on physical display** | SPI display presents frames, hardware buttons control a compatible game, initial audio output confirmed. | #1, #2 |
| E3 | **Stable real-time FreeRTOS emulation** | One owner task advances virtual emulated time; display/input/audio tasks communicate safely; measured sustained frame rate and no major underruns. | #2, #3, #4 |
| E4 | **Standalone handheld v1.0** | Documented hardware assembly, repeatable ROM loading, durable saves, power and memory budget, performance testing and release firmware. | #4, #5 |

## Rules for milestone completion

1. Attach test logs, captured frames or on-device evidence to a tracking issue or release notes.
2. All critical acceptance tests must pass; any exceptions are explicitly documented.
3. An epic's stories can contribute to several checkpoints and an epic can stay open after a milestone completes.
4. This table is a **milestone specification** in documentation, not native GitHub Milestones; those require creation and issue assignment separately.

## Existing backlog

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
