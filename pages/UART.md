- [UART2.patch](../assets/UART2_1661945568979_0.patch)
- [uart+mbox.patch](../assets/uart+mbox_1662108255563_0.patch)
- [RE_ _Aegis_ About bypass UART data for BIOS on DEC1515.msg](../assets/RE_Aegis_About_bypass_UART_data_for_BIOS_on_DEC1515_1662108812456_0.msg)
- ![image.png](../assets/image_1662108269712_0.png)
- \#define UART_RECV ((AHB_byte *) (UART_ADDR + 0x000))
- ```
  if (OUTDEV_DEBUG & OUTDEV_UART)
  {
    	// wait for THRE
    	timeout = UART_TIMEOUT;
   	while (uart_IsBusy())
  {
   	if (--timeout <= 0)
      break;
  }
  	//send the data
  	uart_Write(c);
  }
  ```
- -
  +    DPRINTF(1, ("*UART_LSR = %x\n",*UART_LSR));
  +    DPRINTF(1, ("*UART_LSR & BIT0 = %d\n",*UART_LSR & BIT0));
  +    DPRINTF(1, ("UART_RECV = %x\n", *UART_RECV));
-