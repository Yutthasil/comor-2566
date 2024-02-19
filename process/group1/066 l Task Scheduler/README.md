# Task Scheduler
**Task Scheduler** คือตัวที่ทำหน้าที่ คอยควบคุม **กำหนดการทำงานของ task** ต่างๆ เป็นตัวกำหนดว่า task ไหนจะทำงาน ทำตอนไหน ทำนานแค่ไหน โดยการแบ่งทรัพยากรที่มีจำกัดมาแบ่งปันแต่ละ task ให้ทำงานพร้อมๆกันได้

ประกอบด้วยเครื่องมือ **4** อย่าง คือ
- [**cron**](https://github.com/MaledKhaoSan/Project-Comor/tree/main/066%20l%20Task%20Scheduler/cron) : ทำงานเป็นรอบๆ ทำงานประจำ
- [**at**](https://github.com/MaledKhaoSan/Project-Comor/tree/main/066%20l%20Task%20Scheduler/at) : ทำงานเพียงครั้งเดียว
- [**anacron**](https://github.com/MaledKhaoSan/Project-Comor/tree/main/066%20l%20Task%20Scheduler/anacron) : ทำงานเป็นระยะๆ
- [**Systemd Timer Units**](https://github.com/MaledKhaoSan/Project-Comor/tree/main/066%20l%20Task%20Scheduler/Systemd%20Timer%20Units) : เป็นอีกทางเลือกหนึง นอกเหนือจาก 3 อันบน


## reference
- https://linuxhint.com/schedule_linux_task/
- https://ebookreading.net/view/book/How+Linux+Works++2nd+Edition-EB9781457185519_12.html
- https://www.dropbox.com/scl/fo/sv8iv9uqvwvsab4pmzf1h/h?dl=0&preview=L2v2_Chapter_07-JobScheduling.pdf&rlkey=awurdtyika6gx5y7vhip0bxwc
- https://betterprogramming.pub/how-to-schedule-cron-tasks-in-linux-fc605bf4911e
- https://support.thaidata.cloud/kb/setting-cronjob-crontab-linux/
- https://ioflood.com/blog/at-linux-command/
- https://th.linux-console.net/?p=697
- https://www.geeksforgeeks.org/anacron-command-in-linux-with-examples/
