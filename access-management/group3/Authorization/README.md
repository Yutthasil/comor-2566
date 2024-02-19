<br>

# Authorization 🔐
กระบวนการตรวจสอบว่าสามารถให้เข้าถึงทรัพยากรหรือไม่ หมายถึงการตัดสินใจว่าผู้ใช้จะทำอะไรได้บ้างเช่น การอ่านไฟล์เฉพาะ การรันโปรแกรมเฉพาะ หรือการเชื่อมต่อกับพอร์ตเครือข่ายเฉพาะ โดยทั่วไปแล้ว Authorization จะได้รับตามข้อมูลประจำตัว เช่น รหัสผ่าน

**การเรียกใช้งาน**

`sudoers` : กำหนดค่าให้ผู้ใช้รายอื่นสามารถเรียกใช้คำสั่ง sudo ได้

ตัวอย่าง : 
```
vi /etc/sudoers
```
`chown` : ใช้ในเปลี่ยนเจ้าของ file หรือ directory รวมทั้ง file owner และ group owner

ตัวอย่าง :
```
$ ls -ltr test
```
> -rwx------ 1 root root 0 May 7 00:22 test
```
$ chown games test
$ ls -ltr test
```
> -rwx------ 1 games root 0 May 7 00:22 test

`chmod` : ใช้ในการเปลี่ยนสิทธิ์ในการอ่าน, เขียน และ execute file หรือ folder แบ่งเป็นสิทธิ์ของ file owner, group owner, other user ซึ่งคำสั่งจะถูกแปลงจากเลขฐาน 8 ในการระบุสิทธิ์แต่ละชนิด

ตัวอย่าง : 
```
$ chmod 555 test
$ ls -ltr test
```
> -r-xr-xr-x 1 root root 0 May 7 00:22 test

`chgrp` : ใช้ในเปลี่ยนเจ้าของ group ของ file หรือ folder

ตัวอย่าง : 
```
$ chgrp staff test
$ ls -ltr test
```

> -rw-r--r-- 1 root staff 5 May 6 23:46 test

`getfacl` : แสดง base ACL และ extended ACL  แต่ละไฟล์ที่ระบุสามารถแก้ไขด้วย คุณสามารถระบุว่าจะแสดงการเข้าถึง ค่าเริ่มต้นของไฟล์ หรือค่าเริ่มต้นของไดเร็กทอรี คุณยังสามารถเปลี่ยนรูปแบบการแสดงผลเริ่มต้นได้อีกด้วย

ตัวอย่าง :
```
getfacl file
```
ผลลัพธ์ : 

> #file: file<br>#owner:  WELLIE<br>#group:  SYS<br>user::rwx   <=== The owner's permission bit setting<br>group::rwx  <=== The group's permission bit setting<br>other::rw-  <=== Permission bit setting if neither user nor group<br>user:  WELLIE2: rw-<br>group:SYS1:rwx

`setfacl` : ตั้งค่า แก้ไขหรือลบ ACL ไปยังไฟล์และไดเร็กทอรีปกติ นอกจากนี้สามารถอัปเดตและลบรายการ ACL แต่ละไฟล์และไดเร็กทอรีที่ระบุโดย path ถ้าไม่ได้ระบุ path ชื่อไฟล์และไดเร็กทอรีจะถูกอ่านจาก standard input (stdin)

ตัวอย่าง :
```
setfacl -s user::rwx,group::---,other::---,user:billy:r-x foo
```
> Authorization errors Error: “An I/O operation failed or was interrupted. For further details see the “Raw Error Message” and the additional messages”<br>Error: “List of potentially invalid parameters : Service Account Credentials”<br>Error: "Client is unauthorized to retrieve access tokens using this method, or client not authorized for any of the scopes requested."

**สาเหตุ :** ข้อผิดพลาดเหล่านี้เกี่ยวข้องกับ Service Account Authorization มักเกิดขึ้นเมื่อไม่มีการให้สิทธิ์ที่จำเป็นแก่บัญชีบริการหรือบัญชีผู้ใช้ บัญชีบริการต้องการสิทธิ์เข้าถึงการอ่าน domain-wide

**วิธีแก้ปัญหา :**
ตรวจสอบว่าบัญชีบริการได้รับการกำหนดค่าอย่างถูกต้องด้วย domain-wide services.
ตรวจสอบให้แน่ใจว่าบัญชีผู้ใช้มีบทบาทในการเข้าถึง reports access.

<br>

**บทถัดไป [Access Control, Firewall](https://github.com/Pooh303/User-Access-Management-3/tree/main/Access%20Control%2C%20Firewall)**
