# Repository Setup ด้วย APT
ติดตั้ง Repository ด้วยคำสั่ง `add-apt-repository` ซึ่งเป็นสคริปต์ภาษา Python ที่จะช่วยติดตั้ง Repository ลงที่ `/etc/apt/sources.list` หรือจะแยกไฟล์ที่ `/etc/apt/sources.list.d` directory ก็ได้ ซึ่งคำสั่งนี้สามารถใช้เพื่อนำ Repository ที่มีอยู่แล้วออกได้ด้วย

การจะใช้คำสั่ง `add-apt-repository` นั้น จะต้องมีแพ็กเกจ `software-properties-common` ด้วย สามารถติดตั้งได้โดย
```
sudo apt update
sudo apt install software-properties-common
```

## ติดตั้ง Repository ด้วย `add-apt-repository`
### Syntax
```
add-apt-repository [options] repository
```

Repository ที่จะติดตั้ง สามารถเป็นได้ทั้งไฟล์ `sources.list` หรือ PPA Repository ในรูปแบบ `ppa:<user>/<ppa-name>` ก็ได้

สามารถใช้คำสั่ง `man add-apt-repository` เพื่อดูคู่มือของ `add-apt-repository` ว่าทำอะไรได้บ้างได้

Ubuntu ตั้งแต่เวอร์ชั่น 18.04 เป็นต้นไป `add-apt-repository` จะอัพเดท package index ให้ด้วย ถ้า นำเข้ repository public key เข้ามา

**Package Index** คือ Database ที่เก็บข้อมูลของ repository ที่มีอยู่ทั้งหมดในระบบ

## ขั้นตอนการติดตั้ง Repository
### สมมุติว่าจะติดตั้ง MongoDB จาก Official Repository

เริ่มต้นด้วยการนำเข้า repository public key
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
```
แล้วเพิ่ม MongoDB repository ด้วย
```
sudo add-apt-repository 'deb [arch=amd64] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse'
```
Repository จะถูกเพิ่มเข้าในไฟล์ `sources.list`
เสร็จแล้วก็จะสามารถติดตังแพ็กเกจใหม่ๆจาก repository ที่ติดตั้งได้แล้ว!
```
sudo apt install mongodb-org
```
ถ้าอยากลบ repository ก็สามารถทำได้โดยการเติม `--remove` ไปในคำสั่ง
```
sudo add-apt-repository --remove 'deb [arch=amd64] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse'
```

### เพิ่ม PPA Repository
Personal Package Archive (PPA) คือบริการที่ให้ผู้ใช้อัพโหลด Ubuntu source package ของตัวเองได้

เวลาเพิ่ม PPA Repository ด้วยคำสั่ง `add-apt-repository` ตัวคำสั่งจะสร้างไฟล์ใหม่ในไดเรกทอรี `/etc/apt/sources.list.d/`

เช่น ต้องการติดตั้ง FFA ของ Jonathon F ที่ให้ FFmpeg เวอร์ชั่น 4.x มา
```
sudo add-apt-repository ppa:jonathonf/ffmpeg-4
```
หลังจากกด Enter, Terminal จะแสดงข้อความ
```
Press [ENTER] to continue or Ctrl-c to cancel adding it.
```
ในขั้นตอนนี้ PPA repository public key นั้นจะถูกดาวน์โหลดโดยอัตโนมัติ
หลังจาก PPA ถูกเพิ่มเข้าระบบแล้ว สามารถติดตั้ง package ได้ทันที
```
sudo apt install ffmpeg
```




### Reference
* [How To Add Apt Repository In Ubuntu | Linuxize](https://linuxize.com/post/how-to-add-apt-repository-in-ubuntu/#apt-sources)
