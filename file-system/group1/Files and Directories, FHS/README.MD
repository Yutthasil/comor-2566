![Cabinet](/Assets/Files%20and%20Directories,%20FHS.jpg)

## เนื้อหาในหัวข้อนี้
* [Filesystem](#filesystem)
* [Root Directory](#root-directory)
  * [`/bin`](#bin)
  * [`/boot`](#boot)
  * [`/dev`](#dev)
  * [`/etc`](#etc)
  * [`/home`](#home)
  * [`/lib`](#lib)
  * [`/lost+found`](#lostfound)
  * [`/media`](#media)
  * [`/mnt`](#mnt)
  * [`/opt`](#opt)
  * [`/proc`](#proc)
  * [`/root`](#root)
  * [`/sbin`](#sbin)
  * [`/usr`](#usr)
  * [`/var`](#var)
  * [`/srv`](#srv)
  * [`/tmp`](#tmp)
  * [คำสั่งใน `/bin`](#คำสั่งใน-bin)
* [File types](#file-types)
  * [Regular file](#regular-file)
  * [Directories](#directories)
  * [Hard links](#hard-links)
  * [Character and block device files](#character-and-block-device-files)
  * [Local Domain Sockets](#local-domain-sockets)
  * [Named pipes](#named-pipes)
  * [Symbolic links](#symbolic-links)
* [อ้างอิง](#references)

# Filesystem
Filesystem หมายถึง วิธีการจัดการและโครงสร้างข้อมูลที่ระบบปฏิบัติการใช้ในการติดตามดูไฟล์บนดิสก์หรือพาร์ติชัน หรือก็คือเป็นวิธีการจัดระเบียบไฟล์บนดิสก์ คำนี้ยังใช้กับพาร์ติชันหรือดิสก์ที่ใช้เก็บไฟล์ หรือประเภทของระบบไฟล์อีกด้วย

# Root Directory
![FSH](/Assets/GNU-Linux_directory_tree.png)
* Linux มีโครงสร้าง directory เป็นแบบลำดับชั้นเดียว (Single hierarchical directory) นั้นก็คือทุกอย่างเริ่มต้นจาก root directory หรือก็คือเครื่องหมาย `/` จากนั้นขยายไปเป็น directory รองต่างๆ ซึ่งจะ ต่างจากระบบปฏิบัติการ Window ที่จะมี "ไดรฟ์" ต่างๆ เช่น A, B, C, D, E เป็นต้น โดย Linux จัดเรียง directory ที่ถัดจาก root directory ตามลำดับความสำคัญในกระบวนการบูธจากมากไปน้อย

โครงสร้างมาตรฐานของ root directory (`/`) ที่กำหนดโดยมาตรฐาน Filesystem Standard (FSSTND) จะมี
### Directory ที่จำเป็นดังต่อไปนี้

| Directory  | คำอธิบาย                            |
|-------|---------------------------------------|
| [`/bin`](#bin)   | เก็บ library คำสั่งพื้นฐานที่จำเป็นสำหรับการทำงานของระบบเบื้องต้น |
| [`/boot`](#boot)  | เก็บไฟล์ที่เกี่ยวข้องกับการบูธเครื่อง                     |
| [`/dev`](#dev)   | เก็บไฟล์พิเศษที่มีความเกี่ยวข้องกับ device ที่เชื่อมต่อกับระบบ                 |
| [`/etc`](#etc)   | เก็บไฟล์ system config ของ host                  |
| [`/lib`](#lib)   | รวม library ที่ใช้ร่วมกันที่จำเป็นและโมดูลเคอร์เนล              |
| [`/media`](#media) | ไลบรารีสำหรับสื่อแบบถอดได้ เช่น ไดรฟ์ USB               |
| [`/mnt`](#mnt)   | เป็น directory สำหรับเชื่อมต่ออุปกรณ์เก็บข้อมูลแบบชั่วคราวหรือแบบ removable เช่น USB เป็นต้น                   |
| [`/opt`](#mnt)   | ใช้เก็บโปรแกรมส่วนขยายอื่นๆ หรือโปรแกรมประเภท third party software ที่ไม่ได้ถูกติดตั้งมาตั้งแต่แรกกับระบบ                           |
| [`/sbin`](#sbin)  | สำหรับเก็บ library หรือ command line tool ที่ใช้ได้เฉพาะ root user                        |
| [`/srv`](#srv)   | เก็บข้อมูลสำหรับ service ที่ให้บริการโดยระบบ                        |
| [`/tmp`](#tmp)   | เก็บไฟล์ชั่วคราว                                       |
| [`/usr`](#usr)   |ลำดับชั้นรอง  (Secondary hierarchy) สำหรับไฟล์และโปรแกรมที่เกี่ยวข้องกับผู้ใช้ส่วนใหญ่     |
| [`/var`](#var)   | เก็บไฟล์ที่มีการเปลี่ยนแปลงไฟล์ชั่วคราวที่สร้างโดยโปรแกรมหรือผู้ใช้ เช่น log หรือ spool files                       |

### Directory เพิ่มเติมดังต่อไปนี้
| Directory  | คำอธิบาย                             |
|-------|---------------------------------------|
| [`/home`](#home) | Home directory ของผู้ใช้                     |
| [`/lib`](#lib)  | เก็บ library สำหรับการทำงานของโปรแกรม |
| [`/root`](#root) | Home directory สำหรับ root user              |


* โดยไดเร็กทอรีอื่นๆใน root directory ทั้งหมดถือว่าเป็น "children" ของ root directory (`/`) ซึ่งพาร์ติชันที่มีร root file system จะถูกโหลดเป็นอันดับแรกในตอนบูตระบบ และระบบจะไม่สามารถบูตได้หากไม่พบพาร์ติชันนี้

# /bin
คำสั่งพื้นฐานที่จำเป็นสำหรับการทำงานของระบบ 
ไดเร็กทอรี /bin สามารถใชัได้โดยทั้ง root user และ ผู้ใช้ปกติ โดยจะมีคำสั่ง shell bash ใช้ทั่วไป เช่น cp, mv, rm, cat, ls เป็นต้น

| คำสั่ง | คำอธิบาย |
|---|---|
| [`chmod`](#chmod)| เปลี่ยนแปลงสิทธิ์การเข้าถึงไฟล์ |
| [`chown`](#chown) | เปลี่ยนแปลงเจ้าของและกลุ่มของไฟล์ |
| [`cp`](#cp) | คัดลอกไฟล์และไดเร็กทอรี |
| [`date`](#date) | แสดงวันที่และเวลา |
| [`dd`](#dd) | แปลง(convert) และคัดลอก(copy) ไฟล์ |
| [`df`](#df) | แสดงการใช้พื้นที่ดิสก์ของระบบไฟล์ |
| [`dmesg`](#dmesg) | เป็นการให้แสดงผลเหมือนตอน Boot |
| [`echo`](#echo) | แสดงข้อความออกทางหน้าจอ |
| [`false`](#false) | คืนค่าสถานะทำงานผิดพลาด |
| [`hostname`](#hostname) | แสดงหรือตั้งชื่อโฮสต์ของระบบ |
| [`kill`](#kill) | คำสั่งสำหรับยกเลิก Process |
| [`ln`](#ln) | สร้างลิงก์ระหว่างไฟล์ |
| [`login`](#login) | เริ่มเซสชันบนระบบ |
| [`ls`](#ls) | แสดงรายการเนื้อหาของไดเร็กทอรี |
| [`mkdir`](#mkdir) | สร้างไดเร็กทอรี |
| [`mknod`](#mknod) | สร้างไฟล์พิเศษแบบบล็อกหรืออักขระ |
| [`more`](#more) | แสดงข้อความทีละหน้า |
| [`mount`](#mount) | ใช้ในการเมาท์ระบบไฟล์จากอุปกรณ์จัดเก็บข้อมูล เช่น ฮาร์ดดิสก์ หรือดิสก์ USB |
| [`mv`](#mv) | ย้าย/เปลี่ยนชื่อไฟล์ |
| [`ps`](#ps) | แสดงสถานะของกระบวนการ |
| [`pwd`](#pwd) | แสดงชื่อไดเร็กทอรีทำงานปัจจุบัน |
| [`rm`](#rm) | ลบไฟล์หรือไดเร็กทอรี |
| [`rmdir`](#rmdir) | ลบไดเร็กทอรี |
| [`sed`](#sed) | ตัวแก้ไขข้อความแบบสตรีม |
| [`sh`](#sh) | คำสั่งเรียกใช้ Bourne again shell ของระบบ Unix,Linux |
| [`stty`](#stty) | แก้ไขการตั้งค่าของการแสดงผลทาง terminal หรือ print การตั้งค่าของ terminal ณ ปัจจุบัน|
| [`su`](#su) | เปลี่ยน user login |
| [`sync`](#sync) | flush บัฟเฟอร์เขียนลง disk เพื่อให้ค่าใน cache กับค่าในที่เก็บข้อมูลตรงกัน |

# /boot
&nbsp;&nbsp;&nbsp;&nbsp;boot directory นั้นเก็บไฟล์ทั้งหมดที่เกี่ยวข้องและใช้งานในกระบวนการบูธ โดย /boot จะถูกใช้ก่อนที่ kernel จะ execute user-mode program แต่ก็จะมีไฟล์บางไฟล์ที่ไม่ได้ใช้ในตอนบูธ เช่น configuration file (GRUB) และ map installer

&nbsp;&nbsp;&nbsp;&nbsp;ตามที่กล่าวไปข้างต้นที่ /boot จะเก็บสิ่งที่ใช้งานก่อนที่ kernel จะ execute user-mode program ซึ่งไฟล์ที่ถูกเรียกใช้เหล่านี้อาจรวมไปถึงไฟล์ backup ของคำสั่งที่ใช้ในกระบวนการ boot หลัก, Sector/system map files (ไฟล์ข้อมูลเกี่ยวกับ disk layout), คำสั่งหลักของระบบปฏิบัติการ และ boot ไฟล์อื่นๆที่เราไม่สามารถแก้ไขได้โดยตรง คำสั่งที่ทำการจัดเรียงลำดับสำหรับ boot loader เพื่อให้ boot ได้นั้นจัดเก็บไว้ใน /sbin, ไฟล์ config สำหรับ boot loader จัดเก็บไว้ใน /etc และ system kernel จะอยู่ใน / หรือไม่ก็ใน /boot (ตาม Debian จะเป็น /boot แต่จริงๆแล้วเป็น symbolic link ไปที่ / ตามหลักมาตรฐาน FSSTND)  

ถ้าหากเราลองใช้คำสั่ง `ls` แสดงรายการของสิ่งที่อยู่ใน directory ก็จะมีไฟล์ประมาณนี้ : 

![boot_dir](/Assets/boot_dir_ls.png)

 * `config−kernel−version`
จัดเก็บข้อมูลการ config ของ kernel ซี่งเป็นไฟล์ที่มีความสำคัญมากเมื่อ compile kernel บนระบบหรือ device module อื่น โดยไฟล์นี้ถูกสร้างขึ้นมาอัตโนมัติและเราไม่ควรไปแก้ไขมันโดยตรงๆ
สี่งที่อยู่ในไฟล์ config ก็จะมีประมาณนี้ : 
```
CONFIG_DM_ERA=m
CONFIG_DM_CLONE=m
CONFIG_DM_MIRROR=m
CONFIG_DM_LOG_USERSPACE=m
CONFIG_DM_RAID=m
CONFIG_DM_ZERO=m
CONFIG_DM_MULTIPATH=m
CONFIG_DM_MULTIPATH_QL=m
CONFIG_DM_MULTIPATH_ST=m
CONFIG_DM_MULTIPATH_HST=m
CONFIG_DM_MULTIPATH_IOA=m
CONFIG_DM_DELAY=m
# CONFIG_DM_DUST is not set
CONFIG_DM_INIT=y
CONFIG_DM_UEVENT=y
CONFIG_DM_FLAKEY=m
CONFIG_DM_VERITY=m
...
```
 * `System.map-VERSION` :
เป็นเหมือน look-up table สำหรับ matching ค่าและ function กับพื้นที่ใน memory ซี่ง content ที่อยู่ด้านในจำเป็นต้องเป็น superuser ที่สามารถเห็นได้
```
ffffffff839217f0 d __event_enter__openat2
ffffffff839217f8 d __event_exit__openat
ffffffff83921800 d __event_enter__openat
ffffffff83921808 d __event_exit__open
ffffffff83921810 d __event_enter__open
ffffffff83921818 d __event_exit__fchown
ffffffff83921820 d __event_enter__fchown
ffffffff83921828 d __event_exit__lchown
ffffffff83921830 d __event_enter__lchown
ffffffff83921838 d __event_exit__chown
ffffffff83921840 d __event_enter__chown
ffffffff83921848 d __event_exit__fchownat
ffffffff83921850 d __event_enter__fchownat
ffffffff83921858 d __event_exit__chmod
...
```
 * `vmlinuz−kernel−version` :
 โดยปกติจะเป็น kernel หรือ symbolic link ไปที่ kernel
 * `/grub` :
 เป็น subdirectory ที่มีไฟล์ GRUB configuration รวมถึง boot-up image<br>&nbsp;&nbsp;&nbsp;&nbsp;
 GNU GRand Unified Boot loader (GRUB) คือ เป็นระบบ boot ที่ทำโดย GNU project ซี่งเป็น program ที่ทำให้สามารถเลือกระบบปฏิบัติการที่ลงไว้หรือ kernel เพื่อทำการโหลดตอนกระบวนการ boot และทำให้ user สามารถส่ง argument ไปยัง kernel ได้

# /dev

`/dev` จัดเก็บไฟล์พิเศษที่เกี่ยวข้องกับ device หรืออุปกรณ์ต่อพ่วงอื่นๆ โดยไฟล์ใน directory นี้จะเป็นเหมือน interface เพื่อให้สามารถ interact กับอุปกรณ์ hardware เช่น harddrive, CD-ROM, speakers, printers หรือ modems ได้

โดย `/dev` มี subdirectory อยู่หลายอัน ซึ่งแต่ละอันก็จัดเก็บไฟล์ device ที่เกี่ยวข้องกับ device บางแค่ประเภท อย่างเช่น `/dev/disk/id-by-uuid` จัดเก็บไฟล์ device สำหรับ harddisk ที่มีชื่อตาม universally unique identifier (UUID) ซึ่งไฟล์ device พวกนี้ใน subdirectory เป็น symbolic link ไปยังไฟล์ device ใน `/dev` ทำให้เราสามารถเข้าถึง device ได้โดยใช้ไฟล์ใน `/dev` หรือไฟล์ที่อยู่ใน `/dev/disk/id-by-uuid` เป็นต้น

ถ้าเราลอง ls -l เพื่อแสดงรายการไฟล์ใน /dev มา จะได้ผลลัพธ์ดังนี้ : 
```
crw-r--r-- 1 root root     10, 235 Feb  8 19:09 autofs
drwxr-xr-x 2 root root         320 Feb  8 19:14 block
drwxr-xr-x 2 root root          80 Feb  8 19:09 bsg
crw-rw---- 1 root disk     10, 234 Feb  8 19:09 btrfs-control
drwxr-xr-x 3 root root          60 Feb  8 19:09 bus
lrwxrwxrwx 1 root root           3 Feb  8 19:09 cdrom -> sr0
drwxr-xr-x 2 root root        3760 Feb  8 19:09 char
crw--w---- 1 root tty       5,   1 Feb  8 19:09 console
lrwxrwxrwx 1 root root          11 Feb  8 19:09 core -> /proc/kcore
drwxr-xr-x 6 root root         120 Feb  8 19:09 cpu
crw------- 1 root root     10, 124 Feb  8 19:09 cpu_dma_latency
crw------- 1 root root     10, 203 Feb  8 19:09 cuse
drwxr-xr-x 7 root root         140 Feb  8 19:09 disk
brw-rw---- 1 root disk    253,   0 Feb  8 19:09 dm-0
drwxr-xr-x 2 root root          60 Feb  8 19:09 dma_heap
drwxr-xr-x 3 root root         100 Feb  8 19:09 dri
crw------- 1 root root     10, 126 Feb  8 19:09 ecryptfs
crw-rw---- 1 root video    29,   0 Feb  8 19:09 fb0
lrwxrwxrwx 1 root root          13 Feb  8 19:09 fd -> /proc/self/fd
crw-rw-rw- 1 root root      1,   7 Feb  8 19:09 full
crw-rw-rw- 1 root root     10, 229 Feb  8 19:09 fuse
crw------- 1 root root    238,   0 Feb  8 19:09 hidraw0
crw------- 1 root root     10, 228 Feb  8 19:09 hpet
drwxr-xr-x 2 root root           0 Feb  8 19:09 hugepages
crw------- 1 root root     10, 183 Feb  8 19:09 hwrng
crw------- 1 root root     89,   0 Feb  8 19:09 i2c-0
lrwxrwxrwx 1 root root          12 Feb  8 19:09 initctl -> /run/initctl
drwxr-xr-x 4 root root         340 Feb  8 19:09 input
crw-r--r-- 1 root root      1,  11 Feb  8 19:09 kmsg
lrwxrwxrwx 1 root root          28 Feb  8 19:09 log -> /run/systemd/journal/dev-log
brw-rw---- 1 root disk      7,   0 Feb  8 19:09 loop0
brw-rw---- 1 root disk      7,   1 Feb  8 19:09 loop1
brw-rw---- 1 root disk      7,   2 Feb  8 19:09 loop2
brw-rw---- 1 root disk      7,   3 Feb  8 19:09 loop3
...
```
จะเห็นว่ามีบางไฟล์ที่ขึ้นว่าเป็นประเภท b (block) หรือ c (character) โดย device เหล่านี้จะมีเลขที่เกี่ยวข้องกับมันอยู่แทนที่จะเป็นขนาดไฟล์ ซึ่งเลขเหล่านี้เป็นตัวระบุ device ให้กับระบบ

# /etc

`/etc` เป็นเหมือนมันสมองของระบบ จัดเก็บไฟล์การตั้งค่าทั้งหมดที่เกี่ยวข้องกับระบบไว้ทั้งใน /etc และใน subdirectory ซึ่งไฟล์การตั้งค่าหรือไฟล์ configuration ที่ใช้ควบคุมการทำงานของโปรแกรม โดยเราควรที่จะ backup directory นี้บ่อยๆเพื่อถ้าเราลงระบบปฏิบัติการใหม่หรือ config สูญหายจะได้ไม่ต้องเสียเวลา config ใหม่

### ตัวอย่าง file หรือ subdirectory ใน /etc
* /etc/fstab : เป็นไฟล์ config สำหรับการ `mount` และ `supermount` (mount คือการเชื่อมต่อ file system ของอุปกรณ์เก็บข้อมูล เช่น USB, flashdrive หรือ harddisk เข้ากับ directory ที่เจาะจง) ซึ่งไฟล์นี้จะแสดงรายการ file system ที่ถูก mount อัตโนมัติตอน startup ด้วยคำสั่ง `mount -a`
* /etc/passwd : เป็นไฟล์ที่จัดเก็บ password ของ user ที่ถูกเข้ารหัสและมีข้อมูลที่เกี่ยวข้องกับ user อื่นๆเช่น username, home directory เป็นต้น
```
usbmux:x:113:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
nitruzx:x:1000:1000:Tj:/home/nitruzx:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
mgr01:x:1001:1001::/home/mgr01:/bin/sh
mgr02:x:1002:1002::/home/mgr02:/bin/sh
dev01:x:1003:1004::/home/dev01:/bin/sh
dev02:x:1004:1005::/home/dev02:/bin/sh
sale01:x:1005:1007::/home/sale01:/bin/sh
sale02:x:1006:1008::/home/sale02:/bin/sh
Kat1:x:1007:1010::/Kitkat/Kat1:/bin/bash
Kat2:x:1008:1011::/Kitkat/Kat2:/bin/bash
Kat3:x:1009:1012::/Kitkat/Kat3:/bin/bash
Kat4:x:1010:1013::/Kitkat/Kat4:/bin/bash
```
 * /etc/shadow : จัดเก็บ password ของ user ที่เอามาจาก /etc/passwd แต่จตะมีการ hash เพิ่มเข้าไปทำให้ไม่สามารถอ่านได้ยกเว้น root user ทำให้การถูกล่วงรู้ password นั้นยากขึ้น
 * /etc/hosts : ไฟล์นี้ระบุชื่อของเครื่องและ IP โดยอาจมี domain ของบาง IP ซึ่งไฟล์นี้จะมี IP เข้ามาเรื่อยๆหากเครื่องเชื่อมต่อกับ network
 ```
 ::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
 ```
 * /etc/profile : เป็นไฟล์และคำสั่งที่จะถูก execute ณ ตอน login หรือตอน startup โดย Bourn หรือ C shell ทำให้ admin ของระบบสามารถตั้งค่า default ให้กับทุก user ได้
 * /etc/network/ : เป็น subdirector6y ที่เก็บไฟล์การตั้งค่าเกี่ยวกับ network เช่นพวก interface การเชื่อมต่อ หรือ dhcp
 * /etc/networks : แสดงผลรายการของ network ที่เครื่องนี้อยู่ ณ ปัจจุบัน
```
# symbolic names for networks, see networks(5) for more information
link-local 169.254.0.0
```

# /home
&nbsp;&nbsp;&nbsp;&nbsp;ด้วยความที่ระบบปฏิบัติการ Linux ในหนึ่งเครื่องอาจมีผู้ใช้ได้หลายคน ซึ่งแต่ละ user ก็จะมี directory ที่เป็นของตนเอง สามารถเขัาถึงได้เฉพาะตัว user ที่เป็นเจ้าของ directory หรือไม่ก็ root user ซึ่งนั้นก็คือ home directory โดยสามารถเข้าถึงโดย path : `/home/{ชื่อ user}`

&nbsp;&nbsp;&nbsp;&nbsp;user จะสามารถทำอะไรก็ได้ใน home directory ของตนไม่ว่าจะเป็นการสร้างไฟล์, ลบไฟล์, ลง program เพิ่มหรืออื่นๆอีกมากมาย

&nbsp;&nbsp;&nbsp;&nbsp;ใน home directory จะเก็บไฟล์ config ของ user นั้นๆไว้ โดยจะถูกเรียกว่าไฟล์ dot (`.`) เนื่องจากชื่อขึ้นต้นด้วย `.` โดยปกติแล้วไฟล์นี้จะซ่อนไว้อยู่ ถ้าอยากจะเห็นไฟล์นี้จำเป็นต้องตั้งค่าใน file manager หรือใช้คำสั่ง `ls -a` ใน terminal ถ้าการตั้งค่าใน file config ใน home directory กับ file config ในระบบมีส่วนที่ขัดแย้งกัน มันจะยึดตามไฟล์ config ใน home

&nbsp;&nbsp;&nbsp;&nbsp;home directory อาจมีขนาดใหญ่ขึ้นเรื่อยๆ จากการจัดเก็บไฟล์ที่ download มา, ไฟล์จากการ compile, การลง program เพิ่ม, ไฟล์จากเมล, รูปภาพ, เพลง และไฟล์อื่นๆอีกมากมายตามที่ user ต้องการ


# /lib

/lib เก็บ library สำหรับการทำงานของโปรแกรมต่างๆ ประกอบด้วย module ของ kernel และ image library (library ภาษา C) ที่จำเป็นสำหรับการบูตระบบและรันคำสั่งในระบบไฟล์ของรูท เช่น ไฟล์ไบนารีในไดเร็กทอรี /bin และ /sbin 

โดยสามารถระบุ library ได้ง่ายจากนามสกุลไฟล์ .so ซึ่งเทียบเท่ากับไฟล์ DLL (Dynamically Linked Library เป็นชุดของโปรแกรมเล็กๆ ที่โปรแกรมใหญ่สามารถนำไปใช้เมื่อโปรแกรมต้องการทำงานบางอย่างให้สำเร็จ) ในระบบ Windows ซึ่ง library เหล่านี้มีความสำคัญสำหรับการทำงานพื้นฐานของระบบ

module ของ kernel (ไดรเวอร์) จะอยู่ใน subdirectory `/lib/modules/'kernel-version'` ซึ่งเพื่อให้แน่ใจว่าการคอมไพล์ module ทำงานถูกต้อง เราควรตรวจสอบว่า `/lib/modules/'kernel-version'/kernel/build` ชี้ไปที่ `/usr/src/'kernel-version'` หรือไม่
```
.                  groff                                 mime                 rsyslog
..                 grub                                  modprobe.d           sasl2
apparmor           grub-legacy                           modules              sftp-server
apt                hdparm                                modules-load.d       snapd
binfmt.d           init                                  multipath            software-properties
byobu              initcpio                              nagios               ssl
cloud-init         initramfs-tools                       needrestart          sysctl.d
cnf-update-db      kernel                                netplan              systemd
command-not-found  klibc                                 networkd-dispatcher  sysusers.d
compat-ld          klibc-K8e6DOmVI9JpyGMLR7qNe5iZeBk.so  nvidia               tc
console-setup      libdmmp.so                            open-iscsi           terminfo
crda               libdmmp.so.0.2.0                      openssh              tmpfiles.d
cryptsetup         libhandle.so.1                        os-prober            ubiquity
dbus-1.0           libhandle.so.1.0.3                    os-probes            ubuntu-advantage
dpkg               libmpathcmd.so                        os-release           ubuntu-release-upgrader
dracut             libmpathcmd.so.0                      pam.d                udev
environment.d      libmpathpersist.so                    pkgconfig            udisks2
file               libmpathpersist.so.0                  pm-utils             ufw
finalrd            libmultipath.so                       policykit-1          update-notifier
firmware           libmultipath.so.0                     polkit-1             usrmerge
girepository-1.0   linux                                 python2.7            valgrind
git-core           linux-boot-probes                     python3              x86_64-linux-gnu
gnupg              locale                                python3.10           xfsprogs
gnupg2             lsb                                   python3.11
gold-ld            man-db                                recovery-mode
```


# /lost+found

ถ้าหากเครื่องเกิดการ crash หรือเครื่องดับจากสาเหตุอะไรก็ตาม เมื่อสามารถ boot กลับมาได้จะมีการตรวจสอบระบบไฟล์โดยคำสั่ง `fsck` โดย `fsck` จะทำการตรวจสอบระบบทั้งหมดและพยายามกู้คืนไฟล์ที่เสียหายหากพบเจอ ซึ่งผลของการกู้นี้จะมาอยู่ใน /lost+found นี้นั้นเอง

ซึ่งไฟล์ที่กู้คืนมาได้อาจไม่สมบูรณ์เหมือนก่อน แต่ก็อาจจะเป็นส่วนที่สำคัญที่คุ้มค่าจะกู้กลับมา

`/lost+found` มีอยู่ในทุก partition หากพบเจอไฟล์อะไรใน lost+found ให้ลองย้ายมันกลับไปในตำแหน่งที่เดิมของมัน หรือถ้าเราเจอ symbolic link ที่เสียหาย link ไปที่ไฟล์อยู่ เราควรลงไฟล์นั้นใหม่จาก RPM(Red Hat Package Manager) ที่เกี่ยวข้องกับไฟล์นั้น


# /media

directory นี้ประกอบไปด้วย subdirectory ที่จะเป็นจุดเชื่อมต่อระบบไฟล์ของอุปกรณ์สื่อบันทึกที่สามารถถอดออกได้ เช่นพวก แผ่นดิสก์, ซีดีรอม เข้ากับ filesystem ของระบบปฏิบัติการ

สาเหตุที่มี `/media` นี้สืบเนื่องมาจากว่ามันมีหลายที่ที่ถูก mount เช่นใน `/cdrom`, `/mnt` หรือ `/mnt/cdrom` ซึ่งการที่มีการ mount อยู่ใน root directory หลายที่นี้ทำให้ directory มาก `/`
แม้ว่าการใช้ subdirectory ใน `/mnt` เป็นจุด mount เป็นเรื่องปกติในปัจจุบัน แต่ก็ขัดแย้งกับวิธีเก่าที่ใช้ /mnt เป็นจุด mount ชั่วคราว

directory หรือ symbolic link ที่จะต้องมีใน `/media` ถ้าหากมีการลง subsystem ที่เกี่ยวข้อง :
* floppy : ไดรฟ์ดิกส์ก์แบบฟลอปปี
* cdrom : ไดรฟ์ซีดีรอม
* cdrecorder : ตัวเขียนซีดี
* zip : ไดรฟ์ Zip

บนระบบที่มีหลายอุปกรณ์สามารถเชื่อมต่อได้ directory ที่ถูก mount สามารถสร้างได้ โดยการเพิ่มตัวเลขต่อท้ายชื่อที่แสดงอยู่ด้านบน โดย directory โดยตัวเลขนั้นเริ่มต้นด้วย '0' แต่ชื่อที่ไม่ได้ระบุด้านบนก็ยังต้องมีตัวเลขอยู่ อย่างเช่น ชื่อที่ถูกต้องตามมาตรฐานกับไดรฟ์ซีดีรอมสองไดรฟ์ อาจจะมี `/media/cdrom0` และ `/media/cdrom1`


# /mnt

directory นี้เป็นจุดที่ทำการ mount ทั่วไปที่ไม่ว่าจะ mount filesystem หรือ mount device การ mount เป็นกระบวนการที่ทำให้ filesystem สามารถใช้งานได้ในระบบ หลังจากที่ทำการ mount จะสามารถเข้าถึงไฟล์ได้ภายใต้จุดเชื่อมต่อ(mount-point) 

ใน `/mnt` มักประกอบด้วย mount หรือ subdirectory ที่ใช้ต่อฟลอปปีดิสก์และซีดี ซึ่งเรายังสามารถสร้างจุด mount เพิ่มเติมได้ใน `/mnt`ถ้าต้องการ จุด mount มาตรฐาน ได้แก่ `/mnt/cdrom` และ `/mnt/floppy`

เราสามารถสร้างจุด mount ที่ไหนก็ได้บนระบบ แต่ตามธรรมเนียมและเพื่อความสะดวกในการใช้งานจริง เราไม่ควรจะสร้างจุด mount กระจัดกระจายหลายที่ใน filesystem โดยที่ผู้จำหน่ายบางเจ้า เช่น Debian นั้นให้ `/floppy` และ `/cdrom` เป็นจุด mount ในขณะที่ Redhat และ Mandrake ใส่ไว้ใน `/mnt/floppy` และ `/mnt/cdrom` ตามลำดับ

## Mounting

เราจำเป็นต้องทำการ `"mount"` ก่อนที่จะใช้งาน filesystem ระบบ โดยระบบปฏิบัติการจะดำเนินการต่างๆ เพื่อให้แน่ใจว่าทุกการทำงานเป็นไปได้อย่างถูกต้อง เนื่องจากไฟล์ทั้งหมดใน UNIX อยู่ในโครงสร้าง single directory tree การ mount จะทำให้เนื้อหาของระบบไฟล์ใหม่ที่เชื่อมต่อเข้าไปดูเหมือนเป็นเนื้อหาของ subdirectory ภายใน filesystem ที่ mount ไว้อยู่แล้ว

วิธีการใช้คำสั่ง [`mount`](#mount)


# /opt

directory นี้จัดเก็บ software หรือแพ็คเกจส่วนขยายทั้งหมดที่ไม่ได้เป็นส่วนหนี่งในการติดตั้งของ default ตัวอย่างเช่น แพ็คเกจ StarOffice, Kylix, Netscape Communicator และ WordPerfect มักจะพบได้ใน directory นี้

เพื่อให้เป็นไปตามมาตรฐาน FSSTND แอปพลิเคชันของ Third-party ทั้งหมดควรต้องติดตั้งใน directory นี้ โดยแพ็คเกจที่จะติดตั้งที่นี่ จะจัดเก็บเป็นไฟล์ static (เช่น font, clipart ไฟล์ database) ซึ่งเก็บใน subdirectory ของแพ็คเกจนั้นๆ เช่น `/opt/{ชื่อ packet}` หรือ `/opt/{ชื่อผู้ให้บริการ}` (คล้ายกับวิธีที่ Windows จะติดตั้งซอฟต์แวร์ใหม่ลงในไดเร็กทอรีของตัวเอง `C:\Windows\Progam Files\ชื่อโปรแกรม`)


# /proc

/proc ต่างจาก directory อื่นตรงที่มันเป็น virtual filesystem ซึ่งเป็นระบบไฟล์เสมือนของข้อมูล process มันไม่ได้มีไฟล์ที่เป็นไฟล์จริงๆข้างใน แต่เป็นไฟล์ที่เกิดขึ้นตอน runtime หรือตอนที่ระบบ boot และหายไปตอนปิดเครื่อง เป็นไฟล์ที่เก็บข้อมูลของ process ที่รันอยู่ ด้วยเหตุนี้ จึงสามารถมองว่าเป็นศูนย์กลางการควบคุมและเป็นข้อมูลสำหรับ kernel  

&nbsp;&nbsp;&nbsp;&nbsp;คำสั่งของระบบส่วนใหญ่มันเรียกไฟล์ใน directory นี้


# /root

directory นี้เป็น home directory ของ admin หรือก็คือ root user โดยที่แต่ในอดีต `/` คือhome directory ของ admin แต่ เพื่อความเป็นระเบียบมากขึ้น 'root' จึงมีโฮมไดเร็กทอรีเป็นของตัวเอง

แล้วคำถามคือ ทำไมไม่อยู่ใน `'/home'` แทน ซึ่งก็เนื่องจาก `/home` มักจะอยู่บนพาร์ติชันที่แตกต่างกันหรือแม้กระทั่งบนระบบอื่น ซึ่งอาจทำให้ 'root' เข้าถึงไม่ได้หากมีการ mount เฉพาะ `/`

ถึงตามมาตรฐาน FSSTND ก็กล่าวไว้ว่านี้ที่ที่แนะนำสำหรับ home directory ของ root user จะอยู่ แต่ก็ยังกล่าวไว้อีกว่า : 

 * หาก home directory ของ root user ไม่ได้อยู่บนพาร์ติชันของ root จะต้องกำหนดให้ default เป็น `/` หากไม่สามารถค้นหาตำแหน่งได้
 * ไม่แนะนำให้ใช้ root user สำหรับงานที่ผู้ใช้ทั่วไปสามารถทำได้ และควรใช้เฉพาะสำหรับการจัดการดูแลระบบเท่านั้น
 * ด้วยเหตุนี้ แนะนำว่าไม่ควรมี subdirectory สำหรับอีเมลและแอปพลิเคชันอื่นๆ ใน home directory ของ root user และควรนำเมลที่เป็นสำหรับ admin ระบบ เช่น root, postmaster และ webmaster ให้ไปยัง user ที่มีสิทธ์ทั่วไป


 # /sbin

Linux แยกระหว่างโปรแกรมคำสั่งที่ใช้งานทั่วไป กับโปรแกรมคำสั่งที่ใช้สำหรับการ maintain ระบบ หรือของเฉพาะ admin ซึ่งโปรแกรมคำสั่งประเภทหลังจะอยู่ใน directory นี้หรือไม่ก็ใน `/usr/sbin` (สำหรับโปรแกรมคำสั่งที่มีความสำคัญน้อยกว่า) โปรแกรมคำสั่งสำหรับ admin ระบบที่ติดตั้งเองจะถูกวางไว้ใน /usr/local/sbin

โปรแกรมคำสั่งจะถูก execute เมื่อรู้ว่ามีการ mount /usr แล้ว โดยทั่วไปจะอยู่ใน /usr/sbin directory นี้ประกอบด้วย binary ที่จำเป็นต่อการทำงานของระบบ ซึ่งรวมไปถึงโปรแกรมคำสั่งของ admin ระบบ,  เครื่องมือที่ช่วย maintainance และการ config ของฮาร์ดแวร์ ซึ่งคุณอาจพบโปรแกรมคำสั่งเช่น lilo, fdisk, init, ifconfig, ฯลฯ อยู่ที่นี่

อีก directory ที่ประกอบด้วย binary ของระบบคือ `/usr/sbin` ซึ่ง directory นี้ประกอบด้วย binary เพิ่มเติมอื่นๆ ที่เป็นประโยชน์สำหรับผู้ดูแลระบบ คุณจะพบ network daemon สำหรับระบบกับ binary อื่นๆ ที่ปกติแล้วจะมีเฉพาะ admin เท่านั้นที่สามารถเข้าถึงได้ แต่ไม่จำเป็นสำหรับการบำรุงรักษาหรือซ่อมแซมระบบ 

มาตรฐาน FSSTND ก็ได้กล่าวไว้ว่า

>    `/sbin` ควรประกอบด้วย binary ที่จำเป็นสำหรับ boot, restore, recovery และ repair ระบบเท่านั้น โดยเป็นส่วนเสริมจาก binary ใน `/bin`

### binary คือโค้ดคำสั่งที่สามารถรันได้


`/sbin` จะมีไฟล์ต่อไปนี้ หากมีการลง package เพิ่ม:

* `fastboot`: รีบูตระบบโดยไม่ตรวจสอบดิสก์ (optional)
* `fasthalt`: หยุดการทำงานของระบบโดยไม่ตรวจสอบดิสก์ (optional)
* `fdisk`: เครื่องมือจัดการพาร์ติชัน (optional)
* `fsck`: เครื่องมือตรวจสอบและซ่อแซมระบบไฟล์ (optional)
* `fsck.*`: เครื่องมือตรวจสอบและซ่อแซมระบบไฟล์เฉพาะสำหรับ filesystem บางประเภท (optional)
* `getty`: โปรแกรม `getty` <br>(ย่อมาจาก get tty ซึ่งเป็นโปรแกรมที่จัดเตรียม terminal เมื่อมีการตรวจจับการเชื่อมต่อเข้ามา เช่น เมื่อมีการ ssh เข้ามาจะมีการขึ้นหน้าให้ login เข้าเครื่องเพื่อเป็นการระบุตัวตนของ user)(optional)
* `halt`: คำสั่งเพื่อหยุดการทำงานของระบบ (optional)
* `ifconfig`: กำหนดค่าการเชื่อมต่อเครือข่าย network (optional)
* `init`: สร้าง process ของ user-mode โดยจะรันจนกว่าเครื่องจะปิด (optional)
* `mkfs`: คำสั่งสำหรับสร้าง filesystem (optional)
* `mkfs.*`: คำสั่งสำหรับสร้าง filesystem เฉพาะบางประเภท (optional)
* `mkswap`: คำสั่งสำหรับกำหนดพื้นที่ swap <br>(การ swap คือเมื่อ RAM เต็มทำให้ page ที่ยังไม่ถูกใช้งานในหน่วยความจำถูกย้ายไปยัง swap-space ซึ่งอยู่ใน hard drive เพื่อให้มีพื้นที่ RAM เพิ่ม กระบวนการนี้เรียกว่าการ swap) (optional)
* `reboot`: คำสั่งสำหรับรีบูตระบบ (optional)
* `route`: เครื่องมือสำหรับกำหนดตารางเส้นทาง IP (optional)
* `swapon`: เปิดใช้งานการเพจจิ้งและการสว๊าป (optional)
* `swapoff`: ปิดใช้งานการเพจจิ้งและการสว๊าป (optional)
* `update`: เดมอนสำหรับล้างบัฟเฟอร์ระบบไฟล์เป็นระยะ (optional)

---
# /usr
`/usr` เป็นส่วนที่สำคัญเพราะในส่วนนี้ประกอบไปด้วย  user binaries, their documentation, libraries, header files และอื่นๆ supporting libraries ก็อยู่ที่นี่ user program เช่น telnet, ftp ฯลฯ... ก็อยู่ที่นี่เช่นกัน ส่วนของ home directory ของแต่ละ user ก็อยู่ที่นี่ถ้าเป็น ปฏิบัติการ UNIX (/home/username) ดังนั้นจึงทำให้ผู้คนเรียกส่วนนี้ว่า user resource แทนที่จะเรียกว่า user ธรรมดา

* `/usr/X11R6` <br> ประกอบด้วย libraries, executables, docs, fonts ฯลฯ
* `/usr/X11R6/bin` <br> XFree86 system binaries. ส่วนที่จำเป็นในการเริ่มต้นระบบ กำหนดค่า และ running X windowing system. X, xf86config, xauth, xmodmap และ xpenguin ก็อยู่ที่นี่.
*  `/usr/X11R6/include` <br> ไฟล์ส่วนหัวของระบบ XFree86 จำเป็นสำหรับการ compile แอพพลิเคชั่นบางตัวที่ใช้ X toolkit.
*  `/usr/X11R6/lib` <br> เก็บ libraries ของระบบ XFree86
* `/usr/X11R6/lib/modules` <br> XFree86 system modules. โหลดเมื่อเริ่มต้น `video4linux`, `DRI` and `GLX` extensions and drivers หากไม่มีโมดูลพวกนี้ input บางตัวไม่ทำงาน
*  `/usr/X11R6/lib/X11/fonts` <br> XFree86 system fonts. แบบอักษรที่ใช้โดย '`xfs`' (X Font Server) และโปรแกรมประเภทนั้น.
* `/usr/bin` <br> มี binary ส่วนใหญ่ในระบบ การดำเนินการใน directory แตกต่างกันอย่างมาก ตัวอย่างเช่น vi, gcc, gnome−session และ mozilla ทั้งหมดอยู่ที่นี่
* `/usr/doc` <br> เก็บเอกสารไว้รวมกันที่นี่ เอกสารจริงอยู่ใน /usr/share/doc และมีการเชื่อมโยงจากที่นี่
* `/usr/etc` <br> ตามทฤษฎีแล้วเป็นอีก directory สำหรับไฟล์ configuration แทบไม่ได้ใช้งานเลยตอนนี้
* `/usr/games` <br> กาลครั้งหนึ่ง directory นี้มีไฟล์เกมบนเครือข่าย ตอนนี้ไม่ค่อยได้ใช้
* `/usr/include` <br> directory สำหรับ header file ซึ่งจำเป็นสำหรับการ compile source code พื้นที่ของ user
* `/usr/include/`'package−name' <br> สำหรับ application ที่มี header file เฉพาะ
* `/usr/info` <br> ใช้เพื่อเก็บไฟล์ สำหรับระบบ document info อยู่ใน '`/usr/share/info`'
* `/usr/lib` <br> เก็บ libraries ของโปรแกรมที่ใช้บ่อย
* `/usr/local` <br> เป็นตำแหน่งที่ดีในการเก็บโปรแกรมที่ compile เองหรือจากบุคคลที่สาม. `/usr/local` มีไว้สำหรับใช้โดยผู้ดูแลระบบเมื่อทำการติดตั้งซอฟต์แวร์ภายในเครื่อง จะต้องไม่ถูกเขียนทับเมื่อมีการอัพเดตซอฟต์แวร์ <br> บางครั้ง ระบบอาจใช้สำหรับโปรแกรมและ ข้อมูล ร่วมกันระหว่างกลุ่มโฮสต์ แต่ไม่พบใน `/usr`
. ซอฟต์แวร์ที่ติดตั้งในเครื่องจะต้องอยู่ภายใน /usr/local แทนที่จะเป็น /usr ( เว้นแต่จะถูกติดตั้งเพื่อแทนที่หรืออัพเกรดซอฟต์แวร์ใน /usr )
* `/usr/man` <br> มันถูกย้ายไปที่ `/usr/share/man`
* `/usr/sbin` <br> มีโปรแกรมสำหรับการรันโดย '`root`' เช่น '`/sbin`' ก็คือ
  ไม่ใช่ส่วนหนึ่งของ $PATH ของผู้ใช้ ตัวอย่างของไบนารีที่รวมอยู่ที่นี่ ได้แก่ `chroot`, `useradd`, `in.tftpd` และ
  `pppconfig`
* `/usr/share` <br> directory นี้มีไฟล์ 'ที่สามารถแชร์ได้' ข้อมูลที่ไม่จำเป็นต้องแก้ไขควรเก็บข้อมูลนั้นไว้ใน '`/usr/share`' (หรือ '`/usr/local/share`' หากติดตั้งในเครื่อง) แต่แนะนำให้สร้าง directory ย่อย ใน `/usr/share` เพื่อใช้เก็บไฟล์ที่ต้องการแชร์
* `/usr/share/doc` <br> ตำแหน่งของ document file เฉพาะแพ็คเกจ directory นี้จะมีข้อมูลที่เป็นประโยชน์ซึ่งอาจไม่มีอยู่ใน man page นอกจากนี้ยังอาจมี templates และ configuration files สำหรับบางอย่างที่ทำให้การกำหนดค่าง่ายขึ้นมาก
* `/usr/share/info` <br> ตำแหน่งของข้อมูล แต่คนนิยมอ่าน manpage มากกว่า
* `/usr/share/ma`n <br> Manual pages. ซึ่งแบ่งออกเป็น 8 ส่วน ประกอบด้วย user programs, system calls, library functions and subroutines, special files, file format, games, miscellaneous, system administration
* `/usr/src` <br> เก็บ kernel sources, header files และ documentation
* `/usr/tmp` <br> เก็บไฟล์ชั่วคราวของ user แต่ในรุ่นใหม่ๆ ไม่พบการใช้งานเลย ซึ่งตัวนี้อาจจะได้รับผลมาจาก UNIX

# /var
`/var` ประกอบด้วยข้อมูลตัวแปร เช่น  logging files, mail และ printer spool directories, transient and
 temporary files. บางส่วนของ /var ไม่สามารถแชร์ระหว่างระบบที่ต่างกันได้ ตัวอย่างเช่น /var/log, /var/lock และ /var/run. ส่วนอื่นๆ อาจถูกแชร์ โดยเฉพาะ /var/mail, /var/cache/man, /var/cache/fonts และ /var/spool/news เนื่องจากอาจมีสถานการณ์ที่คุณอาจต้องการ mount /usr เป็นแบบ read only เช่น หากอยู่ใน CD หรือในคอมพิวเตอร์เครื่องอื่น '/var' ทำให้เราไม่สามารถเขียนตัวแปรลง /usr เพราะมีข้อมูลตัวแปร เช่น ไฟล์และdirectoryที่ระบบจะต้องสามารถ write ระหว่างการดำเนินการ ในขณะที่ /usr ควรมีเฉพาะข้อมูลคงที่เท่านั้น บาง directory สามารถใส่ลงใน partitions หรือ ระบบที่แยกจากกัน เช่น เพื่อการสำรองข้อมูลที่ง่ายขึ้น เนื่องจากโทโพโลยีเครือข่ายหรือข้อกังวลด้านความปลอดภัย ไดเร็กทอรีอื่นๆ จะต้องอยู่บน partition root เนื่องจากมีความสำคัญต่อกระบวนการ boot directory 'ที่ติดตั้งได้' คือ: '/home', '/mnt', '/tmp', '/usr' และ '/var' สิ่งจำเป็นสำหรับการบูทคือ: '/bin', '/boot', '/dev', '/etc', '/lib', '/proc' และ '/sbin'

# /srv

`/srv`

เอาไว้เก็บพวกไฟล์ข้อมูลของเครื่องเซิร์ฟเวอร์และที่ administrator ไว้ดังนั้นคนที่สามารถเข้าไปได้ต้องมีสิทธิ์ administrator และไว้เก็บไฟล์เพื่อให้เข้ามาใช้บริการต่างๆที่ระบบได้ติดตั้งไว้

โครงสร้างข้อมูลข้างในของ `/srv` เป็นไปตามโปรโตคอล เช่น FTP, rsync, WWW, CVS


# /tmp

`/tmp` ประกอบด้วยไฟล์ส่วนใหญ่ที่จำเป็นชั่วคราว หลายโปรแกรมใช้สิ่งนี้เพื่อสร้าง log file
 และสำหรับการจัดเก็บข้อมูลชั่วคราว อย่าลบไฟล์ออกจากไดเร็กทอรีนี้ นอกซะจากว่าคุณจะรู้ตัวว่าทำอะไรอยู่
 ไฟล์เหล่านี้จำนวนมากมีความสำคัญสำหรับโปรแกรมที่รันอยู่  และการลบออกอาจส่งผลให้
 ระบบล่ม โดยปกติแล้วจะมีขนาดไม่เกินสองสาม KB อยู่แล้ว บนระบบส่วนใหญ่ ไดเร็กทอรีนี้จะถูกล้าง
 ออกตอนบูตหรือเมื่อปิดระบบ
 
# คำสั่งใน /bin

## `chmod`
```
chmod [option] [กำหนดสิทธิ์]  file/directory
```
ซึ่งการกำหนดสิทธิ์ สามารถใช้ได้สองรูปแบบ คือ <br>
- ใช้ตัวเลข โดยที่ read=4, write=2, execute=1 (ex. rwx=7, r-x=5, --x=1)<br>
- กำหนดโดยใช้สัญลักษณ์ u=user owner, g=group owner, o=other (ex. u=rwx) <br>
### ตัวอย่าง
ถ้าต้องการกำหนดสิทธิ์ของ Folder SHE ให้ user owner สามารถ rwx, group owner สามารถ rx, other ไม่สามารถทำอะไรได้เลย
```
chmod 750 SHE
```
หรือ
```
chmod u=rwx,g=rx,o= SHE
```
อีกตัวอย่าง คือ ถ้าต้องการให้ทุกคนทำอะไรกับ SHE ก็ได้
```
chmod 777 SHE
```
หรือ
```
chmod ugo=rwx SHE
```
## `chown`
```
chown [option] [userowner] [:groupowner]  file/directory
```
ใช้เพื่อเปลี่ยน owner ในกรณีที่ตั้งผิดหรืออยากแก้ไข owner โดยใช้ได้ทั้ง user หรือ group owner 
### ตัวอย่าง
ถ้าต้องการเปลี่ยน owner ของ Folder SHE ให้ user owner คือ User02 และ group owner เปลี่ยนเป็น lazyboy
```
chown User02 SHE
chown :lazyboy SHE
```
หรือสามารถเขียน
```
chown User02 :lazyboy SHE
```
## `cp`
```
cp [option] [path/filename] [path/destination] 
```
ใช้เพื่อ copy file ไปไว้ใน destination ที่ต้องการ
### ตัวอย่าง
ถ้าต้องการ copy file จาก /path/filetarget.txt ไปไว้ที่ /despath
ซึ่ง despath เป็น directory ที่จะใส่ไฟล์
```
cp /path/filetarget.txt /despath
```
## `date`
```
date [option] [+FORMAT]
```
ใช้เพื่อแสดงเวลา ซึ่งเป็นเวลาปัจจุบันอ้างอิงกับเวลาในเครื่อง server
### ตัวอย่าง
ถ้าต้องการ แสดงเวลา year/month/day hour:min:sec

```
date +'%Y/%m/%d %H:%M:%S'
```
หรือ ถ้าไม่ใส่ format จะได้แบบนี้
```
date # ผลลัพธ์ -> Thu Feb 8 11:26:38 AM UTC 2024
```
## `dd`
```
dd if=<ตำแหน่ง directory/file ที่ต้องการ> of=<ตำแหน่งที่จะเอาไฟล์ ไปไว้> [Options]
```
if ย่อมาจาก input file และ of ย่อมาจาก output file <br>
ใช้ในการสร้าง file backup ข้อมูลภายใน hardisk ที่เชื่อมต่ออยู่ และทำการ wirte ลง file ที่กำหนด
### ตัวอย่าง
ถ้าต้องการ backup file และ restore จาก backup image

```
ทำการ backup file ใส่ backup image
```
dd if =/dev/sda2 of=~/hdadisk.img

restore จาก backup image
```
dd if=hdadisk.img of=/dev/sdb3
```
## `df`
```
df [option] [file]
```
ใช้ในการเช็กข้อมูล disk partition ในเครื่อง เช่น ชื่อ path, ขนาด, ปริมาณใช้งาน พื้นที่ disk แต่ละ patition (ไม่มีในตัวอย่างนะครับ)
### ตัวอย่าง
ถ้าต้องการแสดงพื้นที่ disk หน่วย kb และ mb/gb

หน่วย kb
```
df
```

หน่วย mb/gb
```
df -h
```
## `dmesg`
```
dmesg [option] [file]
```
ใช้ในการ control หรือ print ข้อมูลใน kernel ring buffer <br>
ส่วนใหญ่ใช้ดู error หรือตรวจสอบการทำงานระบบ
### ตัวอย่าง
ถ้าต้องการเอาข้อมูล bootup messages ไปส่งให้ใครสักคนดู โดยต้องการไฟล์ชื่อ boot.messages

```
dmesg > boot.messages
```
ว้าว ทีนี้ผมก็สามารถเอาไฟล์ boot.messages ไปส่งได้เลยโดยไม่ต้องมานั่งพิมพ์เอง

## `echo`
```
echo [option] [string]
```
ใช้ในการแสดงผลข้อความบนหน้าจอ terminal
### ตัวอย่าง
ถ้าต้องการแสดงข้อความ Love You ที่ terminal

```
echo "Love You"
```
## `false`
```
false
```
ใช้สำหรับ logic ส่งค่าเป็นเท็จออกมา นิยมใช้เพื่อนหยุดการทำงาน หรือ เช็คเงื่อนไข
### ตัวอย่าง
ตัวอย่างนี้ อาจจะสับสนเล็กน้อยคือ ถ้า if แล้วเป็นจริงจะแสดงข้อความ What แต่ถ้าไม่ใช่จะแสดงข้อความ No

```
if false; then echo "What"; else echo "No"; fi
```
## `hostname`
```
hostname [option]
```
ใช้ในการแสดงข้อมูลชื่อของเครื่อง server
### ตัวอย่าง
ต้องการทราบชื่อ server และ ip address

ต้องการทราบชื่อ
```
hostname
```

ต้องการทราบ ip address
```
hostname -i
```
## `kill`
```
kill [option] <process ID>
```
ใช้ในการยกเลิกการทำงานของ process ซึ่งถ้าเรายกเลิกตัวที่มี sub process ตัว sub process ก็จะยกเลิกด้วย สามารถยกเลิกได้ด้วย process ID
### ตัวอย่าง
ต้องการยกเลิกการทำงาน process id 0

```
kill 0
```

ต้องการยกเลิกทันที
```
kill -9 0
```
## `ln`
```
ln <file ต้นทาง> <file ที่ลิ้งค์ไปต้นทาง>
```
ใช้ในการสร้างลิ้งค์ไปยังไฟล์ เพื่อเรียกใช้งานไฟล์ที่เราต้องการแต่เราสามารถเรียกผ่านไฟล์อื่นได้
### ตัวอย่าง
ต้องการใช้การทำงานของ MAX ผ่านการเรียกใช้ mx

```
ln MAX mx
cat mx # ผลลัพธ์ -> ข้างใน MAX
```
## `login`
```
login <username>
```
ใช้ในการเริ่มต้น session หรือ การเข้าใช้ระบบของ user ซึ่งเมื่อใช้คำสั่งก็จำเป็นต้องใส่รหัสให้ถูกด้วยจึงจะสามารถ login ได้
### ตัวอย่าง
ต้องการเข้าสู่ระบบ username: `GAME`

```
login GAME
```
## `ls`
```
ls [option] [file]
```
ใช้ในการแสดงข้อมูลใน directory ซึ่งนิยมนำมาใช้คู่กับ option ในการแสดงข้อมูล เพราะจะช่วยกรองหรือแสดงส่วนที่ต้องการได้ง่าย
### ตัวอย่าง
ต้องการแสดงข้อมูลใน directory ปัจจุบัน และ แสดงข้อมูลใน directory /user/passwd

```
ls
ls /user/passwd
```
## `mkdir`
```
mkdir [option] <directory>
```
ใช้ในการสร้าง directory
### ตัวอย่าง
ต้องการสร้าง directory Book

```
mkdir Book
```
## `mknod`
```
mknod [option] <name> <type> [major minor]
```
ใช้ในการสร้างไฟล์พิเศษ เช่น ไฟล์บล็อค(buffered) ไฟล์ตัวอักษร(unbuffered) pipe file(FIFO) <br>
พวกที่ใช้ในการส่งข้อมูล
### ตัวอย่าง
ต้องการสร้างไฟล์ block file และ character file ที่อุปกรณ์1และอุปกรณ์2
และ สร้าง pipe ชื่อ pipelink1
```
mknod /dev/blockfile  b 1 2
mknod /dev/characterfile  c 1 2
mknod pipelink1 p
```
## `more`
```
more [option] <file>
```
ใช้ในการอ่านข้อมูลและค้นหาข้อมูลใน file
### ตัวอย่าง
ต้องการแสดงข้อมูล file1 ตั้งแต่บรรทัดที่ 3 ขึ้นไป
แสดงทุกบรรทัด
```
more file1
```

แสดงตั้งแต่บรรทัดที่3
```
more +3 file1
```
## `mount`
```
mount [block device]
mount <device> <path>
```
การ remount
```
mount --bind <olddir> <newdir>
```
ใช้ในการเชื่อมต่ออุปกรณ์ที่เสียบอยู่เข้ากับ file system
### ตัวอย่าง
ต้องการเชื่อมอุปกรณ์ device1 เข้ากับ /path
```
mount device1 /path
```
---
## `mv`
```
mv [option] <old path> <new path>
mv [option] -t <directory> <source>
```
ใช้ในการย้ายไฟล์ เปลี่ยนชื่อไฟล์ ย้ายdirectory
### ตัวอย่าง
ต้องการนำ file1 ไปเก็บที่ directory test และเปลี่ยนชื่อเป็น file0 จากนั้นย้าย test ไปที่ temp
```
mv file1 test/.
mv file1 file0
mv test /tmp
```
## `ps`
```
ps [option]
```
ใช้ในการแสดง process ที่ทำงานอยู่
### ตัวอย่าง
ต้องการแสดง process ทั้งหมดที่ทำงานอยู่
```
ps
```
## `pwd`
```
pwd [option]
```
ใช้ในการแสดง directory หรือ path ที่อยู่ปัจจุบัน หรือ fullpath นั่นเอง
### ตัวอย่าง
ต้องการแสดง path ที่กำลังทำงานอยู่
```
pwd
```
## `rm`
```
rm [option] <file/directory>
```
ใช้ในการลบไฟล์ หรือ directory
### ตัวอย่าง
ต้องการลบไฟล์ file1 และ directory dirtarget
```
rm file1
```
เพิ่ม -rf ในกรณีที่ข้างใน directory มีไฟล์อยู่
```
rm -rf dirtarget
```
## `rmdir`
```
rmdir [option] <directory>
```
ใช้ในการลบ directory
### ตัวอย่าง
ต้องการลบ directory dirtarget
```
rmdir dirtarget
```
## `sed`
```
sed [option] {script-only-if-no-other-script} [input-file]
```
ใช้ในการจัดรูปแบบข้อความให้แสดงผลในแบบที่ต้องการ หรือทำให้อ่านง่ายขึ้น
### ตัวอย่าง
ต้องการให้ขึ้นบรรทัดห่างกันเพิ่มอีก 1 บรรทัด ในตอนที่แสดง file1
```
sed G file1
```
## `sh`
```
sh [option] [file.sh]
```
ใช้ในการ run file ที่เป็น .sh แต่ถ้าใช้แค่ sh โดยไม่ใส่ไฟล์มันจะเปิดหน้าต่างให้เขียน script ไปเรื่อยๆและ run ทีละลำดับตามที่เขียน
### ตัวอย่าง
ต้องการให้ run file1.sh และต้องการเขียน script และ run ต่อเนื่องด้วยตัวเอง
```
sh file.sh
sh
```
## `stty`
```
stty [-F DEVICE | --file=DEVICE] [SETTING]
```
ใช้ในการแก้ไขการตั้งค่าของการแสดงผลทาง terminal และควบคุม parameter ของอุปกรณ์ที่เชื่อมต่อ
### ตัวอย่าง
ต้องการให้ปิดการแสดงผลของ echo (ถ้าเราปิด echo ตอนเราพิมพ์ก็จะมองไม่เห็นเหมือนกัน)
```
stty -echo
```
## `su`
```
su [option] [userid]
```
ใช้ในการ login ด้วย user id อื่น และ ถ้าใส่แค่ su จะเป็นการ login เข้า root แต่ก่อนจะเข้าได้ ทั้งสองต้องใส่รหัส
### ตัวอย่าง
ต้องการให้ login ด้วย username: Jake
```
su - Jake

login root
su
```
## `sync`
```
sync [target1] [target2] ...
```
ใช้ในการทำให้ค่าทั้งหมดที่กำหนด ตรงกัน
### ตัวอย่าง
ต้องการไฟล์ $HOME/.bashrc $HOME/my/important/file sync ตรงกันและต้องการให้ทั้งหมด sync ตรงกัน
```
sync $HOME/.bashrc $HOME/my/important/file

ทั้งหมด
sync
```

---
# File Types
มีประเภทพื้นฐานทั้งหมด 7 แบบ ถึงแม้จะมีประเภทใหม่โผล่มาแต่ก็จะยังอิง ประเภทเหล่านี้ในการสร้าง

|       File type       | Symbol |     Created by     |  Removed by  |
|:---------------------:|:------:|:------------------:|:------------:|
| Regular file          |    -   | editors, [`cp`](#cp), etc.  | [`rm`](#rm)          |
| Directory             |    d   | [`mkdir`](#mkdir)  | [`rmdir`](#rmdir), [`rm`](#rm) -r |
| Character device file |    c   | [`mknod`](#mknod)  | [`rm`](#rm)           |
| Block device file     |    b   | [`mknod`](#mknod)  | [`rm`](#rm)           |
| Local domain socket   |    s   | socket system call | [`rm`](#rm)           |
| Named pipe            |    p   | [`mknod`](#mknod)  | [`rm`](#rm)           |
| Symbolic link         |    l   | [`ln`](#ln) -s     | [`rm`](#rm)           |

## Regular file

ไฟล์ทั่วไปประกอบด้วยชุดของไบต์ ซึ่ง filesystem ไม่ได้กำหนดโครงสร้างใดๆ กับเนื้อหาของไฟล์ ตัวอย่างของไฟล์ทั่วไป ได้แก่ ไฟล์ข้อความ, ไฟล์ข้อมูล, โปรแกรมที่เรียกใช้งานได้, และ library ที่ใช้ร่วมกันในเครื่องก็เป็น regular file 

สามารถเข้าถึงได้แบบตามลำดับ (sequential access) และเข้าถึงได้แบบสุ่ม (random access)

เราสามารถสร้างไฟล์พวกนี้ได้ทั้งแบบที่มีนามสกุลไฟล์และแบบไม่มีนามสกุลไฟล์
นามสกุลไฟล์ คือ กลุ่มตัวอักษรที่อยู่ต่อท้ายชื่อไฟล์ โดยทำหน้าที่เหมือนบัตรประจำตัวที่เป็นเกี่ยวดับประเภทของข้อมูลภายใน และยังช่วยจัดกลุ่มไฟล์ที่มีเนื้อหาลักษณะคล้ายคลึงกันได้ด้วย โดยทั่วไปแล้ว ก็จะมีนามสกุลเฉพาะที่เรารู้จักกันดี เพื่อให้ง่ายต่อการจดจำและการประมวลผลของระบบคอมพิวเตอร์ ตัวอย่างเช่น ไฟล์เอกสารมักจะมีนามสกุลเป็น .docx, ไฟล์รูปภาพจะเป็น .jpg หรือ .png เป็นต้น

แม้ว่าระบบไฟล์ของ Linux ไม่จำเป็นต้องใช้นามสกุลไฟล์ แต่การที่เรารู้จักนามสกุลไฟล์ ทำให้เราสามารถระบุประเภทของเนื้อหาที่เก็บไว้ในไฟล์ได้ง่าย เช่น ถ้าเราเห็นไฟล์มีนามสกุล .mp4 เราก็จะรู้ได้เลยว่ามันเป็นไฟล์วิดีโอ

## Directories

Directory คือ ที่เก็บข้อมูลที่สามารถเก็บไฟล์อื่นๆไว้ข้างในได้ directory เองก็เป็นไฟล์ชนิดหนึ่งเช่นกัน แต่ directory เก็บเป็นตำแหน่งที่ตั้งของไฟล์อื่น สามารถสร้าง directory ได้ด้วยคำสั่ง `mkdir` และลบออกได้ด้วยคำสั่ง `rmdir` แต่ต้องเป็น directory ที่ว่างเปล่าเท่านั้นที่สามารถลบได้ หากต้องการลบ directory ที่มีไฟล์อยู่ข้างใน สามารถทำได้โดยใช้คำสั่ง `rm -r`

สัญลักษณ์ "." และ ".." แทนด้วย directory และ parent directory ของมันตามลำดับ สัญลักษณ์เหล่านี้ไม่สามารถถูกลบได้ เนื่องจาก root directory ไม่มี parent directory ดังนั้น path `/..` จึงเทียบเท่ากับ path `/` และก็เทียบเท่ากับ `/`1

## Hard links

เป็นการสร้างช่องทางให้เข้าถึงไฟล์ได้อีกทาง เป็นเหมือนการทำสำเนามาจาก Inode ใน harddisk โดยทั้งตัวที่สร้างใหม่กับตัวไฟล์เดิมจะเหมือนกัน ถึงแม้ตัวต้นฉบับโดนลบแต่ตัว hardlink จะยังสามารถใช้งานได้อยู่ โดยระหว่างที่ regular file นั้นมีแค่ชื่อเดียว แต่ hard links ทำให้เราสามารถสร้างชื่อที่ชื้ไปยังข้อมูลตัวเดียวกันได้ใน disk เหมือนกับการสร้าง shortcut ไปยังไฟล์เดียวกันโดยไม่ได้คัดลอกเนื้อหาไฟล์ 

คุณสามารถสร้างฮาร์ดลิงก์ได้ด้วยคำสั่ง `ln` และลบออกได้ด้วยคำสั่ง `rm` การจำคำสั่ง `ln` ซึ่งคลายกับคำสั่ง `cp` โดยคำสั่ง `cp oldfile newfile` สร้างสำเนาของไฟล์ oldfile ชื่อ newfile แต่คำสั่ง `ln oldfile newfile` ทำให้ชื่อ newfile เป็นการอ้างอิงไปยัง oldfile


## Character and block device files

ระบบปฏิบัติการLinux มองอุปกรณ์ฮาร์ดแวร์ทั้งหมด (เช่น ฮาร์ดไดร์ฟ เครื่องพิมพ์ จอภาพ โปรแกรมจำลองเทอร์มินัล และไดร์ฟซีดี/ดีวีดี) เป็นไฟล์พิเศษ สิ่งนี้หมายความว่าโปรแกรมประยุกต์สามารถเข้าถึงและใช้ไฟล์และอุปกรณ์ในลักษณะเดียวกัน คุณลักษณะนี้ช่วยให้การพัฒนาโปรแกรมในLinuxง่ายและยืดหยุ่น 
Linux 
จัดเก็บไฟล์พิเศษหรือไฟล์อุปกรณ์ทั้งหมดไว้ภายใต้directory /dev ไฟล์พิเศษมีสองประเภท: ไฟล์อุปกรณ์พิเศษแบบอักขระและไฟล์อุปกรณ์พิเศษแบบบล็อก ไฟล์อุปกรณ์พิเศษแบบอักขระ แสดงถึงอุปกรณ์ที่ถ่ายโอนข้อมูลเป็นไบต์ เช่น จอภาพหรือเครื่องพิมพ์ ไฟล์อุปกรณ์พิเศษแบบบล็อก แสดงถึงอุปกรณ์ที่ถ่ายโอนข้อมูลเป็นบล็อก เช่น ฮาร์ดไดร์ฟ

## Local domain sockets
Socket คือ การเชื่อมต่อระหว่างกระบวนการที่ช่วยให้สามารถ สื่อสารได้อย่างถูกต้อง UNIX กำหนด Socket หลายประเภท ซึ่งส่วนใหญ่เกี่ยวข้องกับเครือข่าย Local domain sockets สามารถเข้าถึงได้จากโฮสต์ในเครื่องเท่านั้น และถูกอ้างอิงผ่าน object file system แทนที่จะเป็น พอร์ตเครือข่าย บางครั้ง ทั้งสองก็รู้จักกัน เป็น “UNIX domain sockets” Syslog และ X Window System เป็นตัวอย่างของสิ่งอำนวยความสะดวกมาตรฐานที่ใช้ Local domain sockets แต่ยังมีอีกมากมาย รวมถึง database และ app server.<br> Local domain sockets ถูกสร้างขึ้นด้วยการเรียกระบบ Socket และลบออกด้วยคำสั่ง rm หรือ การเรียกระบบยกเลิกการเชื่อมโยง เมื่อไม่มีผู้ใช้อีกต่อไป


## Named pipes
เช่นเดียวกับ Local domain sockets, pipe ที่มีชื่อ มีการสื่อสารระหว่างสองกระบวนการที่ทำงานบนโฮสต์เดียวกัน มีชื่อเรียกอีกอย่างว่า “file FIFO” (เช่นเดียวกับ financial accounting, FIFO ย่อมาจากวลี “เข้าก่อน ออกก่อน”) คุณสามารถสร้าง pipe name ด้วย mknod และลบออกด้วย rm pipe ที่มีชื่อและ Local domain sockets มีจุดประสงค์ที่คล้ายกันS


## Symbolic links
Symbolic links หรือ "Soft links" ลิ้งค์ไฟล์ด้วยชื่อ เมื่อ kernel พบ Symbolic links ในระหว่างการค้นหา pathname ตัว kernel จะเปลี่ยนเส้นทางความสนใจไปที่
pathname ที่จัดเก็บเป็นเนื้อหาของลิงก์ ความแตกต่างระหว่าง "Hard links" และ "Symbolic links" ก็คือ Hard links เป็นการอ้างอิงโดยตรง ในขณะที่ Symbolic links
เป็นการอ้างอิงตามชื่อ.เนื่องจาก "Symbolic links" สามารถมี path ที่กำหนดเองได้ จึงสามารถอ้างถึงไฟล์บนระบบไฟล์อื่นหรือไฟล์ที่ไม่มีอยู่จริงได้ "Symbolic links" ยังสามารถสร้าง loop ได้


# References
* Siever, E., Figgins, S., Love, R., & Robbins, A. (2009). Linux in a nutshell (6th ed.). O'Reilly Media, Inc.
* Nemeth, E., Snyder, G., Hein, T., & Seebass, S. (2017). UNIX and Linux system administration handbook (5th ed.). Addison-Wesley
* Red Hat, Inc. (n.d.). GRUB (Grand Unified Bootloader) [Thai]. Retrieved from https://access.redhat.com/documentation/th-th/red_hat_enterprise_linux/5/html/installation_guide/s1-grub-whatis
* Oracle. (n.d.). About Devices - Oracle Linux Documentation - 6.5. Retrieved from https://docs.oracle.com/en/operating-systems/oracle-linux/6/admin/ol_about_devices.html
* The Linux Documentation Project. (n.d.). The Linux File-System Hierarchy. Retrieved from https://tldp.org/LDP/Linux-Filesystem-Hierarchy/Linux-Filesystem-Hierarchy.pdf
* Red Hat, Inc. (n.d.). Linking to Linux Explained. Retrieved from https://www.redhat.com/sysadmin/linking-linux-explained
* `chmod`
  * Saixiii. (2017, May 9). chmod - คำสั่งเปลี่ยนสิทธิ์ในการเข้าถึง File. https://www.oreilly.com/library/view/hp-ux-11i-system/0131018833/0131018833_ch21lev1sec6.html
  * The Linux Documentation Project. (n.d.). chmod(1). https://www.redhat.com/sysadmin/linux-file-permissions-explained
* `chown`
  * Saixiii. (2017, May 9). chown - คำสั่งเปลี่ยนเจ้าของ file หรือ directory. https://man7.org/linux/man-pages/man2/chown.2.html
  * The Linux Documentation Project. (n.d.). chown(1). https://man7.org/linux/man-pages/man1/chown.1p.html
* `cp`
  * Saixiii. (2017, May 9). cp - คำสั่งทำสำเนาหรือ copy ข้อมูล. https://www.geeksforgeeks.org/cp-command-linux-examples/
  * The Linux Documentation Project. (n.d.). cp(1). https://man7.org/linux/man-pages/man1/cp.1.html
* `date`
  * Saixiii. (2017, May 9). date - คำสั่งแสดงเวลาวันเดือนปี. https://medium.com/@kp0853953/date-command-in-linux-528a090792c
  * The Linux Documentation Project. (n.d.). date(1). https://man7.org/linux/man-pages/man1/date.1.html
* `dd`
  * Saixiii. (2017, May 9). dd - คำสั่ง backup ข้อมูลใน harddisk. https://man7.org/linux/man-pages/man1/dd.1.html
  * The Linux Documentation Project. (n.d.). dd(1). https://man7.org/linux/man-pages/man1/dd.1.html
* `df`
  * Saixiii. (2017, May 9). df - คำสั่งแสดงข้อมูลพื้นที่ Disk ทั้งหมด. https://knowledge.broadcom.com/external/article/181064/how-to-monitor-percent-free-disk-space-o.html
  * The Linux Documentation Project. (n.d.). df(1). https://man7.org/linux/man-pages/man1/df.1p.html
* `dmesg`
  * The Linux Documentation Project. (n.d.). dmesg(1). https://linux.die.net/man/1/dmesg
* `echo`
  * The Linux Documentation Project. (n.d.). echo(1). https://linux.die.net/man/1/echo
  * Saixiii. (2017, May 9). echo - คำสั่งในการแสดงผลบนหน้าจอ screen. https://www.ionos.ca/digitalguide/server/configuration/linux-echo-command/
* `false`
  * The Linux Documentation Project. (n.d.). false(1). https://man7.org/linux/man-pages/man1/false.1.html
  * Michael Kerrisk (2023, November 03). false(1) - Linux manual page. https://www.commandlinux.com/man-page/man1/
* `hostname`
  * Saixiii. (2017, May 9). hostname - คำสั่งใช้แสดง hostname ของเครื่อง. https://phoenixnap.com/kb/linux-hostname-command
  * The Linux Documentation Project. (n.d.). hostname(1). https://man7.org/linux/man-pages/man1/hostname.1.html
* `kill`
  * Saixiii. (2017, May 9). kill - คำสั่งส่งสัญญาณไปยัง process. https://tonylixu.medium.com/linux-kill-command-aefb2fff46b7
  * The Linux Documentation Project. (n.d.). kill(1). https://man7.org/linux/man-pages/man1/kill.1.html
* `ln`
  * The Linux Documentation Project. (n.d.). ln(1). https://linux.die.net/man/1/ln: https://linux.die.net/man/1/ln
  * Saixiii. (2017, May 9). ln - คำสั่งสร้าง link ไปยัง file หรือ directory. https://saixiii.com/ln-linux-command/: https://saixiii.com/ln-linux-command/
* `login`
  * The Linux Documentation Project. (n.d.). login(1). https://linux.die.net/man/1/login: https://linux.die.net/man/1/login
* `ls`
  * Saixiii. (2017, May 9). ls - คำสั่งแสดงรายการไฟล์และโฟลเดอร์. https://saixiii.com/ls-linux-command/: https://saixiii.com/ls-linux-command/
  * The Linux Documentation Project. (n.d.). ls(1). https://linux.die.net/man/1/ls: https://linux.die.net/man/1/ls
* `mkdir`
  * The Linux Documentation Project. (n.d.). mkdir(1). https://linux.die.net/man/1/mkdir: https://linux.die.net/man/1/mkdir
  * Saixiii. (2017, May 9). mkdir - คำสั่งสร้าง directory ใหม่. https://saixiii.com/mkdir-linux-command/: https://saixiii.com/mkdir-linux-command/
* `mknod`
  * The Linux Documentation Project. (n.d.). mknod(1). https://linux.die.net/man/1/mknod: https://linux.die.net/man/1/mknod
  * IBM. (2015, October 19). mknod command. https://www.ibm.com/docs/en/aix/7.2?topic=m-mknod-command: https://www.ibm.com/docs/en/aix/7.2?topic=m-mknod-command
* `more`
  * The Linux Documentation Project. (n.d.). more(1). https://linux.die.net/man/1/more: https://linux.die.net/man/1/more
  * Saixiii. (2017, May 9). more - คำสั่งแสดงผลข้อมูลทีละหน้า. https://saixiii.com/more-linux-command/: https://saixiii.com/more-linux-command/
* `mount`
  * Saixiii. (2017, May 9). mount - คำสั่ง mount file system. https://saixiii.com/mount-linux-command/: https://saixiii.com/mount-linux-command/
  * The Linux Documentation Project. (n.d.). mount(8). https://linux.die.net/man/8/mount: https://linux.die.net/man/8/mount
* `mv`
  * The Linux Documentation Project. (n.d.). mv(1). https://linux.die.net/man/1/mv: https://linux.die.net/man/1/mv
  * Saixiii. (2017, May 9). mv - คำสั่งย้ายไฟล์หรือเปลี่ยนชื่อไฟล์. https://saixiii.com/mv-linux-command/: https://saixiii.com/mv-linux-command/
* `ps`
  * Saixiii. (2017, May 9). ps - คำสั่งแสดงสถานะ process ที่กำลังทำงานอยู่. https://saixiii.com/ps-linux-command/: https://saixiii.com/ps-linux-command/
  * The Linux Documentation Project. (n.d.). ps(1). https://linux.die.net/man/1/ps: https://linux.die.net/man/1/ps
* `pwd`
  * The Linux Documentation Project. (n.d.). pwd(1). https://linux.die.net/man/1/pwd: https://linux.die.net/man/1/pwd
  * Saixiii. (2017, May 9). pwd - คำสั่งแสดงตำแหน่งของ directory ปัจจุบัน. https://saixiii.com/pwd-linux-command/: https://saixiii.com/pwd-linux-command/
* `rm`
  * Saixiii. (2017, May 9). rm - คำสั่งลบไฟล์. https://saixiii.com/rm-linux-command/: https://saixiii.com/rm-linux-command/
  * The Linux Documentation Project. (n.d.). rm(1). https://linux.die.net/man/1/rm: https://linux.die.net/man/1/rm
* `rmdir`
  * The Linux Documentation Project. (n.d.). rmdir(1). https://linux.die.net/man/1/rmdir: https://linux.die.net/man/1/rmdir
  * Saixiii. (2017, May 9). rmdir - คำสั่งลบ directory ว่าง. https://saixiii.com/rmdir-linux-command/: https://saixiii.com/rmdir-linux-command/
* `sed`
  * Saixiii. (2017, May 9). sed - คำสั่งแก้ไข file แบบ stream editor. https://saixiii.com/sed-linux-command/: https://saixiii.com/sed-linux-command/
  * The Linux Documentation Project. (n.d.). sed(1). https://linux.die.net/man/1/sed: https://linux.die.net/man/1/sed
* `sh`
  * The Linux Documentation Project. (n.d.). sh(1). https://linux.die.net/man/1/sh: https://linux.die.net/man/1/sh
  * IBM. (2021, February 16). sh shell command. https://www.ibm.com/docs/pl/aix/7.1?topic=s-sh-command: https://www.ibm.com/docs/pl/aix/7.1?topic=s-sh-command
* `stty`
  * The Linux Documentation Project. (n.d.). stty(1). https://linux.die.net/man/1/stty: https://linux.die.net/man/1/stty
* `su`
  * Saixiii. (2017, May 9). su - คำสั่งเปลี่ยนเป็น user อื่น. https://saixiii.com/su-linux-command/: https://saixiii.com/su-linux-command/
  * The Linux Documentation Project. (n.d.). su(1). https://linux.die.net/man/1/su: https://linux.die.net/man/1/su
* `sync`
  * The Linux Documentation Project. (n.d.). sync(8). https://linux.die.net/man/8/sync: https://linux.die.net/man/8/sync
  * Computer Hope. (n.d.). sync unix command. https://www.computerhope.com/unix/sync.htm: https://www.computerhope.com/unix/sync.htm