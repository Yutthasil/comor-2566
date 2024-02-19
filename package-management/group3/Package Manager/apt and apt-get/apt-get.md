# apt-get

## อะไร คือ apt-get package manager
apt-get เป็น tool ที่ช่วยจัดการ package ใน Debian-based Linux เช่น Ubuntu หน้าที่หลักคือการดึงข้อมูล เเละ package จากแหล่งที่มาที่น่าเชื่อถือ 
เพื่อทำการ ติดตั้ง(install),อัพเกรด(upgrade), ลบ(removal) package รวมถึง dependency ของ package

## คำสั่งต่างๆ

### Install
ติดตั้ง package 1อันหรือมากกว่า
```
apt-get install ชื่อpackage
Example
apt-get install vim nano mc
```

ถ้าหากมี package อยู่เเล้วเเต่ต้องการที่จะย้อนกลับไปเป็น default state สามารถใช้คำสั่ง reinstall ได้
```
apt-get install –reinstall ชื่อpackage
```



### Uninstall
คำสั่งสำหรับถอนการติดตั้ง package ที่ต้องการ
```
apt-get remove ชื่อpackage
```
คำสั่งสำหรับถอนการติดตั้ง package เช่นเดียวกันเเต่จะทำการลบ configuration file ของ package ออกไปด้วย
```
apt-get purge [package_name]
```

### Upgrade
คำสั่งสำหรับ update package ทั้งหมดที่ผู้ใช้ติดตั้ง เพื่อให้ระบบรู้ว่ามีเวอร์ชันล่าสุดของ package อยู่เป็นการเตรียมการก่อนการใช้ upgrade
```
apt-get update
```
คำสั่งสำหรับติดตั้งเวอร์ชันล่าสุดของ package ที่ผู้ใช้ติดตั้ง โดยต้องทำการ update ก่อนการ upgrade
```
apt-get upgrade
```




### คำสั่งอื่นๆ
คำสั่งสำหรับทำการตรวจสอบว่ามี package ที่เกิดความเสียหายหรือไม่
```
apt-get check
```
คำสั่งสำหรับลบ files cache ของ package
```
apt-get clean
```
คำสั่งสำหรับเสดงข้อมูลของ package เช่น เวอร์ชัน, คำอธิบายของ package 
```
apt-get show
```
คำสั่งสำหรับแสดง listของ package ตามเงื่อนไขที่เรากำหนด
```
apt-get list
Ex
sudo apt-get list --installed
จะเเสดง list ของ package ที่ผู้ใช้ติดตั้งเอาไว้
```


# reference
1)https://www.geeksforgeeks.org/apt-get-command-in-linux-with-examples/
