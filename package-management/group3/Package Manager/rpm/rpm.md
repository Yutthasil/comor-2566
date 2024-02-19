# RPM (Red Hat Package Manager)
## RPM คืออะไร 
RPM (Red Hat Package Manager) เป็น default open source และเป็น utility ใน package management ที่ค่อนข้างได้รับความนิยมสำหรับคนที่ใช้ Red Hat (ex. RHEL, CentOS และ Fedora) โดย RPM เป็นเครื่องมือที่ช่วยทำให้ผู้ใช้งาน หรือผู้ดูแลระบบสามารถทำการ install, update, uninstall, query, verify รวมไปถึงจัดการ package ในระบบปฏิบัติการ Unix/Linux ได้

## 5 basic modes for RPM command
**Command** | **Purpose**
--- | ---
 Install | ใช้สำหรับติดตั้งแพ็คเกจ RPM
 Remove | ใช้เพื่อลบ หรือยกเลิกการติดตั้งแพ็คเกจ RPM
 Update | ใช้เพื่ออัปเดตแพ็คเกจ RPM ที่มีอยู่
 Verify | ใช้เพื่อตรวจสอบแพ็คเกจ RPM
 Query | ใช้ในการสืบค้นแพ็คเกจ RPM

## RPM Command Options
**Command** | **Purpose**
--- | ---
-h, --hash | พิมพ์เครื่องหมายแฮชขณะติดตั้งแพ็คเกจ (เห็นได้ตอนดาวน์โหลด)
-l, --list | แสดงรายการไฟล์ในแพ็คเกจ
-s, --state	 | แสดงสถานะของไฟล์ที่อยู่ใน list
-v, --verbose | ทำให้ output ที่ออกมามีความละเอียดมากขึ้น


## การ Check dependencies ก่อนติดตั้ง RPM
การตรวจ dependencies ก่อนติดตั้งจะช่วยป้องกันปัญหาที่อาจเกิดขึ้นในกระบวนการติดตั้งหรือในการใช้งานแพ็คเกจนั้น ๆ ในภายหลังได้
```
sudo rpm -qpR [ ชื่อ package ]
```
  * **q** – บอกให้ RPM ทำการค้นหาแพ็คเกจ
  * **p** – ระบุแพ็คเกจที่จะค้นหา
  * **R** – แสดง requirements สำหรับแพ็คเกจ
### Example
```
[root@tecmint]# rpm -qpR BitTorrent-5.2.2-1-Python2.4.noarch.rpm

/usr/bin/python2.4
python >= 2.3
python(abi) = 2.4
python-crypto >= 2.0
python-psyco
python-twisted >= 2.0
python-zopeinterface
rpmlib(CompressedFileNames) = 2.6
```
credit: https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/

# Install
ขั้นตอนแรกของการติดตั้ง RPM คือเราจะต้องดาวน์โหลดไฟล์ RPM มาก่อน โดยสามารถทำได้ 2 วิธี
## Download RPM Files from the Internet
สามารถดาวน์โหลดไฟล์ RPM จากอินเทอร์เน็ตโดยใช้เว็บเบราว์เซอร์โดยตรง หรือใช้คำสั่ง wget (ถ้าไม่มีคำสั่งนี้ให้ทำการติดตั้งก่อน)

### การใช้งาน wget
```
wget [option] [URL]
```
### Example
```
wget https://example.com/path/to/your/package.rpm
```

## Download RPM Files from the Repository
ในส่วนนี้เราสามารถใช้ yum และ dnf ช่วยให้เราสามารถดาวน์โหลดไฟล์ RPM ได้

## Install RPM File
เมื่อเราดาวน์โหลดไฟล์ RPM มาเรียบร้อยแล้ว ขั้นตอนต่อไปคือการติดตั้งโดยใช้คำสั่ง rpm
```
sudo rpm -i [package_name]
```

## Check ว่าติดตั้ง rpm เรียบร้อยแล้ว
```
rpm -q  [package_name]
```
### Example
```
[root@tecmint]# rpm -q BitTorrent

BitTorrent-5.2.2-1.noarch
```
credit: https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/

## Remove
```
sudo rpm -e  [package_name]
```

## Update
```
sudo rpm -Uvh [package_name]
```
### Example
```
[root@tecmint]# rpm -Uvh nx-3.5.0-2.el6.centos.i686.rpm
Preparing...                ########################################### [100%]
   1:nx                     ########################################### [100%]
```
credit: https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/

## Verify
ใช้ตรวจสอบ package RPM ทั้งหมด
```
sudo rpm -Va
```
### Example
```
[root@tecmint]# rpm -Va

S.5....T.  c /etc/rc.d/rc.local
.......T.  c /etc/dnsmasq.conf
.......T.    /etc/ld.so.conf.d/kernel-2.6.32-279.5.2.el6.i686.conf
S.5....T.  c /etc/yum.conf
S.5....T.  c /etc/yum.repos.d/epel.repo
```
credit: https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/

## Query
 * ค้นหาไฟล์ของ RPM package
```
rpm -qf [ query name]
```
### Example
```
[root@tecmint]# rpm -qf /usr/bin/htpasswd

httpd-tools-2.2.15-15.el6.centos.1.i686
```
credit: https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/


 * ค้นหารายละเอียดของ package นั้น
```
rpm -qi [ query name]
```
### Example
```
[root@tecmint]# rpm -qi vsftpd

Name        : vsftpd				   Relocations: (not relocatable)
Version     : 2.2.2				   Vendor: CentOS
Release     : 11.el6				   Build Date: Fri 22 Jun 2012 01:54:24 PM BDT
Install Date: Mon 17 Sep 2012 07:55:28 PM BDT      Build Host: c6b8.bsys.dev.centos.org
Group       : System Environment/Daemons           Source RPM: vsftpd-2.2.2-11.el6.src.rpm
Size        : 351932                               License: GPLv2 with exceptions
Signature   : RSA/SHA1, Mon 25 Jun 2012 04:07:34 AM BDT, Key ID 0946fca2c105b9de
Packager    : CentOS BuildSystem <http://bugs.centos.org>
URL         : http://vsftpd.beasts.org/
Summary     : Very Secure Ftp Daemon
Description :
vsftpd is a Very Secure FTP daemon. It was written completely from
scratch.
```
credit: https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/

 * ค้นหา document ของ package นั้น
```
rpm -qdf (query document file)
```
### Example
```
[root@tecmint]# rpm -qdf /usr/bin/vmstat

/usr/share/doc/procps-3.2.8/BUGS
/usr/share/doc/procps-3.2.8/COPYING
/usr/share/doc/procps-3.2.8/COPYING.LIB
/usr/share/doc/procps-3.2.8/FAQ
/usr/share/doc/procps-3.2.8/NEWS
/usr/share/doc/procps-3.2.8/TODO
```
credit: https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/


# All Reference
1) https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/

2) https://phoenixnap.com/kb/how-to-install-rpm-file-centos-linux/

3) https://access.redhat.com/solutions/1189/

4) https://phoenixnap.com/kb/rpm-command-in-linux/

5) https://operavps.com/docs/install-rpm-file-in-linux/


