# Lab 1: Jiří Tomešek

   [My Digital-electronics-2 GitHub repository](https://github.com/xtomes07/Digital-electronics-2)


### Blink example

1. What is the meaning of the following binary operators in C?
   * `|`    OR
   * `&`    AND
   * `^`    XOR
   * `~`    NOT
   * `<<`   binární posun vlevo
   * `>>`   binární posun doprava

2. Complete truth table with operators: `|`, `&`, `^`, `~`

| **b** | **a** |**b or a** | **b and a** | **b xor a** | **not b** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 | 1 |
| 1 | 0 | 1 | 0 | 1 | 0 |
| 1 | 1 | 1 | 1 | 0 | 0 |


### Morse code

1. Listing of C code with syntax highlighting which repeats one "dot" and one "comma" on a LED:

```c
int main(void)
{
    // Set pin as output in Data Direction Register
    // DDRB = DDRB or 0010 0000
    DDRB = DDRB | (1<<LED_GREEN);

    // Set pin LOW in Data Register (LED off)
    // PORTB = PORTB and 1101 1111
    PORTB = PORTB & ~(1<<LED_GREEN);

    // Infinite loop
    while (1)
    {
        // Pause several milliseconds
        _delay_ms(SHORT_DELAY);
        
        PORTB = PORTB ^ (1<<LED_GREEN);      //LED ON -krátká doba pro tečku
        _delay_ms(SHORT_DELAY);
        
        PORTB = PORTB ^ (1<<LED_GREEN);      //LED OFF
        _delay_ms(SHORT_DELAY);
        
        PORTB = PORTB ^ (1<<LED_GREEN);      //LED ON - dlouhá doba pro čárku
        _delay_ms(3*SHORT_DELAY);
       
       PORTB = PORTB ^ (1<<LED_GREEN);       //LED OFF
        _delay_ms(SHORT_DELAY);
        
    }

    // Will never reach this
    return 0;
}
```


2. Scheme of Morse code application, i.e. connection of AVR device, LED, resistor, and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![Schema](schema.png)
