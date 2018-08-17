#                       Dhrystone
                        
This SoftConsole Makefile project demonstrates how to configure and use the Dhrystone Benchmark.

##                      Mi-V Soft processor
This example uses a Mi-V Soft processor MiV_RV32IMA_L1_AHB. The design is 
built for debugging MiV_RV32IMA_L1_AHB through the SmartFusion2 FPGA programming 
JTAG port using a FlashPro5. To achieve this the CoreJTAGDebug IP is used to 
connect to the JTAG port of the MiV_RV32IMA_L1_AHB.

Optionally, The design can be build to use Olimex ARM-USB-TINY-H JTAG probe. 
For this,The JTAG pins must be routed through Fabric to the top level pins.

All the platform/design specific definitions such as peripheral base addresses,
system clock frequency etc. are included in hw_platform.h. The hw_platform.h is 
located at the root folder of this project.

The MiV_RV32IMA_L1_AHB firmware projects needs the riscv_hal and the hal firmware
(RISC-V HAL).

The RISC-V HAL is available through Firmware catalog as well as the link below:
https://github.com/RISCV-on-Microsemi-FPGA/Solutions/tree/master/Mi-V-Firmware

## Target hardware

This example project is targeted at a SmartFusion2 M2S150 advanced development kit. 
The example project is built using a clock frequency of 83MHz. Trying to execute 
this example project on a different design will result in incorrect baud rate 
being used by CoreUART and timer load value.

This example project can be used with another design using a different clock
configuration. This can be achieved by overwriting the content of this example
project's "hw_platform.h" file with the correct data from your Libero design.

An example design for SmartFusion2 150 Ad. Dev Kit is available at 
https://github.com/RISCV-on-Microsemi-FPGA/SmartFusion2-Advanced-Dev-Kit