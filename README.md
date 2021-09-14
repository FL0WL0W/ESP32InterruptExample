# Interrupt Example

registers an interrupt on pin 35 and outputs a short pulse on pin 5

Also starts a FreeRTOS task to blink an LED

This example shows bad interrupt jitter.
 # Potential Causes of jitter
 - Higher priority interrupts taking prioirty over gpio interrupt. (nothing apparent on first inspection of all registered interrupts)
 - FreeRTOS has a lot of critical sections that disable interrupts, this potentially causes the interrupts to be delayed
 # Potential Fixes
 - let FreeRTOS run on core 0 and all realtime code run on core 1. No support from Espressif on this.
 - Remove all offending RTOS stuff (systick, context switching, watchdog? etc.) from application core
