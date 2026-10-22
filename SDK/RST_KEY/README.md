# RST_KEY demo

This example is copied from the RGB demo. It changes the STM32G474RE PG10/NRST
pin to a pull-up GPIO input named `RST_KEY`.

- Key released (high): RGB LED off.
- Key pressed (low): RGB LED on.

On the first boot, `RST_Key_EnableGPIO()` programs the `NRST_MODE` option byte
to GPIO-only mode and launches an option-byte reload. After that, the board's
RST button no longer resets the MCU; it is read as a normal active-low key.

To restore the hardware reset function, use STM32CubeProgrammer to change the
NRST option-byte mode back to reset input/output mode.
