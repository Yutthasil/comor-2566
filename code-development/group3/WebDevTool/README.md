
# Web DevTool

คือเครื่องมือช่วยนักพัฒนาแก้ไขและปรับปรุงโค้ดสำหรับ
การพัฒนาเว็บ เครื่องมือมีฟังก์ชันหลายๆอย่างเพื่อที่ให้นักพัฒนาสามารถพัฒนาให้โปรเจคนั้นมีประสิทธิภาพ และเครื่องมือมีให้เลือกใช้ตามงาน แต่ในรายงานนี้จะพูดถึง PHP

<br>

## PHP
	
เป็นช่วยในการจัดการเนื้อหาในฐานข้อมูลและมีความยืดหยุ่นในการจัดการฐานข้อมูล จุดประสงค์สำคัญของ PHP คือ การประมวลผลก่อนจะส่ง HTML ในกับผู้ใช้งานแตละผู้ใช้จะมีการประมวลผลไม่เหมือนกัน เช่น การจดจำรหัสผ่านของแต่ละ User เมื่อตอน user Login เข้ามาอีกครั้งจะไม่ต้องจำเป็นในการกรอกรหัสใหม่ จะเห็นได้ว่ามีการประมวลผลของแต่ละ user

<br>

## ใช้ PHP ร่วมกับ Linux ดียังไง

การใช้ PHP ร่วมกับ Linux ดีเพราะ Linux เป็นระบบปฏิบัติการที่จัดการกับโฮสต์เว็บไซต์ได้ดี และ PHP เป็นภาษาที่มีความยืดหยุ่นและสามารถทำงานร่วมกับเว็บเซิร์ฟเวอร์ได้อย่างเหมาะสม การใช้คู่กันนี้ช่วยให้นักพัฒนาสามารถสร้างและดูแลระบบเว็บไซต์และแอปพลิเคชันได้อย่างมีประสิทธิภาพ

<br>

## วิธีติดตั้ง PHP บน Linux

<br>

ติดตั้ง PHP

 <br>

  ```bash
  sudo apt install php คือคำสั่งติดตั้ง php
  ```

 <br>

ตรวจสอบการติดตั้ง PHP

 <br>

   ```bash
   php -S localhost:8080
   ```

 <br>

คำสั่งนี้คือคำสั่ง ที่สร้าง localhost ที่พอร์ด 8080 ทำให้สามารถ ทดสอบและดูผลลัพธ์ได้ใน http://localhost:8080 และถ้ามัน run คำสั่งสำเร็จนั้นก็แปลว่าติดตั้ง PHP และ เพราะถ้าไม่สำเร็จจะไม่สามารถใช้คำสั่งได้ 

### ผลลัพธ์ :
<br>
   
   <img src='https://owlhowto.com/content/images/2023/06/php-server-started.png?ezimgfmt=ng:webp/ngcb2' width='1000' height='150'>

<br>

## สร้าง Script PHP

1. สร้าง directory ด้วยคำสั่ง
   <br>

   ```bash
       mkdir ชื่อของdirectoryที่จะสร้าง
   ```
   <br>
   
2. เข้าไปที่ directory ที่สร้างด้วยคำสั่ง
   <br>

   ```bash
       cd ชื่อของdirectoryที่สร้างมา
   ```
   <br>

3. สร้างไฟล์ php
   <br>

   ```bash
       sudo nano ชื่อไฟล์.php
   ```
   <br>

จากนั้นจะสามารถเขียน Script ตามตัวอย่างได้เลย

<br>
   
   <img src='https://owlhowto.com/content/images/2023/06/app-php-code-1.png?ezimgfmt=ng:webp/ngcb2' width='1000' height='300'>

<br>		

### จากนั้นกด Ctrl + x เพื่อออก และกด Y เพื่อบันทึก จากนั้นกด enter

<br>

## วิธีการเรียกใช้ PHP

<br>

  สามารถเรียกใช้หรือดูผลลัพธ์ได้โดย
<br>

   ```bash
   php -S localhost:8080 ชื่อไฟล์ที่ตั้งไว้.php
   ```
   <br>

## Refference
```bash
   https://www.zend.com/blog/installing-php-linux
   https://www.geeksforgeeks.org/how-to-install-php-on-linux/
   https://ngangasn.com/web-development-tools-that-are-super-helpful-for-linux-web-developers/?expand_article=1
   https://owlhowto.com/how-to-run-php-script-on-localhost-on-linux/
   ```
   <br>
  

