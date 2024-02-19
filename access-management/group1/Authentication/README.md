# What is Authentication?

**Authentication** คือ การรับรองความถูกต้องเป็นกระบวนการที่ระบบคอมพิวเตอร์ระบุผู้ใช้ที่สามารถเข้าถึงระบบ อุปกรณ์ หรือเครือข่าย เป็นกลไกการควบคุมการเข้าถึงที่ระบุผู้ใช้ผ่านข้อมูลระบุตัวตนที่กำหนดไว้ล่วงหน้า เช่น ชื่อผู้ใช้และรหัสผ่าน

ผู้ดูแลระบบสามารถใช้โปรโตคอลการตรวจสอบสิทธิ์เพื่อควบคุมสิ่งที่ผู้ใช้แต่ละคนสามารถเข้าถึงได้หรือไม่สามารถเข้าถึงได้ การทำเช่นนี้ ผู้ใช้ที่ไม่ได้รับอนุญาตจะไม่สามารถเข้าถึงข้อมูลที่ละเอียดอ่อน ตัวอย่างเช่น ผู้ดูแลระบบสามารถควบคุมสิ่งที่ผู้ใช้ X สามารถเข้าถึงได้โดยไม่ต้องเปิดเผยข้อมูลที่ละเอียดอ่อนใดๆ ที่เกี่ยวข้องกับผู้ใช้ Y

การรับรองความถูกต้องช่วยยับยั้งอาชญากรไซเบอร์ไม่ให้เข้าถึงเครือข่ายหรือระบบของคุณ การเข้าถึงโดยไม่ได้รับอนุญาตจะนำไปสู่การโจรกรรมข้อมูล การละเมิดกฎระเบียบ และสแปมแวร์หรือมัลแวร์อย่างหลีกเลี่ยงไม่ได้ Adobe, Yahoo และ Equifax เป็นหนึ่งในบริษัทชั้นนำที่มีประวัติการละเมิดข้อมูลล่าสุด

# Common Types of Authentication

เป็นไปไม่ได้ที่จะเข้าใจระบบการตรวจสอบความถูกต้องโดยไม่ทราบประเภทการตรวจสอบความถูกต้องทั่วไป ทีมรักษาความปลอดภัยจะพิจารณามาตรการรับมือเพื่อปรับปรุงเทคนิคของตนอยู่เสมอ นี่เป็นความพยายามในการต่อต้านความพยายามในการปรับปรุงอย่างต่อเนื่องของอาชญากรไซเบอร์

หากไม่มีการปรับปรุงที่โดดเด่น กลยุทธ์การตอบสนองต่อเหตุการณ์ และระบบรักษาความปลอดภัยระดับแนวหน้า บริษัทต่างๆ จะไม่สามารถยืนหยัดต่อความท้าทายที่เกี่ยวข้องกับการรับรองความถูกต้องของศตวรรษที่ 21 ได้

ต่อไปนี้เป็นประเภทการรับรองความถูกต้อง 5 อันดับแรกที่ผู้ดูแลระบบ Linux ทุกคนควรรู้

* **Password-Based Authentication (การรับรองความถูกต้องด้วยรหัสผ่าน)** - รหัสผ่านเป็นประเภทการตรวจสอบสิทธิ์ที่ใช้บ่อยที่สุด มีอยู่ในรูปแบบของตัวอักษร อักขระพิเศษ หรือตัวเลข ผู้ดูแลระบบและผู้ใช้จะต้องสร้างรหัสผ่านที่ซับซ้อนซึ่งประกอบด้วยตัวเลือกต่างๆ เพื่อการปกป้องสูงสุด แต่เมื่อใช้รหัสผ่าน ให้ระวังสุขอนามัยที่ไม่ดีและการโจมตีแบบฟิชชิ่ง เนื่องจากอาจทำให้ความปลอดภัยของคุณอ่อนแอลง
* **Certificate-Based Authentication (การรับรองความถูกต้องตามใบรับรอง)** - นี่เป็นอีกวิธีหนึ่งที่เทคโนโลยีสามารถใช้เพื่อระบุผู้ใช้ อุปกรณ์ หรือเครื่องจักร ใบรับรองดิจิทัลเหล่านี้เป็นเอกสารอิเล็กทรอนิกส์ที่มีแนวคิดเดียวกันกับที่ใช้ในหนังสือเดินทางหรือหนังสือเดินทาง ประกอบด้วยคีย์สาธารณะของผู้ใช้แต่ละรายและลายเซ็นดิจิทัล ผู้ออกใบรับรองจะออกใบรับรองเหล่านี้ ซึ่งมีประโยชน์ในการพิสูจน์ความเป็นเจ้าของคีย์สาธารณะ
* **Multi-Factor Authentication (การรับรองความถูกต้องแบบหลายปัจจัย)** - วิธีการตรวจสอบสิทธิ์นี้ต้องใช้วิธีอิสระในการระบุผู้ใช้มากกว่าหนึ่งวิธี MFA เพิ่มการรักษาความปลอดภัยหลายชั้น รวมถึงการทดสอบ captcha รหัสสมาร์ทโฟน ลายนิ้วมือ และการจดจำใบหน้า มันมีประโยชน์ในการป้องกันการแฮ็กบัญชี
* **Token-Based Authentication (การรับรองความถูกต้องตามโทเคน)** - ประเภทการตรวจสอบสิทธิ์เหล่านี้ทำให้ผู้ใช้สามารถป้อนข้อมูลประจำตัวของตนได้เพียงครั้งเดียว เมื่อพวกเขาทำเช่นนั้น พวกเขาจะได้รับสตริงอักขระที่เข้ารหัส (โทเค็น) ที่ไม่ซ้ำกันซึ่งพวกเขาจะใช้ในการเข้าถึงระบบที่ได้รับการป้องกัน โทเค็นดิจิทัลเป็นหลักฐานเพียงพอว่าคุณได้รับอนุญาตให้เข้าถึงระบบ
* **Biometric Authentication (การรับรองความถูกต้องตามชีวภาพ)** - วิธีนี้ใช้ข้อมูลชีวภาพของแต่ละบุคคลหรือคุณลักษณะทางชีววิทยาที่เป็นเอกลักษณ์เพื่อให้สามารถเข้าถึงได้ ไบโอเมตริกซ์ ได้แก่ การจดจำใบหน้า เครื่องสแกนลายนิ้วมือ การจดจำเสียง และเครื่องสแกนดวงตา

# Common Linux Authentication System
ในสภาพแวดล้อม Linux การรับรองความถูกต้องยังคงเป็นข้อกำหนดของ syadmin อย่างเป็นทางการสำหรับการเข้าสู่ระบบ และบนแพลตฟอร์ม Linux ส่วนใหญ่ **/etc/passwd** มักจะใช้สำหรับจัดเก็บข้อมูลผู้ใช้ ไฟล์ข้อความประกอบด้วยข้อมูลเข้าสู่ระบบของผู้ใช้ การเข้ารหัสรหัสผ่าน รหัสผู้ใช้เฉพาะที่เป็นตัวเลข (UID) และรหัสกลุ่มตัวเลข (GUD) ไฟล์ข้อความยังมีโฮมไดเร็กตอรี่ของผู้ใช้และเชลล์ที่ต้องการ

ดังนั้น รายการทั่วไปใน /etc/passwd มักจะดูใกล้เคียงกับสิ่งนี้;

``` Bash
ken:x:1000:1000:KenTech:/home/ken:/bin/ bash
```

ดังที่คุณจะพบว่าอาร์เรย์ของระบบการรับรองความถูกต้องและการอนุญาตมักใช้ในขอบเขต Linux การออกแบบแต่ละแบบมีประโยชน์สำหรับวัตถุประสงค์หรือการใช้งานที่แตกต่างกัน แต่ที่น่าสนใจกว่านั้นคือ คุณสามารถใช้โปรโตคอลการอนุญาตได้มากกว่าหนึ่งโปรโตคอลในเครื่องคอมพิวเตอร์เครื่องเดียว

ยิ่งไปกว่านั้น ระบบทั้งหมดนี้ยังมีความสัมพันธ์กับ PAM ไม่ทางใดก็ทางหนึ่ง 

# What is Linux Single Sign - On (SSO)

Linux⁣ Single Sign On (SSO) เป็นวิธีการรับรองความถูกต้องที่ปลอดภัยซึ่งสามารถลด ⁢ความซับซ้อนและ ⁢ต้นทุน ⁤ ในการจัดการการเข้าถึงของผู้ใช้ในองค์กรขนาดใหญ่ ในระบบการลงชื่อเข้าระบบครั้งเดียว ผู้ใช้ ⁢จำเป็นต้องเข้าสู่ระบบเพียงครั้งเดียว⁣ ด้วยชุดข้อมูลรับรองชุดเดียวเพื่อ ⁢เข้าถึงหลายแอปพลิเคชัน

ระบบการรับรองความถูกต้องนี้มีข้อดีหลายประการ ซึ่งรวมถึง:

* **Reduced authentication cost (ลดต้นทุนการตรวจสอบสิทธิ์)**: ไม่จำเป็นต้องจัดการข้อมูลรับรองสำหรับแต่ละแอปพลิเคชันอีกต่อไป ซึ่งช่วยลดต้นทุนด้านไอทีในการควบคุมการเข้าถึงของผู้ใช้
* **Better visibility and contro (การมองเห็นและการควบคุมที่ดีขึ้น)**: SSO ช่วยให้ผู้ดูแลระบบ IT ควบคุมการเข้าถึงแอปพลิเคชันและข้อมูลต่างๆ ของผู้ใช้จากส่วนกลาง ช่วยให้กระบวนการอนุญาตง่ายขึ้นและทำให้ติดตามกิจกรรมของผู้ใช้ได้ง่ายขึ้น
* **Improved security (การรักษาความปลอดภัยที่ได้รับการปรับปรุง)**: ‌SSO ปรับปรุง ⁢ความปลอดภัยโดยทำให้แน่ใจว่าผู้ใช้ตรวจสอบสิทธิ์ตนเองทุกปี และในบางกรณี โดยการกำหนดให้มีการตรวจสอบสิทธิ์แบบหลายปัจจัย
ระบบ Linux Single Sign On กำลังเป็นที่นิยมมากขึ้นเรื่อยๆ ในการลดความซับซ้อนในการรับรองความถูกต้องที่ปลอดภัย⁤ เทคโนโลยีที่เชื่อถือได้นี้สามารถให้ผลประโยชน์มากมาย รวมถึงการลดต้นทุน การมองเห็นและการควบคุมที่ดีขึ้น และการรักษาความปลอดภัยที่ดีขึ้น

ระบบ Linux Single Sign On กำลังเป็นที่นิยมมากขึ้นเรื่อยๆ ในการลดความซับซ้อนในการรับรองความถูกต้องที่ปลอดภัย⁤ เทคโนโลยีที่เชื่อถือได้นี้สามารถให้ผลประโยชน์มากมาย รวมถึงการลดต้นทุน การมองเห็นและการควบคุมที่ดีขึ้น และการรักษาความปลอดภัยที่ดีขึ้น

# Benefits of Implementing Linux SSO

Linux Single ‍Sign-On (SSO) เป็นกระบวนการที่อนุญาตให้ผู้ใช้เข้าสู่ระบบหลายระบบด้วยชื่อผู้ใช้ ⁢ และรหัสผ่านเดียว การนำเทคโนโลยีนี้มาใช้ให้ประโยชน์อันมีค่ามากมายแก่ธุรกิจ

* **Better Security(การรักษาความปลอดภัยที่ดีขึ้น)** : การใช้ Linux SSO ช่วยเพิ่มความแข็งแกร่ง ⁤ การปกป้องข้อมูลแบบอัตโนมัติ โดยการป้องกันไม่ให้แฮกเกอร์เข้าถึงหลายแอปพลิเคชันด้วยชุดข้อมูลรับรองชุดเดียว ด้วยการมีการตรวจสอบสิทธิ์เพียงจุดเดียว⁣ ผู้ใช้สามารถเข้าถึงแอปพลิเคชันได้อย่างปลอดภัยและรวดเร็ว⁣
* **Increased Productivity(ผลผลิตที่เพิ่มขึ้น)** : เนื่องจากผู้ใช้ต้องจำข้อมูลรับรองเพียงชุดเดียว ⁢ความยุ่งยากในการจดจำและป้อนรหัสผ่านหลายชุด⁤ จึงหมดไป สิ่งนี้ทำให้กระบวนการตรวจสอบความถูกต้องมีความคล่องตัวและราบรื่นยิ่งขึ้น ซึ่งท้ายที่สุดจะนำไปสู่ประสบการณ์ผู้ใช้ที่ดีขึ้นและประสิทธิภาพการทำงานที่เพิ่มขึ้น

นอกจากนี้ Linux SSO ⁣ ยังช่วยลดเวลา ‍และค่าใช้จ่ายที่เกี่ยวข้องกับการรับรองความถูกต้องของผู้ใช้ได้อย่างมาก ด้วย ⁢ กระบวนการที่เรียบง่าย การรับรองความถูกต้องสามารถจัดการได้อย่างสมบูรณ์ในพื้นหลัง ⁢ โดยไม่ต้องให้ตัวแทนฝ่ายบริการลูกค้าเข้ามาแทรกแซง สิ่งนี้ช่วยให้ธุรกิจต่างๆ สามารถมุ่งเน้นไปที่พื้นที่อื่นๆ ของการดำเนินงานของตนโดยที่เวลาและทรัพยากรถือเป็นสิ่งสำคัญ

# What is IDENTITY MANAGEMENT
IdM คือวิธีสร้างที่เก็บข้อมูลประจำตัว การตรวจสอบสิทธิ์แบบรวมศูนย์ การควบคุมโดเมนสำหรับบริการ Kerberos และ DNS และนโยบายการอนุญาต ทั้งหมดนี้บนระบบ Linux โดยใช้เครื่องมือ Linux แบบเนทีฟ แม้ว่าซอฟต์แวร์ระบุตัวตน/นโยบาย/การอนุญาตแบบรวมศูนย์จะไม่ค่อยใหม่นัก แต่การจัดการข้อมูลประจำตัวเป็นหนึ่งในตัวเลือกเดียวที่รองรับโดเมน Linux/Unix
Identity Management มอบสกินที่รวมเป็นหนึ่งสำหรับบริการเครือข่ายทั่วไปที่กำหนดมาตรฐาน รวมถึง PAM, LDAP, Kerberos, DNS, NTP และบริการใบรับรอง และช่วยให้ระบบ Red Hat Enterprise Linux ทำหน้าที่เป็นตัวควบคุมโดเมนได้
การจัดการข้อมูลประจำตัวจะกำหนดโดเมน โดยมีเซิร์ฟเวอร์และไคลเอ็นต์ที่แชร์บริการที่จัดการจากส่วนกลาง เช่น Kerberos และ DNS บทนี้จะอธิบายก่อนว่าการจัดการข้อมูลประจำตัวคืออะไร บทนี้ยังครอบคลุมถึงวิธีที่บริการเหล่านี้ทำงานร่วมกันภายในโดเมน และวิธีที่เซิร์ฟเวอร์และไคลเอนต์โต้ตอบกัน

**thank you for refference : https://logmeonce.com/resources/linux-single-sign-on/ , https://access.redhat.com/documentation/th-th/red_hat_enterprise_linux/6/html/identity_management_guide/introduction , https://linuxhint.com/linux-authentication-systems/**

