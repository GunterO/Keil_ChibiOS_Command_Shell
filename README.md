# Keil_ChibiOS_Template

ChibiOS + Keil µVision

Simple template (2 blinking LED's) to use ChibiOS with Keil µVision v4 / v5 and a STM32F429I-Discovery board.

Some changes were made to the ChibiOS source files to make it compile in µVision:

conf\chconf.h
-------------
```c++
 #define CH_MEMCORE_SIZE                 0
```
=> 
```c++
#define CH_MEMCORE_SIZE                 1024
```
This because the missing `Image$$RW_IRAM1$$ZI$$Limit` and `Image$$RW_IRAM2$$Base` definitions in the latest µVision compilers.
Feel free to change this value, but don't set it to 0 because automatic/full RAM size management is not working for now. 

os\hal\platforms\STM32\OTGv1\usb_lld.c
--------------------------------------
Commented out these lines ad the end of ´usb_lld_pump()´ to get rid of a "unreachable" compiler warning:
```c++
chSysUnlock();
return 0;
```
