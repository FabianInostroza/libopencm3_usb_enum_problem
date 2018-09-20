Code showing enumeration problems when EP0 size <= 16

To compile for STM32F103 run: make
To compile for STM32F105 run: make CFLAGS=-DSTM32F105

There is always a delay before enumeration succeds or fails.

In Linux it always succeeds.
In Windows enumeration succeeds if connected to a USB 3.0 controller otherwise fails.

dmesg output with EP0 size = 16
```
[ 1512.237846] usb 1-1.2: new full-speed USB device number 52 using ehci-pci
[ 1517.522336] usb 1-1.2: New USB device found, idVendor=0483, idProduct=5740, bcdDevice= 2.00
[ 1517.522342] usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 1517.522345] usb 1-1.2: Product: CDC-ACM Demo
[ 1517.522348] usb 1-1.2: Manufacturer: Black Sphere Technologies
[ 1517.522350] usb 1-1.2: SerialNumber: DEMO
[ 1517.522893] cdc_acm 1-1.2:1.0: ttyACM0: USB ACM device
```

dmesg output with EP0 size >= 32
```
[ 1628.284429] usb 1-1.2: new full-speed USB device number 63 using ehci-pci
[ 1628.396691] usb 1-1.2: New USB device found, idVendor=0483, idProduct=5740, bcdDevice= 2.00
[ 1628.396697] usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 1628.396700] usb 1-1.2: Product: CDC-ACM Demo
[ 1628.396703] usb 1-1.2: Manufacturer: Black Sphere Technologies
[ 1628.396705] usb 1-1.2: SerialNumber: DEMO
[ 1628.397418] cdc_acm 1-1.2:1.0: ttyACM0: USB ACM device
```

Note the timestamps between the 'new full-speed USB device' messages and 'New USB device found'

Sometimes, when connected in a USB (3.0?) hub with EP0 size <= 16
```
[  451.419581] usb 2-3.1: new full-speed USB device number 19 using xhci_hcd
[  461.777487] usb 2-3.1: device descriptor read/all, error -110
[  461.855265] usb 2-3.1: new full-speed USB device number 20 using xhci_hcd
[  472.017170] usb 2-3.1: device descriptor read/all, error -110
[  472.017271] usb 2-3-port1: attempt power cycle
[  472.619045] usb 2-3.1: new full-speed USB device number 21 using xhci_hcd
[  472.642093] usb 2-3.1: New USB device found, idVendor=0483, idProduct=5740, bcdDevice= 2.00
[  472.642098] usb 2-3.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[  472.642101] usb 2-3.1: Product: CDC-ACM Demo
[  472.642104] usb 2-3.1: Manufacturer: Black Sphere Technologies
[  472.642107] usb 2-3.1: SerialNumber: DEMO
```

Compilers tested:
arm-none-eabi-gcc (GNU Tools for ARM Embedded Processors) 5.4.1 20160919 (release) [ARM/embedded-5-branch revision 240496] in Linux
arm-none-eabi-gcc (GNU Tools for Arm Embedded Processors 7-2018-q2-update) 7.3.1 20180622 (release) [ARM/embedded-7-branch revision 261907] in Linux

