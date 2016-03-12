#Atmel ICE Mac Driver (for use with avrdude)
 
If you get the error:
 
avrdude: usbdev_open(): error claiming interface 0: Permission denied
avrdude: usbdev_open(): error claiming interface 1: Permission denied
avrdude: usbdev_open(): error claiming interface 2: Permission denied
avrdude: usbdev_open(): no usable interface found
avrdude: usbdev_open(): did not find any USB device "usb" (0x03eb:0x2111)
avrdude: jtag3_open_common(): Did not find any device matching VID 0x03eb and PID list: 0x2111
 
 
OSX is claiming the USB Device. The trick is to install a dummy kext to prevent that. The method is outlined here:http://www.proxmark.org/forum/vi...
 
you'll have to change the pid and vid to match that of Atmel ICE.
 
For your convenience, I've attached the kext (contains no code, only Info.plist)
 
extract the tar archive:
tar -xf AtmelICE.kext.tar.bz2
copy it to
/System/Library/Extensions (as root (sudo))
sudo cp AtmelICE.kext /System/Library/Extensions
 
change permissions and ownership:
chown -R root:wheel /System/Library/Extensions/AtmelICE.kext
chmod -R 755 /System/Library/Extensions/AtmelICE.kext
 
reload the kext cache:
kextcache -system-caches
 
(You might want to unplug and plug-in the device again).

