# CPU Management
หน้าที่ของ CPU Management คือ เพื่อจัดการการทำงานของ CPU หากการใช้งานสูง จะแสดงให้เห็นว่าประสิทธิภาพของระบบไม่ดี จึงควรหลีกเลี่ยง
## TOP
เพื่อที่จะดูรายการทั้งหมดที่กำลังทำงานอยู่ทั้งหมด เราสามารถใช้คำสั่ง top ได้(Table of process) โดยจะแสดงข้อมูล users, tasks, CPU load และ memory usage
```
top
```

ผลลัพธ์:

![alt text](https://github.com/63070078/Resources-Management-3/blob/main/img/top.png?raw=true)

ซึ่งสามารถเลื่อนขึ้นหรือลงด้วยปุ่ม Page up หรือ Page down ได้


### Option
สามารถเลือกใช้ option ต่างๆได้ ดังนี้
```
#help แสดง command syntax ที่สามารถใช้ได้
top -h

#ซ่อนรายการที่เป็นสถานะ idle
top -i

#แสดง process ที่มี ID หรือ username ตรงกับข้อมูลที่ input โดย
top -u | -U [ID or name]

#กำหนดจำนวนรอบการรีเฟรชข้อมูลของ top แล้วออกจากการทำงาน
top -n [X]
```

### ในขณะที่ top กำลังทำงานสามารถใช้คำสั่งอื่นๆได้
k --> การส่งสัญญาณ เมื่อกดปุ่ม k แล้วจะสามารถใส่ค่า PID ของ process นั้นๆได้ หากไม่ใส่คำสั่งสัญญาณ จะเป็นการ kill process นั้นๆ
![alt text](https://github.com/63070078/Resources-Management-3/blob/main/img/kill1.png)
![alt text](https://github.com/63070078/Resources-Management-3/blob/main/img/kill2.png)

#### การเรียงลำดับ Process
ค่า default ของ top จะมีการเรียงลำดับจากค่าคอลัมน์ %CPU จากมากไปน้อย
สามารถใช้คำสั่งอื่นๆ เพื่อเรียงค่าได้ดังนี้
```
- M --> เรียงลำดับโดยใช้ค่า %MEM
- N --> เรียงลำดับโดยใช้ค่า PID
- T --> เรียงลำดับโดยใช้ค่า Time
- P --> เรียงลำดับโดยใช้ค่า %CPU
```

#### การเปลี่ยนหน่วย
สามารถเปลี่ยนหน่วยการแสดงผลได้ตามผู้ใช้ต้องการ โดย ปุ่ม E จะเป็นการเปลี่ยนหน่วยส่วนบนของ top และ e จะเป็นการเปลี่ยนหน่วยส่วน process ของ top
[![E-e](https://github.com/63070078/Resources-Management-3/blob/main/img/eEimg.png)


ใช้คำสั่ง q เพื่อออกจากการทำงาน
```
q
```

## mpstat
คำสั่ง mpstat สำหรับดูข้อมูลประสิทธิภาพ และการทำงานของ CPU โดยเฉพาะ แตกต่างกับ top ที่เป็นการดูประสิทธิภาพการทำงานของระบบโดยรวม
![mpstat](https://github.com/63070078/Resources-Management-3/blob/main/img/mpstat.png)
