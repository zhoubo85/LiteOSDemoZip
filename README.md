# LiteOSDemoZip

This is a liteOS project for stm32L476 and NEUL BC95(NB module)

## some information about this code ##

### 1:About Keil project file
-  the keil project file is in projects/STM32L476VE_THUNDERSOFT/.
   If you have installed Keil 5.13 or later version, you can double click the
   project file(HuaweiLiteOS.uvprojx) to show the LiteOS project.
   
### 2: Some thing about LiteOS run the nb demo ### 
- a: the nb demo task function is in file user/ocean_sample.c 
   void oceancon_sampletask(void * pvParameters) is the task function.
- b: the nb device driver are nb_core.c neul_bc95_data.c at_interface.c
- c: stm32L476 communicate with NB module by USART2
- d: nb module connect huawei occean connect platform main steps are in oceaninterface/ocean_interface.c
       ocean_sample.c will call  ocean_interface.c's function , and ocean_interface.c will call nb_core.c's function
       like ocean_sample.c-->ocean_interface.c-->nb_core.c-->at_interface.c-->uart2
       
### 3: how nb module communicate with huawei occean connect platform ### 
- stpe1(init nb module): ret = ocean_res_init(CON_NB, TRAN_MAX, NB_NEUL_BC95);
- step2(upload local user data): ocean_send_data(data, len);
- step3(recive platform's data):n = ocean_recv_data(test_rbuf, 512);
- step4(deal with  special user data ): ocean_dev_control(test_rbuf, n);
   
### Other ### 
- if you want know how to use LiteOS kernel API, please see https://github.com/LITEOS/LiteOS_Kernel/blob/master/doc/HuaweiLiteOSKernelDevGuide.md
  this doc is writen in chinese
  
- more information about nb module , please see Quectel_BC95_AT_Commands_Manual_V1.5.pdf