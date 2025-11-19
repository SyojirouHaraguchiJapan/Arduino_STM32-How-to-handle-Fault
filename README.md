# Arduino_STM32 How to handle Fault
## 1. Abstruct
 Arduino_STM32 library is based on  Leaflabs Maple_mini board and hardware. 
 And on-board ERROR_LED connected to PB1.
 So, libmaple library support this ERROR_LED as default.
## 2. Fault support
 The fault support in libmaple is quite simple.
 If fault occured, the ERROR_LED only blink at fade mode until RESET.
 Because there is no other hardware to output any error message or status. 
 And even If there were some hardware, it is hard to output under high IRQ level processing which inhibit many general I/O routine. 
## 3. For another board such as BluePill
 If you wanted to detect fault occur as same as Maple_mini, only adjust port number to on-board LED's one such as PC13.
 There is only need add following lines to "util.c" top.
 
 Target file: 'C:\Program Files (x86)\Arduino188\hardware\Arduino_STM32\STM32F1\cores\maple\libmaple\util.c`
```
/*
 * Re-define ERROR_LED_PORT and ERROR_LED_PIN to PC13_LED for fit to BluePill
 */
#if defined(ERROR_LED_PORT) && defined(ERROR_LED_PIN)
#undef  ERROR_LED_PORT
#undef  ERROR_LED_PIN
#endif

#define ERROR_LED_PORT   GPIOC
#define ERROR_LED_PIN    13
```








