Arduino_STM32 How to handle Fault
1. Abstruct
 Arduino_STM32 library is based on  Leaflabs Maple mini board and hardware. And on-board ERROR_LED connected to PB1.
 So, libmaple library support this ERROR_LED as default.
2. Fault support
 The fault support in libmaple is quite simple.
 If fault occured, the ERROR_LED only blink at fade mode until RESET.
 Because there is no other hardware to output any error message or status. And even If there were some hardware, it is hard to output under high IRQ level process which inhibit many general I/O routine. 