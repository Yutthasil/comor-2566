# Eclipse

โปรแกรม eclipse เป็นอีกโปรแกรมที่ใช้สำหรับใช้พัฒนาเซอร์เวอร์ และแอปพลิเคชั่น โดยมีข้อดีที่ติดตั้งง่าย และรองรับหลากหลายภาษาเช่น ภาษา C,Java,HTML,XML [1]

## วิธีการติดตั้ง Eclipse ในระบบปฏิบัติการ Linux

1. ติดตั้ง Java ในระบบปฏิบัติการ Ubuntu หรือ Linux ที่เป็นเดเบี้ยน

        sudo apt install -y openjdk-11-jdk


2. หลังจากนั้น Download ตัวไฟล์ Package
  https://www.eclipse.org/downloads/packages/


3. เมื่อได้ไฟล์ tar.gz มาแล้ว ให้แยกไฟล์ด้วยคำสั่ง
        
        tar -xvf eclipse-inst-linux64.tar.gz

4. คำสั่งด้านบนจะทำการแยกไฟล์และใส่ไว้ใน directory ที่ชื่อว่า eclipse-installer จากนั้นให้เราเปลี่ยน directory โดยใช้คำสั่ง

        cd eclipse-installer/

5. หน้าต่างของ installer ของโปรแกรมจะขึ้นมา
 ดังนี้

![](eclipse1.jpg)

6. ให้ทำตาขั้นตอนการ install ต่อไป 

![](eclipse2.jpg)



## Reference

https://www.aosoft.co.th/article/312/Eclipse-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3.html [1]

https://www.makeuseof.com/install-eclipse-ide-on-linux/ [2]

