# IDE

IDE หรือ Integrated development enviroment คือ Software สำเร็จรูปที่มีเครื่องมืออำนวยความสะดวกให้ Code Developer ใช้ในการพัฒนา Software ซึ่งหลักๆ จะประกอบด้วย 3 อย่างนี้ คือ Source Code Editor, Build Automation Tools และ Debugger

<br>

## IDE on Linux

### 1. GNOME builder 
   <br>
   
   โดย IDE นี้จะเป็น Software Open source ที่ใช้พัฒนา Application หรือ Software ใน Desktop Environment ของ GNOME (GNU Object Model Environment).
   <br>
   
   ข้อดีของ GNOME Builder :
   <br>
   
   - มีคีย์ลัดที่สะดวกสะบาย
   - สามารถใช้งานร่วมกับ Git ได้
   - รองรับ Application Flatpak.
   - สามารถพัฒนาได้หลายภาษา
   <br>

   Command Line สำหรับติดตั้ง Gnome Builder

   <br>

   ```bash
   sudo apt install gnome-builder
   ```
   <br>
   
   ตัวอย่าง Gnome Builder :
   
   <br>
   
   <img src='https://i.redd.it/4eq8430ko5971.png' width='1280' height='640'>

<br>
   
### 2. Eclipse
   <br>

   เป็น Software Open Source ที่สามารถพัฒนาได้หลายภาษา เช่น Java, HTML, C และอื่นๆ โดยจุดเด่นของ Software นี้คือการที่มี plug-in ให้ใช้มากมาย ซึ่งอำนวยความสะดวกต่อ Code Developer เป็นอย่างมาก
   <br>
   
   ข้อดีของ Eclipse :
   <br>

   - มี Eclipse Plug-in ช่วยในการพัฒนา Code
   - ติดตั้งง่าย
   - พัฒนาได้หลายๆ ภาษา
   - ใช้งานร่วมกับ J2SDK ได้ทุก Version
   <br>
   
   ขั้นตอนการติดตั้ง Eclipse บน Linux:
   <br>
   
   1. เช็คว่ามี snap หรือไม่
      <br>
      
      ```bash
      snap version
      ```
      <br>
   2. ถ้าไม่มี snap ให้ติดตั้งโดยคำสั่งนี้
      <br>
      
      ```bash
      apt install snapd -y
      ```
      <br>
   3. เชื่อม /var/lib/snapd/snap กับ /snap ใน home directory หลังติดตั้งเสร็จ
       <br>
      
       ```bash
       ln -s /var/lib/snapd/snap /snap
       ```
       <br>
   4. หลังจากนั้น ก็ update snap package ด้วยคำสั่งนี้
       <br>
      
       ```bash
       snap refresh
       ```
       <br>
   5. ติดตั้ง Eclipse ผ่าน Snap Store
       <br>
      
       ```bash
       snap install --classic eclipse
       ```
       <br>
   หรือสามารถติดตั้งโดย [Eclipse Installer](https://www.eclipse.org/downloads/packages/) ก็ได้
   <br>
   
   ตัวอย่าง Eclipse :
   <br>
   
   <img src='https://storage.googleapis.com/ubuntu-18/images/install-eclipse-ubuntu-18.jpg' width='1280' height='640'>

<br>

### 3. NetBeans IDE
   <br>

   เป็น Software Open Source โดยเน้นพัฒนาภาษา Java เป็นหลัก แต่ก็สามารถใช้พัฒนาภาษาอื่นได้เช่นกัน โดนจุดเด่นของ Software นี้คือความสามารถในการพัฒนาเป็น modules ได้

   <br>

   ข้อดีของ NetBeans IDE :
   <br>

   - สามารถแยกโปรแกรมเป็น Modules ทำให้พัฒนาได้ง่าย
   - มีระบบที่สามารถตรวจ Syntax ของ Code
   - มี Add-on ให้ใช้เพื่อพัฒนาภาษาอื่นนอกจาก Java

   <br>

   การติดตั้ง NetBeans IDE บน Linux (Debian/Ubuntu):
   <br>
   
   1. ติดตั้ง JDK (Java Development Kit)
      <br>

      ```bash
      sudo apt install -y openjdk-11-jdk
      ```

      <br>

   2. หลังจากนั้นให้เช็คว่าเครื่งของคุณติดตั้ง JDK เรียบร้อบหรือไหมโดยคำสั่ง
      <br>

      ```bash
      java -version
      ```

      <br>

   3. เมื่อติดตั้งเรียบร้อยแล้ว ต่อมาก็ใช้คำสั่งนี้เพื่อ Download NetBeans DEB Package
      <br>

      ```bash
      wget https://github.com/codelerity/netbeans-installers/releases/download/v16-build1/apache-netbeans_16-1_amd64.deb
      ```

      <br>

   4. หลังจากนั้นก็ติดตั้ง NetBeans DEB Package
      <br>

      ```bash
      sudo dpkg -i apache-netbeans_*_amd64.deb
      ```

      <br>
   
   การติดตั้งผ่าน Linux Installer (สามารถติดตั้งได้กับระบบปฏิบัติการ Linux ส่วนใหญ่)
   <br>

   1. หากบนเครื่องไม่มี JDK ให้ติดตั้งก่อน
      <br>

      Debian
      <br>

      ```bash
      sudo apt install -y openjdk-11-jdk
      ```

      <br>

      RHEL
      <br>

      ```bash
      sudo yum install java-11-openjdk
      ```

      <br>

      Arch Linux
      <br>

      ```bash
      sudo pacman -S jdk-openjdk
      ```

      <br>

      openSUSE
      <br>

      ```bash
      wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.rpm
      sudo rpm -ivh jdk-17_linux-x64_bin.rpm
      ```

      <br>

   2. Download Installer
      <br>

      ```bash
      wget https://archive.apache.org/dist/netbeans/netbeans-installers/14/Apache-NetBeans-14-bin-linux-x64.sh
      ```

      <br>

   3. ทำให้ Installer เป็น File Executable
      <br>

      ```bash
      chmod +x Apache-NetBeans-14-bin-linux-x64.sh
      ```
      <br>

   4. Run Installer Script
      <br>

      ```bash
      sudo ./Apache-NetBeans-14-bin-linux-x64.sh
      ```
      <br>

   ตัวอย่าง Netbeans IDE (Debian) :
   <br>

   <img src='https://linux.how2shout.com/wp-content/uploads/2022/01/Apache-Launch-NetBeans-on-Debian-11.png' width='900' height='640'>

<br>

### 4. Visual Code Studio (VS Code)
   <br>

   Visual Code Studio เป็น IDE แบบ Open Source ที่สามารถใช้งานได้หลาย Platform เช่น Linux, Mac OS และ Windows โดยรองรับได้การพัฒนาหลายภาษา เช่น C, C++, CSS, HTML, Java, JavaScript และอื่นๆ

   <br>

   ข้อดีของ Visual Code Studio :
   <br>

   - รองรับหลายภาษา
   - ใช้งานกับ Project ใหญ่ๆ ได้
   - มีส่วนเสริม (Extension) อำนวยความสะดวกในการพัฒนา

   <br>

   การติดตั้งผ่าน Snap (Ubuntu):
   <br>

   1. ติดตั้ง package ของ VS Code
      <br>
      
      ```bash
      sudo snap install --classic code
      ```
      <br>

   2. ตรวจสอบว่าติดตั้งเรียบร้อยหรือไหมด้วยคำสั่งนี้
      <br>

      ```bash
      code --version
      ```
      <br>

   การติดตั้งผ่าน APT (Ubuntu) :
   <br>

   1. Update Repository เพื่อสามารถติดตั้ง VS Code เวอร์ชั่นล่าสุด ด้วยคำสั่งนี้
      <br>

      ```bash
      sudo apt update
      ```
      <br>

   2. ติดตั้ง Package Dependencies
      <br>

      ```bash
      sudo apt install software-properties-common apt-transport-https wget -y
      ```
      <br>

   3. Import GPG Key เพื่อเช็คความถูกต้องของ Package ที่ลงมา
      <br>

      ```bash
      wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
      ```
      <br>

   4. เพิ่ม Repository ของ VS Code
      <br>

      ```bash
      sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
      ```
      <br>

   5. ติดตั้ง VS Code
      <br>

      ```bash
      sudo apt install code
      ```
      <br>

   6. ตรวจสอบการติดตั้ง VS Code ด้วยคำสั่งนี้
      <br>

      ```bash
      code --version
      ```
      <br>

   ตัวอย่าง Visual Studio Code (Ubuntu):
   <br>

   <img src='https://www.tecmint.com/wp-content/uploads/2020/05/Install-Visual-Studio-Code-in-Ubuntu.png' width='1000' height='640'>

   <br>

# Compiler
<br>

Compiler หรือ คอมไพรเลอร์ เป็น Software พิเศษที่ทำหน้าที่นำ Source Code ไป Compile เพื่อแปลงจากภาษาที่มนุษย์เข้าใจไปเป็นภาษาที่ตัวเครื่องคอมพิวเตอร์เข้าใจ โดยถ้าในกระบวนการ Compile ตรวจพบ Code ที่ผิดพลาดหรือ Syntax ไม่ถูกต้อง Compiler จะแจ้งให้ Developer ทราบเพื่อแก้ไขให้ถูกต้อง
<br>

## Compiler on Linux

- GCC (GNU Compiler Collection)
  <br>

  เป็น Compiler ที่ใช้ในการ Compile ภาษาโดยเฉพาะ C, C++ และอื่นๆ เเต่เดิม GCC ออกแบบให้เป็น Compiler บนระบบปฏิบัติการ GNU ปัจจุบันเปิดให้ใช้ในแบบ Free Software โดยเป็น GNU Public Lincense
  <br>

  ### ข้อดีของ GCC :

  - เป็น Free Software
  - มี Bugs น้อย
  - เป็น Compiler พื้นฐานในหลาย ๆ
  <br>

  ### วิธีติดตั้ง :

  Debian, Ubuntu และ Linux Mint

  ```bash
  apt install build-essentials
  ```

  RedHat Enterprise Linux, Fedora, CentOS, และ Amazon Linux

  ```bash
  yum group install 'Development Tools'
  ```
  <br>
  
  ### ตัวอย่าง GCC :
  <br>
  
  <img src='https://linuxconfig.org/wp-content/uploads/2022/03/00-how-to-install-gcc-the-c-compiler-on-ubuntu-22-04-lts-jammy-jellyfish-linux.png'>
  
# Refference

- IDE
  - [IDE on Linux](https://github.com/madbob/awesome-linux-dev?tab=readme-ov-file#editors-and-ide)
  - [IDE คืออะไร?](https://stackpython.medium.com/ide-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3-%E0%B9%81%E0%B8%99%E0%B8%B0%E0%B8%99%E0%B8%B3-ide-integrated-development-environment-%E0%B8%AA%E0%B8%B3%E0%B8%AB%E0%B8%A3%E0%B8%B1%E0%B8%9A%E0%B8%A1%E0%B8%B7%E0%B8%AD%E0%B9%83%E0%B8%AB%E0%B8%A1%E0%B9%88%E0%B8%AB%E0%B8%B1%E0%B8%94%E0%B9%80%E0%B8%82%E0%B8%B5%E0%B8%A2%E0%B8%99-python-f03e4cc8d343)
<br>

- GNOME Builder
  - [What is GNOME Builder? & Command Line Download](https://ubunlog.com/th/gnome-builder-ide-proposito-general/#google_vignette)
  - [ข้อดี Gnome Builder (TH)](https://th.linux-console.net/?p=8505)
  - [Download GNOME Builder](https://wiki.gnome.org/Apps/Builder/Downloads)
  - [Gnome Builder Example Picture](https://i.redd.it/4eq8430ko5971.png)
<br>

- Eclipse
  - [Eclipse คืออะไร? (TH)](https://www.aosoft.co.th/article/312/Eclipse-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3.html)
  - [ประโยชน์ของ Eclipse (TH)](https://eclipse4sl.org/%E0%B8%9B%E0%B8%A3%E0%B8%B0%E0%B9%82%E0%B8%A2%E0%B8%8A%E0%B8%99%E0%B9%8C%E0%B8%82%E0%B8%AD%E0%B8%87-eclipse-%E0%B9%82%E0%B8%9B%E0%B8%A3%E0%B9%81%E0%B8%81%E0%B8%A3%E0%B8%A1%E0%B8%AA%E0%B8%B3%E0%B8%AB/)
  - [How to Download](https://adamtheautomator.com/how-to-install-eclipse/#Installing_Eclipse_on_Linux)
  - [Eclipse Installer](https://www.eclipse.org/downloads/packages/)
  - [Eclipse Official Site](https://www.eclipse.org/)
  - [Eclipse on Linux Example Picture](https://storage.googleapis.com/ubuntu-18/images/install-eclipse-ubuntu-18.jpg)
<br>

- NetBeans IDE
  - [NetBeans คืออะไร?](https://www.aosoft.co.th/article/316/%E0%B8%A3%E0%B8%B9%E0%B9%89%E0%B8%88%E0%B8%B1%E0%B8%81%E0%B8%81%E0%B8%B1%E0%B8%9A-NetBeans.html)
  - [NetBeans คืออะไร?](https://www.mindphp.com/%E0%B8%84%E0%B8%B9%E0%B9%88%E0%B8%A1%E0%B8%B7%E0%B8%AD/73-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3/2239-netbeans-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3.html)
  - [How to Download (EN) & ข้อดีและประโยชน์ของ NetBeans](https://www.makeuseof.com/how-to-install-netbeans-on-linux/)
  - [How to Download (TH)](https://www.thaicreate.com/java/java-netbean-ide-windows.html)
  - [NetBeans IDE Example Picture](https://linux.how2shout.com/wp-content/uploads/2022/01/Apache-Launch-NetBeans-on-Debian-11.png)
<br>

- Visual Code Studio
  - [What is Visual Code Studio & How to Download (EN)](https://phoenixnap.com/kb/install-vscode-ubuntu)
  - [What is Visual Code Studio & How to Download ซึ่งมีวิธีของ Debian และ Linux Mint (TH)](https://th.linux-console.net/?p=1771)
  - [Pros and Cons of Visual COde Studio (EN)](https://www.quora.com/What-are-the-pros-and-cons-of-Visual-Studio-Code-as-an-IDE)
<br>

- Compiler
  - [What is Compiler? (TH)](https://www.mindphp.com/%E0%B8%84%E0%B8%B9%E0%B9%88%E0%B8%A1%E0%B8%B7%E0%B8%AD/73-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3/3596-compiler-%E0%B8%84%E0%B8%AD%E0%B8%A1%E0%B9%84%E0%B8%9E%E0%B8%A3%E0%B9%80%E0%B8%A5%E0%B8%AD%E0%B8%A3%E0%B9%8C-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3.html)
  - [What is Compiler (EN)](https://www.techtarget.com/whatis/definition/compiler)
  - [Compiler on Linux](https://gcc.gnu.org/)
  - [How to Download GCC](https://www.incredibuild.com/integrations/gcc)
  - [GCC on Linux Pros and Cons](https://www.quora.com/What-are-the-advantages-and-disadvantages-or-limitations-of-using-one-instead-of-the-other-compiler-in-C-and-C-Linux-i-e-GCC-or-G)
  - [GCC on Linux Example Picture](https://linuxconfig.org/wp-content/uploads/2022/03/00-how-to-install-gcc-the-c-compiler-on-ubuntu-22-04-lts-jammy-jellyfish-linux.png)
