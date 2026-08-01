## Description

This project demonstrates **bare-metal programming** on the **STM32F401RE** microcontroller without using the STM32 HAL or LL libraries. It focuses on directly accessing memory-mapped peripheral registers through custom C structures with bit-fields, providing a clearer understanding of how the STM32 hardware operates at the register level.

The project enables the GPIOA peripheral clock, configures **PA5** as an output for the onboard LED, configures **PA0** as a digital input with an internal pull-down resistor, and continuously reads the input state to control the LED.

Rather than manipulating registers with hexadecimal masks and bitwise operations, this implementation maps hardware registers into C structures, making the code more readable and easier to understand while still remaining true bare-metal programming.

### Features

- Bare-metal STM32 programming
- Direct memory-mapped register access
- Custom register mapping using C structures and bit-fields
- GPIO peripheral clock configuration (RCC)
- GPIO input and output configuration
- Internal pull-down resistor configuration
- LED control using push-button input
- No STM32 HAL or external libraries used

### Hardware

- STM32 Nucleo-F401RE
- STM32F401RE Microcontroller
- Onboard User LED (PA5)
- User Push Button (PA0)

### Learning Objectives

This project helps understand:

- ARM Cortex-M memory-mapped peripherals
- STM32 register-level programming
- Register mapping using C structures
- Bit-fields in Embedded C
- GPIO configuration
- Volatile pointers
- Embedded software architecture without abstraction libraries

This project is intended as a learning exercise for embedded systems and serves as a foundation for future bare-metal drivers such as UART, Timers, PWM, ADC, SPI, I2C, and Interrupts.