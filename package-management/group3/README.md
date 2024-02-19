# PackageManagement-3

COMPUTER ORGANIZATION AND OPERATING SYSTEM (Chapter: Package Management, Section: 3)

## Introduction to Package Management

Ubuntu มีระบบในการจัดการ Package ที่ครอบคลุมสำหรับ การติดตั้ง, อัพเกรด, กำหนดค่า รวมไปถึงการ ลบ Software นอกจากนี้ยังสามารถตรวจสอบและเข้าถึงฐานข้อมูลที่มีองค์ประกอบมากกว่า 60,000 Software packages อีกด้วย

- ### Package คืออะไร ?

  แพ็คเกจ (package) ใน Linux ก็เปรียบเสมือน Program บน Window ซึ่งจะประกอบไปด้วย หลายๆไฟล์ที่ใช้ในการทำงาน เช่น การติดตั้งโปรแกรมในลีนุกซ์ตระกูล Debian

- ### Package Management Tools

  เป็นเครื่องมือที่ใช้ในการจัดการ Package ทั้งติดตั้ง และถอนการติดตั้ง มีตั้งแต่ simple command-line ไปจนถึง Interface Graphics ที่ใช้ง่ายเหมาะสำหรับมือใหม่ที่กำลังหัดใช้ Ubuntu และทำให้การติดตั้งและจัดการซอฟต์แวร์บนระบบ Linux ง่ายขึ้น
  Linux มี Package Management Tools มากมายหลายชนิด แต่ที่นิยมใช้กัน ได้แก่

  - apt และ apt-get ใช้บนระบบ Debian และ Ubuntu
  - yum ใช้บนระบบ Red Hat และ CentOS
  - dnf (Dandified yum) ใช้แทน yum บนระบบ Fedora
  - zypper ใช้บนระบบ openSUSE
  - rpm
  - dpkg เป็นเครื่องมือสำหรับจัดการแพ็คเกจบนระบบ Linux ซึ่งช่วยให้เราสามารถติดตั้ง สร้าง ลบ และจัดการแพ็คเกจ Debian ได้

  ซึ่ง Tools เหล่านี้ก็มีคุณสมบัติที่คล้ายคลึงกัน รวมถึงมีข้อดีและข้อเสียที่แตกต่างกันไป โดยเกณฑ์จะขึ้นอยู่กับความชอบของผู้ใช้ และระบบ Linux ที่ใช้ ทำให้ไม่มีข้อสรุปว่า Tools ไหนดีที่สุด

## Introduction to Repository Setup

- ### Respository คืออะไร?
  Respository เป็นคลัง Package เวลาเราจะติดตั้งโปรแกรมอะไร ก็ไปดาวน์โหลด Package ของโปรแกรมนั้นๆ ตาม Respository ที่มันอยู่ ซึ่งโดยปกติแล้ว พวก Respository จะอยู่บน Internet เพื่อให้เครื่องที่สามารถเชื่อมต่อ Internet ได้ สามารถ Update Software ได้อย่างสม่ำเสมอ แต่บางครั้งการ Update ผ่าน Internet อาจจะเปลือง Traffic การทำ Local Respository ก็อาจจะตอบโจทย์มากกว่า ซึ่ง Package เหล่านี้ก็มีการแบ่ง ตาม Distribution ที่ใช้ด้วย เช่น ตระกูล Redhat/Fedora/SUSE จะใช้ไฟล์ .rpm แต่ถ้าเป็นตระกูล Debian/Ubuntu ก็จะใช้ไฟล์ .deb ซึ่งไม่สามารถใช้ร่วมกันได้ สามารถแบ่งได้หลักๆ 2 ประเภท
  - Official Repository
    จัดทำโดยผู้พัฒนาหรือผู้จัดจำหน่าย Linux ผ่านการทดสอบ และมีความเสถียรสูง
  - Unofficial Repository
    จัดทำโดยนักพัฒนาจากภายนอก มักมี Software Version ล่าสุด หรือ ซอฟต์แวร์ที่ไม่มีใน Repository ทาง Official
- ### ทำ Respository Setup ไปเพื่ออะไร?
  - **การจัดการ Software**
    - ทำให้สามารถ ติดตั้ง / อัปเดต / ลบ ได้สะดวกมากขึ้น โดยไม่ต้องดาวน์โหลดและคอมไพล์จากต้นทาง
    - ทำให้สามารถควบคุม Version ของ Software บนเครื่องได้
    - มั่นใจได้ว่าระบบสามารถทำงานได้อย่างสม่ำเสมอ และมีความปลอดภัย
    - ทำให้สามารถ Update Software เป็น Version ล่าสุด หรือ เลือกติดตั้ง Software ใน Version ที่ต้องการได้
  - **การแบ่งปัน Software**
    - ทำให้ผู้พัฒนา สามารถแบ่งปัน Software ของตนเอง ให้แก่ผู้อื่นได้อย่างง่ายดาย
    - ทำให้ผู้ใช้ สามารถค้นหาและติดตั้ง Open Source Software ได้สะดวกมากขึ้น
    - ทำให้ผู้ใช้ สามารถสร้างและใช้งาน Software ภายในองค์กร ได้อย่างมีประสิทธิภาพ
  - **การสำรองข้อมูล**
    - สำรอง Data และ Settings ต่างๆได้สะดวกมากขึ้น
    - กู้คืน Data และ Settings ได้ง่าย
    - จัดการ ควบคุม การสำรองและกู้คืน Data ได้อย่างมีประสิทธิภาพ

## Referenecs

### Mainpage

- https://feversecure.wordpress.com/2017/10/18/วิธีใช้-apt-get-บน-linux-ฉบับง่ายๆ/#:~:text=*แพ็คเกจ%20(package)%20ใน%20Linux,สำหรับหา%20packages%20ใหม่ๆ
- https://suchart.wordpress.com/debianubuntu-package-management/
- https://bard.google.com/chat/3cc46de7841e2fc6
- https://jetsadamalaisirirat.medium.com/การทำ-local-repository-สำหรับ-redhat-centos-ece9c4545960
- https://bigta.wordpress.com/2011/04/30/installing-program-in-linux/

## Members

| ID       | Name                       | Role                                  | pic|
| -------- | -------------------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 65070193 | นาย ยงยุทธ ชาณุภาต         | dpkg                                  | ![alt text](https://scontent.fbkk2-7.fna.fbcdn.net/v/t1.15752-9/426808601_753551526736661_4821947487512836668_n.jpg?_nc_cat=111&ccb=1-7&_nc_sid=8cd0a2&_nc_eui2=AeES0e984_5b6rWnX3AXwP-RmwpGCNtqx32bCkYI22rHfbJtvY_nvCjWPoIqnu_gzfGuWLQkpxBbO8CVDqoIrIK4&_nc_ohc=T-xX3H_b608AX-SV4oC&_nc_ht=scontent.fbkk2-7.fna&cb_e2o_trans=t&oh=03_AdSSoUsv6B8UtGfemj1h12vzoLX0F3Nb_8xo67L5ZKf8Aw&oe=65F0592D)|
| 65070201 | นาย วชิรวิชญ์ นกเล็ก       | Repository setup using apt            | ![most handsome guy](https://media.discordapp.net/attachments/981114077411696680/1206266588865634335/inbound9210442700284694057_1.jpg?ex=65db624e&is=65c8ed4e&hm=68ce81bd09055bded98015a6cb4f9f56b0ff023de4a75de5a0bba363668acd03&=&format=webp&width=497&height=671) |
| 65070233 | นาย สหัสวรรษ วงศ์บุญธเนธ   | apt และ apt-get                       | ![image](https://github.com/WHY2BX/PackageManagement-3/assets/117964233/af4e8b72-ab4c-4022-919a-1aa87c77122b)|
| 65070236 | นาย สิรภพ ดรัณภพธนกูล      | zypper                                | ![alt text](https://scontent.fbkk2-7.fna.fbcdn.net/v/t1.15752-9/426483416_6729756173795016_7015428031258575924_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=8cd0a2&_nc_eui2=AeHnud6WGanXIWe2re6RY17rtq4UJt9In_q2rhQm30if-tRWWjFIxXJFZjXMKmrxpTehaf1ZPEwcrTgrp9qYxgE5&_nc_ohc=nVgQw7Qpz6QAX90farz&_nc_oc=AQmqR8L04Zi_AU8BB3RLg-wjUhMeive5PbTYeJgtC8xD3quGQ3m4EP4UIxK_ofOpX3c&_nc_ht=scontent.fbkk2-7.fna&cb_e2o_trans=t&oh=03_AdT35nxNeIf10bodo58uZq5fwYmyThPaybRYTr93KxncTQ&oe=65F05340)|
| 65070238 | น.ส.สิริมงคล ทองขวัญใจ     | rpm                                   | ![alt text](https://media.discordapp.net/attachments/998863837400932373/1205912829966684240/1707517924173.jpg?ex=65da18d7&is=65c7a3d7&hm=5d0bcb255d0a8d1c8d134b5a8f5fda9aed2b3f01a18c264ae283dbfd0227731f&=&format=webp)|
| 65070239 | น.ส.สุชานันท์ อุ่นหมั่นกิจ | yum                                   | ![alt text](https://scontent.xx.fbcdn.net/v/t1.15752-9/405013974_373489541963217_5665276776927551710_n.jpg?stp=dst-jpg_s206x206&_nc_cat=107&ccb=1-7&_nc_sid=510075&_nc_eui2=AeEBJICt4xHlw3wzlf5Crf_mdyQyLveLh-93JDIu94uH76aSdnlDUbj-gooz1SupXek0Wy_y69Wm7jp7d8c5LABN&_nc_ohc=xSmOpJNCCRUAX8XJG99&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdSz0sWMdWWK1EDR7sb0_ouQZ5xFhPLvAuVxEk0rmIArQQ&oe=65EEDADC) |
| 65070241 | น.ส.สุพิชชา วิเศษเจริญ     | Mainpage & Repository setup using yum | ![alt text](https://media.discordapp.net/attachments/998863837400932373/1206104986941919352/image.png?ex=65dacbcd&is=65c856cd&hm=83546b5ee15201064614db0779590b1d79bee6c638b3a03b8b18f6bc7d74a6b3&=&format=webp&quality=lossless)
