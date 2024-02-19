<a id="process-management"></a>
# :round_pushpin: What is Process Management in Linux?
Process Management ใน Linux คือกระบวนการควบคุมและตรวจสอบกระบวนการที่กำลังทำงาน การสร้าง การควบคุม และการยุติการทำงานทั้งหมดในระบบ รวมถึงการจัดสรรทรัพยากรของกระประมวลผล โดยหลักการของ Process Management ประกอบไปด้วย 3 หลักนี้
<br><br>
1. Process Initiation (การเริ่มต้นกระบวนการ):
<br>การเริ่มต้นกระบวนการใหม่, ซึ่งอาจเกิดจากการใช้คำสั่งหรือโปรแกรมที่ทำงานตลอดเวลา.
      <br><br>
2. Process Control (การควบคุมการทำงาน):
<br>การควบคุมกระบวนการที่กำลังทำงาน ลำดับการทำงาน ว่ากระบวนการใดสำคัญกว่าจึงมาก่อน การติดตามและจัดการกระบวนการที่กำลังทำงานอยู่ การจัดสรร CPU, หน่วยความจำ, ทรัพยากรอื่นๆ
      <br><br>
3. Process Termination (การหยุดกระบวนการ):
<br>การสิ้นสุดการทำงานของกระบวนการเมื่อทำงานเสร็จสิ้น หรือ การที่ผู้ใช้บังคับให้หยุด, โดยจะคืนทรัพยากรที่ใช้ไป และสิ้นสุดการทำงานของตัวเอง

> [!TIP]
> ด้วยหลักการของ Process Management ทั้งสามนี้ช่วยให้ระบบปฏิบัติการสามารถจัดการกระบวนการในระบบได้อย่างถูกต้อง 

---

<a id="process-initiation"></a>
# :bulb: Process Initiation
พื้นฐานหรือหลักการทำงานของ Process Initiation จะทำหน้าที่สร้างกระบวนการใหม่ (process) เพื่อรันโปรแกรมนั้น ๆ บนระบบปฏิบัติการ คือการสร้างโปรแกรมใหม่ขึ้นมาเพื่อทำงานตามชุดคำสั่งและ Process Initiation สามารถเกิดขึ้นได้หลายวิธีตามบริบทที่ใช้ เช่น


1. ผู้ใช้รันโปรแกรม:
    - ผู้ใช้พิมพ์คำสั่งบน command line เช่น `ls`, `cd`, `mkdir`, `grep`
    - ผู้ใช้รันโปรแกรมผ่าน graphical user interface (GUI).

        ### :computer: ตัวอย่างเหตุการณ์เมื่อผู้ใช้พิมพ์คำสั่งบน Command Line
        #### `ls` - แสดงรายการ file และ directory
        > คำสั่ง `ls` จะแสดงเนื้อหาใน directory ปัจจุบัน ระบุรายการ file และ directory ทั้งหมด
        > ```ruby
        > $ ls
        > Desktop  Documents  Downloads  Music  Pictures  Videos
        > ```

        #### `cd` - เปลี่ยน directory
        > คำสั่ง `cd` จะเปลี่ยน directory ปัจจุบันเป็น "Documents."
        > ```ruby
        > $ cd Documents
        > ```

        #### `mkdir` - สร้าง directory
        > คำสั่ง `mkdir` จะสร้าง directory ใหม่ชื่อ "NewDirectory."
        > ```ruby
        > $ mkdir NewDirectory
        > ```

        #### `grep` - ค้นหาข้อความในไฟล์
        > คำสั่ง `grep` จะค้นหาข้อความที่ระบุในเนื้อหาของไฟล์ (เช่น "รูปแบบ" ใน "ชื่อไฟล์.txt").
        > ```ruby
        > $ grep "รูปแบบ" ชื่อไฟล์.txt
        > ```

2. การเริ่มทำงานโดยระบบปฏิบัติการ:
    - ระบบปฏิบัติการรัน scripts ที่ตั้งเวลาไว้
    - ระบบปฏิบัติการเริ่มโปรแกรม daemon ที่ทำงานพื้นหลัง
    - ระบบปฏิบัติการตอบสนองต่อ events ต่างๆ เช่น การกดปุ่มบน keyboard
        ### :computer: ตัวอย่างเหตุการณ์ Process Initiation จาก Scripts ที่ตั้งเวลาไว้

        #### สมมติว่าเรามี script ชื่อ `daily_backup.sh` 
        > ที่ใช้สำหรับสำรองข้อมูลทุกวันเวลา 12:00 นาฬิกา โดยให้ระบบปฏิบัติการเรียกใช้ script นี้ตามกำหนดเวลาที่กำหนด
        > ```ruby
        > # daily_backup.sh
        > #!/bin/bash
        > 
        > # ทำงานสำหรับการสำรองข้อมูล
        > echo "Running daily backup..."
        > # คำสั่งสำหรับสำรองข้อมูล
        > # ...
        > 
        > # สิ้นสุด script
        > ```
        > จากนั้นให้กำหนดตัวแปร environment หรือ cron job ในระบบปฏิบัติการเพื่อทำงาน script ตามเวลาที่ต้องการ
        >```ruby
        ># ตั้งค่า cron job เพื่อเรียกใช้ script ทุกวันที่ 2 เวลา 2 โมงเช้า
        >0 12 * * * /path/to/daily_backup.sh
        >```
        >
        > ในที่นี้เราให้ cron job ระบบปฏิบัติการเรียกใช้ `daily_backup.sh` ทุกวันเวลา 12:00 นาฬิกา เป็นตัวอย่างการเริ่มต้นกระบวนการ (Process Initiation) จาก script ที่ตั้งเวลาไว้

        <br>

        ### :computer: ตัวอย่างเหตุการณ์ Process Initiation จาก Daemon

        โปรแกรม daemon เป็นโปรแกรมที่ทำงานแบบ <a href="">background process</a> โดยไม่ต้องมีผู้ใช้เรียกใช้งานโดยตรง เรามีตัวอย่างเป็น daemon ที่เป็น web server ซึ่งทำงานตลอดเวลาเพื่อตอบรับ requests จาก clients

        > ตัวอย่างโปรแกรม daemon ของ web server (ในที่นี้เราให้ตั้งตัวอย่างเป็น Apache HTTP Server)
        > ```ruby
        > # ในการเริ่ม Apache HTTP Server เป็น daemon
        > sudo service apache2 start
        > ```
        > 
        > ในที่นี้เราให้ `apache2` เป็นตัวอย่างของโปรแกรม daemon ที่ทำงานพื้นหลังโดยไม่ต้องมีผู้ใช้เรียกใช้งานโดยตรง เป็นตัวอย่างการเริ่มต้นกระบวนการ (Process Initiation) จากโปรแกรม daemon
        >
        > <p align="center"><img src="https://github.com/MaledKhaoSan/Project-Comor/blob/main/assets/process_initiation.png?raw=true" alt="Logo" width="auto" height="auto"></p>


> [!TIP]
> การสร้างกระบวนการใหม่ของ Process Initiation นั้นอาจจะใช้วิธีการ fork() และ exec() หรือวิธีการอื่น ๆ ขึ้นอยู่กับระบบปฏิบัติการและลักษณะการทำงาน
<br>

---


<a id="process-tracking"></a>
# :bulb: Process Tracking
เป็นกระบวนการที่ให้ระบบปฏิบัติการติดตามและบันทึกข้อมูลเกี่ยวกับกระบวนการที่กำลังทำงานในระบบ ซึ่งเป็นส่วนหนึ่งของ Process Management ในระบบปฏิบัติการ

1. Process ID (PID): หมายเลขที่ระบุกระบวนการเฉพาะตัว
2. Parent Process ID (PPID): หมายเลขที่ระบุกระบวนการหลักที่สร้างกระบวนการนี้ (parent process)
3. สถานะ (Status): บอกถึงสถานะปัจจุบันของกระบวนการ เช่น กำลังทำงาน (Running), หยุดชั่วคราว (Stopped), หรือ หยุด (Terminated)
4. เวลาการใช้งาน (Execution Time): ระยะเวลาที่กระบวนการทำงานจริง
5. การใช้ทรัพยากร (Resource Usage): การใช้ทรัพยากรเช่น CPU, หน่วยความจำ

---


> [!NOTE]
> ## :raising_hand: ต่อไปเราจะลงลึกในหัวข้อ Process Control (การควบคุมการทำงาน)
> ที่มีบทบาทสำคัญในการจัดการลำดับการทำงานของกระบวนการ, การติดตามและจัดการกระบวนการที่กำลังทำงานอยู่, และการจัดสรรทรัพยากรเช่น CPU และหน่วยความจำ.
>

---

# :bulb: Process Control

Process Control (การควบคุมการทำงาน) เป็นส่วนสำคัญของ Process Management ในระบบ Linux ซึ่งมีบทบาทในการควบคุมลำดับการทำงานของกระบวนการ, การติดตามและจัดการกระบวนการที่กำลังทำงาน, และการจัดสรรทรัพยากร เช่น CPU, หน่วยความจำ, และทรัพยากรอื่น ๆ ต่อไปนี้คือการทำงานที่เกี่ยวข้องกับ Process Control:

1. การสั่งรันคำสั่ง (Running a command): เมื่อผู้ใช้รันคำสั่งบนระบบ Linux, มันจะเป็นการสร้างกระบวนการ (process) เพื่อทำงานตามคำสั่งที่กำหนด.

2. Linux Manages Tasks Using Processes (Linux จัดการงานโดยใช้กระบวนการ): ในระบบปฏิบัติการ Linux, การจัดการงานหลาย ๆ อย่างเป็นไปผ่านกระบวนการ ซึ่งเป็นตัวกลางที่ช่วยจัดการทรัพยากรและควบคุมการทำงานของโปรแกรม.

3. Parent/Child Relationship (ความสัมพันธ์ระหว่าง Parent และ Child): กระบวนการสามารถเริ่มกระบวนการย่อย (subprocess) ได้ ซึ่งจะเกิดความสัมพันธ์ระหว่างกระบวนการหลัก (parent process) และกระบวนการย่อย (child process).

4. Users Can Only Control Their Processes (ผู้ใช้สามารถควบคุมกระบวนการของตนเอง): แต่ละผู้ใช้บนระบบ Linux สามารถควบคุมกระบวนการที่เป็นของตนเองได้ เขาสามารถดูข้อมูล, หยุด, หรือเรียกคำสั่งอื่น ๆ ในบริบทของกระบวนการของตน.

5. Root Can Control All System and User Processes (Root สามารถควบคุมกระบวนการทั้งระบบและผู้ใช้): ผู้ใช้ที่มีสิทธิ์ root (superuser) สามารถควบคุมทุกระบวนการในระบบ, รวมถึงกระบวนการที่เป็นของผู้ใช้ทั้งหมด. Root มีอำนาจสูงสุดในการควบคุมและจัดการทรัพยากรระบบ.
---

<div align="center">
      ตัวอย่างคำสั่ง
      <table>
      <thead>
      <tr>
      <th style="text-align:left">คำสั่ง</th>
      <th style="text-align:center">ประเภท</th>
      <th style="text-align:right">ตัวอย่าง</th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td style="text-align:left">ps</td>
      <td style="text-align:center">แสดงรายการ process ทั้งหมด</td>
      <td style="text-align:right">ps aux</td>
      </tr>
      <tr>
      <td style="text-align:left">kill</td>
      <td style="text-align:center">ยุติการทำงานของ process</td>
      <td style="text-align:right">kill -9 1234</td>
      </tr>
      <tr>
      <td style="text-align:left">renice</td>
      <td style="text-align:center">เปลี่ยนระดับความสำคัญของ process</td>
      <td style="text-align:right">renice -n 10 1234</td>
      </tr>
      <tr>
      <td style="text-align:left">job controls</td>
      <td style="text-align:center">ควบคุมการทำงานของ process ในรูปแบบ job</td>
      <td style="text-align:right">bg %1, fg %2</td>
      </tr>
      </tbody>
      </table>
</div>


---


1. ### :computer: Listing Processes
    #### `ps` - แสดงข้อมูลเกี่ยวกับกระบวนการที่กำลังทำงาน
    > ```ruby
    > $ ps
    > ```
    > ```
    > PID TTY           TIME CMD
    > 1234 pts/0     00:00:01 bash
    > 5678 pts/0     00:00:00 ps
    > ```

    #### `ps -ef` - แสดงข้อมูลเกี่ยวกับกระบวนการที่กำลังทำงาน
    > -e แสดงกระบวนการทั้งหมด<br>
    > -f แสดงข้อมูลเพิ่มเติม (full format)<br>
    > -ef แสดงข้อมูลทั้งหมดที่เป็นรูปแบบของ "extended format" 
    > ```ruby
    > $ ps -ef
    > ```
    > ```
    > UID        PID  PPID  C STIME TTY          TIME CMD
    > root         1     0  0 Jan01 ?        00:00:05 /usr/lib/systemd/systemd
    > root         2     0  0 Jan01 ?        00:00:00 [kthreadd]
    > root         3     2  0 Jan01 ?        00:00:00 [ksoftirqd/0]
    > ...
    > john       5678  5623  0 10:15 pts/0    00:00:00 ps -ef
    > ```
    <br>

2. ### :computer: Searching For Processes
    #### `pgrep` - ค้นหา process ตามเงื่อนไขหรือชื่อที่ระบุ
    > คำสั่ง `pgrep` ใช้ในการค้นหากระบวนการ (processes) โดยใช้ชื่อหรือเงื่อนไขที่กำหนด<br>
    > ```ruby
    > $ pgrep [options] name
    > ```

    ####  ตัวเลือก `-i` เพื่อค้นหาโดยไม่สนใจตัวอักษรตัวใหญ่-เล็ก (case-insensitive)<br>
    > ```ruby
    > $ pgrep -i sshd
    > ```

    ####  ตัวเลือก `-l` เพื่อแสดงผลรายการของกระบวนการพร้อมกับ PID ด้วย:<br>
    > ```ruby
    > $ pgrep -l -i sshd
    > ```

    #### ตัวเลือก `--u` เพื่อค้นหาเจ้าของ process โดยระบุชื่อ<br>
    > ```ruby
    > $ pgrep -u owner
    > ```


3. ### :computer: Watching Processes
    #### `watch` - ส่งสัญญาณให้ หยุดทำงาน
    >  คำสั่ง `watch` ใช้เพื่อติดตามและแสดงผลลัพธ์จากคำสั่งหรือโปรแกรมที่รันตลอดเวลาตามช่วงเวลาที่กำหนด
    > ใช้ `watch` ร่วมกับ `ps`
    > `watch` จะทำให้คำสั่ง `ps` รีเฟรชและแสดงผลลัพธ์ทุก 2 วินาที (ตามค่าเริ่มต้น). สามารถกำหนดช่วงเวลาใหม่โดยใช้ตัวเลือก `-n` ตามด้วยเวลาที่ต้องการ
    > ```ruby
    > $ watch -n 5 ps
    > ```


    ####  `watch ps aux`
    > แสดงผลลัพธ์ที่เป็นตารางแบบ real-time แสดงข้อมูลเกี่ยวกับกระบวนการที่กำลังทำงานบนระบบ. ข้อมูลที่แสดงรวมถึงรายละเอียดต่าง ๆ เกี่ยวกับแต่ละกระบวนการ
    > ```ruby
    > $ watch ps aux
    > ```

    > ```
    > Every 2.0s: ps aux
    >
    > USER       PID  %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    > user      1234  0.0  0.1 123456  7890 ?        S    Jan01   0:00 /path/to/command
    > user      5678  1.0  0.2 234567 12345 ?        R    Jan01   1:23 /another/command
    > ...
    >  ```

4. ### :computer: Managing Jobs
    เป็นกระบวนการควบคุมและจัดการกับกระบวนการ (process) ที่กำลังทำงานหรือหยุดทำงานในระบบปฏิบัติการ Linux หรือ UNIX-like systems โดยใช้เทคนิคที่เรียกว่า Job Control.

    #### `Job Control`
    > คำสั่ง bg (<a href="">Background</a>) และ fg (<a href="">Foreground</a>) ใช้เพื่อควบคุมการทำงานของ jobs (งาน) ในระบบปฏิบัติการ Linux หรือ UNIX-like systems. นี่คือตัวอย่างคำสั่ง:

    #### คำสั่ง `jobs` สามารถใช้เพื่อดู background jobs ที่กำลังทำงานอยู่ได้
    > ตัวอย่างการใช้ jobs
    > ```ruby
    > $ jobs
    > [1]+  Done                    sleep 3
    > ```

    #### จำลองเหตุการณ์ว่า
    > `Job 1` มีคำสั่ง sleep 1000 และอยู่ในสถานะ "Stopped"<br>
    > `Job 2` มีคำสั่ง sleep 2000 และอยู่ในสถานะ "Stopped"
    > <br><br>
    > ดังนั้น, เราสามารถใช้คำสั่ง fg และ bg เพื่อเปลี่ยนสถานะของ jobs:
    > <br><br>
    > `fg 2`: คำสั่งนี้จะทำให้ job ที่มีหมายเลข 2 ทำงานใน foreground<br>
    > `bg 1`: คำสั่งนี้จะทำให้ job ที่มีหมายเลข 1 ทำงานใน background

    > Job ที่มีหมายเลข 2 ถูกเปลี่ยนจากสถานะ "Stopped" เป็น "Running" และทำงานใน foreground
    > ```ruby
    > $ fg 2
    > ```
    > ```ruby
    > [1]+ Stopped sleep 1000
    > [2]- Running sleep 2000 &
    >```

    #### คำสั่ง `jobs` สามารถใช้เพื่อดู background jobs ที่กำลังทำงานอยู่ได้
    > Job ที่มีหมายเลข 1 ถูกเปลี่ยนจากสถานะ "Stopped" เป็น "Running" และทำงานใน background
    > ```ruby
    > $ bg 1
    > ```
    > ```ruby
    > [1]+ Running sleep 1000 &
    > [2]- Running sleep 2000 &
    >```



---

### Foreground และ Background Processes

- **Foreground Processes:**
    - การทำงานที่อยู่เบื้องหน้าสามารถสื่อสาร หรือ รับคำสั่งผู้ใช้ และ แสดงผลลัพธ์บนหน้าจอได้ทันที
    - คือกระบวนการที่ป้องกันผู้ใช้ไม่ให้ใช้ shell จนกว่ากระบวนการนั้นจะเสร็จสิ้น.
    - มี parent process และกระบวนการใหม่เรียกว่า child process
    
        #### `fg` - การนำ background process มาทำงานใน foreground process
        >  คำสั่ง `fg` ใช้เพื่อนำโปรแกรมที่ทำงานใน background มาทำงานใน foreground:
        > ```ruby
        > $ fg
        > ```
        > ในตัวอย่างนี้, `fg %1` จะนำ `my_program` มาทำงานใน foreground
        > ```ruby
        > $ jobs
        > [1]   Running                 my_program &
        > [2]   Running                 another_program &
        > $ fg %1
        > ```


- **Background Processes:**
    - การทำงานที่อยู่บนพื้นหลัง โดยไม่รบกวน หน้า console และผู้ใช้สามารถป้อนคำสั่งอื่นได้ในขณะที่กระบวนการนี้กำลังทำงาน.
    - เพื่อให้คำสั่งทำงานเป็น background process, ให้เพิ่มเครื่องหมาย ampersand (&) หลังคำสั่ง

        #### `&` - เพื่อให้คำสั่งหรือโปรแกรมทำงานใน background
        >  sleep 3 & ถูกรัน, มันจะทำให้โปรแกรม sleep ทำงานใน background
        > ```ruby
        > $ sleep 3 &
        > [1] 12345
        > ```

        > sleep 3 วินาทีผ่านไป, จะมีข้อความที่แสดงขึ้นบอกว่า job ที่มีหมายเลข 1 เสร็จสิ้น
        > ```ruby
        > [1]+  Done                    sleep 3
        > ```


> [!CAUTION]
> **ข้อควรระวัง**
> - โปรแกรม background อาจทำงานไม่เสร็จสิ้น หากผู้ใช้ logout ออกจากระบบ
> - โปรแกรม background อาจใช้ทรัพยากรระบบมากเกินไป


> [!NOTE]
> ## :raising_hand: ต่อไปเราจะพูดถึง Process Termination (การหยุดกระบวนการ)
> ซึ่งเป็นขั้นตอนสุดท้ายใน Process Management ที่เกี่ยวข้องกับการสิ้นสุดกระบวนการทำงานของกระบวนการ.
>

---

<a id="process-termination"></a>
# :bulb: Process Termination

Process Termination (การหยุดกระบวนการ) เป็นขั้นตอนสุดท้ายใน Process Management ในระบบ Linux ซึ่งมีบทบาทในการสิ้นสุดกระบวนการทำงานของกระบวนการ โดยมีลักษณะการทำงานดังนี้:

1. ### :computer: Signals

    เป็นวิธีที่ระบบใช้เพื่อสื่อสารกับกระบวนการ (process) ในระหว่างการทำงาน. สัญญาณสามารถถูกส่งไปยังกระบวนการเพื่อให้ทำหน้าที่ต่าง ๆ เช่น หยุดการทำงาน, รีเซ็ต, หรือแจ้งเตือน.

    #### SIGNAL สามารถใช้ผ่าน shortkey ได้
    > `Ctrl+z` หยุดการทำงานของโปรแกรมชั่วคราว<br>
    > `Ctrl+c` หยุดการทำงานของโปรแกรมถาวร

    > ในระบบปฏิบัติการ Linux, สัญญาณ (Signal) เป็นวิธีที่ระบบใช้เพื่อสื่อสารกับกระบวนการ (process) ในระหว่างการทำงาน. สัญญาณสามารถถูกส่งไปยังกระบวนการเพื่อให้ทำหน้าที่ต่าง ๆ เช่น หยุดการทำงาน, รีเซ็ต, หรือแจ้งเตือน.


3. ### :computer: Force Kill
    #### `Force Kill` - ส่งสัญญาณให้ หยุดทำงาน
    >  คำสั่ง `kill` ใช้เพื่อหยุดการทำงาน โดยมักใช้ร่วมกับ `PID` (Process ID) ของกระบวนการ
    > ```ruby
    > $ kill [signal] PID
    > ```

    ### SIGNAL ที่ใช้บ่อยในระบบปฏิบัติการ:
    - **SIGKILL (สัญญาณ KILL):**
        - กรณีเราต้อง force kill โปรแกรมที่ไม่สามารถหยุดด้วยสัญญาณอื่น ๆ
        - ใช้เพื่อสั่งให้กระบวนการหยุดทันที โดยไม่มีโอกาสที่จะทำงานต่อ.
        - การใช้ SIGKILL จะทำให้กระบวนการถูกทำลายทันที.

        > ```ruby
        > $ kill -9 2901
        > ```

        > ```ruby
        > $ kill -KILL %1
        > ```

        > ```ruby
        > $ kill -SIGKILL -p 2901
        > ```

    - **SIGTERM (สัญญาณ TERMINATE):**
        - ใช้เพื่อสั่งให้กระบวนการจบการทำงาน.
        - กระบวนการมีโอกาสที่จะทำงานสักพักต่อจากที่ได้รับ SIGTERM.

        > ```ruby
        > $ kill -15 PID
        > ```
    - **SIGSTOP (สัญญาณ STOP):**
        - ใช้เพื่อหยุดกระบวนการชั่วคราว.
        - กระบวนการสามารถถูกรีสตาร์ทได้.

        > ```ruby
        > $ kill -19 PID
        > ```

    - **SIGCONT (สัญญาณ CONTINUE):**
        - ใช้เพื่อทำให้กระบวนการทำงานต่อจากที่ถูกระงับ (Suspended).

        > ```ruby
        > $ kill -18 PID
        > ```

        ---

        > [!TIP]
        > ## :raising_hand:  สามารถใช้คำสั่ง `pkill` หรือ `killall`
        > เพื่อส่งสัญญาณไปยังกระบวนการ. กรณีที่เราอยากหยุดกระบวนการจำนวนหลายๆ กระบวนการในครั้งเดียว (stop many processes at once)
        >
        >  คำสั่ง `killall` หยุดกระบวนการทั้งหมดที่ `users` เป็นเจ้าของ
        > ```ruby
        > $ killall -u users
        > ```

    
    -  **Hang-up signal**
        - เป็นสัญญาณที่ถูกส่งไปยังกระบวนการเมื่อผู้ใช้ล็อกเอาท์จากระบบ หรือปิด session นั้น ๆ บนทางการเชื่อมต่อ (session) เมื่อมีการส่งสัญญาณ HUP มายังกระบวนการนั้น ๆ จะทำให้กระบวนการสิ้นสุดการทำงาน (terminate).

        #### `nohup` - การ ignore HUP signal
        >  คำสั่ง `nohup` ใช้เพื่อกำหนดให้กระบวนการไม่สนใจสัญญาณ HUP signal
        > ```ruby
        > $ nohup myjob.sh &
        > ```

---

> [!TIP]
> ## :raising_hand: สรุป
> Process Termination (การหยุดกระบวนการ) เป็นขั้นตอนสุดท้ายของ Process Management ที่เกี่ยวข้องกับการสิ้นสุดกระบวนการทำงานของกระบวนการ โดยมีการใช้คำสั่ง `kill`, `pkill`, `killall` เพื่อส่งสัญญาณหยุดทำงานแก่กระบวนการ และใช้ `wait` และ `exit` เพื่อรอและคืนทรัพยากรต่าง ๆ ที่ใช้งานของกระบวนการก่อนหน้า.
>

---

<a id="process-priority"></a>
# :bulb: Process Priority
ไม่ใช่ทุกระบวนการมีสิทธิ์เข้าถึง CPU เท่ากัน เพราะเนื่องมาจาก
กระบวนการแต่ละตัวมีลำดับความสำคัญในการใช้ CPU เมื่อมีการแชร์ทรัพยากร CPU ระหว่างกัน. ทำให้ลำดับความสำคัญสามารถถูกกำหนดโดยผู้ใช้ผ่านค่า niceness.

<div align="center">
      ลำดับความสำคัญ niceness
      <table>
      <thead>
      <tr>
      <th style="text-align:left">ค่า niceness สูงสุด</th>
      <th style="text-align:center">ค่าเริ่มต้น</th>
      <th style="text-align:right">ค่า niceness ต่ำสุด</th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td style="text-align:left">-20</td>
      <td style="text-align:center">0</td>
      <td style="text-align:right">19</td>
      </tr>
      </tbody>
      </table>
</div>

#### `nice` - เปลี่ยนระดับความสำคัญของกระบวนการ
> คำสั่งนี้จะเรียกใช้ `process_name` ด้วยค่า niceness ที่ 10 จะทำให้ `process_name` มีลำดับความสำคัญต่ำลง.
> ```ruby
> $ nice -n 10 process_name
> ```

<a id="monitoring-processes"></a>
# :bulb: Monitoring Processes
Multi-Session Command Line Utilities คือเครื่องมือที่ช่วยในการจัดการหลาย session หรือหน้าจอ terminal ได้พร้อมกันใน shell เดียว ซึ่งช่วยเพิ่มประสิทธิภาพในการทำงานบน command line ของระบบปฏิบัติการ Linux หรือ Unix โดยเฉพาะ

คำสั่ง `top` ใน Linux มีหน้าที่ให้ข้อมูลเกี่ยวกับการทำงานของกระบวนการ (process) ในเครื่องคอมพิวเตอร์ของคุณในเวลาจริง ซึ่งจะแสดงข้อมูลทั้งหมดที่เกี่ยวข้องกับประสิทธิภาพของระบบ เช่น CPU usage, Memory usage, และรายการกระบวนการที่กำลังทำงานอยู่ในระบบ.

#### `top` สามารถควบคุมและทำงานได้ผ่าน interactive keys ต่างๆ ที่มีดังนี้:

-  `h` เพื่อดูคู่มือและคำสั่งที่ใช้งานได้
-  `r` เพื่อให้สามารถเปลี่ยนระดับความสำคัญ (nice value) ของกระบวนการ
-  `q` เพื่อออกจาก `top`




> คำสั่ง `top` มีความสามารถในการแสดงข้อมูลแบบ real-time ทำให้สามารถตรวจสอบและติดตามการทำงานของกระบวนการได้อย่างมีประสิทธิภาพ รายละเอียดของ 
> ```ruby
> $ top -u process_name
> ```

> ```
> top - 15:26:35 up 1 day,  2:34,  1 user,  load average: 0.32, 0.22, 0.18
> Tasks: 178 total,   1 running, 177 sleeping,   0 stopped,   0 zombie
> %Cpu(s):  3.2 us,  1.2 sy,  0.0 ni, 94.3 id,  1.3 wa,  0.0 hi,  0.0 si,  0.0 st
> K iB Mem :  8096588 total,  1862844 free,  2757564 used,  3473180 buff/cache
> KiB Swap:  2097148 total,  2097148 free,        0 used.  4842756 avail Mem 
> 
>   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
>   1294 bob       20   0 3281840 640404 137776 S   3.0  7.9   2:00.52 firefox
>   536 root      20   0  581964  42748  31512 S   1.0  0.5   3:57.38 Xorg
> ...
> ```

#### `uptime`
> คำสั่ง `uptime` จะแสดงข้อมูลเกี่ยวกับระยะเวลาที่ระบบทำงาน, จำนวนผู้ใช้ที่กำลังเข้าสู่ระบบ, และค่า Load averages ในช่วง 1, 5, และ 15 นาทีที่ผ่านมา:
> ```ruby
> $ uptime
> ```
> ```
> 18:24:58 up 5 days, 10:43, 1 user, load average: 0.08, 0.03, 0.05
> ```

>
> - 18:24:58: เวลาปัจจุบัน
> - up 5 days, 10:43: ระยะเวลาที่ระบบทำงาน (5 วัน 10 ชั่วโมง 43 นาที)
> - 1 user: จำนวนผู้ใช้ที่กำลังเข้าสู่ระบบ
> - load average: 0.08, 0.03, 0.05: ค่า Load averages ในช่วง 1, 5, และ 15 นาทีที่ผ่าน
>

<a id="Multi-Session"></a>
# :bulb: Multi-Session Command Line Utilities 
คือเครื่องมือที่ช่วยในการจัดการหลาย session หรือหน้าจอ terminal ได้พร้อมกันใน shell เดียว ซึ่งช่วยเพิ่มประสิทธิภาพในการทำงานบน command line ของระบบปฏิบัติการ Linux หรือ Unix โดยเฉพาะ

`screen` และ `tmux` เป็นตัวอย่างของ Multi-Session Command Line Utilities:

#### `screen Command`

- **screen command**: เป็นคำสั่งที่ให้ความสามารถในการรันหลายๆ กระบวนการ (processes) ใน session ที่แยกกันภายใน terminal เดียว
- สามารถใช้ **screen command** ร่วมกับคำสั่งที่ตรวจสอบหรือติดตามสถานะของกระบวนการระบบ เช่น `top` หรือ `ps`
- มีความสามารถในการ detach session และ re-attach ภายหลัง
- เพื่อทำงานใน **screen program** ต้องใช้คีย์คำสั่งของ **screen** ที่กำหนดไว้

> คำสั่ง `screen` ให้ความสามารถในการสร้าง session หลายๆ อันใน terminal และสามารถ detach และ re-attach session ได้. นอกจากนี้ยังสามารถทำหลาย task พร้อมกันใน terminal เดียว.
การใช้คำสั่ง `screen` ใน Linux มีขั้นตอนดังนี้:

1. เพื่อเริ่มใช้ `screen`, ให้พิมพ์คำสั่งต่อไปนี้ที่ command prompt:
   ```bash
   $ screen
   ```

2. เพื่อตรวจสอบว่ามี session ที่กำลังทำงานหรือไม่, ให้ใช้คำสั่ง:
   ```bash
   $ screen -list
   ```

3. เพื่อ detach session, ให้ใช้คีย์ Ctrl+A ตามด้วย D:
   ```
   (Detached)
   ```

4. เพื่อ re-attach session, ให้ใช้คำสั่ง:
   ```bash
   $ screen -r 85
   ```
   โดยที่ `85` คือ PID (Process ID) ของ session ที่ต้องการ re-attach.

ดังนั้น, สรุปคือคำสั่ง `screen` ให้ความสามารถในการสร้าง, จัดการ, และควบคุม sessions หลาย ๆ อันใน terminal และสามารถทำงานพร้อมกันได้. เพิ่มเติม, มีความสามารถในการ detach และ re-attach session ทำให้สามารถบันทึกการทำงานที่กำลังดำเนินอยู่และกลับมาทำต่อภายหลังได้.

#### `tmux Command`

1. คำสั่ง `tmux` เป็น terminal multiplexer ที่ทำให้เราสามารถทำงานกับหลายๆ terminal window ในรูปแบบแบ่งหน้าจอ, และยังสามารถ detach และ re-attach ได้.
    > ```ruby
    > $ tmux
    > ```

2. เพื่อรันคำสั่งใน session ปัจจุบันของ `tmux`, ให้พิมพ์คำสั่งตามปกติ.

3. เพื่อ detach จากคำสั่งที่กำลังทำงาน, เช่น ถ้าคำสั่ง `top` กำลังทำงาน, ให้กด Ctrl+B, จากนั้นกด D:
   ```
   [detached (from session 0)]
   ```

4. ตัวอย่างการใช้ option ของ `tmux` คือ:
   - `-list-sessions`: เพื่อแสดงรายการ sessions ทั้งหมด.
   - `-new-session`: เพื่อสร้าง session ใหม่.


การแบ่งหน้าต่าง terminal เป็นสองส่วนในแนวตั้ง (vertical split), ให้กด Ctrl+B แล้วตามด้วย % (Shift+5):
   ```ruby
   Ctrl+B, %
   ```
การสร้าง session ใหม่ในหน้าต่าง terminal ในแนวนอน (horizontal split), ให้กด Ctrl+B แล้วตามด้วย ":
   ```ruby
   Ctrl+B, Shift+’
   ```


---

> [!TIP]
> ## :raising_hand: สรุป
> การใช้ Multi-Session Command Line Utilities ช่วยให้ผู้ใช้สามารถทำงานได้มีประสิทธิภาพมากขึ้นโดยสามารถทำหลาย task พร้อมกันใน shell เดียวหรือแบ่งหน้าจอ terminal ให้กับ task ต่าง ๆ ได้.
>

---

<a id="source"></a>
# :card_index_dividers: Source
> [!NOTE]
> Vital details for quick comprehension, essential for users skimming through content.
> - Webpage
>    - Process Management In Linux https://unstop.com/blog/process-management-in-linux
>    - Process Control https://medium.com/@The_CodeConductor/process-control-kill-and-pkill-commands-in-linux-64e60a677606
>    - Check running process https://www.cyberciti.biz/faq/how-to-check-running-process-in-linux-using-command-line/
>    - Linux/Unix Process Management Commands https://www.guru99.com/managing-processes-in-linux.html
>    - Run Bash Script as a Daemon https://www.baeldung.com/linux/bash-daemon-script
>    - Linux Process Priority https://www.atlantic.net/vps-hosting/how-to-set-linux-process-priority-using-nice-and-renice-commands/
>    - Foreground & Background Process https://www.baeldung.com/linux/foreground-background-process
>    - A beginner's guide to tmux https://www.redhat.com/sysadmin/introduction-tmux-linux
>    - Linux Screen, With Commands https://phoenixnap.com/kb/how-to-use-linux-screen-with-commands

