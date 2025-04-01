Another of those super complex problems that has a very simple solution... </br>
makes you wonder: ¿how could i Not see that? </br>

Problem: </br>
when you use / plug a Very Large HDD to USB3.0 on Linux. </br>
most of the times the HDD is Not detected. </br>

IF the USB3.0 enclosure has an external powersupply, </br>
can be turned-On after being plugged or continue to be On un-plugged from USB. </br>

usually external enclosures with ASMedia USB SATA controller. </br>

Manual Solution: </br>
unplug the usb cable with HDD turned-on, and plug again. </br>
that will detect the Very Large USB HDD. </br>

Proper Automatic Permanent solution: </br>

create a file like this: </br>


/etc/modprobe.d/usb-storage.conf </br>
```
options usb-storage delay_use=15
# install usb-storage /bin/true 
# options usb-storage option_zero_cd
# options usb-storage quirks
# options usb-storage swi_tru_install
```

P.D.  </br>
20TB could require more, </br>
some Kernels require more, </br>
and brand to brand differences. </br>
IF helium seal is leaking, more oxygen makes harder to spin-up </br>
etc... </br>

-----

Recomended: </br>
Disable Write-cache </br>
why? </br>
because if there is a Crash, or power loss without UPS, </br>
its easy to recover files, or continue downloading. </br>

/etc/hdparm.conf </br>
```
# -W Disable/enable the IDE drive's write-caching feature
write_cache = off
```


if want to read some of the long conversations, and how the soluton was found: </br>

https://bugzilla.kernel.org/show_bug.cgi?id=216282 </br>

