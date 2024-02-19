# Process-1

Computer Organization and Operating System Assignment (Chapter : Process, Sec : 1)

  

# บทคัดย่อ

  โครงงานในครั้งนี้มีวัตถุประสงค์เพื่อศึกษา ค้นคว้า และทำความเข้าใจเกี่ยวกับ Process ว่าคืออะไร มีขั้นตอนอะไรบ้าง ทำงานอย่างไร และมีคุณสมบัติอย่างไร โดยศึกษาค้นคว้า รวบรวมและ วิเคราะห์ข้อมูลจากอินเทอร์เน็ต เพื่อเผยแพร่ความรู้ให้กับผู้คนทั่วไป 
และผู้คนที่สนใจ เพื่อให้เกิดประโยชน์ และองค์ความรู้ต่อส่วนรวม โดยเผยแพร่ผ่านทางออนไลน์ ทางgithub
  
  ในการทำโครงงานครั้งนี้ทางคณะผู้จัดทำได้จัดทำโครงงานผ่านgithub รวมถึงได้แยกการนำเสนอเป็นหัวข้อต่างๆ เช่น Boot Process, Process Management, Service Management เพื่ีอ ความง่าย และสะดวกต่อต่อการเข้าถึง ค้นหา และค้นคว้าเกี่ยวกับ Process


# Boot Process

Boot Process ของ Linux เป็นส่วนสำคัญของฟังก์ชันการทำงาน เนื่องจากเป็นขั้นตอนเริ่มต้นของการเริ่มต้นระบบปฏิบัติการ การทำความเข้าใจกระบวนการบูท Linux ถือเป็นสิ่งสำคัญสำหรับผู้ดูแลระบบ นักพัฒนา และใครก็ตามที่ทำงานกับ Linux

### Boot Process คืออะไร ?
Boot Process เป็นลักษณะพื้นฐานของระบบปฏิบัติการใดๆ เป็นกระบวนการที่ทำการ โหลดระบบปฏิบัติ(OS)ลงในหน่วยความจำ(Memory)ของคอมพิวเตอร์, กำหนดค่าเริ่มต้นของส่วนประกอบต่างๆ และเตรียมที่จะดำเนินการ แอปพลิเคชันของผู้ใช้

Boot process ของ Linux ประกอบด้วยหลายขั้นตอนที่มีความสำคัญต่อการทำงานของระบบปฏิบัติการ ซึ่งขั้นตอนต่างๆ ของกระบวนการบูทใน Linux มีดังนี้
## ขั้นตอน Boot Process ของ Linux
1.  [**System startup:**](/BootProcess/SystemStartup/README.MD) เป็นขั้นตอนแรกที่เกิดขึ้นเมื่อทำการเปิดเครื่อง มันจ่ายไฟฟ้าให้กับส่วนประกอบหลักทำงาน เช่น BIOS,UEFI ซึ่งโปรแกรมนี้จะทำการตรวจสอบฮาร์ดแวร์และสร้างการเชื่อมต่อเพื่อติดต่อกับอุปกรณ์ภายในเครื่องเพื่อทำให้เครื่องพร้อมรับคำสั่งต่อไป
2.  [**Bootloader Stage:**](/BootProcess/BootloaderStage/README.md) หลังจากขั้นตอนที่ 1 และสถานะของเครื่องปกติ ตัว BIOS,UEFI จะทำการ boot ตัว 
 storage ต่างๆ เพื่อหา bootloader ซึ่งจะทำหน้าที่เลือกและโหลดระบบปฏิบัติการที่จะเริ่มต้น เมื่อผู้ใช้เลือกระบบปฏิบัติการที่ต้องการเริ่มต้น โปรแกรมบูตโลดเดอร์จะโหลด kernel และ initramfs(ถ้ามี)
ใน linux ก็จะมี bootloader หลักๆคือ 
> - [LILO  (LInux Loader)](/BootProcess/BootloaderStage/README.md#LILO)
> - [GRUB/GRUB2 (Grand Unified Bootloader)](/BootProcess/BootloaderStage/README.md#GRUB)
3. [**Kernel Stage:**](/BootProcess/Kernel/README.md) โปรแกรมบูตโลดเดอร์จะโหลด kernel ของระบบปฏิบัติการ Linux ลงในหน่วยความจำ (RAM) และเริ่มต้นการทำงานของ kernel ซึ่งรวมถึงการเข้าถึงทรัพยากรของเครื่องคอมพิวเตอร์ที่จำเป็นสำหรับการทำงาน
4. [**Init process:**](/BootProcess/InitProcess/README.md) Kernel จะเริ่มต้นกระบวนการ init ซึ่งเป็นโปรแกรมแรกที่เริ่มต้นในระบบของ Linux ในที่นี้ parent ของกระบวนการ Linux ทั้งหมดคือ Systemd ตามขั้นตอนการบูต Systemd จะดำเนินการต่างๆ
โปรแกรม init จะมี PID (Process ID) เป็น 1 และมีหน้าที่เป็นตัวควบคุมการทำงานของกระบวนการอื่นๆ ในระบบ เช่น การสร้างกระบวนการ(process) อื่นๆ และการจัดการกับบริการ(service) ต่างๆ
6. [**Runlevel/Target:**](/BootProcess/Runlevels/README.md) ในระบบปฏิบัติการ Linux จะมีสถานะ runlevel หรือ target เป็นตัวเลขตั้งแต่ 0-6 เพื่อระบุสถานะการทำงานของระบบ จากนั้นโปรแกรม init จะโหลดการกำหนดค่าของ runlevel หรือ target และเริ่มต้นการบริการตามที่กำหนด
# Process Management

### Process Management คืออะไร ?

Process Management คือ งานในการควบคุมและติดตาม processes ที่ทำงานอยู่บนระบบ Linux โดยรวมไปถึงกระบวนการจัดการทรัพยากร, การจัดลำดับการทำงานบน CPU, และการยกเลิกกระบวนการเมื่อจำเป็น  

## ประเภทของ Processes

### Foreground processes หรือ interactive processes

processes เหล่านี้จะไม่ได้ intitialize จากระบบต้องถูกดำเนินการโดยผู้ใช้หรือโปรแกรมเมอร์ processes เหล่านี้จะรับ input และส่ง output คืนกลับไป ในขณะที่ processes เหล่านี้กำลังทำงานอยู่เราจะไม่สามารถเริ่ม process ใหม่ได้ใน terminal เดียวกัน

### Background processes หรือ non interactive processes

processes เหล่านี้จะถูกดำเนินการโดยจากระบบหรือผู้ใช้ก็ได้ processes เหล่านี้มี PID หรือ process เฉพาะและสามารถเริ่ม processes ใน terminal เดียวกันได้

## สถานะของ process ใน Linux

- **Running :** process ที่กำลังดำเนินการอยู่ใน CPU

- **Sleeping :** process ที่กำลังรอให้ทรัพยากรที่จะใช้นั้นว่าง

-  **Stopped :** process ที่ถูกทำลายโดยผู้ใช้

-  **Zombie :** process ที่ดำเนินการเสร็จเรียบร้อยแล้วแต่ยังไม่ได้ถูกล้างโดยระบบ

-  **Orphan :** process ปัจจุบันที่ parent process ถูกทำลายไปแล้ว  

## ตัวอย่างคำสั่งของ Process Management ใน Linux

|คำสั่ง|คำอธิบาย|วิธีการใช้|
|----|--------------|--------------|
|ps|แสดงข้อมูลเกี่ยวกับ processes ที่ทำงานอยู่|`ps`|
|top|ให้ข้อมูลแบบ real-time เกี่ยวกับ processes ระบบและทรัพยากรที่ถูกใช้งาน|`top`|
|kill|ทำลาย process นั้นโดยการส่งสัญญาณไปยัง process นั้น|`kill [process_id]`|
|nice|ปรับลำดับความสำคัญของ process|`nice -n [priority] [command]`|
|renice|เปลี่ยนลำดับความสำคัญของ process ที่กำลังทำงานอยู่|`renice [priority] [process_id]`|
|pidof|แสดงหมายเลข ID ของ process|`pidof [process_name]`|
|jobs|แสดงรายการงานทั้งที่กำลังทำงานหรือหยุดทำงานไปแล้ว|`jobs`|
|bg|สำหรับการส่ง process ที่กำลังทำงานไป background|`bg [job_id]`|
|fg|สำหรับการส่ง process ที่กำลังทำงานไป foreground|`fg [job_id]`|

## Process Management ในทางปฏิบัติ

### การระบุและการยุติ processes ใน Linux

การระบุและการยุติ processes สามารถทำได้โดยใช้คำสั่งเหล่านี้ใน Linux
คำสั่ง`PS`ใช้ในการหา process ID (PID) ของ process ที่ต้องการจัดการ ตัวอย่างเช่น ถ้าหากจำเป็นที่ต้องปิด process นั้นก็ต้องรู้ process ID (PID) ของตัวนั้นที่แน่ชัดก่อน  
คำสั่ง`kill`ใช้เพื่อทำลาย processes ด้วย process ID (PID)  
คำสั่ง`killall`ใน Linux ใช้เพื่อทำลาย processes ด้วยชื่อ เป็นการทำลาย process วิธีที่มีประสิทธิภาพโดยมันจะทำการส่งสัญญาณไปยัง processes ตามชื่อที่ได้มีการระบุไว้

### การจัดลำดับความสำคัญของ Processes ใน Linux
การจัดลำดับความสำคัญของ process ที่กำลังทำงานอยู่สามารถทำได้โดยใช้คำสั่ง `nice`  `renice` ใน Linux  
คำสั่ง`nice`ใน Linux ใช้เพื่อปรับลำดับความสำคัญของ process โดยจะกำหนดลำคัญความสำคัญที่ต่ำกว่าให้กับ process เพื่อลดการใช้ทรัพยากร  
คำสั่ง`renice`ใน Linux ใช้เพื่อปรับลำดับความสำคัญของ process ที่เริ่มการทำงานไปแล้ว โดยสามารรถปรับเพ่ิ่มหรือลดลำดับความสำคัญของ process ได้ขึ้นอยู่กับค่าที่ระบุ
### การวิเคราะห์ทรัพยากรที่ใช้ใน Linux
คำสั่ง`top`ใน Linux ใช้เพื่อการแสดงข้อมูลเกี่ยวกับ process แบบ real-time ที่ทำงานอยู่บนระบบรวมไปถึงการใช้ CPU และ memory โดยจะมี interface ที่ช่วยให้ผู้ใช้ตรวจสอบและจัดการ processes ได้

  

# Service Management

### Service คืออะไร ?

บริการ(Service) คือ โปรแกรมที่ทำงานบน server ตลอดเวลา บริการที่ทำงานบนระบบ Linux มักจะเป็นส่วนสำคัญในการเปิดให้บริการและประสิทธิภาพของระบบคอมพิวเตอร์ด้วยวิธีต่างๆ ที่สามารถปรับแต่งได้ตามความต้องการของผู้ใช้ เช่น Apache web server, MySQL database server, SSH server

### Service Management คืออะไร ?

Service Management คือ ระบบควบคุมและดูแลบริการที่ทำงานบนระบบปฏิบัติการ Linux ด้วยเครื่องมือต่างๆที่มีอยู่ในระบบ หรือชุดคำสั่ง หรือการจัดการผ่านหน้าต่าง (GUI) หรือหน้าอินเตอร์เฟส (CLI) ซึ่งทำให้ผู้ดูแลระบบสามารถเริ่มต้น/หยุดบริการ, ตั้งค่าใหม่ และตรวจสอบสถานะของบริการได้

ใน Linux, บริการ(Service) เป็นสคริปต์ที่ทำงานในพื้นหลัง มันจะตรวจสอบเพื่อรับคำขอที่เข้ามาและส่งคำตอบขึ้นอยู่กับคำขอที่ได้รับอย่างต่อเนื่อง 
บริการแตกต่างจากกระบวนการ(Process) เนื่องจากระบบคือแอปพลิเคชันหรือสคริปต์ที่สามารถทำงานได้ทั้งใน foreground หรือ background

สคริปต์ใดๆนั้นสามารถถูกแปลงเป็นบริการ systemd ที่จะทำงานโดยอัตโนมัติเมื่อระบบเริ่มต้นขึ้น `systemd` ให้เราใช้คำสั่งชุด `systemctl`

## Init System
วัตถุประสงค์พื้นฐานของระบบ `Init` คือเริ่มส่วนประกอบที่ต้องเริ่มต้นหลังจากที่ไคเนิล Linux ถูกบูต (ที่รู้จักโดยทั่วไปว่า "userland") ระบบ Init ยังใช้เพื่อจัดการบริการและเดมอนสำหรับเซิร์ฟเวอร์ในทุกจุดขณะที่ระบบกำลังทำงาน

## Systemd 
Systemd เป็นระบบ init และผู้จัดการระบบที่ได้รับความนิยมอย่างแพร่หลายและกลายเป็นมาตรฐานใหม่ของระบบปฏิบัติการ Linux
ใน systemd, หน่วยหลักสำหรับการดำเนินการคือ `units` ซึ่งเป็นทรัพยากรที่ systemd รู้จักจัดการได้ หน่วยถูกจัดประเภทตามประเภทของทรัพยากรที่พวกเขาแสดงแทนและถูกกำหนดด้วยไฟล์ที่เรียกว่าไฟล์หน่วย (Unit files) ประเภทของแต่ละหน่วยสามารถนำมาคาดเดาได้จากคำต่อท้ายที่ปรากฏในไฟล์

สำหรับงานการจัดการบริการ, หน่วยเป้าหมายจะเป็นหน่วยบริการ (Service Units) ซึ่งมีไฟล์หน่วยที่มีคำต่อท้ายเป็น `.service` อย่างไรก็ตาม สำหรับคำสั่งส่วนมากขอการจัดการบริการนั้นสามารถไม่ต่อท้ายด้วย .service ได้ เพราะ systemd รู้ว่าคุณน่าจะต้องการดำเนินการบริการเมื่อใช้คำสั่งการจัดการบริการ
### ประเภทหน่วยและนามสกุลไฟล์

| ประเภทหน่วย         | นามสกุลไฟล์ | คำอธิบาย                                          |
|----------------------|--------------|----------------------------------------------------|
| หน่วยบริการ          | .service     | บริการระบบ                                    |
| หน่วยเป้าหมาย         | .target      | กลุ่มของหน่วย systemd                          |
| หน่วย Automount        | .automount   | จุด automount ของระบบไฟล์                     |
| หน่วยอุปกรณ์          | .device      | ไฟล์อุปกรณ์ที่ระบบรู้จัก                    |
| หน่วย Mount           | .mount       | จุด mount ของระบบไฟล์                         |
| หน่วย Path            | .path        | ไฟล์หรือไดเรกทอรีในระบบไฟล์                 |
| หน่วย Scope           | .scope       | กระบวนการที่สร้างขึ้นภายนอก                 |
| หน่วย Slice           | .slice       | กลุ่มของหน่วยที่จัดลำดับตามลำดับขั้นตอนการจัดการกระบวนการระบบ|
| หน่วย Socket          | .socket      | Socket สื่อสารระหว่างโปรเซส                   |
| หน่วย Swap            | .swap        | อุปกรณ์ swap หรือไฟล์ swap                     |
| หน่วย Timer           | .timer       | ไทมเมอร์ของ systemd                             |     

### ตำแหน่งของหน่วย systemd ที่มีทั้งหมด

| ไดเรกทอรี                        | คำอธิบาย                                                            |
|----------------------------------|---------------------------------------------------------------------|
| /usr/lib/systemd/system/         | หน่วย systemd ที่กระจายมาพร้อมกับแพ็คเกจ RPM ที่ติดตั้ง              |
| /run/systemd/system/            | หน่วย systemd ที่สร้างขึ้นในเวลาที่เรียกใช้ระบบ                             |
| /etc/systemd/system/            | หน่วย systemd ที่สร้างและจัดการโดยผู้ดูแลระบบ                                |

### คุณสมบัติของ Systemd

- การเริ่มต้นอย่างรวดเร็ว
    > Systemd ให้การพาราเลลที่มีระบบทำงานมากกว่า UpStart ลดเวลาที่ใช้ในการบูตระบบปฏิบัติการผ่านการกระตุ้นด้วย Socket และ D-Bus ซึ่งจะลดเวลาที่ใช้ในการบูตระบบปฏิบัติการ

- การกระตุ้นตามคำขอ (On-Demand Activation)
    > ต่างจาก SysVinit, systemd กระตุ้นบริการเมื่อมีคำขอเท่านั้น, ลดการกระตุ้นที่ไม่จำเป็นของกระบวนการบริการพื้นหลังในระหว่างการบูตระบบ นำไปสู่การบูตระบบที่เร็วขึ้นและการใช้ทรัพยากรระบบได้อย่างมีประสิทธิภาพ

- การจัดการวงจรชีวิตของบริการโดย Cgroups
    > Systemd ติดตามและจัดการวงจรชีวิตของบริการโดยใช้ Cgroups ซึ่งทำให้การหยุดบริการง่ายขึ้นด้วย Cgroups, ทำให้แน่ใจได้ว่าบริการที่เกี่ยวข้องถูกใส่ใน Cgroup เดียวกัน, ทำให้ง่ายต่อการค้นหาและหยุดบริการ

- การจัดการจุด Mount และ Automount
    > Systemd จัดการจุด Mount ระบบไฟล์ที่ติดตั้งไว้ใน /etc/fstab ทำให้สามารถ Mount อัตโนมัติในขณะที่ระบบเริ่มต้นที่เข้ากันได้กับ /etc/fstab, และรองรับการ Mount และ Unmount ตามคำขอโดยไม่ต้องการ autofs

- การจัดการขึ้นรายการทำรายการ (Transactional Dependency Management)
    > Systemd จัดการการทำงานพร้อมกันของงานที่มีการขึ้นรายการที่ต่อกันในระหว่างการบูตระบบ มันคำนวณการขึ้นรายการ สร้างธุรกรรมชั่วคราว และตรวจสอบความสอดคล้องกันก่อนที่จะกระตุ้นบริการ ทำให้งานที่มีการขึ้นรายการขึ้นในลำดับที่ถูกต้อง

- ความเข้ากันได้กับสคริปต์ SysVinit
    > Systemd รักษาความเข้ากันได้กับสคริปต์ SysVinit และ LSB initscripts ลดความจำเป็นในการปรับเปลี่ยน services และ processes ระหว่างการย้ายระบบ ช่วยลดต้นทุนจากการเปลี่ยนจากระบบไปสู่ systemd

- สแนปช็อตและการกู้คืนระบบ (System State Snapshots and Restoration)
    > Systemd รองรับการเริ่มต้นตามคำขอ การเปลี่ยนแปลงระบบแบบไดนามิก และการสร้างสแนปช็อตสำหรับสถานะการทำงานปัจจุบันของระบบ สแนปช็อตช่วยให้ระบบสามารถกู้คืนไปยังจุดที่ระบุได้ มีประโยชน์สำหรับการดีบั๊กและสถานการณ์การกู้คืนระบบ

## Systemctl
Systemctl เป็นเครื่องมือในโหมดคอมมานด์ไลน์ที่อนุญาตให้คุณจัดการและตรวจสอบระบบ Systemd และ Service manager มันประกอบด้วยชุดคำสั่งต่างๆ ที่ใช้ในการบริหารจัดการระบบ ไลบรารี และเดมอนที่ได้ใช้แทน init daemon รุ่นก่อนหน้า (SysV) ด้วยคำสั่งต่างๆที่มีอยู่ systemctl นั้นจะเป็นเครื่องมือที่มีประโยชน์ในการบริหารจัดการ Service ของเซิร์ฟเวอร์ ทั้งให้ข้อมูลที่ละเอียดเกี่ยวกับบริการ systemd แต่ละตัวถึงบริการที่ใช้ทั่วทั้งระบบ
### คําสั่งหลักๆ
- [**Listing Services**](https://github.com/Markkerg/Process-1/blob/main/Systemctl/Listing%20Services/README.md) (แสดงรายการบริการ)
- [**Displaying Service Status**](https://github.com/Markkerg/Process-1/blob/main/Systemctl/Display%20Status/README.md) (แสดงสถานะของบริการ)
- [**Starting and Stopping Services**](https://github.com/Markkerg/Process-1/blob/main/Systemctl/Starting%20and%20Stopping%20Services/README.md) (เริ่มและหยุดบริการ)
- [**Restarting and Reloading**](https://github.com/Markkerg/Process-1/blob/main/Systemctl/Restarting%20and%20Reloading/README.md) (รีสตาร์ทและรีโหลดบริการ)
- [**Enabling and Disabling Services**](https://github.com/Markkerg/Process-1/blob/main/Systemctl/Enabling%20and%20Disabling%20Services/README.md) (เปิดใช้งานและปิดใช้งานบริการ)
- [**Changing a Runlevel**](https://github.com/Markkerg/Process-1/blob/main/Systemctl/Changing%20a%20Runlevel/README.md) (การเปลี่ยน Runlevel)
- [**Shutting Down, Suspending, and Hibernating**](https://github.com/Markkerg/Process-1/blob/main/Systemctl/ShutDown%20Suspending%20Hibernate/README.md) (การปิดเครื่อง การหลับแบบ Suspend และ Hibernation)

# Task Scheduler

### Task Scheduler คืออะไร ?

Task Scheduler คือ ตัวตั้งเวลาเพื่อให้เริ่มการทำงานต่างๆ ช่วยในการจัดการกับงานที่ต้องการให้ระบบทำงานตามเวลาที่กำหนดหรือเหตุการณ์ที่เกิดขึ้น เราสามารถใช้เครื่องมือต่างๆ ที่มีอยู่ในระบบ Linux เพื่อทำหน้าที่เหล่านี้ได้ เช่น cron, systemd timer
แต่โดยทั่วไปแล้ว cron มักถูกใช้มากที่สุดในการจัดการ Task Scheduler ในระบบ Linux เนื่องจากมีความยืดหยุ่นและสามารถใช้งานได้ง่าย

## cron

เป็นระบบตัวจัดการ Task Scheduler ซึ่งใช้ในการทำงานตามตารางเวลาที่กำหนดไว้ ซึ่งประกอบไปด้วย 2องค์ประกอบ คือ

### 1.crontab

เป็นคำสั่งที่ใช้ในการจัดการกับตารางเวลาของ cron jobs โดย crontab จะช่วยให้ผู้ใช้สามารถสร้าง, แก้ไข และลบ cron jobs ได้โดยใช้คำสั่งที่เกี่ยวข้อง

### 2.cron daemon

ระบบ cron daemon ทำหน้าที่ตรวจสอบตารางเวลา crontab และเรียกใช้งานคำสั่งตามตารางที่กำหนด โดย cron daemon จะทำงานเป็นระยะๆ ตรวจสอบไฟล์ crontab ทุกๆ นาทีเพื่อดำเนินการตามตารางเวลาที่กำหนด


# สมาชิก

|รหัสนักศึกษา|ชื่อ-นามสกุล|ส่วนที่รับผิดชอบ|
|----------|---------------|-----------|
|65070110 |นาย นครินทร์ ทิพย์รัตน์| |
|65070175 |นาย ภาณุวิชญ์ คล้ายอุบล| |
|65070183 |นาย ภูวเดช อนันต์คูศรี|Task Scheduler + เพิ่มข้อมูล Boot Process, Process Management, Service Management|
|65070204 |นาย วรพล สาดฟัก|Process Management|
|65070226 |นาย ศุภวิชญ์ ปัทมภาสสกุล|Boot Process|
|65070230 |นาย สมิทธิพงศ์ จูปรางค์|บทคัดย่อ + Boot Process|
|65070231 |นาย สรพณ เนตรนันต์|Service Management|

  

# แหล่งอ้างอิง
### Boot Process
- https://www.scaler.com/topics/booting-process-in-linux/
- https://www.baeldung.com/linux/boot-process
- https://en.wikipedia.org/wiki/Booting_process_of_Linux
### Process Management
- https://www.scaler.com/topics/process-management-in-linux/
- https://www.geeksforgeeks.org/process-management-in-linux/
- https://unstop.com/blog/process-management-in-linux
- https://www.digitalocean.com/community/tutorials/process-management-in-linux
### Service Management
- https://schh.medium.com/linux-services-with-systemd-d0252a27ebce
- https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units
- https://docs.openeuler.org/en/docs/22.03_LTS_SP1/docs/Administration/service-management.html#systemctl-command
- https://www.liquidweb.com/kb/what-is-systemctl-an-in-depth-overview/
- https://linuxhint.com/list-service-systemd/
### Task Scheduler
- https://www.freecodecamp.org/news/cron-jobs-in-linux/
- https://phoenixnap.com/kb/set-up-cron-job-linux#basic-crontab-syntax
- https://vk9-sec.com/exploiting-the-cron-jobs-misconfigurations-privilege-escalation/
- https://www.redwood.com/article/linux-job-scheduling/
