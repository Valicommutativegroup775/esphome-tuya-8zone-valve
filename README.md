# 8-Zone Tuya Irrigation Controller → ESPHome

*[Versión en español](README.es.md)*

## The story

I received an **8-zone smart irrigation controller** from AliExpress. A generic Chinese device with WiFi, controllable via the Tuya Smart / Smart Life app. The PCB model is **TY-W-8L-AC-DZAK** and it uses a **Beken BK7231N** SoC (CBU module).

The first thing I did was integrate it into Home Assistant via **localtuya** ([guide and tools here](https://github.com/gnacho/tuya-8zone-valve-3.5)). It worked, but with limitations: it depended on Tuya cloud for some zones, polling gave errors every 60 seconds, and I didn't have fine control over the hardware.

So I decided to go further: **flash ESPHome** and have total, local control without dependency on Chinese servers.

## The hardware

- **SoC**: Beken BK7231N (CBU module) — NOT an ESP32
- **PCB**: TY-W-8L-AC-DZAK rev 24.9.19
- **Shift registers**: 2x 74HC595 in cascade (16 outputs)
  - First chip (bits 0-7): 8 BT134 triacs → Z1..Z8 terminals (irrigation valves)
  - Second chip (bits 8-15): 8 D1..D8 status LEDs
- **Confirmed shift register pins**:
  - P6 = data (SER)
  - P15 = clock (SRCLK)
  - P17 = latch (RCLK)
  - P8 = Output Enable (OE, active LOW)
- **Buzzer**: P14
- **WiFi LED**: P28
- **Power**: 24 VAC
- **Physical buttons**: SET, UP, DOWN (pins to be identified)

## The flashing

The BK7231N is flashed via UART with [ltchiptool](https://github.com/libretiny-eu/ltchiptool). The process:

1. Open the device and locate the UART pins (TX, RX, GND, 3.3V)
2. Put in download mode (bridge RST to GND during boot)
3. Power via 24VAC (the internal regulator generates 3.3V)
4. Flash with `ltchiptool flash`

Once flashed, updates are **OTA** (via WiFi, no cables).

## Current status

The ESPHome firmware works: WiFi connected, web UI accessible, Home Assistant API operational, OTA working. The 8 irrigation zones are controlled correctly via shift registers.

**In progress** (trial and error method, without being an electronic engineer):

- Identify the exact pins of the 3 physical buttons (SET, UP, DOWN)
- Verify the correct LED to zone mapping
- Adjust inverted logic where necessary

## Roadmap

The goal is to take full advantage of the [ESPHome Sprinkler component](https://esphome.io/components/sprinkler/) — scheduling, valve overlap, auto-advance, reverse watering, pump control, and more.

But first things first: **get the hardware fully working**. Before adding advanced features, we need to:

1. Identify the exact GPIO pins for the 3 physical buttons (SET, UP, DOWN)
2. Verify the correct LED-to-zone mapping
3. Confirm the inverted logic for triacs and LEDs
4. Get the buzzer working as feedback

Once the base is solid, the sprinkler component will give us a proper irrigation controller out of the box.

## Files

| File | Description |
|------|-------------|
| `irrigador-8z.yaml` | Main firmware with sprinkler (8 zones, adjustable durations) |
| `irrigador-8z-diag.yaml` | Diagnostic firmware (individual bits, pin sweep) |
| `secrets.yaml.example` | Secrets template (WiFi, API key, OTA password) |

## Requirements

- ESPHome 2026.5.3+
- LibreTiny framework (integrated in modern ESPHome)
- Home Assistant (optional, for integration)

## License

AGPL-3.0
