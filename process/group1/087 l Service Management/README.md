<a id="Service-Management"></a>
# Service Management คือ
**Service Management** ป็นกระบวนการที่คอยควบคุมและดูแลบริการต่าง ๆ ที่ทำงานบนระบบคอมพิวเตอร์หรือเซิร์ฟเวอร์ เพื่อให้ระบบทำงานได้สมบูรณ์และมีประสิทธิภาพสูงสุด

### มีบทบาทหน้าที่
ให้ผู้ดูแลระบบสามารถควบคุมและดูแลการทำงานของบริการต่าง ๆ บนระบบได้อย่างมีประสิทธิภาพ นอกจากนี้ยังช่วยให้ระบบทำงานได้เสถียรและมีประสิทธิภาพตามที่ตั้งค่าไว้
นามสกุลของไฟล์ที่ใช้ในการจัดการบริการใน Linux มักจะเป็น `.service` และระบบที่ใช้มากที่สุดคือ systemd ซึ่งเป็นระบบ init และการจัดการบริการที่ได้รับการนำเข้ามามากที่สุดในหลายระบบ Linux บนเครื่องหลาย ๆ ประการ

### การจัดการของ Service Management
การจัดการ Service Management ในระบบปฏิบัติการ Linux มักใช้ระบบ init หรือ systemd เพื่อบริหารจัดการบริการ (services) ที่ทำงานในระบบปฏิบัติการนี้ โดยมีคำสั่งหลัก ๆ ดังนี้:
**System V (init.d)**
หลักการของ SysV คือการใช้ไฟล์สคริปต์ (scripts) ที่เรียกว่า init scripts หรือ init.d scripts เพื่อระบุการทำงานของแต่ละบริการที่ต้องการให้ระบบทำงาน. ไฟล์สคริปต์นี้จะถูกเก็บไว้ในไดเรกทอรี `/etc/init.d/`.
**Systemd:**
เป็นระบบ init และระบบจัดการบริการที่ถูกพัฒนาขึ้นเพื่อให้การบริหารจัดการระบบของ Linux เป็นไปอย่างมีประสิทธิภาพและเป็นระบบที่ทันสมัยมากขึ้น. โดยทั่วไป, systemd ถูกใช้แทนที่ระบบ init แบบเก่า เช่น System V (SysV) บนหลายระบบปฏิบัติการ Linux โดยเฉพาะ.

<a id="Service-Management-type"></a>
###  ประเภทของ Service Management
ในระบบปฏิบัติการ Linux มีหลายวิธี แต่วิธีที่ได้รับความนิยมมากที่สุดคือการใช้ระบบการจัดการบริการหรือ "**init system**" ซึ่งเป็นระบบที่ใช้เริ่มต้นและจัดการกระบวนการที่ทำงานในระบบปฏิบัติการ Linux หลายรุ่น ต่อไปนี้คือบรรทัดย่อของบริการหลายประเภทที่สามารถบริหารจัดการได้ใน Linux:
- **System V (SysV):** เป็นระบบ init แบบเก่าที่ใช้สคริปต์ start, stop, restart เพื่อควบคุมบริการ. สคริปต์บริการอยู่ใน `/etc/init.d/` และมักจะมีรายชื่อเรียกว่า `service`.
- **Upstart:** ใช้ในบางระบบเวอร์ชัน Linux เช่น Ubuntu 9.10 และเวอร์ชันก่อนหน้า. มีการใช้งานคล้าย SysV แต่มีการเพิ่มความสามารถในการจัดการกับการเริ่มต้นพร้อมกันของบริการ.
- **systemd:** เป็นระบบ init ที่มีความสามารถมากและเป็นที่นิยมในหลายระบบ Linux ล่าสุด เช่น Ubuntu 15.04 และหลายเวอร์ชันขึ้นไป, Fedora, Debian 8 ขึ้นไป และอื่น ๆ. systemd ให้การจัดการบริการที่มีประสิทธิภาพมากขึ้นและมีการใช้งานที่เร็ว.
- **OpenRC:** ใช้ใน Gentoo Linux และบางระบบ Linux อื่น ๆ. OpenRC มีลักษณะคล้ายกับ SysV แต่มีความยืดหยุ่นมากขึ้น.

<a id="startstopservice"></a>
### Starting and Stopping Services
เพื่อเริ่มต้นบริการ ```systemd``` โดยใช้คำสั่งที่ระบุในไฟล์หน่วยบริการ unit file ให้ใช้คำสั่ง ```start``` สามารถใช้ ```sudo``` ถ้า	กำลังทำงานในฐานะผู้ใช้ที่ไม่ใช่ root เนื่องจากการดำเนินการนี้จะมีผลต่อสถานะของระบบปฏิบัติการ
> [ข้อควรระวัง]
> "start" ไม่ได้มีอยู่จริงในรุ่นของ systemd สำหรับการเริ่มต้นบริการ แต่ในบางกรณี, คำสั่ง "sudo systemctl start [ชื่อบริการ]" อาจถูกใช้แทน โปรดตรวจสอบคำสั่งที่ถูกต้องในระบบของคุณ.
```
	$ sudo systemctl start <application> service
````
อย่างที่กล่าวถึงข้างต้น ***systemd*** รู้จักค้นหาไฟล์ ```*.service ```เพื่อให้บริการคำสั่งการจัดการบริการ ดังนั้น, คำสั่งสามารถพิมพ์ได้ตามนี้:
```
	$ sudo systemctl start <application>
````
แม้ว่าคุณสามารถใช้รูปแบบด้านบนสำหรับการบริหารจัดการทั่วไปได้, อย่างไรก็ตามเพื่อความชัดเจน, เราจะใช้คำส่งพวกนี้พร้อมกับนามสกุล``` .service``` ในคำสั่งทั้งหมดถัดไป, เพื่อชี้ชัดเจนถึงว่าเรากำลังดำเนินการต่ออะไร:
เพื่อหยุดบริการที่กำลังทำงานอยู่ในปัจจุบัน, คุณสามารถใช้คำสั่ง``` stop ```ตามนี้:
```
	$ sudo systemctl stop <application>.service
````

<a id="enaanddis"></a>
### Enabling and Disabling Services
การเปิด/ปิด ```Services ``` ในเซลซันปัจจุบันหากต้องการให้ systemd เริ่มบริการโดยอัตโนมัติที่เริ่มต้นขณะบูตคอมพิวเตอร์ คุณต้องเปิดใช้งานบริการเหล่านั้น

เพื่อเริ่มบริการที่บูตคอมพิวเตอร์ ใช้คำสั่ง ``` enable``` :
```
	$ sudo systemctl enable <application>.service
````
เพื่อปิดใช้งานการเริ่มต้นบริการโดยอัตโนมัติ ใช้คำสั่ง ``` Disable``` .
```
	$ sudo systemctl enable <application>.service
````

### การติดตาม Service
  เพื่อตรวจสอบ `status` ของบริการบนระบบเราสามารถใช้ command:
```
	$ systemctl status <application>.service
````
นี้จะให้ข้อมูลเกี่ยวกับสถานะของบริการ ลำดับของ cgroup และบรรทัดบางบรรทัดแรกของบันทึก
ถ้าเราพิมคำสั่งก็จะได้ประมาณนี้

```
***Output***
nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2015-01-27 19:41:23 EST; 22h ago
 Main PID: 495 (nginx)
   CGroup: /system.slice/nginx.service
           ├─495 nginx: master process /usr/bin/nginx -g pid /run/nginx.pid; error_log stderr;
           └─496 nginx: worker process
Jan 27 19:41:23 desktop systemd[1]: Starting A high performance web server and a reverse proxy server...
Jan 27 19:41:23 desktop systemd[1]: Started A high performance web server and a reverse proxy server.
````

นอกจากนี้ยังมีวิธีการตรวจสอบสถานะที่เฉพาะเจาะจง ตัวอย่างเช่น เพื่อตรวจสอบว่าหน่วยนั้นถูกเรียกใช้ (กำลังทำงาน) คุณสามารถใช้คำสั่ง``` is-active``` :
```
	 $ systemctl is-active <application>.service
````
  
นี้จะแสดงสถานะปัจจุบันของหน่วย ซึ่งโดยทั่วไปจะเป็น ```active```หรือ ```inactive``` โค้ดออกจะเป็น "0" หากเป็น active ทำให้ผลลัพธ์ง่ายต่อการแยกวิเคราะห์ใน ***shell scripts***

  
เพื่อตรวจสอบว่าหน่วยถูกเปิดใช้งานหรือไม่ เราสามารถใช้คำสั่ง ```is-enabled```:
```
	$ systemctl is-enabled <application>.service
````

นี้จะแสดงผลลัพธ์ว่าบริการได้รับการเปิดใช้งานหรือไม่ และจะตั้ง exit code เป็น "0" หรือ "1" ขึ้นอยู่กับคำตอบต่อคำถามของคำสั่ง ระหว่าง ```enabled``` และ ```disabled```

คำสั่งต่อไป   นี้จะแสดงผลลัพธ์ active หากหน่วยกำลังทำงานอย่างถูกต้อง หรือ failed หากมีข้อผิดพลาดเกิดขึ้น หากหน่วยถูกหยุดโดยตั้งใจ ผลลัพธ์อาจเป็น unknown หรือ inactive อีกต่อไป สถานะ exit "0" จะแสดงว่าเกิดความล้มเหลว และสถานะ exit "1" จะแสดงสถานะอื่น ๆ ที่ไม่ใช่ความล้มเหลว คำสั่งนี้จะเช็ค failed State คือ
```
	$ systemctl is-failed <application>.service
````

<a id="systemd"></a>
## Systemd
### Systemd
**Systemd** คือ ระบบบริหารจัดการระบบ และ service ต่างๆ ใน Linux (system and service manager) ได้รับการออกแบบ ให้ทำงานแทนระบบที่มีมาแต่เดิม SysV init Scripts นอกจากนั้น ยังมีลักษณะการทำงานที่เป็นรูปขนาน Parallel ในตอน เริ่มต้นการทำงานของระบบ และ ขณะของการ Boot ระบบ ทำให้ Linux Boot ได้เร็วกว่าเดิม โดยที่ Systemd จะออกแบบให้ส่วนต่างๆ หรือที่เรียกว่า units ที่ภายใน แต่ละ unit จะกำหนดไว้ใน Configuration files ใน directory

### เกี่ยวข้องไงกับ Service Management
**Systemd** เป็นระบบ init และ **Service Management**ที่ใช้ในระบบปฏิบัติการ Linux. ระบบ **init** เป็นกระบวนการแรกที่เริ่มต้นขึ้นในระบบปฏิบัติการเมื่อเริ่มต้น (boot) และมีหน้าที่จัดการกระบวนการอื่น ๆ ในระบบ.
**Systemd** ถูกพัฒนาขึ้นมาเพื่อทำให้การจัดการบริการและการบูตของระบบง่ายขึ้น, มีประสิทธิภาพมากขึ้น, และสามารถทำงานร่วมกับระบบปฏิบัติการ Linux ในรูปแบบที่หลากหลาย.
บางคุณสมบัติหลักของ **systemd** ที่เกี่ยวข้องกับการจัดการบริการได้แก่:
- **Service Units (หน่วยบริการ):** Systemd ใช้หน่วยบริการ (service units) เพื่อบริหารจัดการกระบวนการหลายประการที่ให้บริการในระบบ.
- **Dependency Management (การจัดการขึ้นต่อ):** Systemd สามารถกำหนดความขึ้นต่ำ (dependencies) ระหว่างบริการได้, ซึ่งช่วยให้การเริ่มต้นและการหยุดทำงานของบริการเป็นไปได้ตามลำดับที่ถูกกำหนด.
- **Logging (บันทึกข้อมูล):** Systemd มีระบบบันทึกข้อมูล (journal) ที่ช่วยในการดูและตรวจสอบข้อมูลการทำงานของระบบ.
- **Resource Control (ควบคุมทรัพยากร):** สามารถกำหนดและควบคุมทรัพยากรที่ให้บริการในแต่ละหน่วยได้ เช่น ขีดจำกัดการใช้งาน CPU, หน่วยความจำ, และอื่น ๆ.
- **Socket Activation (การเปิดใช้งานซ็อกเกต):** สามารถให้บริการเปิดใช้งานได้โดยไม่ต้องเริ่มต้นในขั้นตอนเริ่มต้น.
### ตำแหน่ง Systemd Unit Fileได้แก่

| Directory   | Description | 
| ---------- | :--------- | 
| /usr/lib/systemd/system | ไฟล์หน่วย Systemd ที่แจกจ่ายพร้อมกับแพ็คเกจ RPM ที่ติดตั้งไว้ | 
| /run/lib/systemd/system  | ไฟล์หน่วย Systemd ที่สร้างขึ้นในขณะรัน ไดเร็กทอรีนี้มีความสำคัญเหนือกว่าไดเร็กทอรีที่มีไฟล์หน่วยบริการที่ติดตั้งไว้ | 
| /etc/lib/systemd/system   | ไฟล์หน่วย Systemd ที่สร้างโดย `systemctl enable` เช่นเดียวกับไฟล์หน่วยที่เพิ่มเพื่อขยายบริการ ไดเร็กทอรีนี้มีความสำคัญเหนือกว่าไดเร็กทอรีที่มีไฟล์หน่วยรันไทม์   |
<a id="runlevels"></a>
## The Linux Run Levels
  
ใน Linux, ระดับการทำงานหรือ **runlevels** คือโหมดหรือสถานะที่ระบบทำงานในแต่ละขณะ แต่ละ runlevel สอดคล้องกับเซ็ตที่ระบบบริการและกระบวนการที่ถูกเปิดหรือปิดการใช้งาน ระดับการทำงานระบุด้วยตัวเลขที่อยู่ในช่วง 0 ถึง 6 โค้ดเคอร์เนล Linux มาตรฐานรองรับเจ็ดระดับการทำงานทั้งหมด แต่การตั้งค่าเหล่านี้อาจแตกต่างกันไปในการกระจาย Linux และเวอร์ชัน Unix ต่าง ๆ นี่คือ **Seven runlevels** การทำงานใน Linux:
- **Runlevel 0**:  Shuts down the system
- **Runlevel 1**:  Single-user mode (for special administration)
- **Runlevel 2**:  Local Multiuser with Networking but without network service (like NFS)
- **Runlevel 3**:  Full Multiuser with Networking
- **Runlevel 4**:  Not used
- **Runlevel 5**:  Full Multiuser with Networking and Graphical User Interface (GUI)
- **Runlevel 6**:  Reboots the system
  
ควรทราบว่า runlevel 2 ถึง 5 สามารถปรับเปลี่ยนได้ตามความต้องการของคุณเอง เมื่อระบบถูกบูต มีเพียง runlevel เดียวที่ถูกดำเนินการ และมันไม่ได้ถูกดำเนินการต่อเนื่องตามลำดับ เพื่อตรวจสอบ runlevel ปัจจุบันของระบบ Linux มีวิธีง่าย ๆ ด้วยวิธีต่อไปนี้:
1.   ใช้คำสั่ง runlevel: `runlevel` คำสั่งนี้จะแสดง runlevel ที่ระบบกำลังทำงานอยู่ขณะนี้
2.  ใช้คำสั่ง who: `who -r` คำสั่งนี้จะแสดง runlevel ปัจจุบันและข้อมูลอื่น ๆ
## ตัวอย่างการเขียน Service Management
### การติดตั้ง Service Management
**Systemd**
ตรวจสอบการทำงาน
```
	$ ps -p 1 -o comm= | grep systemd
````
ติดตั้งแพ็กเกจของระบบการจัดการบริการ
```
	$ sudo apt-get install systemd
````
 ติดตั้งแพ็กเกจของเครื่องมือการจัดการบริการ 
 > ถ้าไม่ได้ถูกติดตั้ง
 ```
	sudo apt-get install systemd-sysv
````
### การเขียน Service File
1. สร้างไฟล์บริการ (.service) ในไดเรกทอรี `/etc/systemd/system/`.** ตั้งชื่อไฟล์ตามชื่อบริการของคุณ ex. my-service.servic
```
	$ sudo nano /etc/systemd/system/my-service.service
```
2. เพิ่มข้อมูลบริการในไฟล์ .service:
```
[Unit]
Description=My Custom Service
After=network.target

[Service]
ExecStart=/path/to/your/service/executable
Restart=always

[Install]
WantedBy=default.target

```
บันทึกและปิดไฟล์.


### การตั้งค่า Service
สมมุติว่าคุณมีบริการที่เรียกว่า `my-service`. 
#### แบบ Systemd
1. สร้างไฟล์ `.service` สำหรับบริการใน `/etc/systemd/system/my-service.service` บันทึกและปิดไฟล์.
```
[Unit]
Description=My Custom Service
After=network.target

[Service]
ExecStart=/path/to/your/service/executable
Restart=always

[Install]
WantedBy=default.target
```
2. ทำการโหลดการตั้งค่าใหม่:
```
	$ sudo systemctl daemon-reload
```

3. ทดสอบการใช้คำสั่ง:
```
	$ sudo systemctl start my-service
	$ sudo systemctl status my-service
```

4. เปิดใช้งาน
```
	$ sudo systemctl enable my-service
```
> โปรดทราบว่าตัวอย่างนี้เป็นแค่แนวทางทั่วไป ขึ้นอยู่กับลักษณะของบริการและระบบการจัดการบริการของระบบปฏิบัติการ Linux ที่ใช้.
> 
####  แบบSysVinit:
สมมุติว่าคุณมีบริการที่เรียกว่า `my-service`. ต้องการให้บริการเริ่มต้นและทำงานในโหมด daemon
1. สร้างไฟล์สคริปต์ใน `/etc/init.d/my-service`: บันทึกและปิดไฟล์.
```
#!/bin/bash
# chkconfig: 345 20 80
# description: My Custom Service

start() {
    /path/to/your/service/executable &
}

stop() {
    killall my-service
}

case $1 in
    start)
        start
        ;;
    stop)
        stop
        ;;
    restart)
        stop
        start
        ;;
    *)
        echo "Usage: $0 {start|stop|restart}"
        exit 1
esac

exit 0
```
2. ทำให้สคริปต์เป็นไฟล์ที่สามารถรันได้:
```
	$ sudo chmod +x /etc/init.d/my-service
```
3. ใช้ `chkconfig` เพื่อเปิดใช้บริการในโหมด startup:
```
	$ sudo chkconfig --add my-service
	$ sudo chkconfig my-service on
```
4. ทดสอบการใช้คำสั่ง:
```
	$ sudo service my-service start
	$ sudo service my-service start
```
>โปรดทราบว่าตัวอย่างนี้เป็นแค่แนวทางทั่วไป ขึ้นอยู่กับลักษณะของบริการและระบบการจัดการบริการของระบบปฏิบัติการ Linux ที่ใช้.

### ตัวอย่างการใช้ `update-rc.d`:
1. เพิ่มบริการให้ทำงานที่ runlevels ที่กำหนด:
```
	$ sudo update-rc.d <service-name> defaults
```
2. ลบบริการออกจากระบบการเริ่มต้น:
```
	$ sudo update-rc.d -f <service-name> remove
```


## อ้างอิง
**LinkeDin**
[https://www.linkedin.com/pulse/linux-run-levels-the-infosectribune]

**LinuxJourney**
[https://linuxjourney.com/lesson/sysv-overview]

**FOSS4Change**
https://www.youtube.com/watch?v=WPGbOzd0r9E
https://th.linux-console.net/?p=2333

**DigitalOcean.**
https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units#conclusion

**rimuhosting**
https://rimuhosting.com/knowledgebase/linux/managing-services

**cherryservers**
https://www.cherryservers.com/blog/an-ultimate-guide-of-how-to-manage-linux-systemd-services-with-systemctl-command

**LINUX . COM**
https://www.linux.com/training-tutorials/managing-services-linux-systemd/
