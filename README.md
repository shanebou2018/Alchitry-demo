# Alchitry Cu + Io Demo

A Lucid HDL demo project for the [Alchitry Cu](https://alchitry.com/boards/cu/) FPGA
board with an [Alchitry Io](https://alchitry.com/boards/io/) element board plugged in.

## What it does

- The 5 buttons on the Io board are wired straight to the 5 lower bits of the
  Cu's onboard LEDs.
- The 24 DIP switches on the Io board are wired straight to the 24 LEDs on the
  Io board (organized as 3 groups of 8).
- The 4 seven-segment displays on the Io board show a free-running decimal
  counter (0000-9999) that increments about once a second, demonstrating a
  multiplexed 7-segment driver and a chained BCD counter.
- The USB serial RX/TX pins are looped back together.

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
Alchitry Cu IO Demo.alp        - project file (board: Alchitry Cu)
source/alchitry_top.luc        - top-level module, wires everything together
source/multi_seven_seg.luc     - drives the 4-digit multiplexed 7-segment display
source/seven_seg.luc           - binary-to-7-segment decoder for a single digit
source/multi_decimal_counter.luc - chains multiple decimal_counter digits together
source/decimal_counter.luc     - single-digit (0-9) counter with overflow
```

The project also references a few standard components that ship with
Alchitry Labs itself (`reset_conditioner`, `counter`, `decoder`,
`edge_detector`, and the `alchitry`/`io_v1` pin constraint files), so no extra
setup is required beyond having Alchitry Labs V2 installed.

## Customizing

Try changing what drives `io_led`/`led` in `source/alchitry_top.luc`, or
adjust the `DIV` value passed to `counter ctr` to speed up or slow down the
seven-segment counter.
