================================================================================
              RISC-V simple bare metal bootloader example project
================================================================================

Simple boot-loader example program.
 *  This sample project is targeted at a RISC-V design running on the M2S150 
    development board.
 *  You can program the on-board SPI Flash from a command-line program and have the
    boot-loader to load a program from SPI Flash to memory and jump to it.
 *  These actions are driven from a serial command-line interface.

--------------------------------------------------------------------------------
                            Mi-V Soft processor
--------------------------------------------------------------------------------
This example uses a Mi-V Soft processor MiV_RV32IM_L1_AHB. The design is 
built for debugging MiV_RV32IM_L1_AHB through the SmartFusion2 FPGA programming 
JTAG port using a FlashPro5. To achieve this the CoreJTAGDebug IP is used to 
connect to the JTAG port of the MiV_RV32IM_L1_AHB.

Optionally, the design can be build to use the Olimex ARM-USB-TINY-H JTAG probe. 
For this, The JTAG pins must be routed through Fabric to the top-level pins.

All the platform/design specific definitions such as peripheral base addresses,
system clock frequency, etc. are included in hw_platform.h. The hw_platform.h is 
located at the root folder of this project.

The MiV_RV32IM_L1_AHB firmware projects need the riscv_hal and the hal firmware
(RISC-V HAL).

The RISC-V HAL is available through Firmware catalog as well as the link below:

https://github.com/RISCV-on-Microsemi-FPGA/Solutions/tree/master/Mi-V-Firmware
--------------------------------------------------------------------------------
                            How to use this example
--------------------------------------------------------------------------------
This example project requires a USB-UART interface to be connected to a host PC. 
The host PC must connect to the serial port using a terminal emulator such as
HyperTerminal or PuTTY configured as follows:
  - 115200 baud
  - 8 data bits
  - 1 stop bit
  - no parity
  - no flow control

The M2S150 design used to run this example project has 128kb memory space.
This 128k memory space is divided into two parts. 
    The top half (from 0x80010000, LENGTH = 64k) where the bootloader application 
    executes and the bottom half (from 0x80000000, LENGTH = 64k) where the 
    user provided executable is stored. 
  
On-board DIP switch 8 is configured to select between 
    -- Executing the bootloader application
    OR
    -- Copy the preloaded executable from SPI flash and execute it. 

--------------------------------------------------------------------------------
Executing the boot-loader application: (DIP switch 8 --> OFF)
--------------------------------------------------------------------------------
This boot-loader example displays a message on HyperTerminal. Use the interactive 
user interface to give commands from HyperTerminal.

 Type 0 to show this menu
 Type 1 to start Y-modem transfer to memory
 Type 2 to copy the program from memory to flash
 Type 3 to copy the program from flash to memory
 Type 4 to start program loaded in memory
 Type 5 to test Flash device 0
 Type 6 to test memory

Use the following sequence of commands(DIP switch 8 --> OFF) to copy the .bin 
file in memory at the bottom half and start execution:

Select 1 to start YMODEM transfer to memory
    This option will start the YMODEM protocol and allows the user to send the 
    .bin file to the targeted memory address.
    
Type 2 to copy the program from memory to flash
    This option will copy the code to the FLASH. 
    
 Type 3 to copy the program from flash to memory
    This option will check the contents of FLASH. 
 
 Type 4 to start program loaded in memory
    This option will jump the control to the start of the bottom half
    (user-provided .bin file) and start the execution. 

Use the following sequence of commands(DIP switch 8 --> OFF) if you only want to 
download your application to the memory and start executing it without storing 
it into the flash, then use following sequence.

Select 1 to start YMODEM transfer to memory
    This option will start the YMODEM protocol and allows the user to send the 
    .bin file to the targeted memory address.
 
 Type 4 to start program loaded in memory
    This option will jump the control to the start of the bottom half
    (user-provided .bin file) and start the execution. 

--------------------------------------------------------------------------------
Copy the preloaded executable from SPI flash and execute it (DIP switch 8 --> ON)
--------------------------------------------------------------------------------
Turning ON the DIP switch will bypass the bootloader application code, copy the 
preprogrammed executable from FLASH to execution memory and start executing it.
This assumes that the SPI flash already contains a valid executable. It will 
be copied to the executable memory without doing any validity checks and start 
executing it. 

You also need to make sure that the clock frequency of your application matches
that of the bootloader application / libero design combination.

--------------------------------------------------------------------------------
                                Target hardware
--------------------------------------------------------------------------------
This example project is targeted at a SmartFusion2 M2S150 advanced development 
kit design which has CoreTimer enabled. 
The example project is built using a clock frequency of 50MHz. Trying to execute 
this example project on a different design will result in incorrect baud rate 
being used by CoreUART and timer load value.

This example project can be used with another design using a different clock
configuration. This can be achieved by overwriting the content of this example
project's "hw_platform.h" file with the correct data from your Libero design.

An example design for SmartFusion2 150 Ad. Dev Kit is available at 
https://github.com/RISCV-on-Microsemi-FPGA/SmartFusion2-Advanced-Dev-Kit
