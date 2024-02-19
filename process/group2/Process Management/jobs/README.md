# คำสั่ง`jobs`
เป็นคำสั่งที่แสดงรายการของงานที่กำลังอยู่ทั้ง background และ foreground
|อาร์กิวเมนต์|คำอธิบาย|ตัวอย่าง|
|---|-----------|-----|
|`-l`|แสดงรายการงานและ PID|`jobs -l`|
|`-p`|แสดงเฉพาะ PID ของงาน|`jobs -p`|
|`-n`|แสดงรายการเฉพาะ processes ที่มีการเปลี่ยนสถานะจากครั้งที่แล้ว|`jobs -n`|
|`-r`|แสดงรายการงานเฉพาะงานที่กำลังทำงานอยู่|`jobs -r`|
|`-s`|แสดงรายการงานเฉพาะงานที่หยุดทำงานอยู่|`jobs -s`|
## ตัวอย่างการนำไปใช้
- แสดงรายการงานที่ทำงานอยู่ background
> jobs

![jobs.png](../../Assets/jobs/jobs.png)
- แสดงรายการงานที่ทำงานอยู่ background และแสดง PID
> jobs -l

![jobs-l.png](../../Assets/jobs/jobs-l.png)
- แสดงเฉพาะ PID ของงาน
> jobs -p

![jobs-p.png](../../Assets/jobs/jobs-p.png)
***
# แหล่งอ้างอิง
- https://hopeness.medium.com/master-the-linux-jobs-command-a-comprehensive-guide-ce2b791312fa
- https://www.geeksforgeeks.org/process-control-commands-unixlinux/
