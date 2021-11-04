## Preparation tasks (done before the lab at home)

1. Use schematic of the [LCD keypad shield](../../Docs/arduino_shield.pdf) and find out the connection of five push buttons: Select, Left, Up, Down, and Right.
![zapojeni](Images/button-zapojeni.png)
2. According to the connection, calculate the voltage values on pin PC0[A0] if one button is pressed at a time. In this case, the voltage on the pin is given by the [voltage divider](https://www.allaboutcircuits.com/tools/voltage-divider-calculator/), where resistors R3, R4, R5 and R6 are applied successively.
   
   Vpc0(Right)=0V

   Vpc0(Up)= 0,495V

   Vpc0(Down)=1,203V

   Vpc0(Left)=1,970V

   Vpc0(Select)=3,182V

3. Calculate the voltage value if none of the push buttons is pressed.

   Vpc0(none)=5V

   &nbsp;

4. Calculate the ADC values for these voltages according to the following equation if reference is Vref=5V and number of bits for analog to digital conversion is n=10.

   | **Push button** | **PC0[A0] voltage** | **ADC value (calculated)** | **ADC value (measured)** |
   | :-: | :-: | :-: | :-: |
   | Right  | 0&nbsp;V | 0   |  |
   | Up     | 0.495&nbsp;V | 101 |  |
   | Down   | 1,203&nbsp;V | 246 |  |
   | Left   | 1,970&nbsp;V | 403 |  |
   | Select | 3,182&nbsp;V | 651 |  |
   | none   | 5&nbsp;V | 1023 |  |
5.
 | **Operation** | **Register(s)** | **Bit(s)** | **Description** |
   | :-- | :-: | :-: | :-- |
   | Voltage reference    | ADMUX | REFS1:0 | 00: ..., 01: AVcc voltage reference (5V), ... |
   | Input channel        | ADMUX | MUX3:0 | 0000: ADC0, 0001: ADC1, ... |
   | ADC enable           | ADCSRA | ADEN | 1: ADC Enable, 0: ADC Disabled |
   | Start conversion     | ADCSRA | ADSC | 1: Start first conversion/start conversion, 0: stop conversion |
   | ADC interrupt enable | ADCSRA | ADIE | 1: Enable interrupt, 0: Disable interrupt |
   | ADC clock prescaler  | ADCSRA | ADPS2:0 | 000: Division factor 2, 001: 2, 010: 4, ...|
   | ADC 10-bit result    | ADMUX | ADLAR | 0: 10-bit mode(ADCH:L), 1: 8-bit mode(values stored only in ADCH) |
6.
 | **Function name** | **Function parameter(s)** | **Description** | **Example** |
   | :-- | :-- | :-- | :-- |
   | `uart_init` | `UART_BAUD_SELECT(9600, F_CPU)` | Initialize UART to 8N1 and set baudrate to 9600&nbsp;Bd | `uart_init(UART_BAUD_SELECT(9600, F_CPU));` |
   | `uart_getc` | void | Get received byte from ringbuffer. | |
   | `uart_putc` | unsigned char data | Put byte to ringbuffer for transmitting via UART. ||
   | `uart_puts` | const char s | Put string to ringbuffer for transmitting via UART. ||