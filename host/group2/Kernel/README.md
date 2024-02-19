# Kernel
</div>

## หน้าที่ของ Kernel 
Kernal คือศูนย์กลางในระบบ Computer โดยจะทำหน้าที่ควบคุมการทำงานตั้งแต่ Booting server, Start/Stop Program และจัดการกับ Input/Output จาก Software โดย Kernal จะคล้ายกับสะพานเชื่อมระหว่างส่วนของ Application กับ Data Processing ใน Hardware level ซึ่ง Kernal จะอยู่ตรงกลางที่เชื่อม ให้ programและApplicationอื่น ๆ ในระบบ เป็นโปรแกรมพื้นฐานภายใต้ระบบปฏิบัติการคอมพิวเตอร์ (OS) ที่คอยทำหน้าที่เป็นสื่อกลางระหว่างฮาร์ดแวร์ กับ ซอฟต์แวร์และช่วยจัดการทรัพยากรในคอมพิวเตอร์ต่าง ๆ เพื่อให้สามารถเข้าถึงและใช้งานทรัพยากรของระบบได้อย่างมีประสิทธิภาพ และปลอดภัย เช่น การใช้พื้นที่ หน่วยความจำ (RAM) , การใช้ หน่วยประมวลผลกลาง (CPU) การจัดการไฟล์ และ ระบบอื่น ๆ

1. ให้ส่วนติดต่อที่จำเป็นสำหรับผู้ใช้และแอปพลิเคชันสื่อสารกับคอมพิวเตอร์ Kernel ให้ส่วนติดต่อและแอบสมมติที่จำเป็นให้กับผู้ใช้และแอปพลิเคชันเพื่อให้สามารถสื่อสารกับระบบคอมพิวเตอร์ได้ ซึ่งรวมถึงการจัดการกับการอินพุทและเอาท์พุท, ระบบไฟล์, การสื่อสารผ่านเครือข่าย และทรัพยากรอื่น ๆ

2. เริ่มต้นและจัดการแอปพลิเคชัน Kernel รับผิดชอบในการเริ่มต้น, จัดการ, และควบคุมการทำงานของแอปพลิเคชันและโปรเซสที่ทำงานบนระบบ ซึ่งรวมถึงการจัดสรรทรัพยากรระบบ เช่น หน่วยความจำ, เวลา CPU, และการอินพุท/เอาท์พุท

3. จัดการอุปกรณ์ฮาร์ดแวร์ในระบบ Kernel รับผิดชอบในการจัดการอุปกรณ์ฮาร์ดแวร์ที่อยู่ในระบบ โดยให้บริการการสื่อสารและการทำงานร่วมกับอุปกรณ์ฮาร์ดแวร์ต่าง ๆ เพื่อให้ระบบปฏิบัติการสามารถเข้าถึงและใช้งานอุปกรณ์เหล่านั้นได้อย่างมีประสิทธิภาพ

## ประเภทของ Kernel
-  ### Monolithic Kernels (Kernel ระบบเดียว) ###
    เป็น Kernel ที่มีโครงสร้างที่ใหญ่ ซับซ้อน และ ยากต่อการดูแล ภายหลังจึงได้มีการแยก module ออกมาและทำการเลือก load ใช้งานตามความเหมาะสม เป็นเสมือน extension ให้ OS เลือกใช้ ทำให้ไม่ต้องทำการปิดและ compile ใหม่ทั้งหมด เมื่อมีการแก้ bug ประกอบไปด้วยส่วนหลัก ๆ ทั้งหมดของระบบปฏิบัติการ ซึ่งรวมถึงการจัดการหน่วยความจำ, การจัดการกับอุปกรณ์ฮาร์ดแวร์, การจัดการกับโปรเซส, การจัดการกับไฟล์ระบบ, และการเชื่อมต่อเครือข่าย <br> ตัวอย่างของระบบปฏิบัติการที่ใช้ Monolithic Kernel ได้แก่ Linux (ก่อนหน้านี้), UNIX, BSD, MS-DOS, Microsoft Windows 9x Series, Agnix
   
    ### ข้อดี 
   - Efficiency (ประสิทธิภาพ): เคอร์เนลแบบ Monolithic มักจะมีความเร็วมากกว่าเคอร์เนลประเภทอื่น ๆ เพราะว่าไม่จำเป็นต้องสลับไปมาระหว่างโหมดผู้ใช้และโหมดเคอร์เนลสำหรับทุก system call ซึ่งอาจทำให้เกิด overhead
   - Tight integration (การผสานรวมที่แน่นหนา): เนื่องจากบริการระบบปฏิบัติการทั้งหมดทำงานในพื้นที่เคอร์เนล บริการเหล่านี้จึงสามารถสื่อสารกันได้อย่างมีประสิทธิภาพมากขึ้น ช่วยให้ง่ายต่อการ implement ฟังก์ชันการทำงานและ optimizations ที่ซับซ้อน
   - Simplicity (ความเรียบง่าย): เคอร์เนลแบบ Monolithic นั้นง่ายต่อการออกแบบ implement และ debug มากกว่าเคอร์เนลประเภทอื่น ๆ เพราะว่ามีโครงสร้างที่เป็นหนึ่งเดียว ช่วยให้ง่ายต่อการจัดการโค้ด
   - Lower latency (ความหน่วงเวลาน้อย): เคอร์เนลแบบ Monolithic มีความหน่วงเวลาน้อยกว่าเคอร์เนลประเภทอื่น ๆ เพราะว่า system calls และ interrupts สามารถจัดการโดยเคอร์เนลได้โดยตรง
     
    ### ข้อเสีย
    - Stability issues (ปัญหาความเสถียร): เคอร์เนลแบบ Monolithic อาจจะมีความเสถียรน้อยกว่าเคอร์เนลประเภทอื่น ๆ เพราะว่าบั๊กหรือช่องโหว่ด้านความปลอดภัยใด ๆ ในบริการเคอร์เนลสามารถส่งผลต่อระบบทั้งหมด
    - Security vulnerabilities (ช่องโหว่ด้านความปลอดภัย): เนื่องจากบริการระบบปฏิบัติการทั้งหมดทำงานในพื้นที่เคอร์เนล ช่องโหว่ด้านความปลอดภัยใด ๆ ในบริการหนึ่งสามารถทำให้ระบบทั้งหมดตกอยู่ในอันตราย
    - Maintenance difficulties (ความยากลำบากในการบำรุงรักษา): เคอร์เนลแบบ Monolithic อาจจะมีความยากลำบากในการบำรุงรักษามากกว่าเคอร์เนลประเภทอื่น ๆ เพราะว่าการเปลี่ยนแปลงใด ๆ ในบริการหนึ่งสามารถส่งผลต่อระบบทั้งหมด
    - Limited modularity (การแยกส่วนแบบจำกัด): Monolithic มีการแยกส่วนน้อยกว่าเคอร์เนลประเภทอื่น ๆ เพราะว่าบริการระบบปฏิบัติการทั้งหมดถูกผสานรวมเข้ากับพื้นที่เคอร์เนลอย่างแน่นหนา ทำให้ยากต่อการเพิ่มหรือลบฟังก์ชันการทำงานโดยไม่ส่งผลต่อระบบทั้งหมด

-  ### Microkernel (Kernel ไมโคร) ### 
   เป็น Kernel ที่ทำให้มีการแยกส่วนของระบบพื้นฐาน driver, protocol stack, file system ออกมาrunข้างนอก ทำให้ลดขนาดของ Kernel ลงและยังเพิ่ม security และ stability ให้กับ OS ทำให้มีโครงสร้างที่เล็กและมีความเรียบง่าย โดยมีเพียงส่วนของระบบที่จำเป็นสำหรับการทำงานพื้นฐาน <br> ตัวอย่างของระบบปฏิบัติการที่ใช้ Microkernel ได้แก่ QNX, MINIX, AIX, Android OS, EROS, Mach Kernel
   
    ### ข้อดี 
   - Reliability (ความน่าเชื่อถือ): สถาปัตยกรรมไมโครเคอร์เนลออกแบบมาให้มีความน่าเชื่อถือมากกว่าเคอร์เนลแบบ Monolithic เนื่องจากบริการระบบปฏิบัติการส่วนใหญ่ทำงานอยู่นอกพื้นที่เคอร์เนล บั๊กหรือช่องโหว่ด้านความปลอดภัยใด ๆ ในบริการจึงไม่ส่งผลกระทบต่อระบบทั้งหมด
   -  Flexibility (ความยืดหยุ่น): สถาปัตยกรรมไมโครเคอร์เนลมีความยืดหยุ่นมากกว่าเคอร์เนลแบบ Monolithic เพราะอนุญาตให้เพิ่มหรือลบบริการระบบปฏิบัติการที่แตกต่างกันโดยไม่ส่งผลกระทบต่อระบบทั้งหมด
   - Modularity (ความเป็นโมดูลาร์): สถาปัตยกรรมไมโครเคอร์เนลเป็นแบบโมดูลาร์มากกว่าเคอร์เนลแบบ Monolithic เพราะบริการระบบปฏิบัติการแต่ละบริการทำงานแยกอิสระจากบริการอื่น ๆ ทำให้การบำรุงรักษาและ debug ระบบง่ายขึ้น
   - Portability (ความสามารถในการพกพา): สถาปัตยกรรมไมโครเคอร์เนลสามารถพกพาได้มากกว่าเคอร์เนลแบบ Monolithic เนื่องจากบริการระบบปฏิบัติการส่วนใหญ่ทำงานอยู่นอกพื้นที่เคอร์เนล ทำให้ง่ายต่อการย้ายระบบปฏิบัติการไปยังสถาปัตยกรรมฮาร์ดแวร์ที่แตกต่างกัน
     
    ### ข้อเสีย
   - Performance (ประสิทธิภาพ): สถาปัตยกรรมไมโครเคอร์เนลอาจจะช้ากว่าเคอร์เนลแบบ Monolithic เพราะว่าจำเป็นต้องมีการสลับโหมด (context switch) ระหว่างพื้นที่ผู้ใช้และพื้นที่เคอร์เนลมากกว่า
   - Complexity (ความซับซ้อน): สถาปัตยกรรมไมโครเคอร์เนลอาจจะซับซ้อนกว่าเคอร์เนลแบบ Monolithic เพราะว่าจำเป็นต้องมีกลไกการสื่อสารและซิงโครไนซ์ที่มากขึ้นระหว่างบริการระบบปฏิบัติการที่แตกต่างกัน
   - Development difficulty (ความยากในการพัฒนา): การพัฒนาระบบปฏิบัติการบนพื้นฐานของสถาปัตยกรรมไมโครเคอร์เนลอาจจะยากกว่าการพัฒนาเคอร์เนลแบบ Monolithic เพราะว่าจำเป็นต้องใส่ใจในรายละเอียดมากขึ้นในการออกแบบกลไกการสื่อสารและซิงโครไนซ์ระหว่างบริการที่แตกต่างกัน
   - Higher resource usage (การใช้ทรัพยากรมากขึ้น): สถาปัตยกรรมไมโครเคอร์เนลอาจจะใช้ทรัพยากรระบบ เช่น หน่วยความจำและ CPU มากกว่าเคอร์เนลแบบ Monolithic เพราะว่าจำเป็นต้องมีกลไกการสื่อสารและซิงโครไนซ์ที่มากขึ้นระหว่างบริการระบบปฏิบัติการที่แตกต่างกัน
    
-  ### Hybrid kernels (เคอร์เนลแบบผสม) ###
    เป็นการผสมผสานระหว่าง Monolithic Kernel และ Microkernel โดยมีลักษณะทั้งสองคุณสมบัติ ถูกนำมาใช้งานกับ OS ระดับ commercial มีลักษณะคล้าย microkernel แต่ว่ามันได้รวมเอา code เสริมใน kernel space มาเพิ่มความสามารถโดยใช้เป็น extension ให้กับ microkernel  <br> ตัวอย่างของระบบปฏิบัติการที่ใช้ Hybrid Kernel ได้แก่ Microsoft Windows และ macOS ตั้งแต่รุ่น XNU ของ macOS และ Darwin Kernel ที่ใช้งานบน macOS และ iOS
   
    ### ข้อดี 
    - Performance ประสิทธิภาพ: เคอร์เนลผสมสามารถมอบประสิทธิภาพที่ดีกว่าไมโครเคอร์เนล เนื่องจากลดจำนวน context switch ที่จำเป็นระหว่างพื้นที่ผู้ใช้และพื้นที่เคอร์เนล
    - Reliability ความน่าเชื่อถือ: เคอร์เนลผสมสามารถมอบความน่าเชื่อถือที่ดีกว่าเคอร์เนลแบบ Monolithic เนื่องจากแยกไดรเวอร์และคอมโพเนนต์เคอร์เนลอื่นๆ ไว้ในโดเมนการป้องกันที่แยกจากกัน
    - Flexibility ความยืดหยุ่น: เคอร์เนลผสมสามารถมอบความยืดหยุ่นที่ดีกว่าเคอร์เนลแบบ Monolithic เนื่องจากอนุญาตให้เพิ่มหรือลบบริการระบบปฏิบัติการที่แตกต่างกันโดยไม่ส่งผลกระทบต่อระบบทั้งหมด
    - Compatibility ความเข้ากันได้: เคอร์เนลผสมสามารถเข้ากันได้มากกว่าไมโครเคอร์เนล เนื่องจากรองรับไดรเวอร์อุปกรณ์หลากหลายประเภท
     
    ### ข้อเสีย
   - Complexity (ความซับซ้อน): เคอร์เนลผสมอาจจะซับซ้อนกว่าเคอร์เนลแบบ Monolithic เนื่องจากประกอบด้วยทั้งคอมโพเนนต์แบบ Monolithic และ microkernel ซึ่งอาจทำให้การออกแบบและการใช้งานยากขึ้น
   - Security (ความปลอดภัย): เคอร์เนลผสมอาจจะปลอดภัยน้อยกว่าไมโครเคอร์เนล เนื่องจากมีพื้นที่โจมตีที่กว้างกว่า เนื่องจากมีการรวมคอมโพเนนต์แบบ Monolithic
   - Maintenance (การบำรุงรักษา): เคอร์เนลผสมอาจจะยากต่อการบำรุงรักษามากกว่าไมโครเคอร์เนล เนื่องจากมีการออกแบบและใช้งานที่ซับซ้อนกว่า
   - Resource usage (การใช้ทรัพยากร): เคอร์เนลผสมอาจจะใช้ทรัพยากรระบบมากว่าไมโครเคอร์เนล เนื่องจากประกอบด้วยทั้งคอมโพเนนนต์แบบ Monolithic และ microkernel

## ประเภทของอื่นๆ Kernel 
-  ### Exo Kernel ###
      เป็นประเภทของเคอร์เนลที่ยึดหลักการทำงานแบบ End-to-End โดยมีหลักการสำคัญดังนี้
   - มีการแยกส่วนของฮาร์ดแวร์น้อยที่สุด Exo Kernel พยายามลดเลเยอร์ของการแยกส่วน (Abstraction) ระหว่างแอพพลิเคชันกับฮาร์ดแวร์ให้น้อยที่สุด ทำให้ลดโอเวอร์เฮด (Overhead) และอนุญาตให้แอพพลิเคชันสามารถควบคุมและจัดการกับฮาร์ดแวร์ได้โดยตรง
   - จัดสรรทรัพยากรทางกายภาพ หน้าที่หลักของ Exo Kernel คือการจัดการและจัดสรรทรัพยากรทางกายภาพ เช่น หน่วยความจำ CPU และอุปกรณ์ต่างๆ ให้กับแอพพลิเคชันโดยตรง โดยไม่รับผิดชอบงานด้านอื่นๆ เช่น ระบบไฟล์ ระบบเครือข่าย หรือความปลอดภัย
   - เสริม โดยทั่วไปแล้ว Exo Kernel จะไม่ค่อยนิยมใช้งานเท่ากับ Monolithic Kernel หรือ Microkernel เนื่องจากความซับซ้อน อย่างไรก็ตาม Exo Kernel เหมาะสำหรับการใช้งานเฉพาะทางที่ต้องการประสิทธิภาพสูง ความยืดหยุ่น และการควบคุมฮาร์ดแวร์อย่างละเอียด 
  
-  ### Nano Kernel ###
      เป็นประเภทของเคอร์เนลที่ให้การแยกฮาร์ดแวร์ เป็นประเภทของเคอร์เนลที่มีขนาดเล็ก แต่ไม่มีบริการระบบ ในขณะที่ไมโครเคอร์เนลก็ไม่มีบริการระบบเช่นกัน ดังนั้น  Nano Kernel และ Micro Kernel จึงกลายเป็นสิ่งที่คล้ายคลึงกัน
   
## หลักการทำงานของ Kernel 
 การปฏิบัติตามคำสั่งของระบบปฏิบัติการและให้บริการแก่โปรแกรมและผู้ใช้ทั่วไปในการใช้งานเครื่องคอมพิวเตอร์ หลักการทำงานของ Kernel มีหลายองค์ประกอบที่สำคัญ 
    
 1.  เริ่มต้นระบบ เมื่อเปิดเครื่องคอมพิวเตอร์ โปรแกรมบูตโหลดเดอร์ (Bootloader) จะโหลด Kernel เข้าสู่หน่วยความจำหลัก (RAM) หลังจากนั้นจะ เริ่มต้นการทำงานโดยตรวจสอบฮาร์ดแวร์ทั้งหมด เช่น CPU, หน่วยความจำ, อุปกรณ์ I/O ฯลฯ และ เตรียมพร้อมสำหรับการทำงานของระบบปฏิบัติการ

 2.  จัดการทรัพยากร Kernel ทำหน้าที่จัดการทรัพยากรระบบทั้งหมด Kernel จัดสรรทรัพยากรให้กับแอปพลิเคชันที่ร้องขอ และ ควบคุมการเข้าถึงทรัพยากรเพื่อป้องกันความขัดแย้ง
    
 3.  จัดการกระบวนการ Kernel ทำหน้าที่สร้าง ยกเลิก และจัดการกระบวนการต่างๆในระบบ กำหนดเวลา CPU ให้กับกระบวนการต่างๆ จัดการหน่วยความจำให้กับกระบวนการต่างๆ ควบคุมการเข้าถึงไฟล์และอุปกรณ์ต่อพ่วง

 4. สื่อสารกับฮาร์ดแวร์ Kernel ทำหน้าที่สื่อสารกับฮาร์ดแวร์ทั้งหมดของคอมพิวเตอร์ แปลคำสั่งจากซอฟต์แวร์เป็นภาษาที่ฮาร์ดแวร์เข้าใจได้ ควบคุมการทำงานของอุปกรณ์ต่อพ่วงต่างๆ
 5. ให้บริการระบบ Kernel ทำหน้าที่ให้บริการระบบพื้นฐาน เช่น ระบบไฟล์ ระบบเครือข่าย ระบบความปลอดภัย ฯลฯ บริการเหล่านี้ช่วยให้นักพัฒนาซอฟต์แวร์สามารถเขียนโปรแกรมโดยไม่ต้องเขียนโค้ดสำหรับควบคุมฮาร์ดแวร์โดยตรง
 6. ทำงานเป็นพื้นหลัง Kernel ทำงานเป็นพื้นหลังโดยผู้ใช้ไม่ต้องโต้ตอบโดยตรง ผู้ใช้สามารถโต้ตอบกับ Kernel ผ่านระบบปฏิบัติการ


## ข้อควรระวังในการใช้งาน<br> ## 
การเข้าถึงและแก้ไขโค้ดหรือการตั้งค่าใน kernel ต้องมีการให้ความระมัดระวัง เพราะการกระทำไม่ถูกต้องอาจทำให้ระบบล่มหรือทำให้ระบบไม่สามารถ ทำงานได้<br>

# คำสั่งที่ควรรู้
คำสั่งที่ควรรู้ใน kernel :
```
$ lsmod
```
>เป็นคำสั่งที่จะแสดงสถานะของ kernel ทั้งหมดโดยจะแสดงเป็น list modules โดยจะแบ่ง Module, Size, Used by

ผลลัพธ์

![Screenshot 2024-02-09 214709](https://github.com/CosmoGuy112/PHost/assets/112687431/462dff8e-bc64-4784-a7ea-efc7d923dc06)


```
$ insmod [ filename ] [ module options... ]
```
>เป็นคำสั่งที่ insert module เข้าไปที่ kernel โดยตรง โดยคำสั่งนี้ก็เป็นคำสั่งที่ช่วยเพิ่มฟังก์ชั่นของ core ในระบบปฎิบัติการ

```
$ rmmod [Option] <Module>
```
>เป็นคำสั่งที่จะ remove module ใน kernel ออก

| Command | Descript |
|--------------------------------|-----------------------------|
| `rmmod -f [Module]` | เป็นการบังคับลบ Module ออกแม้ว่าจะทำงานอยู่ แต่อาจจะทำให้ เครื่อง crash ได้ |
| `rmmod -s`  | เป็นการส่งผลลัพธ์ของคำสั่ง rmmod ไปยังไฟล์บันทึกระบบ syslog แทนที่จะแสดงบนหน้าจอ โดยคำสั่งนี้มีประโยชน์สำหรับการบันทึกกิจกรรมและติดตามปัญหา |
| `rmmod -v [Module]` | เป็นการแสดง ข้อความเพิ่มเติม เกี่ยวกับการถอด Module ออก โดยคำสั่งนี้มีประโยชน์ในการแก้ Debug |



# References
- https://tips.thaiware.com/1806.html#what-is-a-kernel-task
- https://www.techtarget.com/searchdatacenter/definition/kernel
- https://saixiii.com/what-is-kernel/
- https://th.wikipedia.org/wiki/%E0%B9%83%E0%B8%88%E0%B8%81%E0%B8%A5%E0%B8%B2%E0%B8%87
- https://digilent.com/blog/demystifiying-the-linux-kernel/
- https://www.javatpoint.com/what-is-kernel
- -https://www.computerhope.com/unix/insmod.htm
- https://eng.libretexts.org/Bookshelves/Computer_Science/Operating_Systems/Linux_-_The_Penguin_Marches_On_(McClanahan)/06%3A_Kernel_Module_Management/2.05%3A_Kernel_Module_Management_-_lsmod_Command
- https://www.geeksforgeeks.org/kernel-in-operating-system/
- https://phoenixnap.com/kb/modprobe-command