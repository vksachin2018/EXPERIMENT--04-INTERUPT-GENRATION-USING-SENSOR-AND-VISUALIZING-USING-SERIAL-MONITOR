DATE: 21.10.2024
NAME: GOKUL SACHIN K
ROLL NO :212223220025
DEPARTMENT: BE.IT
EXPERIMENT--04-INTERUPT GENRATION USING SENSOR AND VISUALIZING USING SERIAL MONITOR
Aim:
To Interface a IR Sensor to digital port of iot development board and generate an interrupt and visualize on the serial monitor

Components required:
STM32 CUBE IDE, serial port utility monitor .

Theory :
An infrared (IR) sensor a proximity sensor, or a ‘nearness’ sensor senses whether there is an object near it or not. The IR stands for Infrared sensor. Infrared is the light out of our visible spectrum.

Working of an IR Sensor The white LED here is an IR LED which works as the transmitter and the component next to the IR LED is a photodiode that works as the receiver in the IR sensor.

The IR transmitter continuously emits the IR light and the IR receiver keeps on checking for the reflected light. If the light gets reflected back by hitting any object in front it, the IR receiver receives this light. This way the object is detected in the case of the IR sensor.

The blue knob here is a potentiometer. You can control the range i.e. from how far you want to detect the object by changing the value of the potentiometer.

An IR sensor has two small LED indicators – one for power, which is ON the entire time the sensor is ON; the other is the Signal LED which detects the object. The signal LED has two states or situations:

ON (Active) when it detects an object OFF (Inactive) when it doesn’t detect any object

image Now that we have a little idea about its works, let’s take a look at how to interface it with evive and see it in action.

Connect VCC pin to the +5V pin on evive. Connect GND pin to evive’s GND pin. Connect OUT to any gpio and configure that pin as EXTI mode

Interrupts
Interrupts are asynchronous (i.e. can happen anytime) events that disrupt the normal flow of your program. This allows the microcontroller to focus on a key task and attend to these events (e.g. pressing a button) as they come without needing to wait for them.

With interrupt, we do not need to continuously check the state of the digital input pin. When an interrupt occurs (a change is detected), the processor stops the execution of the main program and a function is called upon known as ISR or the Interrupt Service Routine. The processor then temporarily works on a different task (ISR) and then gets back to the main program after the handling routine has ended.

image The STM32 ARM microcontroller interrupts are generated in the following manner:

The system runs the ISR and then goes back to the main program. The NVIC and EXTI are configured. The Interrupt Service Routine (ISR) also known as the interrupt service routine handler is defined to enable the external interrupts.

Interrupt Lines (EXTI0-EXTI15) The STM32 ARM microcontroller features 23 event sources which are divided into two sections. The first section corresponds t external pins on each port which are P0-P15. The second section corresponds to RTC, ethernet, USB interrupts. Therefore, in the first section, we have 16 lines corresponding to line0 till line15. All of these map to a pin number. image

The diagram below shows how the GPIO pins are connected to the 16 interrupt lines:

Procedure:
click on STM 32 CUBE IDE, the following screen will appear image

click on FILE, click on new stm 32 project image image

select the target to be programmed as shown below and click on next

image

4.select the program name image

corresponding ioc file will be generated automatically image
6.select the appropriate pins as gipo, in or out, USART or required options and configure image image

7.click on cntrl+S , automaticall C program will be generated image image 8. edit the program and as per required image

use project and build all image

once the project is bulild image

click on debug option image

connect the iot board to power supply and usb

After connecting open the STM cube programmer image

click on UART and click on connect image

once it is connected , click on Erasing and programming option image

flash the bin or hex file as shown below by switching the switch to flash mode

image

check for execution of the output by switching the board to run mode
click on the serial port utility image
click on the run to observe the values
STM 32 CUBE PROGRAM :
#if defined (__ICCARM)||defined(__ARMCC_VERSION)
#define PUTCHAR_PROTOTYPE int fputc(int ch,FILE *f)
#elif defined(__GNUC__)
#define PUTCHAR_PROTOTYPE int __io_putchar(int ch)
#endif

PUTCHAR_PROTOTYPE
{
	HAL_UART_Transmit(&huart2,(uint8_t *)&ch,1,0xFFFF);
	return ch;
}

void HAL_GPIO_EXIT_Callback(uint16_t GPIO_Pin)
{
	if(HAL_GPIO_ReadPin(GPIOA,GPIO_PIN_0)==0)
	{
		printf("INTERRUPT OCCURED\n");
	}
	else
	{
		printf("INTERRUPT DOESNOT OCCURED\n");
	}
}

Output screen shots of serial port utility :
Circuit board :
Output:
Screenshot 2024-09-25 051742

Result :
Interfacing a IR SENSOR and interrupt is generated using external interrupt mode , visualized on serial port
