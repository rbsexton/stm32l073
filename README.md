# stm32l073
Application framework for Forth on STM32L073

## Appendices

### Useful STM Documentation

- UM1749 User Manual Description of STM32L0 HAL and Low Layer drivers ( dm00113898-description-of-stm32l0-hal-and-low-layer-drivers-stmicroelectronics) 
- UM1734 STM32Cube(TM) USB device library ( dm00108129-stm32cube-usb-device-library-stmicroelectronics )

### USB Notes.

USB Device IP has to operate independently of software support.

OUT/Host to Device Flow
- Host sends OUT Packet, Plus a data packet. 
- Device ACKs the Packet if its expecting it and has room.  
- Device accepts the data.
- Stack does the callback to CDC_Itf_Receive()
- Firmware calls HAL_PCD_EP_Receive() to set up the next transfer.

IN/Device to Host Flow
- Host sends IN Packet 
- Device Sends data if it has it.  
- USB Stack calls 
- Firmware calls HAL_PCD_EP_Receive() to set up the next transfer.




USBD_CDC_ReceivePacket() is the fn that you call to tell the USB stack that the 
device can accept more data. 

### Memory Usage 

Baseline after first compile
```
text	   data	    bss	    dec	    hex	filename
22836	   1464	   8268	  32568	   7f38	exe/supervisor.out
```

After Ripping out USART code
```
text	   data	    bss	    dec	    hex	filename
18172	   1464	   8068	  27704	   6c38	exe/supervisor.out
```