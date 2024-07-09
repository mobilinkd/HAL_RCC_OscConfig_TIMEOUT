# HAL_RCC_OscConfig TIMEOUT

This documents a defect in the HAL_RCC_OscConfig() function since 1.17.2.

This is meant to run on an STM32L432KC Nucleo32 board with SB17 shorted so that
HSE is available via the MCO from the programmer.

Running the executable that is generated will result in the Nucleo blinking
at 1Hz for 5 seconds after startup, then entering an error handler where it
blinks at 5Hz. In an ideal world, the board would blink at a constant 1Hz
rate.

The AL_RCC_OscConfig() will exit with a TIMEOUT because it cannot shut down
the PLL because the order of operations is incorrect. The PLL should be
disabled before any oscillators are disabled.
