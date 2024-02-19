# File and Directory

ใน Linux System ทุกอย่างคือไฟล์ ไม่ว่าจะเป็น Partition, Hardware, อุปกรณ์ต่าง ๆ, Driver และ Directories

การดำเนินการต่าง ๆ เกี่ยวกับไฟล์มีหลายเรื่องที่ต้องคำนึงมากมาย เช่น กรณีที่ตั้งชื่อไฟล์เหมือนกัน
แต่ต่างกันที่ตัวพิมพ์เล็กหรือตัวพิมพ์ใหญ่ ก็ถือว่าทั้งสองไฟล์นั้นเป็นคนละไฟล์กัน

<br>
<hr>

## ประเภทของไฟล์

#### 1. Regular files

เป็นไฟล์ทั่วไปพวก Media file, Program และ Executable file ไฟล์ชนิดนี้สามารถอยู่ในรูปของ ASCII หรือ Binary

#### 2. Directories

สำหรับ Linux ถือเป็นไฟล์ที่ใช้ในการจัดเก็บไฟล์อื่น ๆ และ Subdirectories

_คำสั่งที่ใช้ในการดู Directories:_

    ls -l /home/ubuntu/ | grep ^d

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-02.png)

#### 3. Special files หรือ Device files

เป็นพวกไฟล์อุปกรณ์ที่เชื่อมโยงกับอุปกรณ์ Hardware ในระบบ สามารถแบ่งเป็น 5 ประเภท ดังนี้

- Block file (b): เป็นไฟล์ที่ทำหน้าที่เป็น Direct inteface สำหรับ Block devices เช่น Hard drive
  โดยเป็นไฟล์ที่แทนอุปกรณ์ที่ถ่ายโอนข้อมูลเป็น Block โดยไฟล์เหล่านี้จะถูกเก็บอยู่ใน /dev

_คำสั่งที่ใช้ในการดู Block file:_

    ls -l /dev | grep ^b

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-03.png)

<br>

- Character device file (c):
  เป็น Hardware file ที่อ่าน/เขียนข้อมูลทีละ 1 ตัวอักษร โดยใช้รูปแบบในการ Input/Output แบบ Serial stream
  และให้การเข้าถึงโดยตรงกับ Hardware ตัวอย่าง Hardware เช่น Terminal, Serial port

_คำสั่งที่ใช้ในการดู Character device file:_

    ls -l /dev | grep ^c

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-04.png)

<br>

- Named pipe file หรือ Just a pipe file (p): ชื่อของ Named pipe เป็นชื่อไฟล์ในระบบไฟล์ โดยทำหน้าที่ส่งข้อมูลจาก Process
  หนึ่งไปยังอีก Process

_คำสั่งที่ใช้ในการดูไฟล์ Named pipe file:_

    ls -l /dev | grep ^p

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-05.png)

<br>

- Symbolic link file (l): ทำหน้าที่ชี้ไปยังไฟล์หรือ Folder อื่น ๆ ทำให้มีความยืดหยุ่นในการใช้ชื่อไฟล์ต่างกันหรืออยู่ใน
  Location ที่ต่างกัน
  ซึ่ง Link มีอยู่ 2 ประเภท ดังนี้
    - Hard link สำหรับคัดลอกไฟล์ต้นฉบับ โดยจะไม่สามารถสร้าง Directory หรือ File ในระบบไฟล์อื่นได้
    - Soft link สำหรับชี้ไปยังไฟล์ฉบับ ซึ่งสามารถสร้าง Directory หรือ File ในระบบไฟล์อื่นได้

_คำสั่งที่ใช้ในการดูไฟล์ Symbolic link file:_

    ls -l /dev | grep ^l

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-06.png)

<br>

- Socket file (s): อนุญาตให้มีการแลกเปลี่ยนข้อมูลโดยไม่ต้องใช้กระบวนการที่ซับซ้อนของเครือข่ายและ Sockets
  โดยใช่ชื่อไฟล์เป็นที่อยู่ แทนการใช้ IP Address และ Port Number

_คำสั่งที่ใช้ในการดู Socket file:_

    ls -l /dev | grep ^s

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-07.png)

<br>
<hr>

### วิธีดูประเภทของไฟล์

- `file` command
  คำสั่งนี้จะแสดงเฉพาะชนิดของไฟล์แต่ไม่แสดงชนิดของเนื้อหาข้างใน

_ตัวอย่างคำสั่ง_

    file fail.txt
    file /dev/*

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-08.png)

<br>

- `ls -l` command
  คำสั่งนี้จะแสดงเนื้อหาภายใน Directory ปัจจุบันด้วย โดยตัวอักษรแรกใน List แต่ละอันบอกถึงชนิดของ File

_ตัวอย่างคำสั่ง_

    ls -l /dev

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-09.png)

<br>

- `stat` command
  คำสั่งนี้แสดงข้อมูลของ File system, ขนาดของไฟล์, สิทธิ์การเข้าถึง, User และ Group IDs

_ตัวอย่างคำสั่ง_

    stat records.csv

![](https://linuxopsys.com/wp-content/uploads/2023/06/Linux-File-Types-142023-10.png)

<br>
<hr>

## สรุปเรื่องประเภทของไฟล์

| ชนิด      | คำอธิบาย                                          | คำสั่งที่่ใช้ในการสร้าง | ที่อยู่ของไฟล์     | ls -l |
|-----------|---------------------------------------------------|-------------------------|--------------------|-------|
| Regular   | ประกอบไปด้วย ข้อมูลพวก Text, Image, Video, Script | touch                   | Directory ไหนก้ได้ | -     |
| Directory | ประกอบไปด้วยชื่อและที่อยู่ของไฟล์อื่น ๆ           | mkdir                   | Directory          | d     |
| Block     | ทำให้เข้าถึง Block device I/O                     | fdisk                   | /dev               | b     |
| Character | เกี่ยวข้องกับการเข้าถึงอุปกรณ์ด้วยตัวอักษร        | mknod                   | /dev               | c     |
| Pipe      | อนุญาตให้มีการรับส่งข้อมูลระหว่างกัน              | mkfifo                  | /dev               | p     |
| Symbol    | เป็นตัวชี้หรือคัดลอกไฟล์อื่น ๆ                    | ln                      | /dev               | l     |
| Socket    | ให้การแลกเปลี่ยนสื่อสารระหว่างกัน                 | socket() System call    | /dev               | s     |

## ตัวอย่างเพิ่มเติมเกี่ยวกับ Regular files

- เริ่มจากการสร้างไฟล์ด้วยคำสั่ง: `touch [file name]`

      touch testfile

- สามารถเช็คว่าไฟล์ถูกสร้างขึ้นเรียบร้อยแล้วหรือไม่ได้: `ls [option] [file name]`

      ls testfile
      testfile

- เพิ่มเนื้อหาเข้าไปในไฟล์ด้วยคำสั่ง: `echo`

      echo "all cat are so cute" > testfile

- แสดงเนื้อหาในไฟล์ด้วยคำสั่ง: `cat`

      cat testfile
      all cat are so cute

- ลบไฟล์ด้วยคำสั่ง: `rm [file_name]`

      rm testfile

> [!NOTE]
>
> - คำสั่ง ls และ rm สามารถใช้กับ Directory ได้
> - หากใช้คำสั่ง echo แล้วเขียนชื่อไฟล์เป็นไฟล์ที่ยังไม่ถูกสร้าง จะเป็นการสร้างไฟล์ใหม่ที่มีเนื้อหาตามที่เขียนไว้
> - ดังนั้นจึงควรระวังในการทำงานเกี่ยวกับไฟล์

## ตัวอย่างเพิ่มเติมเกี่ยวกับ Directories

- ดู Path ของ Directory ปัจจุบันที่เราอยู่ด้วยคำสั่ง: `pwd`

      pwd
      /home/maisan

- เข้าไปใน Subdirectory ด้วยคำสั่ง: `cd [directory name]`

      cd a1
      pwd
      /home/maisan/a1

- ต้องการออกจาก Directory ปัจจุบัน ใช้คำสั่ง: `cd ..`

      cd ..
      pwd
      /home/maisan

- ออกไปยัง Home directory ใช้คำสั่ง: `cd ~` หรือ `cd`

      cd a1
      cd a2
      pwd
      /home/maisan/a1/a2

      cd
      /home/maisan

- [See another command file management here!](https://contabo.com/blog/linux-navigation-and-file-management/)

- [See another file command options here!](https://phoenixnap.com/kb/linux-file-command)

<br>
<hr>

## สิทธิ์การเข้าถึงไฟล์

### 1. ประเภทของ Permissions

| ตัวอักษร | ความหมาย                                   |
|:--------:|:-------------------------------------------|
|    r     | Read: ไฟล์นี้สามารถเปิดอ่านข้อมูลในไฟล์ได้ |
|    w     | Write: ไฟล์นี้สามารถแก้ไขข้อมูลในไฟล์ได้   |
|    x     | Execute: สามารถเข้าไป execute ไฟล์ได้      |

_คำสั่งที่ใช้แสดง Permission_

    ls -l
    total 4
    -rwxrwxrwx 1 kali pentest 21 Dec 18 20:37 note

<br>

แต่ละ Permission สามารถแสดงในรูปแบบ **Numberic Mode** ได้ ดังนี้

| ตัวอักษร | Numberic Mode |
|:--------:|:-------------:|
|    r     |       4       |
|    w     |       2       |
|    x     |       1       |

ตัวอย่างการใช้งาน

- Owner: rwx = 4+2+1 = 7
- Group: r-- = 4+0+0 = 4
- Others: r-- = 4+0+0 = 4

ได้ผลลัพธ์เป็นเลขสามตัวต่อกัน คือ `744`

ตาราง **Octal Permissions**

| binary | octal | permission |
|:------:|:-----:|:----------:|
|  000   |   0   |    ---     |
|  001   |   1   |    --x     |
|  010   |   2   |    -w-     |
|  011   |   3   |    -wx     |
|  100   |   4   |    r--     |
|  101   |   5   |    r-x     |
|  110   |   6   |    rw-     |
|  111   |   7   |    rwx     |

### Advanced File Permissions

|   | ความหมาย                                                                                                                                                                                                     | ตัวอย่างการใช้งาน                                                                                                                                                                                            |
|:-:|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| s | 1) `SUID` ไม่ว่าคนที่เรียกใช้งานไฟล์นี้จะเป็นสิทธิ์อะไรก็ตาม แต่ไฟล์จะทำงานด้วยสิทธิ์ของเจ้าของไฟล์<br/>2) `SGID` ไม่ว่าคนที่เรียกใช้งานไฟล์นี้จะเป็นสิทธิ์อะไรก็ตาม แต่ไฟล์จะทำงานด้วยสิทธิ์ของ Group owner | `SUID`: การแก้ไข password ใน /usr/bin/psswd<br/>`SGID` สำหรับการ Share directory ให้ทุกคนใน group ที่เข้ามาสร้างไฟล์ใน Directory นี้ มี Group owner เป็น Parent directory เพื่อให้สมาชิกในกลุ่มอ่าน/เขียนได้ |
| t | `Sticky Bit` Directory พิเศษที่ทุกคนสามารถอ่านและเขียนได้ แต่ไม่สามารถลบได้ มีแค่เจ้าของไฟล์ (User/Owner) หรือ root เท่านั้นที่สามารถลบได้ มักใช้กับ Share Directory                                         | /tmp                                                                                                                                                                                                         |

- [ตัวอย่างเพิ่มเติมในการทำ SUID และ SGID](https://medium.com/@kanompung/%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%97%E0%B8%B3-suid-%E0%B9%81%E0%B8%A5%E0%B8%B0-sgid-5f9ac6011c5a)
- [รายละเอียดและตัวอย่างเพิ่มเติมเกี่ยวกับ Advanced file permissions](https://datafarm-cybersecurity.medium.com/file-permissions-in-linux-4e671dee72ca)

<br>
<hr>

### วิธีการแก้ไข File Permissions

ใช้คำสั่ง `chmod` โดยมีรูปแบบดังนี้

|  คำสั่ง   | คำอธิบาย                                                    |
|:---------:|-------------------------------------------------------------|
| `chmod u` | สำหรับแก้ Permission ของ User owner                         |
| `chmod g` | สำหรับแก้ Permission ของ User ที่อยู่ใน File's group.       |
| `chmod o` | สำหรับแก้ Permission ของ User ที่ไม่ได้อยู่ใน File's group. |
| `chmod a` | สำหรับ Permission ของ ทั้งหมด                               |

ตัวอย่างคำสั่ง

    chmod ug+rwx example.txt
    chmod o-r example2.txt

จากตัวอย่างเป็นการเพิ่ม Permission read, write, execute ให้กับ User และ Group สำหรับไฟล์ example.txt และลบ Permission
read ของ Other user สำหรับไฟล์ example2.txt

<br>
<hr>

### 2. User owner and Group owner

สามารถดูได้ว่าใครเป็น User owner หรือ Group owner โดยใช้คำสั่งต่อไปนี้

    ls -lh
    total 636K
    -rw-r--r--. 1 paul snooker 1.1K Apr 8 18:47 data.odt
    -rw-r--r--. 1 paul paul 626K Apr 8 18:46 file1
    -rw-r--r--. 1 root tennis 185 Apr 8 18:46 file2
    -rw-rw-r--. 1 root root 0 Apr 8 18:47 stuff.txt

หรือ

    ls -l

รายละเอียดในไฟล์ data.odt (ไฟล์ที่หนึ่ง)

-rw-r--r-- แบ่งได้เป็น 4 ส่วน `-|rw-|r--|r--` โดยอธิบายตามลำดับดังนี้

- ชนิดของไฟล์: - (Regular file)
- สิทธิ์ของ User/Owner หรือเจ้าของไฟล์:
    - `rw-` Read ได้, Write ได้, Execute ไฟล์ไม่ได้
- สิทธิ์ของ Group หรือกลุ่ม:
    - `r--` Read ได้, Write ไฟล์ไม่ได้, Execute ไฟล์ไม่ได้
- สิทธิ์ของ Other หรือคนอื่น ๆ ที่ไม่ใช่เจ้าของ:
    - `r--` Read ได้, Write ไฟล์ไม่ได้, Execute ไฟล์ไม่ได้

จะเห็นว่าใน data.odt มี User paul เป็น `User Owner` และมี Group snooker เป็น `Group owner`

### คำสั่งแสดงผู้ใช้ทั้งหมด

    cut -d: -f1 /etc/passwd | column

### เปลี่ยน User Owner และ Group owner

สามารถทำได้โดยใช้ในผู้ใช้ระดับ root โดยใช้คำสั่ง

- `chgrp`

        ls -l file2
        -rw-r--r--. 1 root tennis 185 Apr 8 18:46 file2
        
        chgrp snooker file2
        ls -l file2
        -rw-r--r--. 1 root snooker 185 Apr 8 18:46 file2

- `chown`

  กรณีเปลี่ยนแค่ User owner

      ls -l FileForPaul
      -rw-r--r-- 1 root paul 0 2008-08-06 14:11 FileForPaul

      chown paul FileForPaul
      ls -l FileForPaul
      -rw-r--r-- 1 paul paul 0 2008-08-06 14:11 FileForPaul

  กรณีต้องการเปลี่ยนทั้ง User owner และ Group owner

      ls -l FileForPaul
      -rw-r--r-- 1 paul paul 0 2008-08-06 14:11 FileForPaul

      chown root:project42 FileForPaul
      ls -l FileForPaul
      -rw-r--r-- 1 root project42 0 2008-08-06 14:11 FileForPaul

[//]: # ()

[//]: # (| Option  | Function           |)

[//]: # (|---------|--------------------|)

[//]: # (| file -s | ใช้สำหรับไฟล์พิเศษ |)

<br>
<hr>

# File System Hierarchy Standard (FHS)

FHS (File System Hierachy Standard) เป็นโครงสร้าง File system แบบ Tree โดยเริ่มจาก Root directory ไล่ลงมาเป็น System
directory และ User directory โดยใช้เพื่อการนิยามชื่อ ที่อยู่ และสิทธิ์การเข้าถึงของไฟล์ชนิดต่าง ๆ และ Directory
เป็นแบบลำดับขั้น (Hierarchy) หากต้องการเข้าถึงทุก Directory ต้องเข้าถึงในฐานะ Root user หรือผู้ใช้ที่มีสิทธิ์สูงสุด

### FHS Standard ได้จัดหมวดหมู่ของแต่ละ System Directory ดังนี้

- จัดในหมวด `Shareable or Not` ก็คือ Directory นั้นสามารถ Shared ผ่าน Network และใช้บนเครื่องคอมพิวเตอร์ได้หลายเครื่อง
- จัดในหมวด `Static` ไม่สามารถแก้ไขได้หรือ `Variable` สามารถแก้ไขได้
  <br>

|              | Not Shareable | Shareable |
|--------------|---------------|-----------|
| **Variable** | /var/lock     | /var/mail |
| **Static**   | /etc          | /opt      |

![](https://ndg-content-dev.s3.amazonaws.com/media/images/linux-essentials-v2/LEv2_13_2.png)

- **The /boot Directory**

  ประกอบไปด้วยไฟล์ที่จำเป็นในการ boot ระบบ อย่างพวก linux karnel เพื่อช่วยให้การ boot เป็นไปได้อย่างถูกต้อง


- **The /dev Directory(dev: device)**

  มีไว้สำหรับเก็บไฟล์อุปกรณ์(device file) ที่ใช้เพื่อเชื่อมต่อกับอุปกรณ์ต่าง ๆ ในระบบ
  ไฟล์ที่จำเป็นเพื่อให้ระบบทำงานได้อย่างถูกต้อง


- **The /etc Directory (etc: et cetera)**

  เก็บพวกไฟล์การตั้งค่าที่สำคัญต่อโปรแกรมทั้งหมด


- **The /lib Directory (lib: library)**

  เป็นส่วนสำคัญสำคัญการ booting ระบบและการทำงานของคำสั่งภายระบบ root file


- **The /media Directory**

  ประกอบไปด้วย subdirectories ที่ใช้เป็น mount point สำหรับสื่อที่สามารถถอดได้ เช่น CD-ROM


- **The /mnt Directory (mnt: mount)**

  โดยทั่วไปใช้เป็นจุดติดตั้งสำหรับระบบไฟล์ที่ติดตั้งเพิ่มเติม (การ mount ใน linux คือการทำให้ระบบของ linux
  มีความพร้อมในการอ่าน/เขียนไฟล์ที่ถูกติดตั้งเข้ามาใหม่ได้)


- **The /opt Directory (opt: optional)**

  เก็บพวก package ที่ติดตั้งมาจากภายนอก


- **The /proc Directory (proc: process)**

  เป็นไฟล์พิเศษที่ถูกสร้างขึ้นใน system memory โดยจะไม่มีการปรากฏอยู่บน disk
  โดยในส่วนนี้จะประกอบด้วยข้อมูลสำคัญเกี่ยวกับสถานะของระบบ ซึ่งมีไว้ควบคุมและจัดการทรัพยากรต่างใน kernal โดย /proc
  ต้องมีการ mounted ก่อน


- **The /sbin Directory (sbin: system binary)**

  เก็บโปรแกรมที่สามารถให้ผู้ใช้ระดับสิทธิ์สูงสุด (root user) เรียกใช้ได้


- **The /srv Directory (sys: system)**

  เก็บข้อมูลที่เฉพาะเจาะจงสำหรับบริการที่ระบบของผู้ใช้กำลังให้บริการ ตัวอย่างเช่น FTP, WWW, หรือ CVS.
  ไดเรกทอรีนี้จะแสดงตำแหน่งของไฟล์ข้อมูลสำหรับบริการที่ระบบบริการนั้น ๆ โดยเฉพาะ


- **The /sys Directory (sys: system)**

  ใช้ระบบไฟล์เสมือน (virtual file system) แบบใหม่ที่เรียกว่า sysfs มีเฉพาะกับ karnel เวอร์ชัน 2.6 กับการ support
  จากอุปกรณ์ hot plug ในเคอร์เนลเวอร์ชัน 2.6, ไดเรกทอรี /sys/ ประกอบด้วยข้อมูลที่คล้ายกับที่อยู่ใน /proc/
  แต่แสดงผลในรูปแบบลำดับชั้นข้อมูลเฉพาะเกี่ยวกับอุปกรณ์ hot plug .


- **The /usr Directory**

  ประกอบด้วยไดเรกทอรีย่อยมากมายที่สำคัญเพื่อรองรับผู้ใช้ โดยให้แอปพลิเคชัน, ไลบรารี, และเอกสาร.


- **The /var Directory (var: variable)**

  ใช้เก็บ subdirectory สำหรับงานที่ไฟล์มีการเปลี่ยนแปลงบ่อย

| Directory  | Contents                                                                                                                                                     |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /          | เป็นฐานของโครงสร้างหรือ root ของ เป็น Directory ที่รวมทุก Directory ไม่ว่าจะเป็น Partition ที่ติดตั้งในเครื่อง, อุปกรณ์ที่สามารถถอดออกได้หรือ Network shares |
| /root      | เป็น Home directory ของ Root user                                                                                                                            |
| /bin       | Binary ที่จำเป็นเช่น `ls`, `rm` โดยเป็นส่วนหนึ่งของ Root file system                                                                                         |
| /home      | Directory ที่ใช้เก็บข้อมูลและไฟล์ส่วนตัวของผู้ใช้                                                                                                            |
| /lib64     | Libraries ที่สร้างขึ้นสำหรับบางสถาปัตยกรรม มีไว้เพื่อให้ระบบสามารถรองรับหลาย ๆ สถาปัตยกรรมได้อย่างยืดหยุ่น                                                   |
| /var/cache | ไฟล์ที่ใช้เพื่อเก็บข้อมูลที่ถูก Cache โดยแอปพลิเคชัน                                                                                                         |
| /var/log   | พวก Log file                                                                                                                                                 |
| /var/lock  | ไฟล์สำหรับจัดการการเข้าถึงทรัพยากรในการ Shared ทรัพยากรร่วมกัน                                                                                               |
| /var/spool | Spool file สำหรับการ Print และที่เกี่ยวของกับ Mail                                                                                                           |
| /var/tmp   | ไฟล์ที่ถูกสร้างไว้ชั่วคราว โดยจะไม่ถูกลบเมื่อระบบทำการ Reboot                                                                                                |

[//]: # ()

[//]: # (| Comment |)

[//]: # (|---------|)

[//]: # (| koako   |)

# Reference

- [Cisco](https://content.netdevgroup.com/contents/linux-essentials/UbvrXt151d/)
- [Javapoint](https://www.javatpoint.com/linux-files#:~:text=In%20Linux%20system%2C%20everything%20is,Files%20are%20always%20case%20sensitive)
- [Redhat FHS](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/reference_guide/s1-filesystem-fhs)
- [Linuxiosys](https://linuxopsys.com/topics/file-types-in-linux)
- [Rackspace](https://docs.rackspace.com/docs/create-files-in-linux)
- [Linuxsto.pdf](https://linux-training.be/linuxsto.pdf?fbclid=IwAR0iJbUx-0Gbl3RaEXDn4iZCTVuzBy1RC7ytevA9XXRx5sxFmDS7zOYrjM8)
- [Greeksforgeeks](https://www.geeksforgeeks.org/linux-directory-structure/)
- [Redhat Linux file permissions](https://www.redhat.com/sysadmin/linux-file-permissions-explained)
- [Medium Linux file permissions](https://datafarm-cybersecurity.medium.com/file-permissions-in-linux-4e671dee72ca)
- [The Complete Reference LInux Sixth Edition.pdf](https://doc.lagout.org/operating%20system%20/linux/Linux%20-%20The%20Complete%20Reference.pdf?fbclid=IwAR07KOfQrR5c1Rd2Vrcew7x8vSd_QI-79OQNH7jnA_grvO_osKb-6V_1740)
