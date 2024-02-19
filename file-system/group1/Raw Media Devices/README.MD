![RAWMedia](/Assets/Raw%20Media%20Device.jpg)
## เนื้อหาในหัวข้อนี้
* [อะไรคือ Raw Media Device](#อะไรคือ-raw-media-device)
* [การนำ Raw Media Device มาใช้งาน](#การนำ-raw-media-device-มาใช้งาน)
* [คำสั่งที่ควรทราบ](#คำสั่งที่ควรทราบ)
  * [`lsblk`](#lsblk---list-block-devices)
  * [`fdisk`](#fdisk---manipulate-disk-partition-table)
  * [`cfdisk`](#cfdisk---display-or-manipulate-a-disk-partition-table)
  * [`mkfs`](#mkfs---build-a-linux-filesystem)
* [อ้างอิง](#อ้างอิงจาก)
## อะไรคือ Raw Media Device

&nbsp;&nbsp;&nbsp;&nbsp;<b>Raw Media Device</b> คือประเภทของ <b>Raw Device</b> ที่สามารถใช้ในการเชื่อมกับ Block Device ที่มีอยู่ (เช่น Harddisk หรือ SSD) และดำเนินการ I/O แบบดิบกับ Block Device นั้นโดยการใช้งาน I/O แบบดิบจะข้าม Cache ที่ปกติเชื่อมโยงกับ Block Device ทำให้โปรแกรมสามารถควบ Timings ของ I/O ไปยัง Physical Device นั้นได้มากขึ้น ที่กล่าวมาข้างต้นทำให้ Raw Device เหมาะสำหรับแอปพลิเคชันที่ซับซ้อน เช่น ระบบจัดการฐานข้อมูล ซึ่งมักจะมีระบบแคชของตัวเอง (เช่น Oracle DBMS)

## การนำ Raw Media Device มาใช้งาน
&nbsp;&nbsp;&nbsp;&nbsp;เริ่มจากการรันคำสั่ง `lsblk` เพื่อแสดงรายการดิสก์ในระบบและระบุไดร์ฟ หากต้องการแสดงข้อมูลเพิ่มเติมให้ใช้คำสั่ง `lsblk -o +MODEL,SERIAL` เพื่อแสดงรายละเอียดรุ่นและหมายเลขประจำเครื่อง เมื่อทราบชื่อไดร์ฟใหม่ที่ต้องการเข้าถึง (สมมติว่าเป็น /dev/sdb) ให้ตั้ง Partition Table บนไดร์ฟ โดยสามารถตั้งได้ด้วยคำสั่ง เช่น `parted`, `gparted`, `fdisk`, `cfdisk` และ `sfdisk` โดยสามารถเลือกใช้ตัวไหนก็ได้ขอเพียงให้มันรองรับ Partition Table แบบ GPT แต่ `gparted` น่าจะเป็นตัวเลือกที่ง่ายที่สุดสำหรับระบบที่มี GUI และสำหรับระบบที่ไม่มี GUI ควรใช้ `fdisk` ซึ่งเป็นคำสั่งที่ใช้งานได้กับระบบ Linux ทุกรุ่น


## คำสั่งที่ควรทราบ
### `lsblk`  - list block devices
&nbsp;&nbsp;&nbsp;&nbsp;คำสั่ง `lsblk` แสดงข้อมูลเกี่ยวกับ Block Device ทั้งหมดที่มีหรือที่ระบุ โดยคำสั่งจะอ่านระบบไฟล์ `sysfs` และฐานข้อมูล `udev` เพื่อรวบรวมข้อมูล หากฐานข้อมูล `udev` ไม่พร้อมใช้งาน หรือ `lsblk` ถูกคอมไพล์โดยไม่รองรับ `udev` คำสั่งจะพยายามอ่าน `LABELs`, `UUIDs` และประเภทระบบไฟล์จากอุปกรณ์บล็อกโดยตรง ซึ่งในกรณีนี้จำเป็นต้องมีสิทธิ์ระดับ root

#### การใช้งานแบบระบบุทั้งหมด
```sh
jarukrit@coosdemo:~$ lsblk
```
ผลลัพธ์
```
NAME                      MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0                       7:0    0  63.9M  1 loop /snap/core20/2105
loop1                       7:1    0    87M  1 loop /snap/lxd/26881
loop4                       7:4    0 114.4M  1 loop /snap/lxd/26741
loop6                       7:6    0  63.5M  1 loop /snap/core20/2015
loop7                       7:7    0  40.9M  1 loop /snap/snapd/20290
loop8                       7:8    0  40.4M  1 loop /snap/snapd/20671
sda                         8:0    0 111.8G  0 disk
├─sda1                      8:1    0     1G  0 part /boot/efi
├─sda2                      8:2    0     2G  0 part /boot
└─sda3                      8:3    0 108.7G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0 100.7G  0 lvm  /
sdb                         8:16   0   3.6T  0 disk
└─sdb1                      8:17   0   3.6T  0 part /mnt/data
```

#### การใช้งานแบบเจาะจง Block Device
```sh
jarukrit@coosdemo:~$ lsblk /dev/sda
```
ผลลัพธ์
```
NAME                      MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0 111.8G  0 disk
├─sda1                      8:1    0     1G  0 part /boot/efi
├─sda2                      8:2    0     2G  0 part /boot
└─sda3                      8:3    0 108.7G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0 100.7G  0 lvm  /
```

#### การใช้งานแบบเจาะจง Block Device และ แสดงข้อมูลเพิ่มเติม
```sh
jarukrit@coosdemo:~$ lsblk /dev/sdb -o +MODEL,SERIAL
```
ผลลัพธ์
```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS MODEL           SERIAL
sdb      8:16   0  3.6T  0 disk             TOSHIBA HDWD240 7191S4G5S5HH
└─sdb1   8:17   0  3.6T  0 part /mnt/data
```
<hr />

### `fdisk` - manipulate disk partition table
&nbsp;&nbsp;&nbsp;&nbsp;`fdisk` เป็นโปรแกรม Text User Interface ที่ใช้สำหรับการสร้างและจัดการ Partition Table โดย
รองรับ Partition Table แบบ GPT, MBR, Sun, SGI และ BSD

&nbsp;&nbsp;&nbsp;&nbsp;Block Device สามารถแบ่งออกเป็น Logical Disk ตั้งแต่หนึ่งดิสก์ขึ้นไป เรียกว่า Partition การแบ่งนี้จะถูกบันทึกไว้ใน Partition Table ซึ่งโดยทั่วไปจะอยู่ที่เซกเตอร์ 0 ของดิสก์
### วิธีใช้งาน
พิมพ์คำสั่ง `sudo fdisk [options] [device]` โดยแทนที่ device ด้วยชื่ออุปกรณ์ฮาร์ดไดร์ฟ ตัวอย่าง: `/dev/sda` หรือ `/dev/hda`
```
Welcome to fdisk (util-linux 2.37.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help):
```
### คำสั่งที่ใช้ใน Switches
* `-b [Sector Size]`
  * กำหนดขนาดของแต่ละเซกเตอร์ของดิสก์ อาจเป็น 512, 1024 หรือ 2048 ระบบส่วนใหญ่ ตอนนี้รู้ขนาดเซกเตอร์โดยอัตโนมัติ ดังนั้นจึงไม่จำเป็น
* `-l`
  * แสดงตารางพาร์ติชันและออก
* `-u` 
  * รายงานขนาดพาร์ติชันเป็นเซกเตอร์แทนกระบอกสูบ
* `-s [Partition]`
  * แสดงขนาดของพาร์ติชัน เว้นแต่จะเป็นพาร์ติชัน DOS
* `-v`
  * พิมพ์หมายเลขเวอร์ชัน จากนั้นออก
* `-C [cylinders]`
  * ระบุจำนวน cylinders บบนดิสก์
* `-H [heads]`
  * ระบุจำนวนหัวต่อ cylinders
* `-S [sectors]`
  * ระบุเซกเตอร์ต่อแทร็กสำหรับการแบ่งพาร์ติชัน
โดย คำสั่ง `p` จะแสดงข้อมูลของ Partition นั้น ๆ
```
Help:
Disk /dev/sda: 35 GiB, 37580963840 bytes, 73400320 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: D06EAB77-C679-8744-A5EE-9B9BECBEABFA

Device     Start      End  Sectors Size Type
/dev/sda1   2048 73400286 73398239  35G Linux filesystem
```
<hr />

### คำสั่งต่างที่ใช้ทำงานทั่วไปมีดังนี้

* `a` สลับสถานะแฟล็กบูตได้บนพาร์ติชันปัจจุบัน
* `b` แก้ไข disklabel ของพาร์ติชัน BSD
* `c` สลับสถานะแฟล็กความเข้ากันได้กับ DOS
* `d` ลบพาร์ติชันปัจจุบัน
* `l` แสดงรายการประเภทพาร์ติชันทั้งหมด
* `m` เมนูหลัก
* `n` สร้างพาร์ติชันใหม่; ขอข้อมูลเพิ่มเติม
* `o` สร้างตารางพาร์ติชัน DOS ว่างเปล่า
* `p` พิมพ์รายการพาร์ติชันทั้งหมดและข้อมูลเกี่ยวกับแต่ละพาร์ติชัน
* `q` ออก; ไม่บันทึก
* `t` แทนที่ประเภทของพาร์ติชันปัจจุบัน
* `u` ปรับเปลี่ยนหน่วยการแสดง/ป้อนข้อมูล ซึ่งต้องเป็น cylinders หรือเซกเตอร์
* `v` ตรวจสอบ: ตรวจสอบข้อผิดพลาด และแสดงสรุปจำนวนเซกเตอร์ที่ไม่ได้จัดสรร
* `w` บันทึกการเปลี่ยนแปลงและออก
* `x` สลับไปใช้คำสั่งแบบ Expert
<hr />

### `cfdisk` - display or manipulate a disk partition table

`cfdisk` เป็นโปรแกรมที่ใช้ Text User Interface แบบ curses สำหรับการแบ่งพาร์ติชันอุปกรณ์บล็อกต่าง ๆ โดยอุปกรณ์เริ่มต้นคือ `/dev/sda`
```
                                       Disk: /dev/sda
                     Size: 35 GiB, 37580963840 bytes, 73400320 sectors
                Label: gpt, identifier: D06EAB77-C679-8744-A5EE-9B9BECBEABFA

    Device                 Start           End       Sectors      Size Type
>>  /dev/sda1               2048      73400286      73398239       35G Linux filesystem


 ┌────────────────────────────────────────────────────────────────────────────────────────┐
 │Partition UUID: 5BA2ED9E-EEA5-5547-B41D-FB08726A9004                                    │
 │Partition type: Linux filesystem (0FC63DAF-8483-4772-8E79-3D69D8477DE4)                 │
 └────────────────────────────────────────────────────────────────────────────────────────┘
     [ Delete ]  [ Resize ]  [  Quit  ]  [  Type  ]  [  Help  ]  [  Write ]  [  Dump  ]
```
### คำสั่งใช้งาน
* ลูกศรขึ้น, ลูกศรลง
  * เลื่อนไปมาระหว่างพาร์ติชัน

* ลูกศรซ้าย, ลูกศรขวา
  * เลื่อนไปมาระหว่างคำสั่งที่ด้านล่างของหน้าจอ

* ปุ่ม Enter
  * เลือกคำสั่งหรือค่าที่ไฮไลต์อยู่

* `d` ลบพาร์ติชัน (อนุญาตให้พาร์ติชันอื่นใช้พื้นที่)
* `g` เปลี่ยนแปลงโครงสร้างของดิสก์ เลือกสิ่งที่ต้องการเปลี่ยน: Cylinder (c), Head (h), หรือ Sector (s)
* `h` ขอความช่วยเหลือ
* `m` พยายามใช้พื้นที่ดิสก์ในพาร์ติชันให้มากที่สุด
* `n` สร้างพาร์ติชันใหม่ ขอข้อมูลเพิ่มเติม
* `p` พิมพ์ตารางพาร์ติชันลงบนหน้าจอหรือไฟล์ รูปแบบที่เป็นไปได้เหมือนกับตัวเลือก `-P`
* `q` ออกโดยไม่บันทึกข้อมูล
* `t` เลือกประเภทระบบไฟล์ใหม่ และเปลี่ยนเป็นประเภทนั้น
* `u` เปลี่ยนหน่วยขนาดพาร์ติชัน ตัวเลือกหน่วยจะหมุนเวียนจากเมกะไบต์เป็นเซกเตอร์เป็น Cylinder และย้อนกลับ
* `W` บันทึกข้อมูล ต้องเป็นตัวพิมพ์ใหญ่ เพื่อป้องกันการเขียนโดยไม่ตั้งใจ
* `b` สลับสัญลักษณ์ระบุว่าพาร์ติชันที่เลือกสามารถบูตได้

<hr />

### `mkfs` - build a Linux filesystem
```
mkfs [options] [fs-options] filesys [blocks]
```
&nbsp;&nbsp;&nbsp;&nbsp;คำสั่ง `mkfs` ใช้ในการสร้าง File System บนอุปกรณ์จัดเก็บข้อมูล เช่น ฮาร์ดดิสก์ พาร์ติชัน ชื่ออุปกรณ์หรือ mountpoint ระบุถึงอุปกรณ์ที่ต้องการสร้างระบบไฟล์ ตัวเลือก -t ระบุชนิดของระบบไฟล์ ตัวอย่างเช่น ระบบไฟล์ Linux Second Extended Filesystem ใช้คำสั่ง mkfs.ext2 (เหมือนกับคำสั่ง `mke2fs`) ส่วนระบบไฟล์ MS-DOS ใช้คำสั่ง `mkfs.msdos` ตัวเลือก fs-options คือตัวเลือกเฉพาะสำหรับแต่ละชนิดของระบบไฟล์ ส่วน blocks คือขนาดของระบบไฟล์เป็นหน่วยบล็อก 1024 ไบต์

#### ตัวเลือก
* `-V` 
  * แสดงผลลัพธ์แบบละเอียด รวมถึงคำสั่งทั้งหมดที่ใช้สร้างระบบไฟล์
* `-t [fs-type]` 
  * ระบุประเภทของระบบไฟล์ที่ `mkfs` จะสร้าง

#### ตัวเลือกเฉพาะ File System
ตัวเลือกเหล่านี้ต้องอยู่หลังตัวเลือกทั่วไป และไม่สามารถใช้ร่วมกันได้ ระบบสร้าง
ระบบไฟล์ส่วนใหญ่รองรับตัวเลือกสามตัวเลือกนี้:

* `-c` 
  * ตรวจสอบบล็อกเสียบนอุปกรณ์ก่อนสร้างระบบไฟล์
* `-l [file]` 
  * อ่านรายการบล็อกเสียบนอุปกรณ์จากไฟล์
* `-v` 
  * แสดงผลลัพธ์แบบละเอียด


## อ้างอิงจาก
* Siever, E., Figgins, S., Love, R., & Robbins, A. (2009). Linux in a nutshell (6th ed.). O'Reilly Media, Inc.
* Nemeth, E., Snyder, G., Hein, T., & Seebass, S. (2017). UNIX and Linux system administration handbook (5th ed.). Addison-Wesley
* Oracle. (2022). Linux Network File System Reference Guide (Release 8.3) [DOC]. Retrieved from https://docs.oracle.com/cd/A83908_02/NT816EE/DOC/nt.816/a73025/ch3.htm
* TLDP.org. (n.d.). Raw Devs HOWTO [HTML]. Retrieved from https://tldp.org/HOWTO/SCSI-2.4-HOWTO/rawdev.html
* TLDP.org. (n.d.). Fdisk Partitioning HOWTO [HTML]. Retrieved from https://tldp.org/HOWTO/Partition/fdisk_partitioning.html
* Michael Kerrisk (Ed.). (2023, January 13). lsblk(8) [Man Page]. Retrieved from https://man7.org/linux/man-pages/man8/lsblk.8.html
* Michael Kerrisk (Ed.). (2023, January 13). fdisk(8) [Man Page]. Retrieved from https://man7.org/linux/man-pages/man8/fdisk.8.html