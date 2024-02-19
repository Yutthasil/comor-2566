<br>

# 🗝️Authentication

คือกระบวนการที่ทำให้ระบบ computer สามารถตรวจสอบได้ว่าใครที่กำลังเข้าสู่ระบบ หรือ ใครที่สามารถเข้าสู่ระบบ computer หรือ network ได้บ้างโดยสามารถควบคุมการเข้าถึงด้วยการตรวจสอบตัวตนที่ตั้งไว้ เช่น username หรือ password 

โดยสามารถแบ่งประเภทที่นิยมใช้ในปัจจุบันได้ 5 แบบคือ

1. Password-based Authentication - เป็นการ Authentication ที่เข้าใจง่ายและสะดวกที่สุดเพราะใช้แค่ Password แต่มีข้อเสียคือด้านความปลอกดภัยเพราะหากถูกผู้อื่นทราบรหัสก็จะถูกเข้าถึงได้ง่าย

2. Certificate-Based Authentication - เป็นการใช้ digital cartificate ต่างๆเช่น public key หรือ digital signature

3. Multi-Factor Authentication - ใช้วิธีการ Authentication มากกว่า 1 ประเภทที่ต่างกันเช่น การทำ 2FA ทำให้ปลอมแปลงตัวตนได้ยากขึ้น

4. Token-Based Authentication - เป็นการมอบสิทธิ์ในการเข้าถึงให้กับ user เป็นการชั่วคราวโดยส่วนมากจะเป็นในรูปแบบ digital token เพื่อยืนยันว่า user นั้นมีสิทธิ์ในการเข้าถึงข้อมูล

5. Biometric Authentication - ใช้อัตลักษณ์ทางกายภาพในการยืนยันตัวตนเช่น ลายนิ้วมือ หรือ ม่านตา

### Identity Management

การจัดการตัวตน ( Identity Management ) คือการพยายามรวบรวม identities ไว้ที่ศูนย์กลางแล้วจัดการผ่านการทำ authentication และ authoriztion policies โดยมีจุดมุ่งหมายเพื่อลดความซ้ำซ้อนของการจัดการข้อมูล โดย User จะทำแค่การเข้าสู่ระบบแค่ครั้งเดียวแต่สามารถใช้ service ได้หลายอย่าง โดยผู้ดูแลระบบจะทำการควบคุมและมอบสิทธิ์ให้กับ user ตาม policies ที่ตั้งไว้

### Single Sign On : SSO

คือเทคโนโลยีที่ทำให้การเข้าใช้งาน service ใดๆสามารถทำให้ user login แค่ครั้งเดียวแทนที่การ login หลายๆครั้ง

ข้อดีของการทำ SSO
- Stronger passwords : พอ user ต้องใช้แค่ password เดียวในทางปฏิบัติ user มักจะตั้งรหัสยากขึ้น
- No repeated passwords : เมื่อ user ต้องใช้รหัสผ่านหลายๆครั้ง ในหลายๆที่ user มักจะใช้ password ซ้ำกันดังนั้นหากรหัสผ่านถูกคนอื่นรู้ก็อาจจะไปใช้งานในที่อื่นได้
- Better password policy enforrcement : การทำ SSO สามารถบังคับใช้ policies การตั้งรหัสได้สูงขึ้น
- Multi-factor authentication : การทำ MFA ในครั้งเดียวผ่าน SSO ทำให้สะดวกกว่าการทำหลายๆครั้ง
- Single point for enforcing password re-entry : สามารถบังคับให้ login อีกครั้งเมื่อผ่านช่วงเวลาหนึ่ง เพราะบาง application อาจไม่รองรับ
- Internal credential management instead of external storage : การทำ SSO จะทำให้รหัสผ่านนั้นถูกเก็บไว้ในที่ที่เดียวทำให้ปลอดภัยมากขึ้น
- Less time wasted on password recovery : หากเกิดปัญหาเช่น user ลืมรหัสการกู้คืนจะง่าขึ้นเพราะใช้แค่รหัสเดียว

### SSO ทำงานยังไง

เมื่อ user sign in ผ่านระบบ SSO, SSO service จะสร้าง token ที่จะจำว่า user นั้นถูกตรวจสอบแล้ว โดยเก็บไว้ใน browser ของ user หรือ server ของ SSO Service เมื่อ user ต้องการใช้แอพ แอพจะตรวจสอบว่ามี token หรือไม่ ถ้ามีจะให้เข้าใช้งาน แต่ถ้าไม่ก็จะถูกบังคับให้ทำการ sign in ผ่านระบบ SSO

**`/etc/nsswitch.conf` คืออะไร?**

คือไฟล์ที่ใช้กำหนดว่าระบบจะค้นหาข้อมูลจากแหล่งไหน โดยเราสามารถ config ไฟล์นี้ได้เมื่อเราเรียกใช้งาน

<img src="https://media.discordapp.net/attachments/1205566248105017374/1205569549462929489/image.png" width="600px" title="hover text">


**`/etc/pam.d` คืออะไร?**

 เป็น directory ที่เก็บไฟล์ที่ให้บริการเกี่ยวกับการทำ Authentication เช่น passwd login sudo
 
 <img src="https://media.discordapp.net/attachments/1205566248105017374/1205572199315152996/image.png" width="600px" title="hover text">


<br>

**บทถัดไป [Authorization](https://github.com/Pooh303/User-Access-Management-3/tree/main/Authorization)**
