# Script

Script เป็นส่วนสำคัญสำหรับช่วยให้สามารถเขียนลำดับของคำสั่งในไฟล์แล้วสามารถดำเนิดการได้ ไม่ต้องเสียเวลาเพราะไม่จำเป็นต้องเขียนคำสั่งซ้ำไปซ้ำมาและสามารถกำหนดเวลาการทำงานได้ด้วย และ Script ยังมีให้เลือกหลาย Script เช่น Bash Script, Python Script, Perl Script, Shell Script และอื่นๆ เลือกใช้ตามงานที่เหมาะสม


### Shell Script

  เป็นโปรแกรม open-source ที่เป็นโปรแกรมสำหรับเขียนชุดคำสั่งเพื่อให้ shell ดำเนินการหน้าทที่ของมันมีหลายอย่างการรวมคำสั่งที่ยาวและคำสั่งที่ซ้ำกันให้เป็น Script เดียวกันทำให้เรียบง่ายต่อการจัดเก็บและสามารถดำเนินการได้ตลอดเวลาถ้ามีการเรียกใช้ ตัวอย่างการใช้งาน เช่น การสํารองข้อมูลไฟล์

### Shell มีให้เลือกใช้ 5 แบบ

  การเลือก shell ควรเลือกตามลักษณะของงาน เช่น ระบบปฎิบัติการอาจเลือกใช้ Shell บ้างประเภทไม่ได้
   <br>
   
   และมีให้เลือกใช้ดังนี้ :
   <br>
   
   - Bourne Shell
   - C shell
   - Bash shell
   - Bash shell
   - Korn shell
   - Z shell
   <br>

  <img src='https://i0.wp.com/saixiii.com/wp-content/uploads/2017/05/shell-kernel.png?resize=768%2C555&ssl=1' width='720' height='500'>

### Shell

  คือ ตัวที่ให้ interface กับผู้ใช้งานและยังรับคำสั่งจากผู้ใช้จากนั้นก็ดำเนินการคำสั่งและให้ผลลัพธ์ของโปรแกรมใน Shell Script

### Kernal

  เป็นส่วนที่เอาไว้สื่อสารกับ hardware และ software kernal มีหน้าที่จัดการทรัพยากรต่าง ในระบบคอมพิวเตอร์
    <br>  
    การทำงานมีส่วนประกอบหลัก 2 ส่วน :
    <br>
   
   - Kernel
   - Shell
   <br>

### วิธีการเขียน Shell Script

  1. สร้างไฟล์ Shell Script สามารถสร้างด้วย editor เช่น nano หรือ vi เป็นต้น วิธีการสร้าง $ vi ชื่อไฟล์.sh
      <br>
      
      ```bash
      vi hello.sh
      ```
  2. กำหนด shebang (`#!`) เพื่อระบุบตำแหน่งของ interpreter ที่ใช้ในการประมวลผลของ script อาจจะเลือกใช้เป็น ‘/bin/sh’ หรือ ‘/bin/bash’ ตามแต่จะเลือกใช้ เราจะเลือกใช้ ‘/bin/sh’ เพราะมั่นใจว่าจะสามารถใช้กับ Linux ได้ ก็จะเขียนดังนี้ ‘#! /bin/sh’ ซึ่งจะหมายถึงใช้ Bourne shell เป็น interpreter ในการประมวล คำสั่งใน Script และ คำสั่งจะถูกดำเนินการโดย Bourne shell ตามที่กำหนดใน shebang line นั้นก็คือ ‘/bin/sh’ นั้นเเอง
      <br>
      
      ```bash
      #!/bin/sh
      ```
  3. ใส่คำสั่ง การใส่คำสั่งสามารถใส่ได้ดังนี้ หลังการกำกหนด interpreter เรียบร้อยแล้วจากนั้นก็ทำการใส่ คำสั่งเข้าไป
      <br>
      
      ```bash
      #!/bin/sh
      ls #ในตัวอย่างนี้ใช้คำสั่ง ls
      ```
  4. การ execute คำสั่ง สามารถพิมพ์ bash ชื่อไฟล์.sh เพื่อ execute คำสั่งได้เลย ตัวอย่าง
      <br>
      
      ```bash
      bash hello.sh
      ```

### Shell Script มีคำสั่งหลายคำสั่ง

  เช่น สร้างตัวแปล การทำloop การรับค่า การcomment และการดำเนินการอื่นๆ ยกตัวอย่างการใช้บ้างคำสั่งดังนี้

  1. สร้างตัวแปล
      <br>
      
      ```bash
      #!/bin/sh
      variable ="Hello"
      echo $variable
      ```
      พอ execute คำสั่งก็จะแสดงคำว่า "Hello" ขึ้นมา

  2. การรับค่าจาก user
      <br>
      
      ```bash
      #!/bin/sh
      echo "what is your name?"
      read name
      echo "How do you do, $name?"
      read remark
      echo "I am $remark too!"
      ```
      โปรแกรมนี้ read จะรับค่าจาก user เก็บที่ name, remark และจากนั้นก็แสดงข้อความผ่านคำสั่ง echo

  3. comment
      <br>
      
      ```bash
      #!/bin/sh
      # sample comment
      pwd
      ```
      ใช้คำสั่ง pwd เพื่อทำcomment ส่วนของcomment คือ "# sample comment" และตัวข้อความนี้จะไม่ถูกนำมา execute เป็นเหมือนคำอธิบายใน โปรแกรมนั้นเฉยๆ

  4. Array
     <br>
     
      ```bash
      txt[0]="a"
      txt[1]="b"
      txt[2]="c"
      
      echo $txt[0] $txt[1] $txt[2]
      echo ${txt[0]} ${txt[1]} ${txt[2]}
      ```
      การแสดง array จำเป็นต้องใช้ "{}" เพื่อที่จะดึงค่าใน array จากนั้นก็กำหนดค่า array ใน "[]" เริ่มตัวแรกคือ 0 ถ้าไม่ใส่ "{}" ค่าจะออกมาแค่ตัวแรก

  5. เงื่อนไข
     <br>
      
      ```bash
      #!/bin/bash
      
      if [ เงื่อนไข ]
      then
       commands
      else
       commands
      fi
      ```
      การใช้ เงื่อนไขจะถูกกำหนดใน "[]" หลัง if ถ้าเงื่อนไขถูกก็จะดำเนินงานหรือคำสั่งหลัง then เราสามารถกำหนดอื่นเมื่อเงื่อนไขใน if ไม่ถูกต้อง เราอาจจะใช้คำสั่ง elif[เงื่อนไขที่กำหนด] หรือ else เมื่อ if ถูกต้องก็จะมาลงเงื่อนไขนี้ทั้งหมด หรือ อาจจะใส่แค่ if ก็ได้ จากนั้นปิดคำสั่งด้วย fi

  5. loop while
     <br>
      
      ```bash
      #!/bin/bash

      while [ เงื่อนไข ]
      do
         commands
          ………….
      done
      ```
      ตัวอย่าง
      <br>
      
      ```bash
      #!/bin/bash

      num=1

      while [ $num -le 10 ]
      do
       echo "Loop $num"
       ((num = $num+1))
      done
      ```
      ในตัวอย่างนี้ ในเงื่อนไขจะเห็น -le มันคือการเปรียบเทียบค่าเงื่อนไขก็จะหมายความว่า num ต้องมีค่าน้อยกว่าหรือเท่ากับ 10 ในขณะที่ num ยังน้อยกว่าและเท่ากับ 10 โปรแกรมก็ยัง loop ต่อไป หลัง do คือคำสั่งที่ดำเนินการใน loop หลัง done ก็คือออกจาก loop แล้ว 
 
และยังมีคำสั่งอื่นๆอีกที่สามารถใช้ใน shell scriptได้

# Reference

- Shell Script
  - [Shell Script คืออะไร](https://www.coursera.org/articles/what-is-shell-scripting)
  - [Kernal คืออะไร](https://www.geeksforgeeks.org/introduction-linux-shell-shell-scripting/)
  - [วิธีการสร้าง Shell Script เบื่องต้น](https://www.guru99.com/introduction-to-shell-scripting.html)
  - [คำสั่งใน Shell Script เบื่องต้น](https://saixiii.com/basic-shell-script/)
