# GPIO_EXTI

Independent STM32CubeMX and Keil MDK example for `STM32G474RET6`.

## Behavior

On the first run, the firmware changes the `PG10/NRST` option byte to GPIO mode and resets the MCU. Each subsequent falling edge on `PG10` runs the `EXTI15_10` callback and toggles the RGB outputs together.

## Connections

| Signal | Pin | Configuration |
| --- | --- | --- |
| User key | PG10/NRST | Active-low input with internal pull-up |
| Red LED | PC0 | Push-pull output, active low |
| Green LED | PC1 | Push-pull output, active low |
| Blue LED | PC2 | Push-pull output, active low |
| USART1 TX | PA9 | 115200 baud serial output |
| USART1 RX | PA10 | 115200 baud serial input |

## Build and use

Open `MDK-ARM/STM32G474RET6.uvprojx` in Keil MDK, build, and program the target. The `.ioc` file contains the matching CubeMX configuration. After the option-byte reset, `PG10` is no longer a hardware reset pin and is used only as the key input.# RST_KEY demo

This example is copied from the RGB demo. It changes the STM32G474RE PG10/NRST
pin to a pull-up GPIO input named `RST_KEY`.

- Key released (high): RGB LED off.
- Key pressed (low): RGB LED on.

On the first boot, `RST_Key_EnableGPIO()` programs the `NRST_MODE` option byte
to GPIO-only mode and launches an option-byte reload. After that, the board's
RST button no longer resets the MCU; it is read as a normal active-low key.

To restore the hardware reset function, use STM32CubeProgrammer to change the
NRST option-byte mode back to reset input/output mode.
