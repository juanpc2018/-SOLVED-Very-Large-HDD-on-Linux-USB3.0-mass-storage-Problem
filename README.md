another of those super complex problems, that has a very simple solution...
makes you wonder: ¿how could i Not see that?

Problem:
when you use / plug a Very Large HDD to USB3.0 on Linux.
most of the times the HDD is Not detected.

IF the USB3.0 enclosure has a external powersupply,
can be turned-On, after being plugged or continue to be On un-plugged from USB.

usually external enclosures with ASMedia USB SATA controller.

Manual Solution:
unplug the usb cable with HDD turned-on, and plug again.
that will detect the Very Large USB HDD.

Proper Automatic Permanent solution:

create a file like this:

-----

/etc/modprobe.d/usb-storage.conf
```
options usb-storage delay_use=15
# install usb-storage /bin/true 
# options usb-storage option_zero_cd
# options usb-storage quirks
# options usb-storage swi_tru_install
```
-----

P.D. 10 seconds can work for 18TB hdds, but... its on the edge.
20TB would require more,
and brand to brand differences.

-----
if want to read some of the long conversations, and how the soluton was found:

https://bugzilla.kernel.org/show_bug.cgi?id=216282

