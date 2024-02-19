# YUM (Yellowdog Updater Modified)
## YUM คืออะไรกันแน่?
Yellowdog Updater Modified หรือที่รู้จักกันในชื่อย่อว่า **_YUM_** เป็นเครื่องมือในการจัดการแพ็คเกจทั้งการติดตั้ง อัพเดต ลบ นิยมใช้ใน Red-Hat-based distros อย่างเช่นพวก CentOS, RHEL, OpenSUSE, Fedora, Rocky Linux. YUM จะแก้ปัญหา dependencies โดยอัตโนมัติ และจะทำการ obsolete processing โดยขึ้นอยู่กับ repository metadata ที่มีอยู่ในระบบ
นอกจากนี้ YUM ยังสามารถจัดการกับแพ็คเกจที่มีอยู่แล้วในระบบ หรือจากแพ็คเกจ **.rpm** ก็ได้ โดยที่ตัวเอกสารกำหนดค่าหลักของ YUM นั้นจะอยู่ที่ **/etc/yum.conf** รวมถึงrepositories ทุกตัวของ YUM ก็จะอยู่ที่่ **/etc/yum.repos.d**

โดยการใช้คำสั่ง YUM ได้นั้นจะต้องเปลี่ยนเป็น root ก่อน หรือไม่ก็ใช้ sudo โดยที่ yum จะมี syntax โดยทั่วไปดังนี้

```
$ sudo yum [options] [command] [package_name]
```

การติดตั้งแพ็คเกจผ่าน YUM สามารถทำได้โดยการใช้คำสั่งต่อไปนี้

```
$ sudo yum install [package_name]
```

ตัวอย่างผลลัพธ์

```
[deepak@localhost ~]$ sudo yum install iotop
...
Resolving Dependencies
--> Running transaction check
---> Package iotop.noarch 0:0.6-4.el7 will be installed
--> Finished Dependency Resolution

...
Installed:
  iotop.noarch 0:0.6-4.el7                                                                                      

Complete!
```

ในส่วนของการอัพเดตแพ็คเกจผ่าน YUM สามารถใช้คำสั่งนี้

```
$ sudo yum update [package_name]
```

ตัวอย่างผลลัพธ์

```
[deepak@localhost ~]$ sudo yum update NetworkManager
...
Resolving Dependencies
--> Running transaction check
---> Package NetworkManager.i686 1:1.18.8-1.el7 will be updated
--> Processing Dependency: NetworkManager = 1:1.18.8-1.el7 for package: 1:NetworkManager-ppp-1.18.8-1.el7.i686
--> Processing Dependency: NetworkManager = 1:1.18.8-1.el7 for package: 1:NetworkManager-tui-1.18.8-1.el7.i686
--> Processing Dependency: NetworkManager(x86-32) = 1:1.18.8-1.el7 for package: 1:NetworkManager-team-1.18.8-1.el7.i686
--> Processing Dependency: NetworkManager(x86-32) = 1:1.18.8-1.el7 for package: 1:NetworkManager-adsl-1.18.8-1.el7.i686
--> Processing Dependency: NetworkManager(x86-32) = 1:1.18.8-1.el7 for package: 1:NetworkManager-ppp-1.18.8-1.el7.i686
--> Processing Dependency: NetworkManager(x86-32) = 1:1.18.8-1.el7 for package: 1:NetworkManager-wifi-1.18.8-1.el7.i686
---> Package NetworkManager.i686 1:1.18.8-2.el7_9 will be an update
--> Processing Dependency: NetworkManager-libnm(x86-32) = 1:1.18.8-2.el7_9 for package: 1:NetworkManager-1.18.8-2.el7_9.i686

...

Updated:
  NetworkManager.i686 1:1.18.8-2.el7_9                 NetworkManager-glib.i686 1:1.18.8-2.el7_9                

Dependency Updated:
  NetworkManager-adsl.i686 1:1.18.8-2.el7_9              NetworkManager-libnm.i686 1:1.18.8-2.el7_9             
  NetworkManager-ppp.i686 1:1.18.8-2.el7_9               NetworkManager-team.i686 1:1.18.8-2.el7_9              
  NetworkManager-tui.i686 1:1.18.8-2.el7_9               NetworkManager-wifi.i686 1:1.18.8-2.el7_9              

Complete!
```

แต่ถ้าไม่ได้มีการระบุชื่อแพ็คเกจไว้ มันก็จะไปทำการอัพเดตแพ็คเกจทุกตัวที่ได้มีการติดตั้งไว้บนระบบ

```
$ sudo yum update
```

## commonly-used commands for YUM
นอกจาก install และ update แล้ว YUM ยังมีคำสั่งพื้นฐานที่ใช้โดยทั่วไปดังนี้

**Command** | **Purpose**
--- | ---
install | ติดตั้งแพ็คเกจหรือหลายแพ็คเกจ
remove | ลบแพ็คเกจออกจากระบบ
search | ค้นหาแพ็คเกจตามคำค้นหา
info | แสดงข้อมูลละเอียดเกี่ยวกับแพ็คเกจที่ระบุ
list | แสดงรายการแพ็คเกจที่ติดตั้งและที่มีในระบบ
update | อัปเดตแพ็คเกจที่ติดตั้งเพื่อให้เป็นเวอร์ชันล่าสุด
repolist | แสดงรายการที่เก็บข้อมูล
history | แสดงสิ่งที่เคยเกิดขึ้นใน transactions ที่ผ่านมา

## commonly-used options for YUM
**Options** | **Purpose**
--- | ---
-C | run จากหน่วยความจำ cache ของระบบ
--security | แพ็คเกจที่สามารถช่วยแก้ปัญหาด้านความปลอดภัย
-y | ตอบตกลงกับทุกๆคำถาม
--skip-broken | ข้ามแพ็คเกจที่ก่อให่เกิดปัญหาไป
-v | แสดงรายละเอียด

นี่เป็นเพียง commands และ options ของ YUM ที่มีการใช้โดยทั่วไปเท่านั้น แต่ YUM นั้นยังมี command และ options ที่น่าสนใจอีกมากมาย สามารถดูตัวอย่างได้ตามรูปด้านล่าง
![alt text](https://access.redhat.com/sites/default/files/images/yumcheat_01_0.png "YUM Command Cheat Sheet")
![alt text](https://access.redhat.com/sites/default/files/images/yumcheat_02_0.png "YUM Command Cheat Sheet")



นอกจากนี้นั้น YUM ยังมี plugin ที่น่าสนใจเช่น **yum-skip-broken** ที่ทำให้สามารถตรวจสอบแพ็คเกจสำหรับปัญหา dependency และข้ามตัวที่มีปัญหาได้

## install yum-skip-broken

```
$ sudo yum -y install yum-skip-broken
```

ตัวอย่างผลลัพธ์

```
Loading "fastestmirror" plugin
Loading mirror speeds from cached hostfile
 * base: mirror.steadfast.net
 * updates: mirror.steadfast.net
 * addons: centos-distro.cavecreek.net
 * extras: mirrors.liquidweb.com
Setting up Install Process
Parsing package install arguments
Resolving Dependencies
--> Running transaction check
---> Package yum-skip-broken.noarch 0:1.1.10-9.el5.centos set to be updated
--> Finished Dependency Resolution

Dependencies Resolved

=============================================================================
 Package                 Arch       Version          Repository        Size 
=============================================================================
Installing:
 yum-skip-broken         noarch     1.1.10-9.el5.centos  base               11 k

Transaction Summary
=============================================================================
Install      1 Package(s)         
Update       0 Package(s)         
Remove       0 Package(s)         

Total download size: 11 k
Downloading Packages:
(1/1): yum-skip-broken-1. 100% |=========================|  11 kB    00:00     
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing: yum-skip-broken              ######################### [1/1] 

Installed: yum-skip-broken.noarch 0:1.1.10-9.el5.centos
Complete!
```

**วิธีการรับมือการข้ามแพ็คเกจที่มีปัญหา dependency**

พิมพ์คำสั่งด้านล่าง

```
$ sudo yum -y upgrade --skip-broken
```

หรือ

```
$ sudo yum -y update --skip-broken
```

# วิธีการแก้ปัญหา yum errors บน CentOS, RHEL หรือ Fedora

สำหรับ CentOS, RHEL และ Fedora นั้น YUM ใช้สำหรับการติดตั้ง อัพเดต และลบแพ็คเกจ RPM ออก ซึ่งในบางครั้งการติดตั้งแพ็คเกจผ่าน YUM นั้นอาจจะพบ errors ได้ ซึ่งด้านล่างนี้จะเป็นวิธีการแก้ปัญหาเหล่านั้นอย่างคร่าวๆ

## 1. วิธีแก้ **404** Errors
เมื่อ metadata ที่มีการดาวน์โหลดผ่าน YUM นั้นมีความล้าสมัย ในบางครั้งก็จะก่อให้เกิด **404** **errors** ได้ดังตัวอย่างด้านล่าง

```
Loaded plugins: fastestmirror
base                                                     | 3.7 kB     00:00
base/primary_db                                          | 4.4 MB     00:09
extras                                                   | 3.5 kB     00:00
http://mirror.steadfast.net/centos/6.4/extras/x86_64/repodata/e0e507c76dc5e5aa66c1f32632b9dc0a9759d97031ab5a028562a7cb7be6e294-primary.sqlite.bz2:
[Errno 14] PYCURL ERROR 22 - "The requested URL returned error: 404
Not Found"
Trying other mirror.
http://mirrors.seas.harvard.edu/centos/6.4/extras/x86_64/repodata/e0e507c76dc5e5aa66c1f32632b9dc0a9759d97031ab5a028562a7cb7be6e294-primary.sqlite.bz2:
[Errno 14] PYCURL ERROR 22 - "The requested URL returned error: 404
Not Found"
Trying other mirror.
```

ซึ่งวิธีการแก้ 404 errors นี่ สามารถทำได้ด้วยการล้างข้อมูล metadata ด้วยคำสั่งด้านล่าง

```
$ sudo yum clean metadata
```

หรือล้างข้อมูลของ yum cache ทั้งหมด

```
$ sudo yum clean all
```

## 2. วิธีแก้ **Connection** **Failure** Errors
ปัญหานี้เกิดจากการที่ไม่สามารถเชื่อมต่อกับ repository ของ servers ได้ด้วยเหตุผลบางอย่าง แต่ถ้ายังสามารถ ping เซิร์ฟเวอร์ได้โดยไม่มีปัญหาใดๆ ให้ลองตรวจสอบดูว่าระบบนั้นทำงานอยู่เบื้องหลัง proxy หรือเปล่า ถ้าเกิดว่า YUM นั้นทำงานอยู่เบื้องหลัง proxy แต่ไม่มีการระบุ proxy ใน yum configuration ก็อาจจะเกิดปัญหาข้างต้นได้ดังตัวอย่างด้านล่าง

```
Loaded plugins: fastestmirror, presto
Loading mirror speeds from cached hostfile
Could not retrieve mirrorlist
http://mirrorlist.centos.org/?release=6&arch=x86_64&repo=os error was
14: PYCURL ERROR 7 - "Failed to connect to
2a02:2498:1:3d:5054:ff:fed3:e91a: Network is unreachable"
Error: Cannot find a valid baseurl for repo: base

http://mirror.nexcess.net/CentOS/6.4/os/x86_64/repodata/repomd.xml:
[Errno 14] PYCURL ERROR 7 - "couldn't connect to host"
Trying other mirror.
http://mirrordenver.fdcservers.net/centos/6.4/os/x86_64/repodata/repomd.xml:
[Errno 14] PYCURL ERROR 7 - "couldn't connect to host"
Trying other mirror.
http://mirrors.cmich.edu/centos/6.4/os/x86_64/repodata/repomd.xml:
[Errno 14] PYCURL ERROR 7 - "couldn't connect to host"
Trying other mirror.
```

ซึ่งวิธีการ configure ตัว proxy ใน YUM configuration นั้นก็คือ

```
$ sudo vi /etc/yum.conf
```

ตัวอย่างผลลัพธ์

```
[main]
proxy=http://proxy.com:8000
```

## 3. วิธีแก้ **Metadata** **Checksum** Errors
ปัญหานี้สามารถเกิดได้จากการที่ metadata ที่ถูกดาวน์โหลดด้วย YUM นั้นไม่ได้รับการอัพเดตจนทำให้ล้าสมัยไป ดังตัวอย่างด้านล่าง

```
epel/pkgtags                                             | 466 kB     00:14     
http://mirror.steadfast.net/epel/6/x86_64/repodata/pkgtags.sqlite.gz: [Errno -1] Metadata file does not match checksum
Trying other mirror.
```

สามารถแก้ได้ด้วยการล้างข้อมูล metadata ด้วยคำสั่ง

```
$ sudo yum clean metadata
```

## 4. วิธีแก้ **Yum** **Lock** Errors
ต้นเหตุของปัญหานี้มักจะมาจาก PackageKit ซึ่งมีหน้าที่อัปเดตอัตโนมัติบนระบบที่มีการใช้ Red hat ซึ่งกระบวนการทำงานของ PackageKit จะเริ่มโดยอัตโนมัติเมื่อมีการเปิดเครื่อง ทำให้เกิด yum lock ดังตัวอย่าง

```
Loaded plugins: langpacks, presto, refresh-packagekit
Existing lock /var/run/yum.pid: another copy is running as pid 1880.
Another app is currently holding the yum lock; waiting for it to exit...
  The other application is: PackageKit
    Memory : 178 M RSS (586 MB VSZ)
    Started: Tue Jul  9 09:43:17 2013 - 00:12 ago
    State  : Sleeping, pid: 1880
```

ซึ่งวิธีแก้ก็คือการปิด PackageKit บนระบบ ซึ่งสามารถทำได้ดังนี้

## Disable PackageKit Temporarily

```
$ sudo yum install --disableplugin=refresh-packagekit <package-name>
```

## Disable PackageKit Permanently

```
$ sudo systemctl disable packagekitd
```

หรือเปิด /etc/yum/pluginconf.d/refresh-packagekit.conf ด้วย text editor และเปลี่ยน enabled=1 เป็น enabled=0

## Remove PackageKit Altogether

```
$ sudo yum remove PackageKit
```

เมื่อรีบูตเครื่องใหม่ ก็จะไม่มีปัญหา yum lock error แล้ว

## 5. วิธีแก้ **Repository** **Database** **Read** Errors
ปัญหานี้สามารถเกิดได้เมื่อคำสั่ง yum ถูกรบกวนระหว่างที่กำลังดาวน์โหลด repository ของฐานข้อมูลอยู่ ทำให้การบันทึกข้อมูลนั้นไม่เสร็จสิ้น และทำให้เกิดความเสียหายดังตัวอย่าง

```
Loaded plugins: langpacks, refresh-packagekit
Error: Error reading from file /var/cache/yum/x86_64/20/rpmfusion-free-updates/1461ed771601e7963990534c16584ab963d9c9f4eea94348ba357b93ab3c621f-primary.sqlite.bz2: compressed file ended before the logical end-of-stream was detected
```

ซึ่งปัญหานี้ก็สามารถแก้ได้ด้วยการล้างข้อมูลตามคำสั่งด้านล่าง

```
$ sudo yum clean metadata
```

## 6. วิธีแก้ **Repository** **Metadata** **Read** Errors
ปัญหานี้เกิดจากการที่ตัว metadata ของ yum เกิดความขัดข้อง

```
removing mirrorlist with no valid mirrors: /var/cache/yum/i386/6/updates/mirrorlist.txt
Error: Cannot find a valid baseurl for repo: updates
```

วิธีแก้นั้นก็คือการล้างข้อมูลทั้งหมดด้วยคำสั่งด้านล่าง

```
$ sudo yum clean all
```

## 7. วิธีแก้ **Packages** **Database** **Error**
ปัญหานี้เกิดจากการที่ฐานข้อมูลของ local RPM นั้นเกิดวามเสียหาย หรือขาดหายไป วิธีแก้คือการสร้างฐานข้อมูลของ RPM ขึ้นมาใหม่ด้วยคำสั่งด้านล่าง

```
$ sudo rm -f /var/lib/rpm/__db*
$ sudo db_verify /var/lib/rpm/Packages
$ sudo rpm --rebuilddb
$ sudo yum clean all
```

## reference
1. https://www.redhat.com/sysadmin/how-manage-packages
2. https://th.linux-console.net/?p=13759#:~:text=YUM%20%E0%B8%A2%E0%B9%88%E0%B8%AD%E0%B8%A1%E0%B8%B2%E0%B8%88%E0%B8%B2%E0%B8%81%20Yellowdog%20Updater%20Modified%20%E0%B9%80%E0%B8%84%E0%B8%A3%E0%B8%B7%E0%B9%88%E0%B8%AD%E0%B8%87%E0%B8%A1%E0%B8%B7%E0%B8%AD%E0%B8%88%E0%B8%B1%E0%B8%94%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%81%E0%B8%9E%E0%B9%87%E0%B8%84%E0%B9%80%E0%B8%81%E0%B8%88%E0%B8%AA%E0%B8%B3%E0%B8%AB%E0%B8%A3%E0%B8%B1%E0%B8%9A%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%81%E0%B8%A3%E0%B8%B0%E0%B8%88%E0%B8%B2%E0%B8%A2%E0%B8%95%E0%B8%B2%E0%B8%A1%20RPM%20%E0%B9%80%E0%B8%8A%E0%B9%88%E0%B8%99,%E0%B9%81%E0%B8%A5%E0%B8%B0%20CentOS%20%E0%B9%81%E0%B8%A5%E0%B8%B0%E0%B8%AD%E0%B8%B7%E0%B9%88%E0%B8%99%E0%B9%86%20%E0%B8%95%E0%B8%B1%E0%B8%A7%E0%B8%88%E0%B8%B1%E0%B8%94%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%81%E0%B8%9E%E0%B9%87%E0%B8%84%E0%B9%80%E0%B8%81%E0%B8%88%20YUM%20%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87%E0%B9%81%E0%B8%9E%E0%B9%87%E0%B8%84%E0%B9%80%E0%B8%81%E0%B8%88%E0%B8%88%E0%B8%B2%E0%B8%81%E0%B9%81%E0%B8%9E%E0%B9%87%E0%B8%84%E0%B9%80%E0%B8%81%E0%B8%88.rpm%20%E0%B9%81%E0%B8%A5%E0%B8%B0%E0%B8%97%E0%B8%B5%E0%B9%88%E0%B9%80%E0%B8%81%E0%B9%87%E0%B8%9A%E0%B8%8B%E0%B8%AD%E0%B8%9F%E0%B8%95%E0%B9%8C%E0%B9%81%E0%B8%A7%E0%B8%A3%E0%B9%8C%20%E0%B8%A1%E0%B8%B1%E0%B8%99%E0%B8%88%E0%B8%B1%E0%B8%94%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%81%E0%B8%9E%E0%B9%87%E0%B8%84%E0%B9%80%E0%B8%81%E0%B8%88%E0%B8%88%E0%B8%B2%E0%B8%81%E0%B8%97%E0%B8%B5%E0%B9%88%E0%B9%80%E0%B8%81%E0%B9%87%E0%B8%9A%E0%B8%A3%E0%B8%B0%E0%B8%9A%E0%B8%9A%E0%B9%81%E0%B8%A5%E0%B8%B0%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%9E%E0%B8%B6%E0%B9%88%E0%B8%87%E0%B8%9E%E0%B8%B2%E0%B9%81%E0%B8%9E%E0%B9%87%E0%B8%84%E0%B9%80%E0%B8%81%E0%B8%88%E0%B9%82%E0%B8%94%E0%B8%A2%E0%B8%AD%E0%B8%B1%E0%B8%95%E0%B9%82%E0%B8%99%E0%B8%A1%E0%B8%B1%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2%E0%B9%81%E0%B8%9E%E0%B9%87%E0%B8%84%E0%B9%80%E0%B8%81%E0%B8%88
3. https://www.golinuxcloud.com/yum-command-in-linux/
4. https://access.redhat.com/articles/yum-cheat-sheet
5. https://www.cyberciti.biz/faq/centos-rhel-fedora-yum-missing-dependency/
6. https://www.xmodulo.com/how-to-fix-yum-errors-on-centos-rhel-or-fedora.html
7. https://www.xmodulo.com/disable-packagekit-centos-fedora-rhel.html
