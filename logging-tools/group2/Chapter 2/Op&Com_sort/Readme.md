# Option และ Command ทั้งหมดของคำสั่ง sort
## Option ทั้งหมดของคำสั่ง sort
### คำสั่งพื้นฐานของ sort

<div align="center" style="width: 100%; margin: auto;">
<table style="width: 100%; border-collapse: collapse;">	
  
| Options                 | Description                | Example   |
| :---------------:  | :---------------------: | :-----------------: |
| -r, --reverse | sortข้อมูลจากตัวสุดท้ายไปยังตัวแรก | sort -r [File.log] | 
| -n, --numberic-sort  | sort ตามค่าตัวเลขของข้อมูลจากน้อยไปมาก | sort -n [File.log] |
| -k, --key=KEYDEF | ระบุ field ที่จะใช้ sort | sort -k [number field] [File.log] |
| -b, --ignore-leading-blanks | ไม่สนช่องว่าง หรือ ทำให้ช่องว่างไม่มีผลต่อการ sort | sort -b [File.log] |
| -t, --field-separtor=SEP| กำหนดตัวแบ่งข้อมูล | sort -t "," [File.log] |
| -u, --unique| ลบบรรทัดที่ซ้ำกันออก | sort -u [File.log] |
| -o, -- output=FILE| เรียงลำดับข้อมูลโดยเขียนไว้ใน output.txt | sort -o [File.log] > output.txt |
</table>
</div>

### คำสั่งขั้นสูงของ sort
<div align="center" style="width: 100%; margin: auto;">
<table style="width: 100%; border-collapse: collapse;">
  
| Options                 | Description                | Example   |
| :---------------:  | :---------------------: | :-----------------: |
| -M, --mont-sort | เรียงลำดับตามเดือน | sort -M [File.log] | 
| -h, --human-numeric-sort | เรียงลำดับตามขนาดของไฟล์ | sort -h [File.log] |
| -g, --general-numeric-sort | เรียงลำดับตามกลุ่ม | sort -g [File.log] |
</table>
</div>
