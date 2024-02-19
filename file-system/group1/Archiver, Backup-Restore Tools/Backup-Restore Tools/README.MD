# Backup/Restore Tools

## ประเภทของ Backup:

- Full backup: สำรองข้อมูลทั้งหมดในระบบ
- Incremental backup: สำรองข้อมูลเฉพาะส่วนที่เปลี่ยนแปลงหลังจาก full backup ครั้งล่าสุด
- Differential backup: สำรองข้อมูลทั้งหมดที่เปลี่ยนแปลงหลังจาก full backup ครั้งล่าสุด

## วิธีการ Backup:

- Local backup: สำรองข้อมูลไปยังอุปกรณ์เก็บข้อมูลภายใน เช่น ฮาร์ดดิสก์
- Remote backup: สำรองข้อมูลไปยังอุปกรณ์เก็บข้อมูลภายนอก เช่น เซิร์ฟเวอร์ FTP หรือ cloud storage

## เครื่องมือ Backup:
- tar: เครื่องมือพื้นฐานสำหรับการ backup และ restore ไฟล์
- cpio: เครื่องมือที่คล้ายกับ tar แต่มีประสิทธิภาพมากกว่า
- rsync: เครื่องมือสำหรับการสำรองข้อมูลแบบ incremental และ differential 
และ สามารถสำรองข้อมูลและกู้คืนข้อมูลระหว่างสองไดเร็กทอรีได้
- dump: เครื่องมือสำหรับการสำรองข้อมูลระบบไฟล์
- dd : เป็นเครื่องมือในการสร้าง file backup ข้อมูลภายใน hardisk ที่เชื่อมต่ออยู่ และทำการ wirte ลง file ที่กำหนด

## การ Restore ข้อมูล:

- การ Restore จาก full backup: คืนค่าระบบทั้งหมดจาก backup
- การ Restore จาก incremental backup: คืนค่าระบบจาก full backup และ incremental backup ล่าสุด
- การ Restore จาก differential backup: คืนค่าระบบจาก full backup และ differential backup ล่าสุด

## ตัวอย่างการใช้งาน 

### tar
```shell
tar -cf etc.tar /etc
```
- การ backup ไฟล์


```shell
tar -xf etc.tar
```
- การ restore ไฟล์

### cpio
```shell
cpio -cvf <ชื่อไฟล์สำรอง.cpio> <ไฟล์หรือไดเร็กทอรี>
```
- สร้างไฟล์สำรอง:
```shell
cpio -ivf <ชื่อไฟล์สำรอง.cpio>
```
- กู้คืนไฟล์ทั้งหมด

```shell
cpio -ivf <ชื่อไฟล์สำรอง.cpio> <ชื่อไฟล์>
```
- กู้คืนไฟล์บางไฟล์:

### rsync
```shell
rsync -av <source_directory> <destination_directory>
```
- สำรองข้อมูลไปยังไดเร็กทอรีระยะไกล
#### option ของ `rsync`
| option | Description    |
|----|---------------|
| -a  |ถ่ายโอนข้อมูลทั้งหมด (สิทธิ์ ความเป็นเจ้าของ โหมด)|
| -v| แสดงรายละเอียดเกี่ยวกับกระบวนการ    |
|-r|บีบอัดข้อมูลระหว่างการถ่ายโอน |
| -z  | บีบอัดข้อมูลด้วย gzip      |
| -e  |  ระบุวิธีการเข้ารหัส (เช่น ssh)    |
| -u  |อัปเดตไฟล์ที่มีอยู่ในไดเร็กทอรีต้นทางเท่านั้น  |
| -d  |ลบไฟล์ที่ถูกลบออกจากไดเร็กทอรีต้นทาง  |


## dump

### ตัวอย่างโครงสร้าง
```shell
dump <level> <filesystem> <device>
```
- <level> ระดับการสำรองข้อมูล (0 - 9)
- <filesystem> ระบบไฟล์ที่จะสำรองข้อมูล
- <device> อุปกรณ์ที่จะเก็บไฟล์สำรองข้อมูล
```shell
dump -0uf /dev/tape /
```
- การ backup ระบบไฟล์ทั้งหมด

```shell
restore -rf /dev/tape
```
- การ restore ระบบไฟล์ทั้งหมด

## dd

### ตัวอย่างโครงสร้างการใช้ dd
```shell
dd if=<source file name> of=<target file name> [Options]
```
### ตัวอย่างการใช้ dd
```shell
dd if=/dev/sda of=/dev/sdb
```
- ทำการ clone hardisk จากลูกหนึ่งไปอีกลูกหนึ่ง
```shell
dd if =/dev/sda2 of=~/hdadisk.img
```

- ทำการ backup partition ที่ต้องการ ไปยัง file ที่กำหนด
```shell
dd if=hdadisk.img of=/dev/sdb3
```
ทำการ restore จาก backup image

## Reference:

* https://saixiii.com/dd-linux-command/
* https://www.geeksforgeeks.org/dump-command-in-linux-with-examples/
* https://arit.rmutsv.ac.th/th/blogs/82-วิธีการใช้-rsync-เพื่อสำรองข้อมูล-บน-linux-1052
* https://www.geeksforgeeks.org/tar-command-linux-examples/ 
* https://www.geeksforgeeks.org/cpio-command-in-linux-with-examples/