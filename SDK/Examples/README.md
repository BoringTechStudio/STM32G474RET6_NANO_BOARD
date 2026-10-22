# STM32G474RET6 Examples

This directory contains the complete migration of the 94 examples from:

`STM32Cube_FW_G4_V1.6.3/Projects/NUCLEO-G474RE/Examples`

Each example is now a self-contained project at:

`Examples/<peripheral>/<example>/`

Every project includes its own:

- `Core/Inc` and `Core/Src` application source tree
- `Drivers` tree containing its required CMSIS, HAL, BSP, and DSP dependencies
- CubeMX `.ioc` file
- `MDK-ARM/*.uvprojx` Keil project

All Keil source and include paths resolve inside the corresponding example directory. The projects no longer rely on source files from the original STM32Cube firmware repository.

## CubeMX configuration

All migrated `.ioc` files are configured for `STM32G474RET6`, use `MDK-ARM V5.32` as the target toolchain, and generate application files under `Core/Src`. The official peripheral, clock, DMA, NVIC, and middleware settings are preserved so that each example can be opened and regenerated in STM32CubeMX independently.

## Validation

All 94 Keil projects have local file references that resolve within their own project directories. `GPIO/GPIO_Demo` was rebuilt after conversion with Keil MDK and completed with zero errors and zero warnings.

## Hardware adaptation

The MCU and LQFP64 package match the NUCLEO-G474RE examples. Examples that use only internal peripherals can be built and run without board-specific pin changes. Examples using LEDs, buttons, serial ports, two-board communication, timers, analog signals, or external clocks retain the original official pin assignments and require the corresponding signal to be connected on the custom board.

The existing board-specific examples remain at the parent level:

- `RGB`
- `RST_KEY`
- `GPIO_EXTI`
- `SPI_LCD_1.47inch`
- `SPI_LCD_2.0inch`
- `SPI_LCD_2.4inch`

Use these projects as the reference for the board's RGB pins (`PC0`, `PC1`, `PC2`), USART1 (`PA9`, `PA10`), 24 MHz HSE, and PG10 key wiring when adapting an official example to the custom board.

## Example count

The migration contains 94 independent examples in 25 peripheral categories: ADC, COMP, CORDIC, Cortex, CRC, DAC, DMA, FLASH, FMAC, GPIO, HAL, HRTIM, I2C, IWDG, LPTIM, OPAMP, PWR, RCC, RNG, RTC, SPI, TIM, UART, USART, and WWDG.

`../tools/MakeExamplesStandalone.ps1` is the idempotent migration utility used to localize the project trees. It is only needed when repeating the migration from the STM32Cube firmware package; the completed example projects do not require that package for their source files.

## Multi-board ports

The same example set has been ported to several STM32G4 boards. Each board keeps its own
self-contained `Examples/` tree, selected by a board macro in the Keil/CubeMX project defines.

| Board folder | Macro | MCU (package) | RGB LED | Examples | Build status |
|---|---|---|---|---|---|
| `STM32G474RET6` | `G4R_NANO` | G474RET6 (LQFP64) | PC0/PC1/PC2 | 94 | source tree |
| `STM32G474VET6` | `G4V_MINI` | G474VET6 (LQFP100) | PC0/PC1/PC2 | 94 | migrated |
| `STM32G474CBT6` | `G4C_NANO` | G474CBT6 (LQFP48, 128 KB flash) | PA0/PA1/PA2 | 94 | 94/94, 0 err / 0 warn |
| `STM32G491VET6` | `G4V_MINI` | G491VET6 (LQFP100) | PC0/PC1/PC2 | 88 | 88/88, 0 err / 0 warn |
| `STM32G431CBT6` | `G4C_NANO` | G431CBT6 (LQFP48, 128 KB flash / 32 KB SRAM) | PA0/PA1/PA2 | 88 | 88/88, 0 err / 0 warn |
| `STM32G431RBT6` | `G4R_NANO` | G431RBT6 (LQFP64, 128 KB flash) | PC0/PC1/PC2 | 88 | 88/88, 0 err / 0 warn |

Board macro / IO mapping:

- `G4R_NANO` — G474RET6 and G431RBT6 (LQFP64): RGB LED PC0/PC1/PC2, keys PG10/PB8, USART1 PA9/PA10.
- `G4V_MINI` — G474VET6 and G491VET6 (LQFP100): RGB LED PC0/PC1/PC2, keys PG10/PB8, USART1 PA9/PA10.
- `G4C_NANO` — G431CBT6 and G474CBT6 (LQFP48): RGB LED PA0/PA1/PA2, keys PG10/PB8, USART1 PA9/PA10.

Notes:

- `G491VET6` and `G431CBT6` have no HRTIM and single-bank flash, so the 4 HRTIM examples and
  `FLASH/FLASH_DualBoot` + `FLASH/FLASH_FastProgram` (6 G474-only examples) are excluded there.
- `G474CBT6` is 128 KB flash (single bank) and LQFP48. All 94 examples still compile, but the
  dual-bank FLASH examples and most HRTIM outputs are not usable at runtime on this package.

Migration / build utilities (in `../tools/`):

- `MigrateRet6ToVet6.ps1` — G474RET6 → G474VET6
- `MigrateVet6ToG491.ps1` — G474VET6 → G491VET6
- `MigrateRet6ToG431.ps1` — G474RET6 → G431CBT6
- `MigrateRet6ToG474CB.ps1` — G474RET6 → G474CBT6
- `SyncBsp.ps1` — propagates the shared BORING BSP to every example copy
- `BuildAllExamples.ps1` — batch-builds every example for a board