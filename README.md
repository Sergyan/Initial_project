# Initial_project

Firmware base for the STM32F446RE NUCLEO board.

## Current application flow

1. CubeMX initializes the HAL, clock and GPIO peripherals.
2. `board_init()` initializes the NUCLEO LED on PA5 and the user button.
3. The application state machine reads the clock and processes the result.
4. The main loop enters `WFI` between events and timer ticks.

## Clock integration

`clock_query()` is a weak hook in `Core/Src/main.c`. The default implementation
returns the elapsed milliseconds from `HAL_GetTick()`. The `.ioc` does not yet
configure the STM32 RTC, so a board-specific RTC implementation can replace the
hook and return `CLOCK_STATUS_BUSY` while the clock is being initialized, then
`CLOCK_STATUS_READY` when the value is available.

## Project

Open `EWARM/Project.eww` with IAR Embedded Workbench for ARM. The CubeMX source
configuration is kept in `Initial_project.ioc`.
