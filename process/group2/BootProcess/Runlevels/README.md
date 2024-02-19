# Runlevel/Target
runlevel เป็นสถานะการทำงานบน Unix และ Unix-based operating system (OS) ซึ่งได้รับการตั้งค่าล่วงหน้าบนระบบที่ใช้ Linux
Runlevels มีหมายเลขตั้งแต่ 0-6 และมีหลายบทบาทสำคัญในการดำเนินงาน การบำรุงรักษา และการจัดการระบบ Linux และ Unix

## จำนวน Runlevels
ใน Unix และ Linux มี 7 runlevels เป็นตัวเลขตั้งแต่ 0-6 แต่ละ level จะมีเป้าหมายที่แตกต่างกัน
ในแต่ละ Runlevel จะมี systemd-target ของแต่ละ level อยู่ 
**systemd-targets** เป็น method ในการเริ่มต้นของ Linux-based systems เป็นคำสั่งที่เขียนออกมาซึ่งแตกต่างจากคำสั่ง runlevel ที่ประกอบด้วยตัวเลขเท่านั้น
### ฟังก์ชั่นของ runlevels มีดังนี้
| Runlevels        | ฟังก์ชัน           | Target  |
| ------------- |:-------------------------:| -------------:|
| 0      | หยุดระบบ | poweroff.target |
| 1      | ทำให้ระบบเข้าสู่ single user mode |  rescue.target  |
| 2      | รับ multiuser mode โดยไม่ต้องมีเครือข่าย |   - |
| 3 | รับ multiuser mode โดยมีเครือข่าย |  multi-user.target   |
| 4 | -      |    - |
| 5 | รับ multiuser โดยมีเครือข่าย และ X windows  |    graphical.target |
| 6 | รีบูตระบบ  |    reboot.target |
- **0:** หยุดระบบ 
- **1:** ทำให้ระบบเข้าสู่ single user mode
- **2:** รับ multiuser mode โดยไม่ต้องมีเครือข่าย
- **3:** รับ multiuser mode โดยมีเครือข่าย
- **4:** ไม่ได้ใช้
- **5:** รับ multiuser โดยมีเครือข่าย และ X windows
- **6:** รีบูตระบบ

# ความสำคัญของ Runlevels
Runlevels ของระบบสามารถระบุว่าเครือข่ายใช้งานได้หรือไม่ รวมไปถึงบูตระบบไปยังอีก runlevels นึงที่ต่างกัน ซึ่งสามารถช่วย sys admins ในการหาแนวทางแก้ไขปัญหาบางอย่างได้
ตัวอย่างเช่น การบูตระบบใน runlevel 1 (single-user mode) สามารถขจัดปัญหาต่างๆ เช่น เครื่องไม่สามารถบูตได้เนื่องจากไฟล์การกำหนดค่าที่เสียหาย หรือการบล็อกผู้ใช้ที่ได้รับอนุญาตจากการเข้าสู่ระบบเนื่องจากไฟล์ /etc/passwd ที่เสียหาย หรือลืมรหัสผ่าน โดยรวมแล้ว ระดับการทำงานช่วยให้ผู้ดูแลระบบสามารถควบคุมพฤติกรรมของระบบได้ดีขึ้น และแก้ไขปัญหาอันเนื่องมาจากพฤติกรรมที่ไม่พึงประสงค์

## วิธีดู Runlevel ปัจจุบัน
จะเป็นการดู default target 
> ### systemctl get-default
![Screenshot 2024-02-11 211731](https://github.com/Markkerg/Process-1/assets/109967528/825b652e-e331-477c-9139-92d691138ee2)

หากต้องการเปลี่ยน default target

> ### systemctl set-default multi-user.target
![Screenshot 2024-02-11 214020](https://github.com/Markkerg/Process-1/assets/109967528/7c06d33c-9c73-42de-ba7e-fbfd0f3a77b4)


## วิธีเปลี่ยน Runlevel
### เปลี่ยนเป็น runlevel 3
> ### systemctl isolate multi-user.target
![Screenshot 2024-02-11 214136](https://github.com/Markkerg/Process-1/assets/109967528/b48ac171-2138-402e-8d8a-bf3641766ed6)

### เปลี่ยนเป็น runlevel 5
> ### systemctl isolate graphical.target
![Screenshot 2024-02-11 214247](https://github.com/Markkerg/Process-1/assets/109967528/0860fdc7-13a1-42fc-a777-1c625b0815cd)




# แหล่งอ้างอิง
- https://www.techtarget.com/searchdatacenter/definition/runlevel
- https://www.tecmint.com/change-runlevels-targets-in-systemd/#:~:text=On%20Unix%2Dlike%20systems%20such,are%20referred%20to%20as%20targets.
- https://www.webopedia.com/definitions/init/
