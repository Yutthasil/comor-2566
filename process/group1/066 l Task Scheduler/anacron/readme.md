# anacron
เป็นคำสั่งที่ใช้เรียกเป็น ระยะ มีข้อดีคือ สามารถใช้งานได้กับเครื่องที่ทำงานไม่ต่อเนื่องได้ ต่างจาก cron ก็คือ ถ้าไม่ทำงานตามที่ตั้งไว้ก็จะข้ามไปเลย แต่ anacron จะตรวจสอบ timestamp ของงาน และตัดสินใจที่จะเริ่มทำงานมั้ย ถ้า timestamp เกินจำนวนวันที่กำหนด ก็จะ เกิด delay

anacron เหมานสำหรับงานที่กำหนดตามรายวัน รายสัปดาห์ และรายเดือน


ซึ่งก็จะมีไฟล์ที่สำคัญ 2 ตัวคือ
- ``` /etc/anacrontab``` ที่เก็บงาน anacron
- ```/var/spool/anacron``` ที่เก็บไฟล์ timestamp

## anacron command
สามารถกำหนดเวลางาน ได้ดังคำสั่งข้างล่าง
```
<period>   <delay>   <job-identifier>   <command>
```
-  **period** หรือ ระยะเวลา : บอกเป็นความถี่ เป็น @daily @weekly etc. หรือ จะระบุเป็นตัวเลขก็ได้
-  **delay**  หรือ ล่าช้า : ใส่เวลาให้ รอ ก่อนเริ่มทำ หน่วยเป็น นาที
- **job-identifier** หรือ รหัสงาน : เป็นชื่อเฉพาะของงาน
-  **command** : คำสั่ง

โดยที่ anacron จะเช็คว่า timestamp ยังอยู่ในช่วงมั้ย ถ้าเลย ก็จะ delay ตามที่ได้กำหนดไว้ เมื่องานเสร็จ เมื่อเสร็จแล้ว ก็จะบันทึกวันที่ลงใน  ```/var/spool/anacron``` และ ระบุไฟล์ job-id ด้วย

ตัวอย่าง
```
@daily    10    example.daily   /bin/bash /home/aaronkilik/bin/backup.sh
```
จากตัวอย่างนี้ ถ้าเครื่องปิด ก็เริ่มทำงานหลัง 10 นาที จากที่เรากำหนด delay เอาไว้

มี 2 ตัวแปรที่สำคัญ คือ 
 - START_HOURS_RANGE : ช่วงเวลาที่งานเริ่ม
 - RANDOM_DELAY :  ตั้ง delay แบบ สุ่ม เพื่อเพิ่ม delay โดย ค่าเรื่มต้นจะเป็น 45

ไฟล์ anacron ก็จะมีหน้าตาแบบนี้
```
# /etc/anacrontab: configuration file for anacron

# See anacron(8) and anacrontab(5) for details.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
HOME=/root
LOGNAME=root

# These replace cron's entries
1       5       cron.daily      run-parts --report /etc/cron.daily
7       10      cron.weekly     run-parts --report /etc/cron.weekly
@monthly        15      cron.monthly    run-parts --report /etc/cron.monthly

@daily    10    example.daily   /bin/bash /home/aaronkilik/bin/backup.sh
```

## syntax
 ```
anacron [-s]  [-f]  [-n] [-d] [-q] [-t anacrontab] [-S spooldir] [job]
anacron [-S spooldir] -u [-t anacrontab] [job] ...
 anacron [-V|-h]
 anacron -T [-t anacrontab]
  ```

option :
-   ```-f ``` : บังคับ execute ไม่สน timestamps
-   ```-u ``` : แค่ update timestamps ไม่ได้ run อะไร
-   ```-s ``` : ทำงานแบบ Serialize หรือเรียงคิว (จะไม่เริ่มใหม่ จนกว่างานก่อนหน้าจะเสร็จ)
-   ```-n ``` : run ทันที ไม่สน delay
-   ```-d ``` : ไม่มีการ fork ไปเบื้องหลัง แจ่มีการส่งข้อมูลไป รวมถึงที่ syslog ด้วย และ ผลลัพธ์ของงานก็จะถูกส่งทาง email
-   ```-q ``` : ไม่แสดงข้อความเบื้องหลัง ใช้ได้กับ  ```-d``` เท่านั้น
-   ```-V ``` (Use specified anacrontab) :  แสดงข้อมูลเวอร์ชั่น
-   ```-h``` (Use specified anacrontab) :  แสดงข้อความการใช้งานสั้นๆ
