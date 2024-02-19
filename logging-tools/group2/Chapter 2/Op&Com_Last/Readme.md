# Option และ Command ทั้งหมดของคำสั่ง last

## Option ทั้งหมดของคำสั่ง last
<div align="center" style="width: 100%; margin: auto;">
<table style="width: 100%; border-collapse: collapse;">
	
| Options                 | Description                | Example   | Result |
| :---------------:  | :---------------------: | :-----------------: | :----------------: |
| -<number> | แสดงกี่บรรทัด | last -5 | <img align="right" width="100%" src="image/lastNumber.png"> |
| -a, --hostlast | แสดง hostname ในคอมลัมสุดท้าย | last -a | <img align="right" width="100%" src="image/lastHostlast.png"> |
| -d, --dns | แปลงเลข IP เป็น hostname | last -d | <img align="right" width="100%" src="image/lastDns.png"> |
| -f, --file <file> | ใช้ไฟล์อื่นแทน /var/log/wtmp | last -f /var/log/dmseg | <img align="right" width="100%" src="image/lastFile.png"> |
| -F, --fulltimes | พิมพ์เวลาและวันที่เข้าสู่ระบบและออกจากระบบแบบเต็ม | last -F | <img align="right" width="100%" src="image/lastFulltime.png"> |
| -i, --ip | แสดงที่อยู่ IP ในรูปแบบจุด | last -i | <img align="right" width="100%" src="image/lastIP.png"> |
| -n, --limit <number> | ระบุจำนวนบรรทัดที่จะแสดง | last -n 5 | <img align="right" width="100%" src="image/lastLimit.png"> |
| -R, --nohostname | ไม่แสดงฟิลด์ hostname | last -R | <img align="right" width="100%" src="image/lastNohostname.png"> |
| -s, --since <time> | แสดงตั้งแต่เวลานี้เป็นต้นมา | last -s “2024-02-07 00:00:00” | <img align="right" width="100%" src="image/lastSince.png"> |
| -t, --until <time> | แสดงรายการที่ย้อนกลับไปตามเวลาที่กำหนด | last -t “2024-01-19 00:00:00” | <img align="right" width="100%" src="image/lastUntil.png"> |
| -p, --present <time> | แสดงรายการที่ตรงตามเวลานั้น | last -p “2024-02-08 15:28:25” | <img align="right" width="100%" src="image/lastPresent.png"> |
| -w, --fullnames | แสดงชื่อผู้ใช้และโดเมนแบบเต็ม | last -w | <img align="right" width="100%" src="image/lastFullnames.png"> |
| -x, --system | แสดงรายการการปิดระบบและการเปลี่ยนแปลงระดับการดำเนินการ | last -x | <img align="right" width="100%" src="image/lastSystem.png"> |
| --time-format <format> | แสดง timestamps ในรูปแบบ (notime/short/full/iso) | last --time-format notime | <img align="right" width="100%" src="image/lastTimeFormat.png"> |
| -h, --help | แสดง help | last --h | <img align="right" width="100%" src="image/lastHelp.png"> |
| -V, --version | แสดง version | last --V | <img align="right" width="100%" src="image/lastVersion.png"> |
</table>
</div>
