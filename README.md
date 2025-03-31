# ARM7_LPC2148

__1. Title: Led Light bilinking System Using LPC2148__

*Objective:* To understand and implement LED control using a microcontroller by turning it on and off at a fixed interval.

__Hardware Connection:__
 - LPC2129 P0.7 --> LED
 - LED --> GND

__Software Simulation:__

![image](https://github.com/user-attachments/assets/f485e25e-c045-4cff-baaf-f41cabf6eb34)


__Hardware Simulation:__

![WhatsApp Image 2025-03-27 at 14 37 50_253a72af](https://github.com/user-attachments/assets/086393bd-ca7c-40ee-8d0e-55f79af4a6e9)

__Code:__
```
#include <lpc21xx.h>
void delay_s(unsigned int dly)
{
	dly=dly*12000000;
	while(dly--);
}
#define LED 7
int main()
{
	IODIR0 |=1<<LED;
	while(1)
	{
		IOSET0=1<<LED;
		delay_s(1);
		IOCLR0=1<<LED;
		delay_s(1);
	}
}
```

_________________________________________________________________________________________________________________________________________________________________________

__2. Title: Traffic Light System Using 2148__

*Objective:* Design a traffic light system using Red, Yellow, and Green LEDs that mimic real-world traffic signals. 

__Hardware Connection:__
 - LPC2129 P0.10 --> LED red
 - LPC2129 P0.11 --> LED yellow
 - LPC2129 P0.12 --> LED green
 - LED --> GND

__Software Simulation:__

![image](https://github.com/user-attachments/assets/acad53e2-bd15-44ed-8595-1399c0006f53)

__Hardware Simulation:__

![WhatsApp Image 2025-03-27 at 14 37 50_22a8a5b2](https://github.com/user-attachments/assets/f0134f17-141d-4021-8ee5-f8dd9fb27309)

__Code:__
```
#include <lpc21xx.h>
#define RED_LED    (1 << 10)  // P0.10
#define YELLOW_LED (1 << 11)  // P0.11
#define GREEN_LED  (1 << 12)  // P0.12
void delay_ms(unsigned int ms)
{
    unsigned int i, j;
    for (i = 0; i < ms; i++)
    {
        for (j = 0; j < 1000; j++); // Rough delay loop
    }
}
int main(void)
{
    // Configure P0.10, P0.11, P0.12 as output
    IO0DIR |= (RED_LED | YELLOW_LED | GREEN_LED);
    while (1)
    {
        // Red LED ON (Stop Signal)
        IO0SET = RED_LED;
        IO0CLR = YELLOW_LED | GREEN_LED;
        delay_ms(5000);
        // Yellow LED ON (Get Ready Signal)
        IO0SET = YELLOW_LED;
        IO0CLR = RED_LED | GREEN_LED;
        delay_ms(2000);
        // Green LED ON (Go Signal)
        IO0SET = GREEN_LED;
        IO0CLR = RED_LED | YELLOW_LED;
        delay_ms(5000);
    }
}
```
___________________________________________________________________________________________________________________________________________________________

__3. Title: LED Binary Counter (1 to 255) Using LPC2148__

*Objective:*\
To interface 8 LEDs with the LPC21xx microcontroller and display binary counting from 1 to 255 by toggling the LEDs accordingly. The program configures Port 0 (pins P0.4 to P0.11) as output and sequentially updates the LED states in a loop with a delay of 100ms between each count.

__Hardware Connection__
