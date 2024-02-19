## การเปลี่ยน Runlevel
ใน Systemd แนวคิดของ runlevels ได้ถูกแทนที่ด้วย targets เพื่อเพิ่มความยืดหยุ่น
### Target (เป้าหมาย)
Target เป็นประเภทพิเศษของไฟล์ Units ที่ใช้ใน systemd ที่กำหนดสถานะระบบหรือจุดซิงโครไนเซชัน ไฟล์เหล่านี้สามารถรู้จักได้จาก suffix ที่เป็น .target เสมอ
Target ใช้ในการจัดการสถานะของระบบและคล้ายกับ runlevels ที่ใช้ในระบบ init อื่นๆ แต่ละ target แทนสถานะที่เฉพาะเจาะจงของระบบได้เช่น multi-user.target graphical.target หรือ rescue.target
### การแมประหว่าง runlevels และ targets
| Runlevel | systemd Target                      | Description                                             |
|----------|------------------------------------|---------------------------------------------------------|
| 0        | runlevel0.target, poweroff.target   | ปิดระบบ                                        |
| 1, s, single     | runlevel1.target, rescue.target     | ระบบทำงานในโหมด single user                         |
| 2, 4     | runlevel2.target, runlevel4.target, multi-user.target | ระบบทำงานใน runlevel ที่กำหนดโดยผู้ใช้หรือสามารถใช้งานใน runlevel 3                    |
| 3        | runlevel3.target, multi-user.target | ระบบทำงานในโหมด multi-user แบบ non-graphical และสามารถเข้าถึงได้จากหลาย console หรือเครือข่าย   |
| 5        | runlevel5.target, graphical.target   | ระบบทำงานในโหมด multi-user แบบ graphical และสามารถเข้าถึงบริการทั้งหมดที่ทำงานในระดับ 3 ผ่านการเข้าสู่ระบบกราฟิก |
| 6        | runlevel6.target, reboot.target     | ระบบทำการรีบูต                                       |
| emergency| emergency.target                   | Emergency shell                                        |

### การดู Startup Target เริ่มต้น
```
systemctl get-default
```
![get-default](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/get-default.png)

### การดูทุก Startup Target
```
systemctl list-units --type=target
```
![list-target](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/list-target.png)

### เปลี่ยน Target เริ่มต้น
```
systemctl set-default name.target
```
> systemctl set-default graphical.target

![default-target](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/default-target.png)

### เปลี่ยน Target ปัจจุบัน
```
systemctl isolate name.target
```
> systemctl isolate graphical.target

![isolate](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/isolate.png)

### เปลี่ยนไปยังโหมด Rescue
```
systemctl rescue
```
![rescue](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/rescue.png)

### เปลี่ยนไปยังโหมด Emergency
```
systemctl emergency
```
![emergency](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/emergency.png)
