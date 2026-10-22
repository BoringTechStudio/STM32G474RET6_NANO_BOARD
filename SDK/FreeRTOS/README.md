# FreeRTOS Applications (STM32G474RET6 / G4R_NANO)

These 9 applications are ported from `STM32Cube_FW_G4_V1.6.3/Projects/STM32G474E-EVAL/Applications/FreeRTOS`
to the G4R_NANO board (STM32G474RET6, LQFP64).

Each project is a standalone AC6 (V6.21) Keil MDK project with local `Drivers`
(CMSIS + HAL + `stm32g4xx_boring` BSP) and `Middlewares` (FreeRTOS V10.2.1, GCC/ARM_CM4F port).

## Applications

| App | Summary |
| --- | --- |
| FreeRTOS_ThreadCreation | Create two threads that blink LEDs and suspend/resume each other |
| FreeRTOS_Mail | Exchange data between threads via mail queue |
| FreeRTOS_Queues | Exchange data between threads via queue |
| FreeRTOS_Semaphore | Synchronize two threads with a binary semaphore |
| FreeRTOS_SemaphoreFromISR | Release a semaphore from the EXTI button ISR |
| FreeRTOS_Signal | Signal a thread from another thread |
| FreeRTOS_SignalFromISR | Signal a thread from the EXTI button ISR |
| FreeRTOS_Mutexes | Protect a shared resource with mutexes |
| FreeRTOS_Timers | One-shot and periodic software timers |

## LED mapping (E-EVAL -> G4R_NANO)

| E-EVAL | G4R_NANO |
| --- | --- |
| LED1 (green) | LED_GREEN (PC1) |
| LED2 (MFX) | LED_BLUE (PC2) |
| LED3 (red) | LED_RED (PC0) |
| LED4 (MFX) | LED_RED (PC0) |
| BUTTON_USER (PC13) | BUTTON_RST (PG10) |

## Build

Open `MDK-ARM/*.uvprojx` in Keil MDK and build (AC6 V6.21, DFP 2.2.0).
All 9 projects compile with 0 errors / 0 warnings.
