# Alchitry Cu + Io Demo

A Lucid HDL demo project for the [Alchitry Cu](https://alchitry.com/boards/cu/) FPGA
board with an [Alchitry Io](https://alchitry.com/boards/io/) element board plugged in.

## What it does

A single lit LED bounces back and forth across the Io board's 24 LEDs
(Knight Rider style):

- **Button 0** speeds the chase up.
- **Button 1** slows the chase down.
- **Button 2** reverses its direction.
- The current speed level (0-7) is shown on the first 7-segment digit.
- The onboard Cu LEDs mirror the raw button states.

## Opening the project

1. Install [Alchitry Labs V2](https://alchitry.com/alchitry-labs/).
2. In Alchitry Labs, choose **File > Open Project** and select
   `Alchitry Cu IO Demo.alp` in this repository.
3. Plug the Alchitry Io board into the Alchitry Cu board, then connect the Cu
   to your computer over USB.
4. Click **Build & Load** (or **Build > Program**) to synthesize the design
   and load it onto the FPGA.

## Project layout

```
Alchitry Cu IO Demo.alp   - project file (board: Alchitry Cu)
source/alchitry_top.luc   - top-level module: chase logic, button handling, display
source/seven_seg.luc      - binary-to-7-segment decoder for the speed digit
```

The project also references a few standard components that ship with
Alchitry Labs itself (`reset_conditioner`, `button_conditioner`, `decoder`,
`edge_detector`, and the `alchitry`/`io_v1` pin constraint files), so no extra
setup is required beyond having Alchitry Labs V2 installed.

## Customizing

- Change the `idx = 26 - speed.q` line in `source/alchitry_top.luc` to shift
  the overall speed range faster or slower.
- Widen `chase_bus` handling to light more than one LED at once for a
  "comet tail" effect.
- Wire up `io_button[3]`/`io_button[4]` (currently unused) for more controls,
  like a reset-to-center button.
