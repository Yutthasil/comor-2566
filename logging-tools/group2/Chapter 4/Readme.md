# Chapter 4 Log files
# log files คืออะไร
ก่อนจะเข้าถึงบทบาทของ log files ในระบบของ linux เรามาทำความเข้าใจเกี่ยวกับ log files ก่อนว่ามันคืออะไร มีประโยชน์ด้านใดบ้าง

**log files** ในที่นี้เปรียบเสมือนสมุดจดบันทึกกิจกรรมต่างๆที่เกิดขึ้นภายในระบบของคอมพิวเตอร์ การติดต่อสื่อสารที่เกิดขึ้นในระบบคอมพิวเตอร์ แสดงถึงต้นทาง, ปลายทาง, เส้นทาง, เวลา, วันที่, ปริมาณ หรืออื่นๆ ถูกบันทึกไว้ใน log files ตามที่กล่าวไปจะเห็นได้เลยว่า log files ทำให้การใช้งานบน internet รู้ว่าต้นสายปลายทางเป็นใคร ทำให้สามารถระบุตัวตนของผู้ใช้งานได้ 

ยกตัวอย่างเพิ่มเติมในการใช้ log files เมื่อมีเทคโนโลยีที่ก้าวหน้า ย่อมเป็นสิ่งที่ดีในการอำนวยความสะดวกให้กับคนอย่างเราๆ แต่ก็ตามสภาพของความเป็นจริงคือ ที่ใดมีดีย่อมมีสิ่งที่ไม่ดีปะปนอยู่ด้วยเช่นกันดังนั้น log files ก็สามารถใช้ในการตรวจสอบแก้ไขปัญหาการส่งข้อมูลผิด ทำให้เกิดความเสียหายในหลายๆส่วน เช่น การขโมยข้อมูล การใส่ร้ายป้ายสี เป็นต้น หรืออีกกรณีคือการกระทำที่เกิดจากโปรแกรมที่ไม่พึงประสงค์ ทำการโจมตีทำให้เกิดความเสียหายในระบบเครือข่าย ซึ่งอาจทำให้เกิดความเสียหายเป็นวงกว้าง การที่มีข้อมูลจาก log files ก็ทำให้เราตรวจสอบที่ไปที่มาของการกระทำเหล่านี้ ทำให้สามารถหาสาเหตุและวิเคราะห์หาวิธีการแก้ไขได้ตรงจุดและไวยิ่งขึ้น

## บทบาทพื้นฐานของ Logfiles ในระบบปฎิบัติการ Linux

log files ในระบบ Linux เป็นไฟล์ที่บันทึกข้อมูลที่เกิดขึ้นในระบบ เช่น การทำงานของโปรแกรม, Error, Warning และกิจกรรมอื่นๆ ที่เกี่ยวข้องกับการใช้งานในระบบ ซึ่ง log files มีบทบาทสำคัญในหลายด้าน
1. **Troubleshooting** : เมื่อเกิด Error ขึ้นในระบบ Linux เราสามารถระบุปัญหาที่เกิดขึ้นได้ด้วย log files โดยการตรวจสอบ system logs, application logs และ service logs เรายังสามารถที่จะระบุ error, warning และข้อความอื่นๆ ที่ชี้ที่ข้อผิดพลาดได้โดยตรง

2. **Diagnosing Performance Issues** : system logs สามารถระบุปัญหาเกี่ยวกับประสิทธิภาพ เช่น memory leaks หรือ ข้อจำกัดของการอ่าน/เขียนข้อมูลของดิสก์ การตรวจสอบ application logs ยังช่วยระบุปัญหาเกี่ยวกับประสิทธิภาพของ application ได้อีกด้วย

3. **Monitoring System Health** : เราสามารถตรวจสอบ logfiles เพื่อดูแนวโน้มสถานะของระบบว่ามีแนวโน้มไปทางที่ดีหรือแย่ หากเกิดแย่ขึ้นมาก็สามารถตรวจจับปัญหาที่เกิดขึ้นได้ก่อนที่มันจะสายไป ทั้งนี้การดู logfiles อาจทำให้เห็นปัญหาที่เกิดขึ้นในระบบได้

4. **Compliance and Auditing** : การบันทึกข้อมูลในระบบ Linux เป็นเครื่องมือสำคัญสำหรับองค์กรในการปฏิบัติตามข้อกำหนดทางกฎหมายและการตรวจสอบ โดยบันทึกนี้ช่วยในการระบุกิจกรรมของระบบและเหตุการณ์ที่สำคัญ เช่น การเข้าถึงข้อมูลที่มีความลับ การเปลี่ยนแปลงในการกำหนดค่าของระบบ และการเข้าถึงข้อมูลที่สำคัญ การเก็บบันทึกอย่างครอบคลุมช่วยให้องค์กรสามารถปรับปรุงความปลอดภัยและการดำเนินการได้อย่างมีประสิทธิภาพในระบบ IT

5. **Security** : Linux logs เป็นเครื่องมือสำคัญในการตรวจจับและตรวจสอบปัญหาด้านความปลอดภัย บันทึกของระบบสามารถใช้ตรวจจับการเข้าถึงระบบโดยไม่ได้รับอนุญาต และบันทึกแอปพลิเคชันช่วยระบุกิจกรรมที่อาจมีลักษณะเสี่ยงภายในแอปพลิเคชันได้ด้วยการตรวจสอบบันทึกเหล่านี้ ทำให้แอดมินสามารถระบุและตอบสนองต่อเหตุการณ์ความปลอดภัยได้อย่างรวดเร็ว

## ประเภทของ Log files ที่สำคัญในระบบ Linux

logfiles ในระบบ linux สามารถแบ่งได้เป็นหลายประเภทตามแหล่งที่มาหรือวัตถุประสงค์ของการบันทึก นี่เป็น 4 ประเภทของ logfiles ที่พบได้บ่อยๆในระบบ Linux

1. **System Logs** : logs นี้จะมีข้อมูลเกียวกับการทำงานของระบบ เช่น ข้อความการบูต (boot messages), ข้อความเกิดจาก kernel, และเหตุการณ์ที่เกี่ยวข้องกับฮาร์ดแวร์ System logs เป็นสิ่งสำคัญสำหรับการแก้ไขปัญหาในระบบ และการตรวจสอบประสิทธิภาพของระบบ

2. **Application Logs** : logs นี้บันทึกข้อมูลการทำงานของ Application ซึ่งรวมถึง Error, Warnings และข้อความอื่นๆ Application logs ใช้ในการวิเคราะห์ปัญหาที่เกิดขึ้นใน application 

3. **Service Logs** : logs นี้บันทึกข้อมูลเกี่ยวกับ services ที่กำลังทำงานบนระบบ ซึ่งรวมถึงบริการเครือข่ายและ*เดมอน Service logs ใช้ในการตรวจสอบกิจกรรมและปรับปรุงประสิทธิภาพของ services 

4. **Event Logs** : บันทึกเหตุการณ์เหล่านี้ประกอบด้วยข้อมูลเกี่ยวกับเหตุการณ์ในระบบ เช่น เข้าสู่ระบบของผู้ใช้, การปิดระบบ, และเหตุการณ์ด้านความปลอดภัย บันทึกเหตุการณ์นี้ใช้ในการตรวจสอบกิจกรรมของระบบ, ติดตามกิจกรรมของผู้ใช้, และสืบสวนเหตุการณ์ด้านความปลอดภัย

## Logfiles ที่สำคัญ
1. **/var/log/kern** เก็บข้อมูล logs และข้อมูลเตือนเกี่ยวกับ Kernel ข้อมูลใน log นี้มีค่าสำหรับการแก้ปัญหา Kernel ที่กำหนด

2. **/var/log/dmesg** ข้อความเกี่ยวกับ driver คำสั่ง dmesg สามารถใช้ดูข้อความในไฟล์นี้ได้

3. **/var/log/cron** เก็บข้อมูลทั้งหมดเกี่ยวกับ Crond (cron jobs) เช่น เมื่อ cron daemon เริ่มต้นงาน ข้อความเกี่ยวกับความล้มเหลวเกี่ยวข้อง ฯลฯ

4. **/var/log/yum.log** หากเราติดตั้ง package โดยใช้คำสั่ง yum ไฟล์ log นี้จะเก็บข้อมูลทั้งหมดที่เกี่ยวข้องซึ่งสามารถใช้ในการกำหนดว่า package และ component ทั้งหมดถูกติดตั้งอย่างถูกต้องหรือไม่

5. **/var/log/faillog** มีข้อมูลเกี่ยวกับการเข้าสู่ระบบที่ล้มเหลวทั้งหมด มีประโยชน์ในการดูเหตุการณ์การพยายามที่ไม่สำเร็จในการโจมตีระบบความปลอดภัย เช่น การพยายามโจมตีการเข้าสู่ระบบ หรือการโจมตีด้วยวิธีการบุกรุกโดยใช้ความแรง

6. **/var/log/syslog หรือ /var/log/messages** ข้อความทั่วไป รวมถึงข้อมูลเกี่ยวกับระบบทั้งหมด สรุปได้ว่า log นี้เก็บข้อมูลกิจกรรมทั่วๆไปในระบบทั้งหมด Redhat-based systems เช่น CentOS หรือ Rhel ข้อมูลจะถูกเก็บใน messages ในขณะที่ Ubuntu และระบบ Debian-based อื่นๆ จะถูกเก็บใน Syslog

7. **/var/log/auth.log หรือ /var/log/secure** เก็บข้อมูล logs การตรวจสอบสิทธิ์การเข้าใช้ระบบ 

8. **/var/log/boot.log** เป็นคลังข้อมูลทั้งหมดเกี่ยวกับการบูตและข้อความที่บันทึกขณะเริ่มต้น

9. **/var/log/maillog หรือ var/log/mail.log** เก็บ logs ทั้งหมดที่เกี่ยวข้องกับเซิร์ฟเวอร์จดหมาย มีประโยชน์เมื่อเราต้องการข้อมูลเกี่ยวกับ postfix, smtpd หรือบริการที่เกี่ยวข้องกับอีเมลที่กำลังทำงานบนเซิร์ฟเวอร์ของเรา

## การเข้าดู Log files ผ่าน CLI
ขั้นตอนแรกให้เราทำการเข้าไปดูที่ /var/log ผ่านคำสั่ง

	cd /var/log
แล้วทำการรันคำสั่ง
	
	ls -la
และนี้คือผลลัพธ์ที่ได้

![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205859121971204106/image.png?ex=65d9e6d2&is=65c771d2&hm=1424b9090e6161c3af2521d91de2cdfc216a18d42ada8398c73926cbfce41cdb&=&format=webp&quality=lossless)

เราจะเห็นได้เลยว่ามี logfiles อยู่ใน dir นี้ ไม่ว่าจะเป็น kern.log, syslog, dmesg, boostrap.log ฯ โดยในที่นี้ผมจะใช้ syslog ในการแสดงผลเป็นส่วนใหญ่ครับ เราไปเริ่มกันที่คำสั่งแรกเลย

### CAT 
เราสามารถใช้คำสั่ง cat เพื่อให้แสดงผลบันทึกที่อยู่ใน logfiles ที่เราต้องการได้ครับ โดยใช้คำสั่ง cat ตามด้วยที่อยู่ของ logfiles ที่เราต้องการที่จะแสดงผล โดยที่นี้เราจะแสดงผลของ syslog ครับ

	cat /var/log/syslog
![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205863416342909018/image.png?ex=65d9ead2&is=65c775d2&hm=a8516712c496a9ec4f67b7e3c17d8bd99528181e03c5c615825550531ed2f2f5&=&format=webp&quality=lossless)

โดยจากผลลัพธ์จะเห็นได้ว่ามีการแสดงผลบันทึกการทำงานของระบบ ข้อมูลต่างๆที่เกี่ยวข้องกับการทำงานของระบบ เช่น ข้อความเกี่ยวกับการบูตของระบบ, ข้อความการเชื่อมต่อเครือข่าย, ข้อความที่เกี่ยวกับการทำงานกับ software ต่างๆ และอื่นๆ ซึ่งจากที่เห็นการบันทึกด้านหน้าจะมีเวลาอยู่ด้วยนั่นเอง

เนื่องจากการใช้ cat ทำให้แสดงผลที่อยู่ใน logfiles ทั้งหมดออกมาเราอาจจะใช้งานร่วมกับ | more (pipe more) เพื่อเรียกดูทีละบรรทัดก็ได้

ถ้าเราอยากแสดงผลเฉพาะบรรทัดที่เราต้องการที่จะดู ยกตัวอย่างเช่นอยากได้เฉพาะข้อความใน logfiles syslog ที่มีคำว่า "error" อยู่ในบรรทัดนั้น เราก็สามารถใช้ **grep** ร่วมกันกับ cat ได้ ยกตัวอย่างการใช้งาน

	cat /var/log/syslog | grep error
![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205865598907842580/image.png?ex=65d9ecda&is=65c777da&hm=287628bcf736e779ec89a7a1099ba540600a25ba8cc18d785684975f35064b65&=&format=webp&quality=lossless)

ก็จะเห็นได้ชัดจากผลลัพธ์เลยว่าทุกบรรทัดที่แสดงผลจะมีคำว่า "error" ร่วมอยู่ด้วย ไปที่คำสั่งต่อไป

### head & tail
คำสั่งนี้ก็เป็นคำสั่งในการแสดงผลเหมือนกันแต่จะแตกต่างจาก **cat** ก่อนหน้าที่จะแสดงผลทั้งหมด head จะแสดงผล 10 บรรทัดแรก ส่วน tail จะแสดงผล 10 บรรทัดสุดท้าย ลองไปใช้งานกันเลย

	tail /var/log/syslog

ผลลัพธ์

![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205868727694917662/image.png?ex=65d9efc4&is=65c77ac4&hm=3a942a3ed5d19322e2e13883d4e16a05b15ed23e07345ed209fbccdccb4df394&=&format=webp&quality=lossless)

	head /var/log/syslog

ผลลัพธ์

![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205869009979838496/image.png?ex=65d9f007&is=65c77b07&hm=bf5dbe8039958edae6fcab577f8d93b44ebca7190977934baaea6da15365fbd2&=&format=webp&quality=lossless)

ผลลัพธ์ที่ออกมาก็เป็นไปตามที่คาดไว้ แต่สมมติว่าเราอยากให้มันขึ้นซัก 20 บรรทัด ทำได้มั้ย? คำตอบคือได้ เพียงเราใส่ **-n** ตามด้วยจำนวนที่เราต้องการก็จะเป็นอันเสร็จสิ้น

	tail -n 20 /var/log/syslog

ผลลัพธ์

![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205870743993327618/image.png?ex=65d9f1a5&is=65c77ca5&hm=55b22019baf519c83a3371d90dac1779d6042fa86bc1eaadb95ee6ac8eebb7bd&=&format=webp&quality=lossless)

หรือหากเราต้องการที่จะดูแบบ realtime คิดว่า logfiles จริงๆแล้วก็คือไฟล์ๆนึงที่เมื่อมีการบันทึกข้อมูล ก็จะเกิดการเปลี่ยนแปลงภายในไฟล์ถ้าเราอยากดูแบบ realtime เราก็สามารถใช้ได้ด้วยคำสั่ง **tail** อีกเช่นเคย แต่เราจะใช้ **-f** 
เข้ามาร่วมวงด้วย โดยที่ **-f** หมายถึง **follow** ซึ่งจะติดตามข้อมูลใหม่ๆที่เข้ามาในไฟล์

	tail -f /var/log/syslog
ผลลัพธ์

![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205872641727012915/image.png?ex=65d9f369&is=65c77e69&hm=9c29efb581780ef2baf5abc373d1d940bb4b76f19aa150351eb82c2d7b677eb2&=&format=webp&quality=lossless)

จากผลลัพธ์ที่ได้รับก็เหมือน tail ปกติ แค่มีเพิ่มเติมขึ้นมาคือเราจะไม่กลับไปสู่สถานะที่สามารถพิมพ์ คำสั่งแบบปกติได้ แต่จะมี ตัว _ (underscore) กระพิบๆอยู่ ถ้าหากมีการ update อะไรภายใน file ที่เราเลือก ซึ่งในที่นี้คือ file syslog ก็จะทำการแสดงผลให้เราเห็นทันที

### Journalctl
เป็นคำสั่งที่ผมคิดว่าใช้งานได้ค่อนข้างดี โดยเราสามารถเลือก service หรือ unit ที่เราต้องการที่จะดู message เกี่ยวกับ service นั้นๆที่เราเลือก มันก็จะทำการแสดง message ทั้งหมดที่เกี่ยวกับ service นั้นๆ ผมจะลองโชว์ message เกี่ยวกับ ssh (secure shell) โดยใช้คำสั่ง **journalctl -u service_name**

![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205878596824993862/image.png?ex=65d9f8f5&is=65c783f5&hm=89127318a764450084b9fad9c697668ced265db964cdcacd983e1b798335eaea&=&format=webp&quality=lossless)

เราก็จะเห็น message ที่เกี่ยวกับ ssh ทั้งหมด หากเราต้องการกำหนดวันเวลาที่ต้องการให้แสดงผล เราสามารถใช้ **--since**และ **--until** ร่วมกับ journalctl ได้

	journalctl -u service_name --since "YYYY-MM-DD HH:MM:SS"
โดยผมจะลองใช้กับ ssh

![enter image description here](https://media.discordapp.net/attachments/1110947924369743925/1205880587722686514/image.png?ex=65d9fad0&is=65c785d0&hm=76331858df66f314b0cd9d148bc498b6cd71f22011e1da212dc4dd675c59666f&=&format=webp&quality=lossless)

 
โดยการที่เราใช้คำสั่ง journalctl ทำให้เราสามารถดู message ที่เกี่ยวกับ service ที่เราต้องการได้อย่างมีประสิทธิภาพ โดยตัว journalctl รู้ว่า message ไหนที่เกี่ยวข้องกับ service หรือ unit ที่เราต้องการจะดูแล้วนำมาแสดงผล ซึ่งในที่หน้าที่ได้ดีกว่าการใช้คำสั่ง tail ร่วมกับ grep

## Linux  Security Log 
Linux  Security Log มีบทบาทสำคัญต่อการDetect หรือBlock ภัยคุกคามที่มีการเข้าถึง
โดยไม่ได้รับอนุญาติ ซึ่งอาจจะส่งผลเสียหลายอย่างตามมา ไม่ว่าจะเป็น การโดนล่วงละเมิดข้อมูล หรือ การแก้ไขข้อมูลจากการ บุกรุกนั้นเอง และนี้จึงเป็นที่มาของ 
**Linux Security Log**
โดยหากจะให้พูดถึงในด้านความปลอดภัยนั้น จะมีเครื่องมือหรือคำสั่งที่สำคัญอยู่ประมาณนึงซึ่งบางอย่างอาจจะเป็นการตรวจจับ หรือบาง
อย่างอาจจะเป็นการป้องกันเลยก็ได้

## Example Of Security Solution
**1.** โดยพื้นฐานแล้วไม่ว่าจะเป็นlinux ubantu หรือ Osใดก็ตามแต่ ขั้นแรกเลยที่เราสามารถจะทำได้และ Basicสุดเลยก็คือ การupdate versionของ Os ให้ใหม่และดีขึ้นนั้นเอง เพราะเราเชื่อว่า การที่ผู้พัฒนานั้นได้ มีการUpdate จะต้องมีการแก้ไข ในจุดต่างๆรวมถึงในด้านความปลอดภัยด้วยนั้นเอง

-โดยคำสั่ง **Update** 2คำสั่ง ตามลำดับ

	apt-get update   
	apt-get upgrade

 ![](https://media.discordapp.net/attachments/904766802196824084/1205970133290590208/apt-get_upgrade.png?ex=65da4e35&is=65c7d935&hm=3074d07cebfb51068342f3649d8d19798428596ce72877091036efe9e2935adf&=&format=webp&quality=lossless&width=877&height=662)

*โดยหากใช้คำสั่ง Update เพียงอย่างเดียว Os  จะไม่ได้มีการติดตั้งอะไรใดๆ ยกเว้นการอัปเดต package ใน systemเท่านั้น จึงต้องทำการใช้คำสั่ง Upgrade ไปด้วยเพื่อติดตั้งPackage เหล่านั้น

![](https://cdn.discordapp.com/attachments/904766802196824084/1205970132980207697/apt-get_update.png?ex=65da4e35&is=65c7d935&hm=cbd45216f06975a5aa46253c04f2b4a829dc17c70d9422195c6084e5c57b8d1b&)	

**2.** การเช็ค log ต่างๆ ด้วยคำสั่งพื้นฐาน
ในวิธีนี้อาจจะเป็นการ manual นิดนึง จากที่เราได้เกริ้น ในเรื่องของLogfile ไปในบางส่วนตั้งแต่ข้างต้นแล้ว  
ไม่ว่าจะเป็นการใช้คำสั่งต่างๆ หลายคำสั่งเราสามารถเช็คตรวจสอบ การเข้าถึงระบบได้ด้วยตัวเราเอง เช่นการเข้าไปเช็คที่ 
**/var/log/auth.log**   หรือ   **grep 'Failed password' /var/log/auth.log** ที่ระบุkeyword **"Failed password"**
การดู LogFile การเข้าสู่ระบบที่สำเร็จหรือล้มเหลว การใช้งาน sudo และเหตุการณ์ที่เกี่ยวข้องกับความปลอดภัยอื่นๆ เป็นต้น เราสามารถตรวจสอบและเชคได้หมดเลย

![](https://media.discordapp.net/attachments/904766802196824084/1205970134880096256/log_password_login.png?ex=65da4e35&is=65c7d935&hm=eb41ca7a9e3caff65ecb6d340c940cce36696da11f0c8f04850c792e611dd6a3&=&format=webp&quality=lossless&width=872&height=662)

**3.** การติดตั้งเครื่องมือต่างๆที่ใช้ในการป้องกัน 

โดย ณ ที่นี้ ผมจะยกตัวอย่างของ **Fail2Ban** 

ซึ่ง **Fail2Ban** นั้นเป็นเครื่องมือที่ใช้ในการป้องกันการโจมตีต่าง ๆ โดยจะตรวจสอบบันทึกของระบบ(log) 
เพื่อตรวจจับการเข้าสู่ระบบไม่สำเร็จหลายครั้งหรือการพยายามเข้าสู่ระบบโดยใช้ข้อมูลที่ไม่ถูกต้อง 
และจากนั้นจะทำตามprocessที่เรากำหนด  เช่น บล็อกการเข้าถึง IP ที่พยายามเข้าสู่ระบบมากเกินไป หรือต้องรอเวลา เป็นต้น
(โดยเฉพาะไอ้พวกที่BruteFrostกันเข้ามานี้ไม่รอด) 

-การติดตั้ง Fail2Ban

	sudo apt-get install fail2ban

![](https://media.discordapp.net/attachments/904766802196824084/1205970134317928530/Failed2Bam.png?ex=65da4e35&is=65c7d935&hm=262d8f1b7d83f99102af90f9fabe290b085fe91082162b50248b88496447a3bb&=&format=webp&quality=lossless&width=876&height=662)

-ทำการ cd เข้าไปที่ directory ที่มีfileไว้สำหรับ config ค่าต่างๆ ของ fail2ban และ duplicate(copy) ไฟล์ **jail.conf** to **jail.local**

 	sudo cd /etc/fail2ban
  	sudo cp jail.conf  jail.local

![](https://media.discordapp.net/attachments/904766802196824084/1205970133554823239/cp_fial2ban_local.png?ex=65da4e35&is=65c7d935&hm=a0a6dfe39ed19c89b71711349ac5cfbf33dd2f621b02b7cbe25288f666c374d3&=&format=webp&quality=lossless&width=867&height=662)


-เข้าไปแก้ไขconfigต่างๆ 

 	sudo nano jail.local

![](https://media.discordapp.net/attachments/904766802196824084/1205970135236616212/Nano_Jail.png?ex=65da4e36&is=65c7d936&hm=338ff1a8518ffba00b532df2205be75f12a191c88ca0261ae5df5484dca88e34&=&format=webp&quality=lossless&width=883&height=662)

*มาถึงตรงนี้แล้ว เราก็สามารถทำการแก้ไขconfigผ่าน jail.localได้เลย ซึ่งผมจะยกตัวอย่างการ configง่ายๆให้เอาล่ะกันน่ะครับ 
(หากจะให้บอกทุกอย่าง มันจะกลายเป็นบทความของ fail2banเลยน่ะเอาจริง) 


 	#enabled = true
	#port = 22
	#action = iptables-multiport
	#logpath = /var/log/auth.log
	#maxretry = 3
	#bantime = 3600

![](https://media.discordapp.net/attachments/904766802196824084/1205970133915271219/Ex_Config_fail2ban.png?ex=65da4e35&is=65c7d935&hm=328904bd8d2623212c8926222527eea4caa5a08e586d3d03573bdfcd355b09b1&=&format=webp&quality=lossless&width=882&height=662)

การตั้งค่าเหล่านี้จะกำหนดค่า Fail2Ban เพื่อตรวจสอบบริการ SSH (sshd) port 22 
หากมีการพยายามเข้าสู่ระบบล้มเหลว3ครั้งเกิดขึ้นภายในหนึ่งชั่วโมง ที่อยู่ IP 
จะถูกแบนเป็นเวลา 3,600 วินาที (1 ชั่วโมง) (ปรับตามใจชอบเลยก็ได้ครับ)



# Other Chapter
- 🛠 [**Introduction Monitoring and Logging Tools**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/README.md)
- 🛠 [**Chapter 1 Monitoring and Logging Tools**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%201/Readme.md)
- 📈 [**Chapter 2 Log Reader and Analysis**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%202/Readme.md)
- 📝 [**Chapter 3 Log Collection and Server**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%203/Readme.md)
- 📩 [**Chapter 5 Working with Texts**](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Chapter%205/Readme.md)

# Source
- [Reference Log Files](https://github.com/Jxwgame/Monitoring-and-Logging-Tools-Sec-2/blob/main/Reference/Chapter%204.md)
