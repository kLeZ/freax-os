# Introduction #

The boot phase, starting from power on and going to the init boot sequence, is an important part of the system. Today has become even more important because of the SecureBoot mechanism, introduced by Microsoft and adopted in all the modern computers, and for the UEFI system, a replacement for the old, well-working, beloved BIOS.

Unfortunately because of these two important changes in the modern computers we have to adapt or redesign the entire boot phase, using magic items such as shim, a signed efi loader which is accepted by SecureBoot.
This little arcane cauldron of bits makes SecureBoot happy while it still can only launch Grub or Lilo or whatever else.

We are very happy with UEFI but still not so glad of SecureBoot, especially because of the way Microsoft launched it (forcing hardware companies to adopt it because of marketing).

# The Boot process, revealed #

We have to deal with a new process but without abandoning the last one, so we need to make a common set of steps after that we started booting with either BIOS or UEFI (with or without SecureBoot).
Other distributions have found a way that we agree, for this kind of problem: that is, using the common boot process starting from Grub2, the only bootloader known to work good either in BIOS or in UEFI. Besides Grub2 we have to have the "shim" magic, in this way SecureBoot can believe that we have a trusted boot sequence.

## BIOS way ##

With the old beloved BIOS, we need only to install Grub2 in MBR, nothing else to do.

## UEFI way ##
### Without SecureBoot, the life is easier ###
If we have UEFI without SecureBoot, we can install Grub2 without further modifications but picking the one written for UEFI, the so called grub2-efi (simply a Grub2 compiled with the efi support).

### With SecureBoot, live harder ###
With SecureBoot, Grub2 remains the same, with the support for efi, but we need to do an extra step in order to install the SecureBoot boot option pointing on Shim and overall we need a separate /boot partition.

## A chart (took from [sysadmin1138.net](http://sysadmin1138.net/mt/blog/2011/01/the-linux-boot-process-a-chart.shtml)) ##

<table cellpadding='2' border='1' cellspacing='2'>
<tbody>
<tr>
<td>
<span>Pre-Boot Enviroinment</span>
</td>
</tr>
<tr>
<td><span>BIOS</span></td>
<td><span>EFI</span></td>
</tr>
<tr>
<td>
<ul>
<li>POST</li>
<li>Read bootable media</li>
<li>Load Master Boot Record</li>
<li>Execute MBR</li>
</ul>
</td>
<td>
<ul>
<li>POST</li>
<li>Read bootable media</li>
<li>Load the GPT table</li>
<li>Mount the EFI system-partition</li>
<li>Load EFI-drivers for the system</li>
<li>Execute MBR</li>
</ul>
</td>
</tr>
<tr>
<td><span>Bootstrap<br>
Environment</span></td>
</tr>
<tr>
<td><span>GRUB</span>(v1)</td>
<td><span>GRUB</span>(v2)</td>
<td><span>(E)LILO</span></td>
</tr>
<tr>
<td>
<ul>
<li>Stage 1 loaded into MBR/EFI and gets executed by BIOS/EFI</li>
<li>Stage 1.5 loaded by Stage 1, including critical drivers</li>
<li>Stage 2, in the boot filesystem, executes</li>
<li>Stage 2 loads the kernel</li>
</ul>
</td>
<td>
<ul>
<li>Stage 1 loaded into MBR/EFI and gets executed by BIOS/EFI</li>
<li>Load first sector of core.img</li>
<li>Continues loading core.img</li>
<li>Loads GRUB config</li>
<li>Loads the kernel</li>
</ul>
</td>
<td>
<ul>
<li>Stage1 loaded into MBR (or EFI by ELILO) and executed by<br>
BIOS/EFI</li>
<li>Stage 1 loads the first cluster of Stage 2, and executes.</li>
<li>Loads LILO information.</li>
<li>Loads the kernel</li>
</ul>
</td>
</tr>
<tr>
<td><span>Kernel Load</span></td>
</tr>
<tr>
<td>
<ul>
<li>The kernel uncompresses into memory</li>
<li>If configured, the kernel mounts the Initial Ramdisk, which<br>
contains needed modules to load the rest of the OS</li>
<li>Mounts the root filesystem, loading any needed modules from<br>
initrd</li>
<li>Swaps / from initrd to the actual root filesystem</li>
<li>Executes the specified init process</li>
</ul>
</td>
</tr>
<tr>
<td><span>UID 1 process</span></td>
</tr>
<tr>
<td><span>Initd</span></td>
<td><span>Systemd</span></td>
<td><span>Upstart</span></td>
<td><span>Launchd</span></td>
</tr>
<tr>
<td>
<ul>
<li>Checks /etc/inittab for loading procedures</li>
<li>Runs scripts specified by inittab</li>
<ul>
<li>Mounts needed filesystems</li>
<li>Loads needed modules</li>
<li>Starts needed services based on runlevel</li>
<li>Finishes setting up userspace</li>
</ul>
</ul>
</td>
<td>
<ul>
<li>Reads /etc/system.conf</li>
<li>Mounts needed filesystems</li>
<li>Loads needed modules</li>
<li>Starts services as needed</li>
</ul>
</td>
<td>
<ul>
<li>Runs startup events listed in /etc/events.d based on<br>
runlevel.</li>
<li>Loads needed modules</li>
<li>Mounts needed filesystems</li>
<li>Starts needed services</li>
</ul>
</td>
<td>
<ul>
<li>Reads /etc/launchd.conf for config details</li>
<li>Reads /etc/launchd.plist for per-driver/service details</li>
</ul>
</td>
</tr>
</tbody>
</table>