# Learning Notes

## Day 1: Toolchain and first program
- Build turns C code into machine code (an .elf file). Run or Debug loads it into the chip through the ST-LINK.
- main.c is the main program file. Code goes only between the USER CODE BEGIN and END markers, or CubeMX will erase it when it regenerates files.
- Arduino setup() is the code before while(1). Arduino loop() is the code inside while(1).

## Day 2: GPIO and timing
- Pins are grouped into ports (A, B, C, D...). The four LEDs are on port D.
- HAL_Delay() freezes the whole program. HAL_GetTick() gives milliseconds since power-on, so the program can keep running while it waits (the same idea as Arduino millis()).
- Clock: 8 MHz crystal, divided by 8, multiplied by 336, divided by 2, gives 168 MHz. APB1 bus runs at 42 MHz, APB2 at 84 MHz.

## Day 3: Interrupts and printf
- Polling means checking again and again. An interrupt means the hardware calls a function when something happens.
- volatile tells the compiler a variable can change outside normal program flow (for example inside an interrupt), so it must always read the real value.
- Keep interrupt callbacks short. Set a flag and let the main loop do the slow work.
- Buttons bounce for a few milliseconds. Ignoring presses within 50 ms is a simple debounce.
- printf output goes through the SWO pin and the ST-LINK to CubeIDE (SWV). Core clock must be set to 168 MHz.

## Questions I should be able to answer
- What is the difference between polling and an interrupt?
- What does volatile do and why is it needed?
- Why should an interrupt callback be short?
- What is debouncing?
