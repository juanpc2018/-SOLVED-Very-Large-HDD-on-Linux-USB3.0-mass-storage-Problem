another of those super complex problems, that has a very simple solution...
makes you wonder: ¿how could i Not see that?

Problem:
when you use / plug a very large HDD to USB3.0 on Linux.
most of the times the HDD is Not detected.

IF the USB3.0 enclosure has a external powersupply,
can be turned-On, after being plugged or continue to be On un-plugged from USB.

usually external enclosures with ASMedia USB SATA controller.

Manual Sollution:
unplug the usb cable with HDD turned-on, and plug again to PC.
that will detect the Very Large USB HDD.

Permanent solution:

create a file like this, here:

-----

/etc/modprobe.d/usb-storage.conf

1. options usb-storage delay_use=15
2. # install usb-storage /bin/true 
3. # options usb-storage option_zero_cd
4. # options usb-storage quirks
5. # options usb-storage swi_tru_install

-----

P.D. 10 seconds can work, but... its on the edge.

-----
if you want to read some of the long conversations about this, and how the solluton was found:
https://bugzilla.kernel.org/show_bug.cgi?id=216282

