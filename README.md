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
File system Journal & Write Cache contradict / collide to each other. </br>

Bigger cache requires more aggresive Journal, higher priority. </br>
No write-cache makes Journal work better. </br>

/etc/hdparm.conf </br>
```
# -W Disable/enable the IDE drive's write-caching feature
write_cache = off
```

verify internal drives connected directly to sata: </br>
$ sudo hdparm -i /dev/sdb </br>
```
/dev/sdb:

 Model=                , FwRev=    , SerialNo=          
 Config={ Fixed }
 RawCHS=16383/16/63, TrkSize=0, SectSize=0, ECCbytes=0
 BuffType=unknown, BuffSize=unknown, MaxMultSect=1, MultSect=1
 CurCHS=16383/16/63, CurSects=16514064, LBA=yes, LBAsects=500118192
 IORDY=on/off, tPIO={min:120,w/IORDY:120}, tDMA={min:120,rec:120}
 PIO modes:  pio0 pio1 pio2 pio3 pio4 
 DMA modes:  mdma0 mdma1 mdma2 
 UDMA modes: udma0 udma1 udma2 udma3 udma4 udma5 *udma6 
 AdvancedPM=no WriteCache=disabled
 Drive conforms to: unknown:  ATA/ATAPI-2,3,4,5,6,7

 * signifies the current active mode
```
USB3.0 drive FAIL </br>
$ sudo hdparm -i /dev/sdd </br>
```
/dev/sdd:
 HDIO_GET_IDENTITY failed: Invalid argument
```
mount point also FAIL </br>
$ sudo hdparm -i /media/jpc/XFS-18TB-2 </br>
```
/media/user/XFS-18TB:
 HDIO_DRIVE_CMD(identify) failed: Inappropriate ioctl for device
 HDIO_GET_IDENTITY failed: Inappropriate ioctl for device
```

--------------------

if want to read the long conversations, how soluton was found: </br>

https://bugzilla.kernel.org/show_bug.cgi?id=216282 </br>

