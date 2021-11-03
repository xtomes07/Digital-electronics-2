# Lab 7: YOUR_FIRSTNAME FAMILYNAME

Link to this file in your GitHub repository:

[https://github.com/your-github-account/repository-name/lab_name](https://github.com/...)


### Analog-to-Digital Conversion

1. Complete table with voltage divider, calculated, and measured ADC values for all five push buttons.

   | **Push button** | **PC0[A0] voltage** | **ADC value (calculated)** | **ADC value (measured)** |
   | :-: | :-: | :-: | :-: |
   | Right  | 0&nbsp;V | 0   |  |
   | Up     | 0.495&nbsp;V | 101 |  |
   | Down   | 1,203&nbsp;V | 246 |  |
   | Left   | 1,970&nbsp;V | 403 |  |
   | Select | 3,182&nbsp;V | 651 |  |
   | none   | 5&nbsp;V | 1023 |  |

2. Code listing of ACD interrupt service routine for sending data to the LCD/UART and identification of the pressed button. Always use syntax highlighting and meaningful comments:

```c
/**********************************************************************
 * Function: ADC complete interrupt
 * Purpose:  Display value on LCD and send it to UART.
 **********************************************************************/
ISR(ADC_vect)
{
    uint16_t value = 0;
    char lcd_string[4] = "0000";

    value = ADC;                  // Copy ADC result to 16-bit variable
    itoa(value, lcd_string, 10);  // Convert decimal value to string

    // WRITE YOUR CODE HERE
    lcd_gotoxy(8, 0); lcd_puts("    ");    // Put ADC value in decimal
	lcd_gotoxy(8, 0); lcd_puts(lcd_string);    // Put ADC value in decimal
	uart_puts("ADC value: ");
	uart_puts(lcd_string);
	uart_puts("\r\n");

	itoa(value, lcd_string, 16);    // Convert to string in decimal
	lcd_gotoxy(13,0); lcd_puts("   ");    // Put ADC value in hexadecimal
	lcd_gotoxy(13,0); lcd_puts(lcd_string);    // Put ADC value in hexadecimal

	lcd_gotoxy(8, 1); lcd_puts("      ");    // Put button name here
	if(value < 11)
	{
		lcd_gotoxy(8, 1); lcd_puts("Right");
	}
	else if(value < 112)
	{
		lcd_gotoxy(8, 1); lcd_puts("Up");
	}
	else if(value < 256)
	{
		lcd_gotoxy(8, 1); lcd_puts("Down");
	}
	else if(value < 413)
	{
		lcd_gotoxy(8, 1); lcd_puts("Left");
	}
	else if(value < 661)
	{
		lcd_gotoxy(8, 1); lcd_puts("Select");
	}
	else{
		lcd_gotoxy(8, 1); lcd_puts("None");
	}

}
```


### UART communication

1. (Hand-drawn) picture of UART signal when transmitting three character data `De2` in 4800 7O2 mode (7 data bits, odd parity, 2 stop bits, 4800&nbsp;Bd).

D = 0b0100_0100

e = 0b0110_0101

2 = 0b0011_0010

   ![your figure](Images/prubehy.jpg)

2. Flowchart figure for function `uint8_t get_parity(uint8_t data, uint8_t type)` which calculates a parity bit of input 8-bit `data` according to parameter `type`. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![your figure](Images/vyvojDiag.jpg)


### Temperature meter

Consider an application for temperature measurement and display. Use temperature sensor [TC1046](http://ww1.microchip.com/downloads/en/DeviceDoc/21496C.pdf), LCD, one LED and a push button. After pressing the button, the temperature is measured, its value is displayed on the LCD and data is sent to the UART. When the temperature is too high, the LED will start blinking.

1. Scheme of temperature meter. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![your figure](Images/zapojeni.png)
