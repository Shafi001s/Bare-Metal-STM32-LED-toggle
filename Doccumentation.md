# Documentation

## Project Overview

This project demonstrates how to control the onboard LED of the STM32F401RE microcontroller using **bare-metal programming**. Instead of relying on STM32 HAL or CMSIS driver functions, the program directly accesses the microcontroller's hardware registers through memory-mapped addresses and custom C structures.

The objective is to understand how GPIO peripherals are configured and controlled at the register level.

---

## Project Structure

```
.
├── main.c          # Main application source code
├── reg.h           # Register structure definitions
└── README.md
```

---

## Register Mapping

The project uses C structures with bit-fields to represent STM32 peripheral registers.

The following registers are mapped:

| Register | Purpose |
|----------|---------|
| RCC_AHB1ENR | Enables the GPIO peripheral clock |
| GPIOx_MODE | Configures GPIO pin modes |
| GPIOx_PUPDR | Configures pull-up/pull-down resistors |
| GPIOx_IDR | Reads GPIO input data |
| GPIOx_ODR | Writes GPIO output data |

Each register is mapped to its corresponding memory address using pointers.

Example:

```c
RCC_AHB1ENR volatile *const pClkCtrlreg =
(RCC_AHB1ENR*)0x40023830;
```

---

## Program Flow

### Step 1 – Enable GPIOA Clock

The GPIOA peripheral clock is enabled by setting the `gpioa_en` bit inside the RCC AHB1ENR register.

```c
pClkCtrlreg->gpioa_en = 1;
```

---

### Step 2 – Configure GPIO Pins

#### PA5 as Output

The onboard LED connected to PA5 is configured as a General Purpose Output.

```c
pPortAModereg->pin_5 = 1;
```

#### PA0 as Input

The push button connected to PA0 is configured as an input.

```c
pPortAModereg->pin_0 = 0;
```

---

### Step 3 – Configure Pull-Down Resistor

An internal pull-down resistor is enabled for PA0.

```c
pPortAPupdr->pin_0 = 2;
```

This keeps the input at logic LOW until the button is pressed.

---

### Step 4 – Read the Input

The program continuously reads the state of PA0.

```c
if(pPortAInreg->pin_0 == 1)
```

---

### Step 5 – Control the LED

If the button is pressed, PA5 is set HIGH to turn on the LED.

```c
pPortAOutreg->pin_5 = 1;
```

Otherwise, the LED is turned off.

```c
pPortAOutreg->pin_5 = 0;
```

---

## Program Logic

```
Start
   │
   ▼
Enable GPIOA Clock
   │
   ▼
Configure PA5 as Output
   │
   ▼
Configure PA0 as Input
   │
   ▼
Enable Pull-Down Resistor
   │
   ▼
Read PA0
   │
   ├── Button Pressed?
   │        │
   │       Yes
   │        │
   │     Turn LED ON
   │        │
   │       No
   │        │
   └────Turn LED OFF
        │
        ▼
      Repeat Forever
```

---

## Memory Map

| Peripheral | Address |
|------------|----------|
| RCC AHB1ENR | `0x40023830` |
| GPIOA MODER | `0x40020000` |
| GPIOA PUPDR | `0x4002000C` |
| GPIOA IDR | `0x40020010` |
| GPIOA ODR | `0x40020014` |

---

## Key Concepts Demonstrated

- Bare-metal embedded programming
- Memory-mapped I/O
- Peripheral clock enabling
- GPIO configuration
- Register-level programming
- C structures
- Bit-fields
- Volatile pointers
- Infinite polling loop
- Input-driven output control

---

## Future Improvements

This project can be extended by implementing:

- GPIO driver abstraction
- LED blinking using Timers
- External Interrupts (EXTI)
- UART communication
- PWM generation
- ADC input reading
- SPI communication
- I2C communication
- CAN communication
- DMA
- FreeRTOS integration

---

## Conclusion

This project provides a solid introduction to bare-metal STM32 programming by demonstrating direct register access using C structures and bit-fields. It builds a strong foundation for developing peripheral drivers without relying on vendor-provided libraries and prepares the way for more advanced embedded systems development.