# cron
**cron** มีรากฐานมาจากคำว่าภาษากรีก chronos มีความหมายว่า เวลา ซึ่ง cron ก็คือ list ของคำสั่งที่ถูกตั้งเวลาไว้ล่วงหน้า

โดย มี
- <ins>**crond**</ins> หรือ **cron deamon** มีหน้าที่ในการรัน task หลายๆ task ตามเวลาที่ได้กำหนดไว้ล่วงหน้า
- <ins>**crondtab**</ins> หรือ **cron tables**  เป็นตัวแก้ไข list ของคำสั่งที่ต้องการจะจัด scheduler สามารถ แก้ไข ลบ หรือ list รายการได้
- <ins>**cron job**</ins> คือ program ที่ run ผ่าน cron

## crontab
เราจะพบ crontab files อยู่ใน 
- <ins>โดยทั่วไป</ins> มักจะพบใน ``` /etc/crontab/```  file
- ส่วน<ins>เพิ่มเติม</ins>จะอยู่ใน ```/etc/cron.d``` directory 
- directory : ```/etc/spool/cron```

แต่ก่อนที่เราจะแก้ไข จัดการ crontab ได้นั้น จะต้องมีสิทธิ์พิเศษของผู้ดูแลระบบก่อน (มีสืทธิ์ที่จะแก้ไข)

## syntax ของ crontab
ในการที่จะติดตั้ง cron job นั้น เราต้องทำการ สร้างบรรทัดที่แสดงด้านลง ลงใน crontab file
```
 $ <minute> <hour> <day of the month> <month> <day of week> comand
```

|     field      |            value            |
|:--------------:|:---------------------------:|
|     minute     |           0 - 59            |
|      hour      |           0 - 23            |
|day of the month|           1 - 31            |
|     month      |           1 - 12            |
|  day of week   |       0 (Sunday) - 6        |
|     comand     |คำสั่งที่เราต้องการจะ execute|


ใช้
- <ins>เครื่องหมายดอกจันท์ *</ins> แทนตัวเลขนั้น ก็หมายความว่า ใช้ทุกค่าที่เป็นไปได้ของ ตำแหน่งงนั้น เช่น * ตรง minute ก็คือเอาทุกช่วง ตั้งแต่ 0 - 59 หรือเรียกง่ายๆ ก็คือ ทำทุกรอบ ทุก 1 นาที แต่ถ้า */5 ก็จะเป็น ทุกๆ 5 นาที
-  <ins>เครื่องหมาย - </ins>  ก็คือบอกช่วง เช่น 10 - 15
- <ins>เครื่องหมาย , </ins> ในการแยก value

เช่น
```
$ */5 * * * * root /usr/root/bkup.sh -> ทำงานทุกๆ 5 นาที
$ 30 22 * * * dev /usr/dev/ant_build.sh -> ทำงานทุกวัน เวลา 22:30 น.
```
ตัวอย่างข้างต้น จะเป็น system crontab แต่ถ้าเป็น user crontab ก็สามารถทำได้ โดยการเปลี่ยนจาก command เป็น user name

นอกจากนี้ เรายังสามารถใช้ keyword มาแทน การเขียน แต่ล่ะ field ได้

| Keyword | meaning |field |
|:--:|:--:|:--:|
|@reboot |ทำงาน**ครั้งเดียว**,ทำงานตอนที่ระบบ<ins>เริ่มต้นทำงาน</ins>  | |
|@yearly| **1 ปีครั้ง** | 0 0 1 1 * |
| @annually | ความหมายเดียวกับ @yearly | |
|@monthly | **1 เดือนครั้ง** |0 0 1 * * |
|@weekly | **1 อาทิตย์ครั้ง** | 0 0 * * 0 |
|@daily |**1วันครั้ง** | 0 0 * * * |
|@midnight |ความหมายเดียวกับ @daily | |
|@hourly | **ทุกชั่วโมง** | 0 * * * * |


## option ของ crontab
เพราะ user ไม่สามารถเข้าถึงdirectory ของ user crontab files ได้ จึงต้องใช้ crontab ให้มันโชว์ และ สามารถแก้ไขได้
โดยมีคำสั่งต่อไปนี้

  - ``` crontab filename ``` : เอาคำสั่ง crontab จากไฟล์อื่น
  - ``` crontab -e ```  หรือ    ``` crontab -u <your_username> -e ``` แก้ไข crontab 
	  - ซึ่งโดยปกติแล้ว default จะให้เป็น vi editor แต่เราสามารถเปลี่ยน ตัว editor โดยการตั้งค่า ``` export EDITOR=<editor name> ```
	  - หลังจากแก้ไขแล้ว ก็จะ save ให้อัตโนมัติ
  - ```crontab -l``` หรือ ```crontab -u <your_username> -l ```ดูคำสั่ง crontab ทั้งหมดในปัจจุปัน
  - ``` crontab -r ``` ลบคำสั่ง crontab ทั้งหมด
  - ``` crontab -u user ``` ควบคุม user crontab

## crond
crond มักจะอ่านจาก ``` /etc/crontab/``` ซึ่งเป็นที่ๆเก็บ package ต่างๆที่ใช้ คุมควบ กำหนด task ต่างๆ โดยปกติแล้ว program software ก็จะสร้าง crontab file ไว้ที่นี้ รวมถึง ติดตั้ง หรือ ลบสิ่งที่ไม่จำเป็น

crond จะทำงานทุกๆ 1 นาที โดยจะตรวจสอบว่ามีงานหรือคำสั่งอะไรมั้ย ถ้าเจอก็จะทำ ซึ่งมักจะไม่จำเป็นจะต้อง restart ตัว crond นอกซะจากว่า crontab จะมีการ update

root user สามารถควบคุมได้ ไม่ว่าจะเป็น
``` 
$ /etc/init.d/crond start
```
``` 
$ /etc/init.d/crond stop
```
``` 
$ /etc/init.d/crond restart
```

## ควบคุมการเข้าถึง cron
ใช้```/etc/cron.allow``` และ```/etc/cron.deny``` ที่สร้างโดย root user ซึ่งมี list ของ user ถูกเก็บไว้

- ถ้าไม่มีทั้ง 2 ไฟล์ ก็จะไม่มีใครเข้ามาแก้ไข crontab ได้
- ถ้ามีแค่ ```/etc/cron.allow``` อย่างเดียว คนที่อยู่ใน list ก็จะสามารถแก้ไขได้
- ถ้ามีแค่ ```/etc/cron.deny``` อย่างเดียว ผู้คนใน list ก็จะไม่มีสิทธิ์แก้ไขได้

ดังนั้น การมีทั้ง 2 file นั้น
```/etc/cron.allow``` จะถูกใช้ และ ```/etc/cron.deny``` จะถูกมองข้ามไป

เช่น
มีผู้ใช้ 10 คน ก็การจำกัดสิทธิ์ แค่ 2 คน ก็เอา 2 คนนั้นใส่ใน ```/etc/cron.allow``` ไม่ต้องสร้าง deny
> แต่ถ้าอยากไม่ให้สิทธิ์เพียง 2 ก็คือ ก็ทำตรงข้าม ใส่ 2 คนนั้นใน ```/etc/cron.deny``` และ ไม่ต้องสร้าง allow

ถ้า user นั้นอยู่ใน list ของ ```/etc/cron.deny``` ก็จะเห็นข้อความว่า คุณไม่มีสิทธิ์เข้าถึงนั้นเอง
