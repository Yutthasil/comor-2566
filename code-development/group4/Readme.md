
 Computer Organization and Operating System Assignment (Chapter: Code Development, Sec:3 )
---

# Introduction to Code Development
สวัสดีผู้ที่เข้ามาอ่านรายงานนี้ รายงานนี้จะพาคนที่เข้ามาอ่านได้มาเรียนรู้เกี่ยวกับ Code Development เบื่องต้น บนระบบประฏิบัติการlinux โดยจะมีการกล่าวถึงการทำงานต่างๆ เช่น scripting, degubber, devtool,shell scripting เป็นต้นโดยในแต่ละหัวข้อจะกล่าวถึงหลักการทำงานต่างๆ โดยรายงานนี้หวังว่าผู้ที่เข้ามาอ่านจะได้ความรู้ไปไม่มากก็น้อย ผิดพลาดประการใดขออภัยณที่นี้ด้วย

## Overview
---

 สำหรับผู้ที่เข้ามาอ่ายงานนี้ คงจะรู้จัก shell script หริอคนที่ไม่รู้จักสามารถมาทำความเข้าใจได้ shell script คิอ การทำงานในรูปแบบของcommand line interceptor โดยผ่าน shell โดย shell ถือได้ว่าเป็นภาษาprogramming ชนิดหนึ่ง

 ทำไมเราถึงต้องรู้จัก shell scripในการใช้งานlinux หรือ unix เพราะจะสามารถทำให้ตัวผู้ใช้สามารถทำงานร่วมกับระบบปฏิบัติการได้อย่างมีประสิทธิ์ภาพ เช่น การจัดการไฟล์ การควบคุมกระบวนการทำงาน เข้าใจการติดต่อสื่อสาร ระหว่างผู้ใช้กับโปรแกรม และเข้าใจการทำงานระหว่างโปรแกรมกับ hardwareต่างๆ

## Subcomponent
---

* Scripting คือ script ที่ใช้บน linux ได้แก่ shell script
* Interpreter คือ โปรแกรมที่ทำหน้าที่ประมวลผล code หรือ script ที่ละคำสั่งไปตามลำดับโดยไม่จำเป็นต้อง compile ทั้งหมด
* compiler คือ โปรแกรมที่ทำหน้าที่ประมวลผล code จากภาษาโปรแกรมให้คอมพิวเตอร์เข้าใจและสามารถรันได้
* Debugger คือ เครื่องมือที่ช่วยในการหาข้อผิดพลาดในขึ้นตอนการพัมนาโปรแกรม
* Devtools คือ เครื่องมือที่ช่วยให้ผู้พัฒนาสามารถพัฒนาโปรแกรมได้อย่างมีประสิทธิ์ภาพ และประหยัดเวลาได้มากขึ้น
* Web Dev Toolคือ เครื่องมือที่ช่วยในการพัฒนาเว็บบน linux 

## Constibuter
| รหัสนักศึกษา   |      ชื่อ-นามสกุล      |  รับผิดชอบ |
|----------|:-------------:|------:|
| 61070086 |   ธัญเทพ อินรุ่ง | script, interpreter, compilers |
| 62070212 |    เสฏฐนันท์ จงเจตน์ดี   | debug, devtools, web Development Tools |
