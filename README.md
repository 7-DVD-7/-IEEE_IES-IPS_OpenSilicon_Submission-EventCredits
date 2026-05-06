![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/test/badge.svg) ![](../../workflows/fpga/badge.svg)

# TinyTapeout: IEEE OpenSilicon Project Credits

A VGA-based credits screen module designed for the TinyTapeout platform. This module displays project contributors, special thanks, and inspirational quotes on a 640x480 VGA display.

## Overview

This hardware module implements a complete VGA controller and character generator. It uses a grid-based tilemap system to render text onto a display without the need for external memory or a microcontroller. The design is implemented in Verilog and is optimized for the TinyTapeout/OpenSilicon submission.

## Features

- **Standard VGA Output**: Generates timing for 640x480 @ 60Hz resolution.
- **Custom Font Engine**: A built-in Font ROM supporting uppercase, lowercase, and punctuation.
- **40x30 Grid System**: Organizes the screen into a tilemap for easy text placement.
- **Dynamic Color Schemes**: Selectable color profiles via input pins.
- **Zero External Dependencies**: All logic and "video RAM" (tilemap) are synthesized directly into the hardware.

## How it Works

### 1. VGA Timing
The module uses a 10-bit horizontal (`h_cnt`) and vertical (`v_cnt`) counter system to generate standard synchronization signals (`hsync` and `vsync`).

### 2. Grid & Tilemap
The screen is divided into 16x16 pixel blocks (downsampled for the character grid). The `row` and `col` signals determine which character from the hardcoded "Tilemap" case statement should be displayed at any given coordinate.

### 3. Font ROM
The `font_row_data` block contains bitmapped representations of characters. When a specific character is selected by the tilemap, the ROM outputs the 8-bit pixel pattern for the current scanline.

### 4. Color Logic
The module supports four selectable color modes via the `ui_in[1:0]` pins:
- `00`: Matrix Green
- `01`: Deep Blue
- `10`: Sunset Orange
- `11`: Classic White

A subtle scanline effect is applied to the colors using the least significant bit of the vertical counter (`v_cnt[0]`).

## Pinout Mapping

| Pin | Function | Description |
|-----|----------|-------------|
| `ui_in[1:0]` | Color Select | Switches between Green, Blue, Orange, and White themes. |
| `uo_out[7]` | HSync | VGA Horizontal Sync |
| `uo_out[3]` | VSync | VGA Vertical Sync |
| `uo_out[6,2]` | Blue [0,1] | 2-bit Blue Channel |
| `uo_out[5,1]` | Green [0,1] | 2-bit Green Channel |
| `uo_out[4,0]` | Red [0,1] | 2-bit Red Channel |

## Credits Displayed

The project features the following contributors and messages:
- **Project Contributors**: Chico Andre Olaguer, Raphael Garcia, Fred Daniel Ignacio, Kyle Patrick Galang, Vito Leon Gamboa, Charles Vincent Dulay, Sofia Nadine Tababa, Joaquin Gabriel Rosario.
- **Project Lead**: Dr. Alexander Co Abad.
- **Special Thanks**: IEEE OpenSilicon, TinyTapeout.
- **Inspirational Quotes**: 
    - *"Do not go gentle into that good night"* - Dylan Thomas
    - *"Life is reason"* - Rocky, Project Hail Mary
    - *"Advancing technology for humanity"*
