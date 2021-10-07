# Lab 3: YOUR_FIRSTNAME FAMILYNAME

Link to my `Digital-electronics-2` GitHub repository:

   https://github.com/xtomes07/Digital-electronics-2


### Data types in C

1. Complete table.

| **Data type** | **Number of bits** | **Range** | **Description** |
| :-: | :-: | :-: | :-- | 
| `uint8_t`  | 8 | 0, 1, ..., 255 | Unsigned 8-bit integer |
| `int8_t`   | 8 | -128,-127,...,127 | Signed 8-bit Integer |
| `uint16_t` | 16 | 0, 1, ...,65535 | Unsigned 16-bit integer |
| `int16_t`  | 16 | -32768, -32767, ..., 32767 | Signed 16-bit integer |
| `float`    | 32 | -3.4e+38, ..., 3.4e+38 | Single-precision floating-point |
| `void`     | 0 | 0 | No return type for function / generic pointer |


### GPIO library

1. In your words, describe the difference between the declaration and the definition of the function in C.
   * Function declaration - prototyp funkce používaný k informování kompilátoru, že s těmito parametry bude existovat taková funkce
   * Function definition - skutečný kód funkce, která bude spuštěna

2. Part of the C code listing with syntax highlighting, which toggles LEDs only if push button is pressed. Otherwise, the value of the LEDs does not change. Use function from your GPIO library. Let the push button is connected to port D:

```c
    // Configure Push button at port D and enable internal pull-up resistor
    // WRITE YOUR CODE HERE
    GPIO_config_input_pullup(&DDRD, BUTTON);

    // Infinite loop
    while (1)
    {
        // Pause several milliseconds
        if (GPIO_read(&PIND, BUTTON) == 0) {
            _delay_ms(BLINK_DELAY);
            PORTC ^= (1 << LED_RED);
            PORTB ^= (1 << LED_GREEN);
        }
    }
```


### Traffic light

1. Scheme of traffic light application with one red/yellow/green light for cars and one red/green light for pedestrians. Connect AVR device, LEDs, resistors, one push button (for pedestrians), and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![your figure]()
