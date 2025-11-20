# Arduino_STM32 How to handle Fault
Arduino_STM32 device rarely stuck and no response until RESET.\
What happen ?\
One of answer is FAULT occured. \
But we can't know this status on such as BluePill, except original Maple_mini.\
Followings are discribed about simple way to know is FAULT occur or not.

## 1. Abstruct
 Arduino_STM32 library is based on  Leaflabs Maple_mini board.\
 And on-board ERROR_LED connected to PB1.\
 So, libmaple library support this ERROR_LED as default.
 ![maple_mini_sch.png](http://cholla.mmto.org/stm32/maple/maple_mini_sch.png)
## 2. Fault support
 The fault support in libmaple library is quite simple.\
 If fault occured, the ERROR_LED only blink at fade mode until RESET.\
 Because there is no other hardware to output any error message or status. \
 And even If there were some hardware, it is hard to output under high IRQ level processing which inhibit many general I/O routine. 
## 3. For another board such as BluePill
 If you wanted to detect fault occur as same as Maple_mini, only adjust port number to on-board LED's one such as PC13.\
 There is only need add following lines to "util.c" top.
 
 `Target file: "C:\Program Files (x86)\Arduino188\hardware\Arduino_STM32\STM32F1\cores\maple\libmaple\util.c"`
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

# Reference
- ### How do I track down a bus fault exception [STMicroelectronics Community](https://community.st.com/t5/stm32-mcus-products/how-do-i-track-down-a-bus-fault-exception/m-p/517298).
- ### How to debug a HardFault on an Arm® Cortex®-M STM32 [STMicroelectronics Community](https://community.st.com/t5/stm32-mcus/how-to-debug-a-hardfault-on-an-arm-cortex-m-stm32/ta-p/672235).
- ### RandomNinjaChef / KeilHardFault.c [GitHub Pages](https://github.com/cturvey/RandomNinjaChef/blob/main/KeilHardFault.c).
- ### Debugging a Cortex-M0 Hard Fault [Arm Community](https://community.arm.com/support-forums/f/embedded-and-microcontrollers-forum/3257/debugging-a-cortex-m0-hard-fault).

























