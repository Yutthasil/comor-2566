# LOCALIZATION 🫧🍶

>[!IMPORTANT]
**Locale**  หรือ รูปแบบข้อมูลท้องถิ่น เป็นส่วนหนึ่งของระบบ Internationalization (i18n) และ Localization (l10n) เพื่อให้โปรแกรมต่าง ๆ สามารถที่จะแสดง และจัดการข้อมูลในแต่ละภาษาและท้องถิ่น ได้อย่างถูกต้องเหมาะสม Locale ต่าง ๆ ของแต่ละภาษาและท้องถิ่นจะมีลักษณะเป็น ส่วน ๆ ซึ่งสามารถเพิ่มเข้าไปในระบบ Localization ต่าง ๆ ได้ และแต่ละ Locale จะเป็น อิสระจากกัน รูปแบบข้อมูลท้องถิ่นอาจจะรวมไปถึงข้อมูลสำหรับจัดการข้อความที่ซับซ้อน เช่นการจัดเรียง การตัดคำ และอื่น ๆ


## Install the Localize CLI

อันดับแรก ทำการติดตั้ง localize ลงใน CLI

With Python and pip installed, use pip to install the Localize CLI :

#### `linux, OS X or Unix` 
        > sudo pip install --ignore-installed localize
        
#### `To upgrade an existing Localize CLI installation, use the --upgrade option :` 
        > pip install --upgrade localize


<a id="POSIX"></a>
## POSIX Locale

ระบบ **Localization ใน Linux** ส่วนใหญ่จะอาศัยระบบหลัก ๆ คือ POSIX Locale ซึ่งอยู่ใน C Library เช่น GLIBC ซึ่งใน POSIX Locale การทำงานจะใช้ค่าตัวแปรระบบ (LC_...) ซึ่ง จะประกอบด้วยส่วนต่าง ๆ ดังนี้

* **LANG** ใช้สำหรับกำหนด Locale ทั้งหมด (มีผลให้มีการเปลี่ยนแปลง Locale เฉพาะทั้งหมด) ซึ่งจะมีการกำหนดไว้ล่วงหน้า
* **LC_ALL** ใช้สำหรับกำหนด Locale ที่จะใช้งาน ในกรณีที่ Locale เฉพาะไม่มีการกำหนด
* **LC_CTYPE** คือ Locale ที่จะใช้สำหรับจำแนกตัวอักษร
* **LC_COLLATE** คือ Locale ที่จะใช้สำหรับการเทียบตัวอักษร
* **LC_MONETARY** คือ Locale ที่จะใช้สำหรับข้อมูลเกี่ยวกับเงินตรา
* **LC_NUMBERIC** คือ Locale ที่จะใช้สำหรับแก้ไขตัวเลข
* **LC_TIME** คือ Locale ที่จะใช้สำหรับข้อมูลวันที่และเวลา
* **LC_MESSAGE** คือ Locale ที่จะใช้สำหรับข้อความต่างๆ

และยังมีส่วนของข้อมูล Locale อีกคือ 

* **Charmap** คือตารางข้อมูลของรหัสอักษร คือ TIS-620 2533
* **Reportoiremap** คือตารางข้อมูลของรหัสอักษรภาษาไทย บนรหัส Unicode

อีกระบบที่นิยมใช้คือ ISO/IEC 14652 ซึ่งเป็นส่วนต่อขยายจาก POSIX LOCALE ซึ่งประกอบด้วย

* **LC_PAPER** Locale ที่จะใช้สำหรับขนาดกระดาษ
* **LC_NAME** คือ Locale ที่จะใช้สำหรับรูปแบบชื่อสกุล
* **LC_ADDRESS** คือ Locale ที่จะใช้สำหรับที่อยู่
* **LC_TELEPHONE** คือ Locale ที่จะใช้สำหรับโทรศัพท์
* **LC_MESUREMENT** คือ Locale ที่จะใช้สำหรับการวัด
* **LC_VERSIONS** คือ Locale ที่จะใช้สำหรับบอกรุ่นที่ของ Locale

<a id="ThaiLocale"></a>
## Thai Locale

ซึ่งสำหรับ ภาษาไทย ก็มี Locale อยู่ในชื่อ th_TH ปัจจุบันและ ใช้ได้ใน รหัสอีกษร TIS-620 (ISO/IEC 8859-11) และ UTF-8

การใช้งานปกติสามารถใช้งานได้โดยกำหนด ตัวแปรระบบ LANG เป็น th_TH หรือตัวแปร Localization ที่ต้องการ ซึ่งปกติจะใช้ รหัสตัวอักษร TIS-620 ถ้าต้องการใช้รหัสตัวอักษร อื่นให้กำหนดโดยใส่ . ตามด้วยรหัสตัวอีกษรที่ต้องการ ในปัจจุบัน ที่ใช้ได้คือ TIS-620 และ UTF-8

<a id="localecmd"></a>
##  Locale Command 📂

### How to View System Locale in Linux 🍡

ใช้ **local** หรือ **localectl** utility
```
$ locale
LANG=en_US.UTF-8 <br>
LANGUAGE=en_US <br>
LC_CTYPE="en_US.UTF-8" <br>
LC_NUMERIC=ro_RO.UTF-8
LC_TIME=ro_RO.UTF-8
LC_COLLATE="en_US.UTF-8"
LC_MONETARY=ro_RO.UTF-8
LC_MESSAGES="en_US.UTF-8"
LC_PAPER=ro_RO.UTF-8
LC_NAME=ro_RO.UTF-8
LC_ADDRESS=ro_RO.UTF-8
LC_TELEPHONE=ro_RO.UTF-8
LC_MEASUREMENT=ro_RO.UTF-8
LC_IDENTIFICATION=ro_RO.UTF-8
LC_ALL=
```

```
$ localectl status

System Locale: LANG=en_US.UTF-8
      LANGUAGE=en_US
      VC Keymap: n/a
      X11 Layout: us
      X11 Model: pc105
```

สามารถดูข้อมูลเพิ่มเติมเกี่ยวกับตัวแปรสภาพแวดล้อมได้ เช่น **LC_TIME** ซึ่งเก็บรูปแบบข้อมูลเป็นเวลาและวันที่
```
$ locale -k LC_TIME

abday="Sun;Mon;Tue;Wed;Thu;Fri;Sat"
day="Sunday;Monday;Tuesday;Wednesday;Thursday;Friday;Saturday"
abmon="Jan;Feb;Mar;Apr;May;Jun;Jul;Aug;Sep;Oct;Nov;Dec"
mon="January;February;March;April;May;June;July;August;September;October;November;December"
am_pm="AM;PM"
d_t_fmt="%a %d %b %Y %r %Z"
d_fmt="%m/%d/%Y"
t_fmt="%r"
t_fmt_ampm="%I:%M:%S %p"
era=
era_year=""
era_d_fmt=""
alt_digits=
era_d_t_fmt=""
era_t_fmt=""
time-era-num-entries=0
time-era-entries="S"
week-ndays=7
week-1stday=19971130
week-1stweek=1
first_weekday=1
first_workday=2
cal_direction=1
timezone=""
date_fmt="%a %b %e %H:%M:%S %Z %Y"
time-codeset="UTF-8"
alt_mon="January;February;March;April;May;June;July;August;September;October;November;December"
ab_alt_mon="Jan;Feb;Mar;Apr;May;Jun;Jul;Aug;Sep;Oct;Nov;Dec"
```

เพื่อแสดงรายการของ locale ที่ใช้ทั้งหมด ใช้คำสั่ง **locale -a**
```
$ locale -a

C
C.UTF-8
en_US.utf8
POSIX
```
<a id="setsys"></a>
### How to Set System Locale in Linux 🎢

หากต้องการเปลี่ยนหรือตั้งค่าภาษาในระบบ ให้ใช้โปรแกรม **update-locale**, **LANG** จะช่วยให้สามารถตั้งค่า locale สำหรับระบบทั้งหมดได้ 

ส่วนคำสั่งต่อไปนี้จะตั้งค่า LANG เป็น **en_IN.UTF-8** และลบค่าสำหรับ LANGUAGE.
```
$ sudo update-locale LANG=LANG=en_IN.UTF-8 LANGUAGE
OR
$ sudo localectl set-locale LANG=en_IN.UTF-8
```

หรือเพื่อกำหนด**ค่าพารามิเตอร์**ของ locale ที่แน่นอน ให้แก้ไขดังตัวอย่าง เช่น
```
$ sudo update-locale LC_TIME=en_IN.UTF-8
OR
$ sudo localectl set-locale LC_TIME=en_IN.UTF-8
```

>[!TIP]
> ถ้าจะหาการตั้งค่า global locale ให้เข้าไปใน   ```/etc/default/locale```
> หรือถ้าระบบของคุณมาจาก Red hat ให้ใช้ ```/etc/sysconfig/i18n```

หากจะตั้งค่า global local สำหรับ single user, สามารถเปิดไฟล์  **~/.bash_profile** และเพิ่มบรรทัด ตามนี้
```
LANG="en_IN.utf8"
export LANG
```

สำหรับข้อมูลเพิ่มเติม ให้ดูในหน้าคำสั่งของ locale, update-locale และ localectl ในเอกสารคู่มือ (man pages)
```
$ man locale
$ man update-locale
$ man localectl
```
###  Update the System Locale and Language 📍

1. ตรวจสอบ locale ของระบบปัจจุบัน :
```
sudo localectl
```
2. แสดงรายการทุก locale ที่พร้อมใช้งาน :
```
sudo localectl list-locales
```
3. ตั้งค่า locale เป็น British English และ UTF-8 encoding :
```
sudo localectl set-locale en_GB.utf8
```

> [!NOTE]
> note : ระบบ locale กำหนดภาษาและการเข้ารหัสชุดอักขระที่ใช้สำหรับการนำเสนอข้อมูลบนอุปกรณ์แสดงผลและบนหลายๆ แอปพลิเคชัน GUI ด้วย ตัวเลือก locale มักถูกระบุในรูปแบบดังนี้ LANGUAGE_COUNTRY.CODESET[@MODIFIERS] ภาษาเป็นรหัสภาษาตามมาตรฐาน ISO 639 เช่น en สำหรับภาษาอังกฤษ; ประเทศเป็นรหัสประเทศตามมาตรฐาน ISO 3166 เช่น GB สำหรับสหราชอาณาจักรและประเทศอังกฤษ; CODESET เป็นชุดอักขระหรือการเข้ารหัส, เช่น utf-8 ดังนั้น, ในตัวอย่างนี้, locale คือ en_GB.utf8.

4. list รายการทุก keymap ที่พร้อมใช้งาน (กดปุ่ม q เพื่อออก) :
```
sudo localectl list-keymaps
```
5. ตั้ง keymap เป็น British English :
```
sudo localectl set-keymap gb
```
6. ทดสอบว่าการเปลี่ยนแปลงได้ถูกนำไปใช้งานแล้วเรียบร้อย โดยการพิมพ์ในหน้าต่าง terminal ถ้าใช้คีย์บอร์ด US English qwerty คีย์ " และ @ ควรจะสลับตำแหน่งกัน

### Update the System Date and Time 🌟

ใช้คำสั่ง timedatectl เพื่อตั้งค่าวันที่และเวลาของระบบ คำสั่งจะอัปเดตนาฬิกาเวลาจริง (RTC) ซึ่งเรียกว่า hardware clock รวมถึงนาฬิกาของระบบที่รักษาโดย kernel ด้วย

1. ตรวจสอบวันและเวลาปัจจุบัน :
```
sudo timedatectl
```
2. list รายการ time zone ทั้งหมด ที่พร้อมใช้งาน (กดปุ่ม q เพื่อออก) :
```
sudo timedatectl list-timezones
```
3. ค้นหาโซนเวลาที่ต้องการ โดยใช้ขีดล่างสำหรับชื่อที่มีสองคำ ตัวอย่างเช่น เพื่อหา Pacific Daylight Time (PDT) :
```
sudo timedatectl list-timezones | grep 'Los_Angeles'
```
4. ตั้งต่า time zone ของคุณ
```
sudo timedatectl set-timezone America/Los_Angeles
```
5. ตั้งค่าวันและเวลาด้วยวิธีด้วยตนเอง:
```
sudo timedatectl set-time '2100-01-01 00:00:00'
```

> [!NOTE]
> หาก NTP services ถูกตั้งค่าให้ใช้งานอยู่ วันที่และเวลาของระบบของคุณจะถูกปรับเพื่อให้ตรงกับเซิร์ฟเวอร์ NTP ที่กำหนดค่าไว้ ในสถานการณ์นั้น จะไม่สามารถแก้ไขวันที่หรือเวลาโดยตรงบนระบบของคุณได้

### Changing the time zone 🦫

popular tools are :
```
$ dpkg-reconfigure tzdata
$ redhat-config-date
$ system-config-date
```
<a id="tzselect"></a>
### Changing timezone with tzselect 🍀

* โปรแกรม tzselect ใช้สำหรับตั้งค่าค่าตัวแปร TZ สำหรับตำแหน่งที่ต้องการ
* ผู้ใช้สามารถเลือกประเทศและสถานที่ในเมนูเพื่อดูค่าที่ตัวแปร TZ ควรจะมีค่าอย่างไร
* คำสั่ง tzselect แสดงค่าสำหรับตัวแปร แต่มันไม่ได้ตั้งค่าตัวแปรนั้น
* ตัวอย่างเช่น หากผู้ใช้อยู่ในรัฐอิซาโกน่า และใช้คำสั่ง tzselect มันจะแจ้งให้ผู้ใช้ตั้งค่าตัวแปร TZ เป็นค่า "America/Phoenix"
* เมื่อใช้คำสั่ง tzselect จะถามคำถามที่เกี่ยวข้องกับทวีปหรือสถานที่ในมหาสมุทรของคุณ

## References
* https://linux.thai.net/pub/thailinux/cvs/docs/thai-howto2/Thai-HOWTO/Thai-HOWTO-2.html
* https://www.baeldung.com/linux/locale-environment-variables
* https://docs.oracle.com/en/learn/oracle-linux-localization/#update-the-system-locale-and-language
* https://developers.localizejs.com/docs/localize-cli
* https://www.tecmint.com/set-system-locales-in-linux/
* https://www.secur.cc/how-to-localize-linux/
