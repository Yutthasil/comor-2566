# Repository Setup using dpkg
  
เหตุใดจึงต้องสร้างพื้นที่เก็บข้อมูล Debian 
 + ควบคุมการอัปเดตและอัปเกรดไฟล์ .deb ได้อย่างละเอียด: แทนที่จะพึ่งพาที่เก็บข้อมูลสาธารณะ สามารถควบคุมเวอร์ชันของไฟล์ .deb ที่ติดตั้งบนระบบได้
 + ติดตั้งไฟล์ .deb เดียวกันกับที่ใช้ในสภาพแวดล้อมทดสอบ: การติดตั้ง File .deb มีประโยชน์สำหรับการจำลองสภาพแวดล้อมเดียวกันบนเซิร์ฟเวอร์จริง
 + หลีกเลี่ยงปัญหา "dependency hell": ที่เก็บข้อมูลส่วนตัวช่วยให้จัดการความสัมพันธ์ระหว่างแพ็คเกจได้ง่ายขึ้น ป้องกันปัญหาที่แพ็คเกจใหม่ไปรบกวนแพ็คเกจอื่นๆ ที่จำเป็น

บนระบบ Debian แพ็คเกจทั้งหมดจะถูกจัดการโดยยูทิลิตี้ APT (apt, apt-get, apt-cache, ฯลฯ) ในการสร้างที่เก็บข้อมูลส่วนตัวที่เข้ากันได้กับ APT จำเป็นต้องมีแพ็คเกจ dpkg-dev

## การติดตั้ง Package dpkg

  + ขั้นตอนที่ 1: อัปเดตแพ็คเกจของระบบ:
```
  sudo apt update && sudo apt upgrade
```
  + ขั้นตอนที่ 2:  ติดตั้งแพ็คเกจ `dpkg-dev`
```
  sudo apt update && sudo apt upgrade
```

## สร้างโฟลเดอร์สำหรับที่เก็บข้อมูลส่วนตัว

 + ขั้นตอนที่ 1: สร้างโฟลเดอร์สำหรับจัดเก็บไฟล์ .deb โดยในตัวอย่างใช้คำสั่ง:
```
  sudo mkdir -p /opt/local/debs
```
 + ขั้นตอนที่ 2:  เปลี่ยนไปยังโฟลเดอร์ที่เพิ่งสร้าง:
```
  cd /opt/local/debs
```
##  เพิ่มแพ็คเกจลงในที่เก็บข้อมูล

ขั้นตอนต่อมานั้นจะต้องดาวน์โหลดแพ็คเกจเบราว์เซอร์ Chrome ลงในที่เก็บข้อมูล เนื่องจากแพ็คเกจนี้ไม่มีอยู่ในที่เก็บข้อมูลเริ่มต้นของ Ubuntu

 + ใช้คำสั่งตามนี้
```
   sudo wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
## สร้างไฟล์ข้อมูลที่จำเป็นสำหรับ APT

 + ขั้นตอนที่ 1: เปลี่ยนสิทธิ์ผู้ใช้เป็น root: ตัวอย่างนี้ใช้คำสั่ง:
```
  sudo su
```
 + ขั้นตอนที่ 2: สร้างไฟล์ Release: คำสั่งนี้จะสร้างไฟล์ข้อมูลเกี่ยวกับแพ็คเกจใน repo:
```
  dpkg-scanpackages . /dev/null > Release
```
 + output
```
dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning: google-chrome-stable
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.
```

 + ขั้นตอนที่ 3: สร้างไฟล์ Packages.gz: คำสั่งนี้จะสแกนไฟล์ .deb และสร้างข้อมูลแพ็คเกจในรูปแบบที่บีบอัด:
```
  dpkg-scanpackages . /dev/null | gzip -9c > Packages.gz
```
 + output
```
dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning: google-chrome-stable
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.
```
หากต้องการแสดงรายการโครงสร้างไดเร็กทอรี repo ในเครื่อง ให้รันคำสั่ง ls:
```
ls -l
```
 + output
```
-rw-r--r-- 1 root root 83325072 May 8 02:29 google-chrome-stable_current_amd64.deb
-rw-r--r-- 1 root root 761 May 17 20:44 Packages.gz
-rw-r--r-- 1 root root 1321 May 17 20:39 Release
```

## เพิ่มที่เก็บข้อมูลลงใน Sources.list


 + ขั้นตอนที่ 1: แก้ไขไฟล์ Sources.list: ใช้คำสั่ง:
```
  sudo nano /etc/apt/sources.list
```
 + ขั้นตอนที่ 2: เพิ่มบรรทัดต่อไปนี้ลงในไฟล์:
```
  deb [trusted=yes] file:/opt/local/debs ./
```
 + deb: ระบุประเภทของที่เก็บข้อมูล
 + trusted=yes: ระบุว่าไว้วางใจที่เก็บข้อมูลนี้
 + file:/opt/local/debs: ระบุตำแหน่งของที่เก็บข้อมูล
 + ./: ระบุว่าที่เก็บข้อมูลอยู่ในไดเร็กทอรี่ปัจจุบัน

## Verification
สามารถตรวจสอบการทำงานของที่เก็บข้อมูลโดยการติดตั้งหรือลบแพ็คเกจจากที่เก็บข้อมูลนี้

 + ขั้นตอนที่ 1: อัปเดตแพ็คเกจ:
```
  sudo apt update
```
 + ขั้นตอนที่ 2: ติดตั้งแพ็คเกจ:
```
  sudo apt install google-chrome-stable
```
 + การลบ package ที่ติดตั้ง
```
  sudo apt remove google-chrome-stable
```

การสร้างที่เก็บข้อมูล Debian ส่วนตัวมีประโยชน์ในหลายกรณี ดังนี้:

1. ติดตั้งแพ็คเกจที่ไม่มีในที่เก็บข้อมูลเริ่มต้น:

บางครั้งแพ็คเกจที่ต้องการอาจไม่มีในที่เก็บข้อมูลเริ่มต้นของ Debian การสร้างที่เก็บข้อมูลส่วนตัวช่วยให้สามารถเพิ่มแพ็คเกจเหล่านี้ลงในระบบของได้อย่างง่ายดาย

2. ควบคุมเวอร์ชันของแพ็คเกจ:

ที่เก็บข้อมูลส่วนตัวช่วยให้สามารถควบคุมเวอร์ชันของแพ็คเกจที่ติดตั้งบนระบบของได้ ตัวอย่างเช่น สามารถติดตั้งเวอร์ชันเฉพาะของแพ็คเกจที่รู้ว่าทำงานได้อย่างถูกต้อง แทนที่จะใช้เวอร์ชันล่าสุดที่มีอาจมี bugs

3. เพิ่มความเร็วในการติดตั้งแพ็คเกจ:

การติดตั้งแพ็คเกจจากที่เก็บข้อมูลส่วนตัวมักจะเร็วกว่าการติดตั้งจาก internet เนื่องจากไม่จำเป็นต้องดาวน์โหลดแพ็คเกจผ่าน internet

4. ปรับแต่งระบบของ:

ที่เก็บข้อมูลส่วนตัวช่วยให้สามารถปรับแต่งระบบของด้วยแพ็คเกจที่ไม่รวมอยู่ใน Debian

5. สำรองข้อมูลแพ็คเกจ:

ที่เก็บข้อมูลส่วนตัวสามารถใช้สำรองข้อมูลแพ็คเกจที่ติดตั้งบนระบบของ

## reference
 + (https://linuxopsys.com/topics/create-your-own-repository-for-packages-on-debian)
 + (https://rpmdeb.com/devops-articles/how-to-create-local-debian-repository/)
