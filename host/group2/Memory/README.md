# Memory

ในระบบปฏิบัติการ "Memory" หมายถึงพื้นที่ที่ใช้เก็บข้อมูลและโปรแกรมขณะทำงานในระบบ โดยปกติแล้วมีหลายประเภทของหน่วยความจำหรือ Memory ในระบบ Linux  หน่วยความจำ (Memory) ใน Linux มีบทบาทสำคัญในการจัดเก็บข้อมูลและรันโปรแกรมต่างๆ บนระบบ ปกติแล้ว RAM (Random Access Memory) จะถูกใช้เป็นหน่วยความจำหลักของระบบ หลักๆจะมี

## Physical Memory (RAM)
เป็นหน่วยความจำที่ติดตั้งในเครื่องคอมพิวเตอร์โดยตรง ซึ่งใช้สำหรับเก็บข้อมูลและโปรแกรมที่กำลังทำงานในระบบปฏิบัติการ และสามารถเข้าถึงได้โดยโปรแกรมที่ทำงานในระบบ

## Virtual memory
เป็นหน่วยความจำเสมือนที่ใช้ในการจำลองพื้นที่หน่วยความจำที่มากขึ้นจากพื้นที่หน่วยความจำที่มีอยู่ใน Linux มีการจัดการโดย Kernel ซึ่งเป็นส่วนที่สำคัญในการจัดการหน่วยความจำ ซึ่งรวมถึงการจัดการหน่วยความจำ

# Commands to Check Memory Use in Linux

### free Command to Display the Amount of Physical and Swap Memory
```bash
  $ free
```
ผลลัพธ์ที่ได้หลังจากใช้ Command

<img width="348*4" alt="image" src="https://github.com/CosmoGuy112/PHost/assets/112687423/9390230e-cbbf-4ca0-92e4-296410751368">
<br>



**` free `** แสดงข้อมูลเกี่ยวกับการใช้หน่วยความจำในระบบ เช่น หน่วยความจำทั้งหมด, หน่วยความจำที่ใช้งาน, หน่วยความจำที่ว่าง, การใช้งานหน่วยความจำแบบเคลื่อนที่, และหน่วยความจำแคช
- ` free -h `
แสดงผลลัพธ์ในรูปแบบที่เป็นมนุษย์อ่านได้ (ในหน่วยความจำตามขนาดของข้อมูล)

- ` free -m  ` จะแสดงข้อมูลในหน่วยเป็นเมกะไบต์ (MB) เพื่อความสะดวกในการอ่าน

- ` free -b ` คำสั่งนี้จะแสดงข้อมูลการใช้งานหน่วยความจำในหน่วยไบต์ (bytes) ที่ไม่ถูกจำกัดโดยการแสดงผลเป็นตัวเลขจำนวนเต็มเท่านั้น หน่วยความจำที่แสดงจะเป็นข้อมูลในรูปแบบที่ไม่มีการเปลี่ยนแปลงขนาดหน่วยความจำ

- ` free -g `
คำสั่งนี้จะแสดงข้อมูลการใช้งานหน่วยความจำในหน่วยเป็นเกีบไบต์ (GB) เพื่อความสะดวกในการอ่าน

- ` free -t ` แสดงผลรวมของหน่วยความจำทั้งหมดที่ใช้งานทั้ง Ram และ Swap

- ` free -s [delay] ` อัปเดตผลลัพธ์ทุก [delay] วินาที

- `c [count]` อัปเดตผลลัพธ์ทั้งหมด [count] ครั้ง

| Name             |   description                                                       |
| ----------------- | ------------------------------------------------------------------ |
| total  | หน่วยความจำที่ติดตั้งทั้งหมด |
| used  | หน่วยความจำที่ใช้งานอยู่ในปัจจุบันโดยกระบวนการที่รันอยู่ (used= total – free – buff/cache) |
| free  | หน่วยความจำที่ไม่ได้ใช้ (free= total – used – buff/cache)|
| shared  | หน่วยความจำที่ใช้ร่วมกัน |
| buffers  | หน่วยความจำที่ระบบปฏิบัติการสงวนไว้เพื่อจัดสรรเป็นบัฟเฟอร์เมื่อกระบวนการต้องการ |
| cached  | ไฟล์ที่ใช้ล่าสุดจัดเก็บไว้ใน Ram |
| buff/cache  | Buffers + Cache |
| available  | การประมาณจำนวนหน่วยความจำที่พร้อมใช้งานสำหรับการเริ่มแอปพลิเคชันใหม่โดยไม่ต้องสลับ |
<br>
<br>


## Show online status information about memory blocks
```bash
  $ lsmem 
```
ผลลัพธ์ที่ได้หลังจากใช้ Command

<img width="279*2" alt="lsmem" src="https://github.com/CosmoGuy112/PHost/assets/112687423/02a4bbbf-50c0-4498-b428-0c5e2f64f6b1">
<br>


- `lsmem` ใช้ในการแสดงข้อมูลเกี่ยวกับการใช้งานหน่วยความจำเชิง Physical Memory ในระบบ โดยจะแสดงข้อมูล เช่น ขนาดของหน่วยความจำทั้งหมด, ข้อมูลเกี่ยวกับ node และ process ที่ใช้งานหน่วยความจำนั้น นอกจากนี้ยังสามารถใช้ในการแสดงข้อมูลเกี่ยวกับ NUMA (Non-Uniform Memory Access) ในระบบ Linux
<br>


## cat Command to Show Linux Memory Information
```bash
  $ cat /proc/meminfo
```
ผลลัพธ์ที่ได้หลังจากใช้ Command

<img width="132*2" alt="cat" src="https://github.com/CosmoGuy112/PHost/assets/112687423/66697506-0659-46ab-80a0-69bfd62c5e8d">
<br>


- `/proc/meminfo` เป็นหนึ่งในไฟล์พิเศษในระบบไฟล์ `/proc` ให้ข้อมูลเกี่ยวกับการใช้งานและสถานะของหน่วยความจำ (RAM) บนระบบเครื่อง Linux ไฟล์นี้จะเป็นข้อมูลของหน่วยความจำเกี่ยวกับการใช้งานในขณะที่คำสั่งถูกเรียกใช้งาน ส่วนของ `/proc/meminfo` จะแสดงข้อมูลที่อยู่ภายใน
<br>
<br>

## Commands to Show detail used Memory in Linux
```bash
  $ vmstat
```
ผลลัพธ์ที่ได้หลังจากใช้ Command

<img width="332*1.5" alt="vvvvv" src="https://github.com/CosmoGuy112/PHost/assets/112687423/772315fc-c032-4932-a6fd-34c30d092114">
<br>


- `vmstat` เป็นคำสั่งที่ไว้แสดงรายงาน CPU activity memory paging รวมๆ ก็คือไว้สำหรับดู performance ของระบบนะเอง
ถ้าเราใช้คำสั่ง `vmstat` โดยไม่มี parameter ต่อท้ายเลย จะหมายถึงแสดงค่าเฉลี่ยของทั้งหมดตั้งแต่เครื่องทำงานมา

ในส่วนที่แสดงในส่วนของ Memory จะมี
- `swpd` จำนวนหน่วยความจำเสมือนที่ใช้ กล่าวอีกนัยหนึ่ง จำนวนหน่วยความจำที่ถูกสลับออกไป
- `free` จำนวนหน่วยความจำที่ไม่ได้ใช้งาน (ปัจจุบันไม่ได้ใช้)
- `buff` จำนวนหน่วยความจำที่ใช้เป็นบัฟเฟอร์
- `cache` จำนวนหน่วยความจำที่ใช้เป็นแคช
<br>
<br>

## Commands to Show detail process Memory in Linux (Top)
```bash
  $ top
```
ผลลัพธ์ที่ได้หลังจากใช้ Command

<img width="511*1.2" alt="top" src="https://github.com/CosmoGuy112/PHost/assets/112687423/ab1463b8-8011-45da-98a6-e3e5a177177a">
<br>


- คำสั่ง `top` อนุญาตให้ผู้ใช้งานสามารถตรวจสอบ Monitor process และการใช้ System Resource โดยจะทำให้รู้ว่า process ไหนกำลังทำงาน process ไหนใช้งานทรัพยากรของเครื่องมากจนเกินไป จะได้สั่งหยุด Kill การทำงาน หากต้องการที่จะออกจากโปรแกรม `top` สามารถทำได้โดยกดที่ป่ม q
<br>
<br>

## htop Command to Find Memory Load of Each Process
```bash
  $ htop
```
ผลลัพธ์ที่ได้หลังจากใช้ Command

<img width="515*1.3" alt="htop" src="https://github.com/CosmoGuy112/PHost/assets/112687423/c3331510-ab66-4d3a-b43c-3353d287aab8">
<br>

- คำสั่ง `htop` แสดงข้อมูลเกี่ยวกับสถานะของระบบและ processes ในเวลาที่เป็นเรียลไทม์ เช่น CPU usage, memory usage, และ process list ที่มีการเรียงตามความสำคัญ โดยสามารถกดปุ่ม Shift + M เพื่อเรียงลำดับกระบวนการตามการใช้งานหน่วยความจำ (Memory usage)
<br>
<br>

## Commands to Delete cache in Linux
```bash
  $ vm.drop_caches=3
```
- คำสั่ง  `vm.drop_caches=3` ใช้ในการลบข้อมูลcache ของหน่วยความจำRAM ในระบบ Linux ซึ่งจะส่งผลให้ข้อมูลในแคชทั้งหมดถูกลบออกจากระบบ ค่า "3" ในการกำหนดค่าให้กับ `vm.drop_caches` หมายถึงการลบข้อมูลแคชทั้งหมด ซึ่งรวมถึง buffer cache, page, cache, และ slab cache ทั้งหมด
- การลบข้อมูลแคชเป็นเครื่องมือที่มีประโยชน์ในบางกรณี เช่น เมื่อต้องการปล่อยหน่วยความจำเพิ่มเติมที่ถูกใช้งานโดยแคช หรือเมื่อต้องการล้างข้อมูลที่ไม่จำเป็นออกจากระบบเพื่อเพิ่มประสิทธิภาพการทำงานของระบบในบางกรณี เช่น เมื่อมีการทดสอบประสิทธิภาพของระบบ หรือต้องการความสมดุลในการใช้งานหน่วยความจำ
- ควรใช้คำสั่ง `vm.drop_caches=3` ด้วยความระมัดระวังเนื่องจากการลบข้อมูลแคชอาจทำให้ระบบช้าลงชั่วคราวในขณะที่ระบบต้องทำการโหลดข้อมูลใหม่เข้าสู่แคชอีกครั้ง และอาจส่งผลให้การทำงานของแอปพลิเคชันหรือระบบที่ได้รับผลกระทบต่าง ๆ อาจเป็นไปได้ ดังนั้นควรใช้คำสั่งนี้โดยคำนึงถึงความเหมาะสมและการจำเป็นของการลบแคชในสถานการณ์ของระบบ
<br>
<br>


# References
- https://ioflood.com/blog/htop-linux-command/
- https://phoenixnap.com/kb/linux-commands-check-memory-usage
- https://tips.thaiware.com/1806.html
- https://th.linux-console.net/?p=2061
- https://saixiii.com/free-linux-command/
- https://coderwall.com/p/ef1gcw/managing-ram-and-swap
- https://it-madmonster.blogspot.com/2009/08/unix-linux-vmstat-command.html
- https://th.linux-console.net/?p=8268
- https://medium.com/olarik/linux-command-top-show-current-running-process-54e8881c31ef
- https://www.ibm.com/support/pages/memory-linux-determining-how-much-memory-you-have-linux
- https://www.site24x7.com/learn/linux/optimize-memory.html
- https://tldp.org/LDP/sag/html/vm-intro.html
- https://docs.kernel.org/mm/physical_memory.html
- https://www.baeldung.com/linux/buffer-vs-cache-memory
