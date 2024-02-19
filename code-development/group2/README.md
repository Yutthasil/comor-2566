# Code-Development-2 #
### Computer Organization and Operating System Assignment (Chapter: Code Devepment, Sec: 2) ###

## Introduction to Code Development ##
รายงานนี้เป็นส่วนหนึ่งของวิชา COMPUTER ORGANIZATION AND OPERATING SYSTEM ซึ่งรายงานนี้จะแสดงเนื้อหาหัวข้อชื่อ Code Development เบื้องต้นครับ
รายงานนี้จะช่วยให้พวกเราได้เรียนรู้เกี่ยวกับ Code Development และส่วนประกอบภายใน Code Development เช่น Scripting, Interpeter, Compiler ฯลฯ
พวกเราหวังว่าอาจารย์ และ เพื่อน ๆ ทุกท่านได้เข้าใจมากขึ้น หลังจากที่ได้อ่านและศึกษาจากรายงานของพวกเราครับ

## Components Overview ##
"Code development in Linux" หมายถึงการพัฒนาโค้ดโปรแกรมที่เกี่ยวข้องกับระบบปฏิบัติการ Linux หรือการสร้างโปรแกรมที่ทำงานบนแพลตฟอร์ม Linux โดยโค้ดที่พัฒนาขึ้นมานั้นอาจเป็นทั้งโปรแกรมเชิงกราฟิก (GUI) และโปรแกรมเชิงคำสั่ง (Command-line) ที่ใช้งานผ่าน Terminal ของ Linux <br>

การพัฒนาโค้ดใน Linux สามารถทำได้โดยใช้ภาษาโปรแกรมต่างๆ เช่น C, C++, Python, Java, JavaScript เป็นต้น นอกจากนี้ยังมีเครื่องมือพัฒนาซอฟต์แวร์ (Software Development Tools) ที่มีคุณสมบัติที่ต่างกัน ซึ่งช่วยให้นักพัฒนาสามารถพัฒนาและทดสอบโค้ดได้อย่างมีประสิทธิภาพ <br>

นอกจากนี้ Linux ยังมีคุณสมบัติและเครื่องมือต่างๆ ที่ช่วยในการพัฒนาซอฟต์แวร์อย่างมีประสิทธิภาพ เช่น การใช้งาน Command Line Interface (CLI) ที่มีเครื่องมือเช่น gcc, g++, make, cmake, git ซึ่งช่วยในการคอมไพล์และสร้างโปรแกรม การจัดการระบบเวอร์ชัน (Version Control Systems) เช่น Git เพื่อการจัดการโค้ดและการทำงานร่วมกันในทีม และยังมี IDE (Integrated Development Environment) ที่รองรับการพัฒนาโปรแกรมบน Linux ได้อย่างมีประสิทธิภาพ เช่น Visual Studio Code, JetBrains IntelliJ IDEA, และอื่นๆ อีกมากมาย<br>
ดังนั้น "Code development in Linux" หมายถึงการพัฒนาโปรแกรมบนระบบปฏิบัติการ Linux โดยใช้เครื่องมือและเทคโนโลยีต่างๆ ที่ใช้งานได้อย่างมีประสิทธิภาพบนแพลตฟอร์มนี้

## Subcomponents Overview ##
<p>
  <b>1. Scripting (สคริปต์): </b> การพัฒนาโค้ดด้วยสคริปต์เป็นวิธีที่ได้รับความนิยมมากใน Linux สคริปต์มักถูกใช้ในการทำงานระดับระบบ, การทำงานกับไฟล์และเครือข่าย, การทำงานบนเซิร์ฟเวอร์, และการทำงานระหว่างโปรแกรมต่างๆ
</p>
<p>
  <b>2. Interpreter (ตัวแปลภาษา): </b> Linux มี Interpreter ที่มากมายที่นิยมใช้ แบ่งแยกตามภาษาโปรแกรมที่ใช้ เช่น Python Interpreter, Ruby Interpreter, Perl Interpreter เป็นต้น
</p>
<p>
  <b>3. Compiler (คอมไพเลอร์): </b> คอมไพเลอร์ใช้สำหรับแปลงโค้ดจากภาษาโปรแกรมให้กลายเป็นรหัสเครื่อง ซึ่งใน Linux มี Compiler ต่างๆ เช่น GCC (GNU Compiler Collection) สำหรับภาษา C/C++, LLVM/Clang Compiler เป็นต้น
</p>
<p>
  <b>4. Debugger (เครื่องมือตรวจสอบโค้ด): </b> เครื่องมือ Debugging ช่วยในการตรวจสอบและแก้ไขข้อผิดพลาดในโค้ด โดย Linux มี Debugger ต่างๆ เช่น GDB (GNU Debugger), Valgrind, LLDB เป็นต้น
</p>
<p>
  <b>5. DevTool (Development Tools): </b> มักใช้สำหรับพัฒนาและจัดการโค้ด มี IDE หรือ Text Editors ที่นิยมใช้ใน Linux เช่น Visual Studio Code, Sublime Text, Emacs, Vim เป็นต้น
</p>
<p>
  <b>6. Web Development Tools: </b> (เครื่องมือพัฒนาเว็บ): สำหรับการพัฒนาเว็บไซต์ นอกจาก Text Editors และ IDE ที่ใช้สำหรับการเขียนโค้ด HTML, CSS, และ JavaScript แล้ว ยังมีเครื่องมืออื่นๆ เช่น Frameworks (React, Angular, Vue.js), CSS Preprocessors (Sass, Less), และ Web Browsers with Developer Tools (Chrome DevTools, Firefox Developer Tools) เป็นต้น
</p>

## Constibuter ##
รหัสนักศึกษา | ชื่อ & นามสกุล | ส่วนที่รับผิดชอบ | ภาพสมาชิก
-------- | -------------------- | ------------ | ----------
65070023 |  นางสาว กุลนันท์ สุนันท์	 | Scripting      | <img width=170 src="https://github.com/Chinjuku/Code-Development-2/blob/main/image/nornor%20(3).jpg"> |
65070052 | นายชินาธิป หวู | บทคัดย่อ, Scripting, DevTools | <img width=170 src="https://github.com/Chinjuku/Code-Development-2/blob/main/image/chinjung.png" />
65070053 |	นางสาว ชุติกาญจน์  ใจคง |	Debugger  | <img width=170 src="https://github.com/Chinjuku/Code-Development-2/blob/main/image/chaaim.jpg">
65070062 |	นาย ณภัทร  มากสมบูรณ์	| Interpreter   |<img width=170 src="https://github.com/Chinjuku/Code-Development-2/blob/main/image/ton.jpg">
65070069 |	นางสาว ณัฐชา  ฤทธิ์คำรพ	| Web Dev Tool | <img width=170 src="https://github.com/Chinjuku/Code-Development-2/blob/main/image/bambam.jpg">
65070084 |	นาย ณัฐวัตร  จันโท	    | Compiler   |<img width=170 src="https://github.com/Chinjuku/Code-Development-2/blob/main/image/gun.png">
65070243 |	นาย สุเมธา  ปานกลาง    | DevTools   |<img width=170 src="https://github.com/Chinjuku/Code-Development-2/blob/main/image/mek.jpg">

## Tools
- Github
- Github Desktop : push & pull file
- Visual Studio Code : แก้ไขไฟล์ README.md


