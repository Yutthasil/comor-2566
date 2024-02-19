# Chapter 5 Working With Text
การทำงานกับข้อความในlinux เกี่ยวข้องกับการจัดข้อมูลเพื่อเอาข้อมูลมาใช้หรือแปลงเป็นเอาต์พุตที่ต้องการ ในlinuxทุกอย่างถือว่าเป็นไฟล์รวมถึงข้อความด้วย การที่เรามีพื้นฐานการใช้คำสั่งต่างๆที่เกี่ยวกับการประมวลผลช้อความในlinuxทำให้ สามารถทำงานเสร็จได้และมีประสิทธิภาพอย่างมากและช่วยประหยัดเวลาในการแก้ไขปัญหาจากงานที่ยากและน่าเบื่อสามารถแก้ไขได้ภายในไม่กี่วินาที<br>
**Working with text ใน linux แบ่งได้หลากหลายประเภทเช่น**<br>
## Working With Text In Linux<br>
**1. การจัดการไฟล์**<br>
การจัดการไฟล์ในLinuxหัวใจสำคัญในการใช้งานระบบ
การจัดการไฟล์ในระบบปฏิบัติการ Linux นั้นหมายถึงกระบวนการควบคุมดูแลและจัดระเบียบไฟล์ข้อมูลโปรแกรมบนระบบLinuxเปรียบเสมือนกุญแจสำคัญที่ช่วยให้ผู้ใช้สามารถใช้งานระบบได้อย่างมีประสิทธิภาพปลอดภัยและสะดวก<br>
* การสร้างและลบไฟล์<br>
* การอ่านและเขียนเนื่อหาในไฟล์<br>
* การค้นหาข้อความในไฟล์<br>
* การแก้ไขไฟล์<br>

**2. การแปลงข้อความ**<br>
แปลงข้อความในlinuxมีความจำเป็นอย่างมาก เพราะหลังจากที่เราได้ทำการแก้ไขแล้วอาจจะมีข้อผิดพลาด/บกพร่องบางอย่าง คำสั่งการแปลงข้อความใน linux จึงมีความสำคัญไม่แพ้กับการแก้ไขไฟล์ เพื่อช่วยในการ format ไฟล์ให้อยู่ในกรอบที่เราวางเอาไว้
เช่น ถ้าเราพิมตัวอักษรในไฟล เป็น ภาษาอังกฤษ ตัวพิมเล็ก แต่เราดันเปลี่ยนใจ อยากได้ ไฟล ตัวพิมใหญ่ทั้งหมด เราก้สามารถใช้ คำสั่งแปลงข้อความของlinux ในการแก้ปัญหาแทนการไปนั้ง ใช้ vim แก้ไข ข้อความทั้งหมดได้ โดยใช้แค่ คำสั่ง tr เดียวเรามาเรียนรู้
ประเภทต่างๆของการแปลงข้อความในlinux กันนะงับผม<br>
* การแปลงรูปแบบตัวอักษร<br>
* การแปลงรูปแบบไฟล์<br>

**3. การกรองข้อความ**<br>
การกรองข้อความในlinux คือการที่เราอยากได้ข้อความแค่บางส่วนที่ต้องการ และละทิ้งส่วนที่เราไม่ต้องการออก อย่างเช่น อยากได้แค่ 3บรรทัดบนสุด ใช้head อยากได้ 3บรรทัดล่างสุดเราใช้ tail ก็คิอกรองข้อความเพิ่อให้เราไม่ต้องไปหาจากในไฟลเองซึ่งลดความยุ่งยากได้มากเลย<br>
* การกรองตามเงื่อนไข<br>
* การเรียงลำดับข้อความ<br>





### การจัดการไฟล์(Managing File)
อย่างที่กล่าวไปการจัดการไฟล์มีบทบาทเกี่ยวกับการเข้าถึงข้อมูล จัดระเบียบข้อมูล จัดการพิ้นที่สำหรับเก็บข้อมูล สำรองข้อมูล รวมๆแล้วเน้นไปทางสร้างข้อมูลเพื่อนำมาใช้ต่อในภายภาคหน้าได้<br>
เรามาเรียนรู้พื้นฐานเกี่ยวกับ การการสร้างและลบไฟล์ ในlinuxกันดีกว่า<br>
**1. เริ่มต้นด้วยการสร้างไฟล**
ก่อนที่จะสร้างไฟล์เราต้องรู้ก่อนว่าตอนนี้เราอยู่ที่ไหนในระบบ<br>
**PWD**<br>
ใช้ Command `PWD`<br>
```
PWD
```
หลังใช้จะบอกว่าเราอยุ่ ณ จุดใดในระบบ<br>
**MKDIR**<br>
Command การ สร้างfolder/directory แรก `mkdir`<br>
ใช้ `mkdir` ตามด้วยชื่อdirectoryที่อยากตั้้ง
ตัวอย่างเช่น<br>
```
 mkdir popo1
```
จะเป็นการสร้าง directory ชื่อ popo1 มา
หากเราใช้คำสั่ง ls ดู Directory ในไฟล์นั้นๆจะพบว่า directory ได้ถูกสร้างขึ้นแล้ว
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/a6b39d8d-6b41-4c3c-9e26-bf450a2f04a5)<br>
**Trick เลฺ็กๆน้อยๆ**<br>
เราสามารถสร้างdirectoryได้ หลายๆอันในทีเดียวเช่นกันเช่น
```
mkdir popo1 popo2 popo3
```
เราได้จะได้ไม่ต้องพิมหลายๆรอบเสียเวลา<br>
แต่หากเรามีไฟล์ชื่อนั้นอยู่แล้ว คำสั่งจะข้ามไป สร้างDirectory อันที่เหลือเลย<br>
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/0a259530-2d95-42ec-9012-34c35bd56369)<br>
หากเราต้องการสร้าง Directory ซ้อนใน Directory อีกทีนึง เราสามารถ ใช้ `/` ในการ เจาะลึกลงไปได้เช่น<br>
```
mkdir popo1/popoinside/popoinsideinsidee
```
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/170e2357-07ed-43e5-9fe8-65b8ccd64328)<br>
จะเห็นได้ว่า ข้างใน `popo4` จะมี directory `popoinside` และ `popoinside` จะมี Directory `popoinsidee` อีกทีนึง<br>
**มาถึงการลบ กันบ้าง**<br>
ถ้าตอนไหนเราอยากลบDirectoryใน linux เราสามารถใช้คำสั่ง `rm -r`ในการลบได้ หรือ`rmdir` <br>
ตัวอย่าง<br>
```
rm -r popo1
```
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/1b1197c4-f72a-4fe7-b0b2-83fd4a631dbc)<br>
จากที่มี Directory popo1ก็จะหายไป<br>
หากต้องการลบ Directory ที่ว่างเปล่าไม่มีอะไรข้างในใช้ `rm -d`<br>
ตัวอย่าง<br>
ณ ตอนนี้เรามีDirectory เหลือ 4 อัน nopbys popo2 popo3 popo4<br>
ใช้คำสั่ง<br>
```
rm -d popo4
```
จะเห็นได้ว่า จะไม่สามารถลบได้เพราะข้างใน popo4 ยังมี content ข้างในอยุ่ นั้นก็คือ popoinside<br>
แต่ถ้าใช้คำสั่ง<br>
```
rm -d popo2
```
จะลบ Directory ได้ทันที<br>
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/e8bb8f37-749a-4c0d-80da-3145efc9ac7a)<br>
**ข้อควรระวัง**<br>
การลบนั้นถ้าเราลบแล้วอาจจะหายไปเลยแต่มีคำสั่งนึงช่วย ย่นการลบให้อีกstep ทำให้ เวลาเราเผลอลบอันไหนแล้วเราใส่คำสั่งนี้ไปมันจะให้เรายืนยันก่อนที่จะลบจะได้ไตร่ตรอง ว่าเราจะลบอันนี้แน่ๆใช้ไหม นั้นก็คือคำสั่ง<br>
`-vi`<br>
มันจะยืนยันก่อนว่าเราจะลบจริงๆใช้ไหม พิม y เพื่อ yes พืม n เพื่อ No<br>
**การสร้างไฟล์เปล่าๆ**<br>
ง่ายๆเราใช่คำสั่ง `touch` ตามด้วยชื่อไฟล์ เพื่อสร้างไฟล์<br>
ยกตัวอย่าง<br>
```
touch gumball
```
จะได้ไฟล์ชื่อ gumball แบบในรูปเลย<br>
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/1377ace3-0fc5-4aac-b945-2250694ace9e)<br>
**การลบไฟล์**<br>
ลบง่ายมาแค่ใช้คำสั่ง rm ตามด้วยชื่อไฟล์จะลบทันที เช่น เราอยากลบ gumball เราใช้คำสั่ง<br>
```
rm gumball
```
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/b2c83a57-57d3-40fb-a0a9-17935260926e)<br>

**2. มาต่อกันที่การอ่านและเขียนเนื้อหาไฟล์**<br>
หลังจากที่ได้เรียนรู้การสร้างไฟล์ และ Directoryแล้วเราต้องเรียนรู้ในการเอาข้อมูลมาใส่ในไฟล์ด้วยเพื่อการนำไปใช่ประโยนชน์ที่หลากหลายมากขึ้น<br>
มาเรียนรู้คำสั่ง `echo` กัน<br>
**Echo**<br>
`echo` เป็นคำสั่งที่จะแสดงผลผ่านTerminal ตาม inputที่เราใส่ไป<br>
ตัวอย่างเช่น<br>
echo คำว่า Hi user ใช้คำสั่ง<br>
```
echo Hi user
```
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/0e5f1b8d-2586-4b02-8781-3ffc1ae082b1)<br>
สามารถใส่ลูกเล่นได้หลายๆแบบแต่ ต้องเติม-e หลัง echo <br>
ตัวอย่างลูกเล่น echo<br>
\n = ขึ้นบรรทัดใหม่<br>
\t = whitespace<br>
\r = ไม่เอาตัวก่อนหน้า\r<br>
\b = จะไม่มีwhitespaceตรงที่พิม<br>
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/710572bf-b4ae-480a-84c9-0412e898a0c5)<br>
เอาแค้นี้ก่อนดีกว่าจริงๆมีลูกเล่นอีกเยอะนะ<br>
และก็ไหนๆเราก็มีไฟลเปล่าๆแล้วเราสามารถ ยัดข้อความที่ echo ใส่ในไฟล์ได้ ไฟล์เราจะได้ไม่เป็นไฟล์เปล่าอีกต่อไปเย้<br>
ใช้คำสั่ง echo "_____" > ชื่อไฟล์.txt เป็นการเขียนทับข้อความลงไฟล์นั้นๆไปเลย<br>
```
echo "Hello My Name Is ZUZIE" > text.txt
```
ตอนนี้ไฟล์ text.txt ก็มีข้อความข้างในว่า "Hello My Name Is ZUZIE" แล้วแต่เราจะดูยังไง เราเลยต้องมีคำสั่ง Catมาช่วยนั่นเอง<br>
**Cat**<br>
ใช้คำสั่ง `cat` ตามด้วยชื่อไฟล์ จะเป็นการแสดงแสดงข้อความข้างในไฟล์ออกมาทางTerminal คล้ายๆกับ echo แต่ต้องเลิอกไฟล์<br>
```
cat text.txt
```
จะได้outputว่า<br>
```
Hello My Name Is Zuzie
```
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/d857bf52-0a89-4eb8-b6be-e32dee718c38)

**3. การค้นหาข้อความในไฟล์**<br>
การที่เรามีข้อมูลแล้วแต่ว่าบางทีนั้นเราต้องการข้อมูลในจุดๆนึงซั่งบางทีข้อมูลมันเยอะเกินทำให้เราอาจจะต้องเสียเวลาในการเลื่อนหาจะ linux เลยมีตัวช่วยในการหาข้อมูลหรือข้อความในไฟล์เพือความสะดวกสะบาย<br>
**GREP**<br>
คำสั่ง grep เอาไว้ใช้หาคำเฉพาะเจาะจงในบรรทัดตามที่เราต้องการ<br>
```
grep "คำที่ต้องการค้นหา" ไฟล์ที่เราต้องการค้นหา
```
เช่น เราจะหา Error ในไฟล์ log.txt เราก็ใช้คำสั่ง grep "error" log.txt<br>
Output(สมมุติ)<br>
```
1:2023-11-16 14:23:54 ERROR: Connection Failed.
2:2023-11-16 14:24:01 ERROR: File not found.
```
สามารถใส่ option ในการหาได้ด้วยเช่น<br>
```
grep <option> <word> <filename>
```
-i = ไม่สนพิมเล็กพิมใหญ่<br>
-v = แสดงoutput ที่ไม่ได้อยู่ในคำที่เราหา<br>
-c = นับจำนวนบรรทัดที่เข้าเงื่อนไข<br>
-h = แสดงบรรทัดที่เข้าเงื่อนไขแต่ไม่ระบุชื่อไฟล์<br>
-n = แสดงบรรทัดที่เข้าเงื่อนไขกับ จำนวนบรรทัดที่เข้าเงื่อนไข<br>
-w = แสดงบรรทัดที่ตรงกับ คำที่หาแบบเป็ะๆ<br>

**4. การแก้ไขไฟลฺ์**<br>
การแก้ไขไฟล์นั้นเป็นสิ้งจำเป็นการที่เราใช้ echo บันทึกทับไฟล์อาจจะยังไม่ตอบโจทย์สำหรับการทำงานกับข้อความต่างๆดังนั้นlinuxจึงมีอุปกรณ์มาเพิ่อทำหน้าที่่แก้ไข บันทึกไฟลฺ์ได้<br>
ซึ่งในตัวอย่างนี้จะแนะนำText Editer 2ตัวก่อน นั้นก็คือ<br>
* Nano
* VIM
##### Nano คืออะไร
nano คือคำสั่ง ilnux มีความสามารถ ในการแก้ไขและบันทึกไฟลได้แต่เมื่อเทียบกับVIMแล้ว nano ยังไม่มีความสามารถเพียงพอที่จะเทียบเท่าแต่ในความใช่งานง่ายถิอว่าเป็น Text Editor ที่เข้าใจได้ง่ายและนำมาใช้งานได้ง่านเลย<br>
**คำสั่งต่างๆใน nano**<br>
การเรียกใช้ nano ใช้คำสั่ง<br>
nano ชื่อไฟล์ที่ต้องการแก้ไข<br>
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/1872d3b4-3432-45f3-90a6-5e192666a8cd)<br>

* Ctrl + G	เปิด help<br>
* Ctrl + X	ปิดโปรแกรม<br>
* Ctrl + O	เซฟข้อมูล<br>
* Ctrl + R	เอาไฟล์อื่่นมาแทรกในไฟล์<br>
* Ctrl + W	ค้นหาคำ<br>
* Ctrl + A	เคอร์เซอไปยังซ้ายสุดบรรทัดนั้นๆ<br>
* Ctrl + E	เคอร์เซอไปยังขวาสุดบรรทัดนั้นๆ<br>
* Ctrl + Y	เลือนเคอร์เซอร์ไปหน้าถัดไป 1 หน้า<br>
* Ctrl + V	เลือนเคอร์เซอร์ไปหน้าก่อนหน้า 1 หน้า<br>
* Ctrl + K	ทำการ Cut ข้อมูลแล้วเกบไว้รอpasteได้<br>
* Ctrl + D	ลบตัวอักษร<br>
* Ctrl + \	ค้นหาและแทนที่ด้วยคำที่ต้องการ<br>
* Ctrl + C	แสดงจุดที่เราอยู่<br>
* Ctrl + ^	คล้ายๆการลากคำพูด แต่มันจะcopyไว้<br>
* Ctrl + U	Paste คำที่เราได้Copy ไว้<br>
**ข้อดีของ Nano**<br>
* ใช้งานง่าย<br>
* เรียนรู้คำสั่งแปปเดียว<br>

**ข้อเสียของ Nano**<br>
*ช้ากว่าVIM<br>
*จำกัดความสามารถในการปรับแต่ง<br>
*ทำงานผ่านCommand Line ไม่ได้<br>

##### VIM(Vi improve) คืออะไร<br>
Vim คือ Text Editer คล้ายๆ nanoเลยแต่จะมีความซับซ้อนกว่า nano พอสมควร vim สนับสนุนการเขียนscript เป็นสิ่งจำเป็นที่ต้องเรียนรู้ถ้าจะ เล่นกับตัวอักษรในLinux<br>
**คำสั่งต่างๆในVim**<br>
การเรียกใช้คำสั่ง vi<br>
![image](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/assets/118421368/54612c2a-6270-401b-9f53-44bfd39c1f1c)<br>

Vim มี 2 Mode<br>
* Insert Mode<br>
* Command Mode<br>
**Insert Mode**<br>
i เพื่อเข้าสู่ Insert Mode จากนั้นพิมตามใจได้เลย

**Command Mode**<br>
esc เพื่อเข้าสู่Command Mode<br>
* x = ลบอักษรที่ไม่ตเองการ<br>
* u = ย้อนคำสั่งล่าสุด<br>
* U = ย้อนคำสั่งทั้งหมดในบรรทัด<br>
* A = เพิ่มข้อความที่จะต่อท้าย<br>
* :+w+q = เซฟ<br>
* :+q+! = Discard การเปลี่ยนแปลงทั้งหมด<br>
* dw = ย้ายเคอร์เซอร์ไปจุดเรื้มต้นเพ่อเปลยี่นคำ<br>
* 2w = ย้ายเคอร์เซอร์ถัดไปสองคำ<br>
* 3e = ย้ายไปจุดสุดท้ายของสามคำข้างหน้า<br>
* 0 = ไปยังจุดเริ่มต้นของบรรทัด<br>
* ctr+-+w = ไปยังอีกหน้าต่าง<br>
* R = เข้าสู่โหมดการแทนที่<br>
* v = เข้าสู่โหมดVisual Block<br>
* :+n = =ขยับไปบรรทัด n<br>
* yy = copyบรรทัดที่อยู่<br>
* 3yy = copy3บรรทัด เลขข้างหน้าหมายถึงจำนวนบรรทัด<br>
* y$ = copy จากเคอร์เซอร์จนถึง บรรทัดสุดท้าย<br>
* y^ = copy จากเริ่มจนจบ<br>
* yiw = copy คำนั้นๆ<br>
* dd = ตัดบรรทักนั้นๆ<br>
* 3dd = ตัด3บรรทัดจากเคอร์เซอร์<br>
* d$ = ตัดทุกอย่างจาก ที่เคอร์เซอร์อยู่<br>
* P = paste ก่อนเคอร์เซอร์<br>
* p = paste หลังเคอเซอร์<br>
**ข้อดีของ VI**<br>
* ยืดหยุ่นและหลากหลาย<br>
* เสถียรมาก<br>
* มีโหมดCommand กับ Insert
* Community Support

**ข้อเสียของ VI**<br>
* ยากที่จะเข้าใจ<br>

### 2. การแปลงข้อความ
การแปลงข้อความจากรูปแบบหนึ่งไปเป็นอีกรูปแบบโดยใช้คำสั่ง linux<br>
**การแปลงรูปแบบตัวอักษร**
**`tr`** <br>
คำสั่ง tr ใช้ในการแปลงตัวอักษรภายในไฟล์ ให้เปลี้ยนไปตามข้อกำหนกของเรา<br>
```
tr [option] [set1]
```
ตัวอย่างการใช้ tr<br>
```
cat popo
```
output<br>
```
kmitl fight
```
เปลี่ยน ตัว kเล็กเป็นตัวใหญ้<br>
```
cat popo |tr 'k' 'K'
Kmitl fight
```
เปลี่ยน ตัวอักษรทั้งไฟล์ เป็นตัวใหญ่<br>
```
tr "[:lower:]" "[:upper:]" < popo
```
output<br>
```
KMITL FIGHT
```
คร่าวๆประมาณนี้ละกันนะ สำหรับคำสั่ง tr<br>

**Fold**<br>
คำสั่งFoldใช้เพื่ออกำหนดระยะความกว้างของบรรทัดตามใจของเรา<br>
```
fold [option] [file]
```
การจำกัดขนาดตัวอักษรต่อ1บรรทัด<br>
```
fold -w[จำนวนที่ต้องการ] [file]
```
การจำกัด byte ต่อบรรทัด<br>
```
fold-b[byteต่อบรรทัด] [file]
```
จำกัดจำนวนตามตัวอักษรและเกิดขึ้นเมื่อมี whitespace
```
fold -w[จำนวนบรรทัด] -s [file]
```

**การแปลงรูปแบบไฟล์**<br>
การแปลงรูปแบบไฟล์ช้วยในการเวลาที่เราค้องการใช้ ไฟล์หลากหลายประเภทเราจะได้สามารถแปลงไฟล์เป็นประเภทที่่เราต้องการ<br>
**pandoc**
สำหรับการแปลงไฟล์เอกสารเราใช้ pandoc ในการแปลงไฟลฺเอกสาร
```
pandoc math.tex -s --mathml  -o mathMathML.html<br>
```
จะแปลงไฟล์text เป็น HTML<br>

### 3. การกรองข้อความ<br>
การกรองข้อความคือการที่เราต้องการคำบางส่วนจากไฟล์จะได้ไม่ต้องหา<br>
**grep**<br>
คำสั่งgrep สามารถทำให้หาคำต่างๆได้โดยใส่คำที่ต้องการ ค้นหาหลังคำสั่ง<br>
```
grep female hospitalpoeple.txt
```
คำสั่งนี้จะทำการหา บรรทัดที่มีผู้หญิงในโรงพยาบาล<br>
**head**<br>
คำสั่ง head สามารถกรองเฉพาะบรรทักแรกๆของไฟล์นั้นๆได้ในกรณีข้อมูลมันเยอะเกินไป<br>
```
head [option] [file]
```
ตัวอยาง<br>
```
head -4 hospital.txt
```
เป็นการ แสดงข้อมูล 4 บรรทักแรกของไฟล์ hospital<br>
**tail**<br>
คำสั่งtail คล้ายๆ head แค่เปลี่ยนจากบรรทัดแรกๆเปลี่ยนเป็นบรรทัดหลังสุด<br>
```
tail [option] [file]
```
ตัวอย่าง<br>
```
tail -5 popo.txt<br>
```
แสดงข้อมูล5 บรรทัดสุดท้ายของไฟล์popo.txt<br>
**more**<br>
คำสั่งแสดงข้อความ โดยจะแสดงผลเป็นทีละหน้า<br>
```
more [option] [file]
```
จะแสดงข้อความทั้งหมดโดยใช้space bar ในการไปหน้าต่อไปและq เพื่อquit<br>
**ข้อควรระวัง**<br>
* กลับไปหน้าก่อนหน้าไม่ได้<br>
* ไม่มีฟังค์ชันค้นหา<br>

**less**<br>
คำสั่งแสดงข้อความ โดยจะแสดงผลเป็นทีบรรทัด<br>
```
less [option] [file]
```
จะแสดงข้อความโดยการใช้spacebarหรือpag down เพื่อลงอีกบรรทัด enter เพื่อกลับขึ้นข้างบน สามารถใช้/keyword หาคำได้<br>
**wc**<br>
คำสั่งการที่เราต้องการรู้ว่าไฟล์ฺนั้นๆมีกี่คำ กี่บรรทัด และกี่byte<br>
```
wc [option] [file]
```
optionต่างๆ ของ wc<br>
-c, --byte = นับจำนวน byte  ตัวอย่าง wc -c [File.log] <br>
-m, --chars = นับจำนวนตัวอักษรและอักขระ  ตัวอย่าง wc -m [File.log] <br>
-l, --line = นับจำนวนบรรทัด  ตัวอย่าง wc -l [File.log] <br>
-L, --max-line-length = นับจำนวนตัวอักษรและอักขระในแถวที่ยาวที่สุด  ตัวอย่าง wc -L [File.log] <br>
-w, --word = นับจำนวนคำในไฟล์ ตัวอย่าง wc -w [File.log] <br>






# Other Chapter
- 🛠 [**Introduction Monitoring and Logging Tools**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/README.md)
- 🛠 [**Chapter 1 Monitoring and Logging Tools**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%201/Readme.md)
- 📈 [**Chapter 2 Log Reader and Analysis**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%202/Readme.md)
- 📝 [**Chapter 3 Log Collection and Server**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%203/Readme.md)
- 📚 [**Chapter 4 Log Files**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%204/Readme.md)

# Source
- [Reference Working with Texts](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Reference/Chapter%205.md)