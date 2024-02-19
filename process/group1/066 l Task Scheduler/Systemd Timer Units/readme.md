# Systemd Timer Units
โดยส่วนใหญ่แล้ว user มักจะใช้ cron ในการทำ task schedular แต่เราก็สามารถใช้ ```systemd``` เพื่อกำหนดเวลาให้งานทำงานโดยอัตโนมัติเหมือนกัน

## timer
การตั้งเวลา เราจะต้องสร้างหน่วยจับเวลาและหน่วยบริการที่เกี่ยวข้องก่อน เริ่มต้นที่ timer

timer คือ ไฟล์ที่ลงท้ายด้วย **.timer** ซึ่งอยู่ในประเภทของ **systemd unit files**
.timer จะเก็บข้อมูลการกำหนดค่าเกี่ยวกับงานที่จะถูก execute ด้วย systemd Timer
file timer จะอยู่ใน ```/etc/systemd/system/```

ภายใน file ก็จะแบ่งเป็น 3 section
- [Unit] : ข้อมูลทั่วไปเกี่ยวไฟล์ systemd unit files
- [Timer] : ประกอบด้วย เวลาที่จะเริ่ม และ task ที่จะ execute
- [Install] : ข้อมูลเกี่ยวกับการติดตั้ง ระบุว่าตัวจับเวลาควรเริ่มต้นเมื่อถึงจุดไหน

และ timer ยังแบ่งได้เป็น 2 ประเภท
> <ins>Monotonic </ins>
> - timer อนุญาตให้ execute หลัง event ที่เกิดขึ้นแล้ว
> - ใช้เป็น **OnBootSec** (system boots) หรือ **OnActiveSec** (systemd unit ที่ active)
```
[Timer]OnBootSec=10sec Unit=greeting.service
```
><ins>Realtime</ins>
> - ทำงานเหมือน cron หรือก็คือทำงานตามที่กำหนด
> - ควรใช้ **OnCalendar**
```
DayofWeek Year-Month-Day Hour:Minute:Second
```
เช่น
```
OnCalendar=*-*-* 02:30:00 -> ทุก 02.30 ของทุกวัน
OnCalendar=Mon *-*-* 02:30:00 -> ทุก 02.30 ของทุกวันจันทร์
OnCalendar=hourly -> ทุกชั่วโมง
OnCalendar=*:0/6 -> ทุก 6 ชั่วโมง
OnCalendar=10:00,18:00 -> ทุกเวลา 10 โมง และ 6 โมงเย็นของทุกวัน
```
## service
ทุก timer ต้องมีตัวกระตุ้น ก็คือ ไฟล์ .service
```
Unit=myscript.service
```
> ทั้ง .timer และ .service ควรมีชื่อ file เหมือนกัน!

และ .service ให้ระบุคำสั่งหรือสคริปต์ที่ควรเรียกใช้เมื่อตัวจับเวลาทริกเกอร์โดยเพิ่มตัวเลือก **"ExecStart"**
```
ExecStart=/usr/local/bin/myscript.sh
```


.timer ที่ได้ก็คือ
```
[Unit]
Description=Run myscript every day at 2:30am

[Timer]
OnCalendar=*-*-* 02:30:00
Persistent=true
Unit=myscript.service

[Install]
WantedBy=timers.target
```

และ .service ที่ได้ก็คือ
```
[Unit]
Description=My script

[Service]
Type=simple
User=myuser
ExecStart=/usr/local/bin/myscript.sh
Restart=on-failure

[Install]
WantedBy=default.target
```
## systemctl Command
systemctl เป็น<ins> interface ที่ใช้ควบคุม systemd units</ins>
เปิดใช้งานคำสั่งได้โดย
```
$ systemctl COMMAND UNIT_NAME [OPTION]
```
หรือ
```
$ systemctl LIST_UNIT
```
เช่น
```
$ sudo systemctl disble myscript.timer
$ sudo systemctl enable myscript.timer
$ sudo systemctl start myscript.timer
```
สามารถตรวจสอบสถานะได้โดยการ เช็ค status ว่าทำงานอยู่มั้ย
```
$ sudo systemctl status name.timer
$ sudo systemctl status name.service
```
หากคุณแก้ไข .timer หรือ.service ในภายหลัง ต้องดูให้แน่ใจก่อนว่าได้โหลด  `systemd`  ใหม่หลังจากนั้นแล้ว ด้วยการใช้คำสั่ง
```
$ sudo systemd daemon-reload
```
