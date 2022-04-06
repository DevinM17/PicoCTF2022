# Drive Geometry | Week 2
First ever hard disk could hold about 10mb of data and was sold for around four thousand dollars!

Basic Drive Geometry Definitions
- Track 
- Sector
![Hard disks](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.i-programmer.info%2Fimages%2Fstories%2FBabBag%2FHardDisk%2Ffig2.jpg&f=1&nofb=1)![Hard Drive Data Recovery | Inside Hard Disk Drives Part 1](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.datarecovery.net%2Fi%2Fmisc%2Fharddrive.gif&f=1&nofb=1)

Head assembly contains two magnetic heads, each in contact with the platter surface
The platter rotates around a spindle typically at 360 revolutions per minute
The heads are placed over the surface by a stepper motor with 80 different positions
The area swept under a head is called a track
There are 80 tracks per surface
Each track is split into sectors
The system finds the sectors on the track by timing and by using an index hole that indicates the first sector
Files on a disk are just referebces to sectors where the data is actually held

A sector is made up of data which is stored as a magnetic pattern created by a "magnetic code"


![[Pasted image 20220228102517.png]]

![[Pasted image 20220228102525.png]]

![[Pasted image 20220228102536.png]]

## Sectors : A subdivision of a track on a magnetic disk
	Each sector stores a fixed amount of user-accessible data - traditionally 512 bytes for HDD's
	CD-ROMS - 2048 bytes
	Newer HDD's - 4096 bytes or 4kib -- known as advanced format (AF)
	A sector is the mimum storage unit of a hard drive
	An operating system will typically operate on blocks of data which may span across many sectors

# Drive Formatting 
### High Level Formatting
	Typical method of formatting a drive
	data can be recovered
	it prepares a disk for reading and writing by erasing the linked data on the disk
	It does some simple testing to make sure all sectors are reliable and then creates internal address tables that is later used to locate new information
		
### Low Level Formatting
	Not typical 
	Data is not recoverable
	Erases the disk entirely and will effectively remove any software, drives, sector address tables and any all other data
	Its more time consuming as the drive has to go through and initalize every setor individually 
	For those security conscious they typically do not only 1 low level format but 3 passes all togethor

# Host Protected Areas (HPA)
An HPA is an area of the hard drive that is not normally visible to an OS, introduced in 2001 this area is used so that computer vendors could store data taht a user cannot damage by dormatting. HPA can be used to hide data

### Investigative Process
**READ_NATIVE_MAX_ADDRESS** returns number of physical sectors - **These can be accessed using ATA commands in identification tools such as ATATool by data Synergy. EnCase, or Forensic Toolskit by access data**
**IDENTIFY_DEVICE** returns number of sectors that a user can access 
Difference shows exisitence and extend of HPA

https://www.datasynergy.co.uk/products/misc/atatool.aspx - Tool for using ATA commands | used by law enforcement, forensic experts, etc

### Creating HPA
**SET_MAX_ADDRESS** limits user access to last sectors 
Rerunning it with maximum physical address unlocks HPA
Volatility bit determines whether HPA exisits after the disk is shut down and restarted
This can be used to temporairly unlock an HPA

# Device Configuration Overlay (DCO)
Introduced in the ATA-6 Standard
A hidden area on HDD's (like HPA)
Limits the apparent maximum number of physical sectors
Not accessible by bios, os, or user
Certian tools can be used to modify the HPA or DCO
**DEVICE_CONFIGURATION_IDENTIFY**

### HPA and DCO: 
![[Pasted image 20220228104802.png]]

# Hard Drives
Must be setup as Master/Slave
On the primary controller, the master drive must be the bootable drive
The secondary controller normally uses the CD-ROM as the master drive
**CD-ROM -** Pressed optical compact disk that contains data, stands for compact disk read-only memory


# Partitioning and Formatting
## Partitions - A way of dividing a hard drive
Partitions do not see each other, could have 1 to 24 logical drives from C: to Z:

Why use partitions?
DOS requires partitions to divide up hard drives
Organizes your hard drive 
It can allow for more than 1 OS (Dual-Booting)

Process: Electronically subdividing the physical hard drive into groups of cylinders called partitions. A hard drive must have at least one partition. Partitioning enables organization of a drive. The boot sector is the first sector of the physical drive and contains information regarding the master boot record **(MBR)** and the partition table. The **two types** of partitions are **primary partition** and **extended partition**.

## Primary Partitions
- Store the operating system 
- A hard drive can have up to four primary partitions
- An active partition is a partition on which the MBR looks out for the operating system
- Only one primary partition can be active at a time

## Extended Partitions
- Not bootable and one hard drive can have only one extended partition
- They are optional 
- they can be divided into many logical drives


# The Boot Sector
- Contains 2 pieces of infomation: MBR - takes control of boot process from POST, and parition table which lists all partitions on the drive

# Volume Boot Sector
* Stores information on the location of the OS boot files

# Master Boot Record (MBR)
- MBR always located in the first sector of the booting device (windows only)
- Located:  Cylinder 0, Head 0, Sector 1
- Is loaded into memory, then relocates itself in order to make room for another copy
- Starting at offset 0x1be 16GB partition table
- last two bytes of sector are 0x55 and 0xaa or "55 AA"

The MBR is nto located in a partition: it is located at a first sector of the device (physical offset 0), preceding the first partition. The boot sector present on a non-partitioned device or within an individual partition is called a volume boot record instead.

The MBR is created when a hard drive is partitioned, but it's not located  
within a partition. This means non-partitioned storage mediums, like  
floppy disks, don't contain a master boot record. The master boot record  
is located on the first sector of a disk


**What is the function of MBR?**  
▪ The Master Boot Record (MBR) is the information in the first sector of  
any hard disk or diskette that identifies how and where an operating  
system is located so that it can be boot (loaded) into the computer's  
main storage or random access memory.

**Details**
What is the size of MBR?  
▪ The MBR (Master Boot Record) is 512 bytes.  
▪ Anyway you have to backup hole 512 bytes of MBR with dd (disk-to-disk)  
command.  
▪ An active partition starts with the value (80h) which indicates to standard  
active partition in the MBR sector  
▪ Other partitions are considered as non-active partitions since they are  
starting with the value (00)

▪ MBR is common for external USB drives (memory sticks, removable hard drives, SD-cards and Linux Systems)  
▪ MBR is located in Sector 0 and contains the Marster Partition Table (MPT)  
▪ MBR has a flag 0x55AA at the end of the sector  
▪ MPT can accommodate up to 4 partition entries (Primary or Extended)  
▪ MPT is 64 Bytes Long  
▪ MBR starts at offset 446 bytes from the beginning.  
▪ offset 0 (1st byte) - boot indicator (0x80 - bootable partition, OS system partition)  
▪ offset 4 (5th byte) - indicates file system  
▪ offset 8-11 (9th to 12th bytes) Starting Sector of the partition  
▪ offset 12-15 (13th to 16th bytes) Partition Size (in sectors)

MBR Values for Partition Type File Systems  
0x07 - NTFS  
0x0C - FAT32  
0x83 - Linux Native  
0x82 - Linux Swap  
0x05 - Extended Primary partition  
https://en.wikipedia.org/wiki/Partition_type
 [Lab](<D:\Desktop\Fleming College\Semesters\Semester IV(Current)\Digital Investigation\Labs\Lab 1\Lab1-MBR.docx>)

# Acqusition - Imaging Drives | Week 3

## Physical Security of Media
Should not store or transport the original media where there is any possibility of: where there is any possibility of:  
	- magnetic interference from external sources could magnetic interference from external sources could  
		affect the magnetic media. affect the magnetic media.  
	- moisture or dampness could affect the magnetic moisture or dampness could affect the magnetic  
	media.

Always store the original magnetic media in a Always store the original magnetic media in a secure location where someone could not either secure location where someone could not either purposefully or innocently access the media.

## Logical Security of Media
An examiner should always be very concerned about inadvertently causing a concerned about inadvertently causing a write to the original mediawrite to the original media  

Booting – changes MAC timesBooting – changes MAC times  
Booting – permits processes to runBooting – permits processes to run  
Never Boot a suspect driveNever Boot a suspect drive

## Destructive Process & Viruses
Do not remove, because removing alters the original media. 
How does an examiner bypass the problem - Do not work on the original work on the original media
Controlled alterations can be made to the copy

## Simple Mistakes
Inexperienced examiners may attempt to prevent alterations by placing the original media in their examination computer as the second non-boot drive.

Will this remove the problem of having it boot up????

Windows OS will access all drives connected in the computer during the boot process. 
The OS’s recycle bin will search all non-removable drives for a \RECYCLED directory
–Will incorporate the boot drive’s recycle bin with the non-boot drive’s recycle bin. 
If no recycle bin is found on the non-boot drive,
–The boot drive will create a \RECYCLED directory on the non-boot drive and
–Incorporate the boot drive’s recycle bin on the non-boot drive.

Many other applications or functions automatically access the non-bootable drive.  
Disable the “Fast Find” and “Task Scheduler” features.  
These are defaults during the installation of Windows, and they will access a non-boot drive to index files and check for tasks.   
Virus scanners and similar applications may also scan the non-boot drive.  
If a file is accessed in the Windows GUI, at the least, the Last Access Date will be changed. 

## Types of copy
Image File 
- DD,Encase, FTK,SMART

Bit Stream Copy
- DD,Ghost
- Safeback,Snapback
- Diskdupe,Paraben
- Smart

bit-stream disk-to-image file
- Most common appraoch

bit-steam disk-to-disk
- When disk-to-image copy is not possible

sparse data copy of an object
- Creates exact copies of active sectors
- Used for large disks

**Why not DOS Copy (logical copy)**
- Will only transfer valid DOS/Windows files.
- Will not transfer erased files.
- Will not transfer files hidden from DOS/Windows.
- Will not transfer the file slack.
- Will not transfer the data in unallocated space. 

**Why an EXACT copy?**
- Prevents any alterations to media
- Ensures all of the data present on the seized media is available for examination. 
- Assists in defending against allegations of loss or destruction of data by the forensic examiner.
- Allows controlled alterations of the imaged computer media, i.e. undeleting files.
- If destructive processes occur because of "booby traps" or if inadvertent alterations of the seized media occur, a new image copy can be made from the original. 
 

**Bitstream copies**
A bitstream copy is frequently referred to as a duplicate image, mirror image or exact copy.  

A bitstream copy is an exact copy of a HDD or partition. 
It is essentially a sector by sector copy, from the first sector of the drive or partition to the last sector of the drive or partition.

**To mount or not to mount**
##### A bitstream copy can be viewed with FTK imager for example
- View deleted files and fragments
- Examine un-allocated and slack space

##### Or the image can be mounted like a physical disk
- View files using native application
- Run AV against the disk
- Scripted analysis
- Copy files (using explorer if you must)

## Safe handling 
The original media must be preserved from physical access and the alteration of the logical data.  

Physically store the media as if it is a valuable article in a locked, controlled secure location with limited or logged access.  The examiner is responsible for the “chain of custody” once the examiner gains possession of the media.

## Statistics
	- 69% of users use disk images rather than disk copies and 20% use partition images.
	- 48% of copies and images are made in the field and 36% are made in laboratories.
	- 55% of the drives imaged are larger than 500GB, 15% 1TB+ and 30% are less than that size.
	- 30% of the drives are IDE and 70% SATA.
	- 25 to 33% of users sometimes mix IDE and SCSI drives in making images or copies, 25% often do so, and 13% always do.


## Drive Imaging Tools
SafeBack (www.forensics-intl.com)
Ghost (www.symantec.com)
Newest version of Ghost has a forensic “switch” now
DD (standard unix/linux utility)
	# dd if=device of=device bs=blocksize
Encase (www.encase.com)
Mareware
FTK (www.accessdata.com)	

## Things to consider
- size of the source object
- compression might be useful
- use digital signatures for verification
- whether you can retain the disk
- how much time you have
- location of the evidence

## Image Integrity
evidentiary issues – doing anything with the object to be imaged under Windows will alter some things (logs, swap space, last modified or last accessed dates, etc.)

especially true of rebooting – if you image an object, reboot and image it again, the images will have different hash values

does it matter? the key is being able to say this is the same disk that was seized

## Imaging Utilities
Acquire
- generate dd command line from your choice
- runs dd under Cygwin
- will create an image of RAM

FTK Imager
- bit-stream disk-to-image copies at logical partition and physical drive level - can segment image
- generate dd, SMART and enCase images
- supports image compression (if you pay)

 [Lab](<D:\Desktop\Fleming College\Semesters\Semester IV(Current)\Digital Investigation\Labs\Lab 2\Lab2-Imaging.docx>)


# USB Forensics / Tracking | Week 4
**Purpose**
- Determining usage of a known USB storage device on a computer system or systems.  
- Collecting identifiers of an unknown USB storage device from a computer system.

## HKEY_LOCAL_MACHINE (HKLM)
![[Pasted image 20220228132933.png]]


 ## HKLM\System\{CurrentControlSet}\Enum\USBSTOR
 ![[Pasted image 20220228133012.png]]

 ## HKLM\System\{CurrentControlSet}\Enum\USBSTOR
 ![[Pasted image 20220228133100.png]]

 ## HKLM\SYSTEM\{Current Control Set}\Enum\USB
 ![[Pasted image 20220228133116.png]]

 ## HKLM\SYSTEM\{Current Control Set}\Enum\USB
![[Pasted image 20220228133144.png]]

## Summary USB/USBSTOR
![[Pasted image 20220228133204.png]]

•Insertion Dates  
•First Insert = Last written LogConf, Device  
Parameters  
•Last Insert = Devices unique identifier under USB  
key  
•Other interim insertion dates possible.  
•(Devices unique identifier under USBSTOR key)

## HKLM\SYSTEM\{CurrentControlSet}\Enum\Storage \Volume
![[Pasted image 20220228133229.png]]

## HKLM\System\MountedDevices
Maps Storage media to Drive letters and Volume  
GUIDs.  
•On Windows 7+ USB devices are mapped using the  
Unique Identifier from the USBSTOR subkeys.  
•On XP the ParentIdPrefix vaklue is used to map USB  
drives to a drive letter and Volume GUID.  
•Volume GUID survive even when a drive letter is  
reassigned.
![[Pasted image 20220228133252.png]]

![[Pasted image 20220228133302.png]]

## HKLM\SOFTWARE\Microsoft\Windows Portable Devices\Devices
![[Pasted image 20220228133327.png]]

## NTUSER.DAT\Software\Microsoft\Windows\ CurrentVersion\Explorer\MountPoints2
•Contains Volume GUID entries for volumes mounted  
while profile logged in.  
•If Ampersand in 2nd character it is not a unique GUID  
•Last Written = last insertion before a reboot.  
•Can assist in attributing the USB device to a User Profile.
![[Pasted image 20220228133358.png]]

## Registry Review
HKLM\System\{Current Control Set}\Enum\USB HKLM\  
System\{Current Control Set}\Enum\USBSTOR  
–Vendor ID, Product ID  
–Manufacturer, Product  
–iSerial  
–First Insertion  
–Last Insertion (Windows 7 only)

•Mounted Devices (System hive)  
–Drive Letter  
–Volume GUID  
•MountPoints2 (NTUSER.DAT)  
–Identify active profile during insertion.  
–An insertion date. (Win 7)  
–Last insertion (XP)

Command Line
•reg query hklm\system\currentcontrolset\enum\  
usbstor /s  
•c:\> reg query hklm\system\currentcontrolset\  
enum\usbstor /s | find /i "Disk&Ven"

PowerShell
•PS C:\> gci -r HKLM:\SYSTEM\  
CurrentControlSet  
•PS C:\> gci -r HKLM:\SYSTEM\  
CurrentControlSet\Enum\USBSTOR | select  
name  
•Remember output commands ie out-gridview  
or Export-CSV

Setupapi.log / Setupapi.dev.log
• C:\Windows\Setupapi.log -WinXP  
• C:\Windows\inf\Setupapi.dev.log -Win7,  
Vista  
• Provides first insertion date  
• Contains enough information to Identify  
device  
• Date is less transient – text based

## C:\Windows\inf\Setupapi.dev.log Windows 7
![[Pasted image 20220228133528.png]]

## Event Logs
Entries available in Vista, Win7 System Logs  
Event ID’s 20001, 20003, 24576, 24577
![[Pasted image 20220228133546.png]]

W10 Issues  
•No longer persistent  
•W10 will periodically clean up the  
•USB and USBSTOR Keys

Tools  
•Nirsoft  
•Woanware  
•USBDetective  
–This can extract data after W10 cleanup  
–Relies on multiple time stamps and data points  
•We can also rely on VSS

Keyword Search
![[Pasted image 20220228133623.png]]

 [USB Data Demo](<D:\Desktop\Fleming College\Semesters\Semester IV(Current)\Digital Investigation\Labs\Lab 3\USB-info.pdf>)
 [Lab](<D:\Desktop\Fleming College\Semesters\Semester IV(Current)\Digital Investigation\Labs\Lab 3\Lab3_USB.docx>)

# File Carving | Week 5
## What is it?
File carving is a process used by computer forensic experts to extract data from a disk drive or other storage media without te assistance of the file system that originally created it.

A method that recovers files at unallocated spaces without any file information.

"Carving" is the general term used for extracting structured data our of the raw data, based on format specfifc characteristics.

It is most often used to recover files from the unallocated drive - unallocated space is the area of a drive which no longer holds any file information as indicatd by the file systems structures like the file table.

## Why is it useful?
▪ Great for recovering files and fragments of files when directory entries are corrupted or  missing.  
▪ Law Enforcement can often recover more images from a suspects hard drive by using  
carving techniques

## Techniques
▪ Most common general file carving techniques are...  
1. Header-footer or header-“maximum file size” carving—Recover files  
based on known headers and footers or maximum file size  
2. File structure-based carving.  
3. Content-based carving

## Header-footer or header-“maximum file size” carving —  Recover files based on known headers and footers or maximum file size
▪ JPEG—”\xFF\xD8′′ header and “\xFF\xD9” footer  
▪ GIF—”\x47\x49\x46\x38\x37\x61′′ header and “\x00\x3B” footer  
▪ PST—”!BDN” header and no footer  
▪ If the file format has no footer, a maximum file size is used in the carving program

## File structure-based carving
▪ This technique uses the internal layout of a file  
▪ Elements are header, footer, identifier strings, and size information

## Content-based carving
▪ Content structure is loose (MBOX, HTML, XML)  
▪ Content characteristics  
▪ Character count  
▪ Text/language recognition  
▪ White and black listing of data  
▪ Statistical attributes (Chi^2)  
▪ Information entropy

## Tools 
Tools widely used for file carving: Data recovery tools play an important  
role in most forensic investigations because smart malicious users will  
always try to delete evidence of their unlawful acts. Some important data  
recovery tools are:  
▪ FTK  
▪ Encase  
▪ Scalpel  
▪ Foremost  
▪ F-Engrave  
▪ PhotoRec  
▪ Revit  
▪ TestDisk  
▪ MagicRescue

## File signatures
https://www.garykessler.net/library/file_sigs.html

JPG  
▪ What does it start with?  
▪ Typically a JPG (JPEG) file starts with... (A Header)  
FF D8 FF E0
![[Pasted image 20220228135337.png]]


▪ What does it end with?  
▪ Typically a JPG (JPEG) file ends with... (A Trailer)  
FF D9
![[Pasted image 20220228135411.png]]

