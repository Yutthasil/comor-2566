
# Option และ Command ทั้งหมดของคำสั่ง lastcomm

<div align="center" style="width: 100%; margin: auto;">
<table style="width: 100%; border-collapse: collapse;">
	
| Options                 | Description                | Example   | Result |
| :---------------:  | :---------------------: | :-----------------: | :----------------: |
| --user name | แสดงรายการบันทึกสำหรับผู้ใช้ที่มีชื่อนี้ | lastcomm --user theerarat | <img align="right" width="100%" src="image/lastcommUser.png"> |
| --command name | แสดงรายการบันทึกสำหรับชื่อคำสั่ง | lastcomm --command sudo | <img align="right" width="100%" src="image/lastcommCommand.png"> |
| -tty name | แสดงรายการบันทึกสำหรับชื่อ tty | lastcomm --tty tty1 | <img align="right" width="100%" src="image/lastcommTty.png"> |
| -f filename, --file filename | อ่านจากชื่อไฟล์แทนไฟล์บัญชีของระบบ | lastcomm -f hehehe | <img align="right" width="100%" src="image/lastcommFile.png"> |
| --ahz hz | ใช้แฟล็กนี้เพื่อบอกโปรแกรมว่า AHZ ควรเป็นอย่างไร (เป็นเฮิรตซ์)  คำสั่งนี้จะพยายามดูไฟล์ acct ที่สร้างบนเครื่องอื่นซึ่งมีลำดับไบต์และรูปแบบไฟล์เหมือนกับเครื่องปัจจุบันของคุณ แต่มีค่า AHZ ที่แตกต่างกัน | lastcomm -ahz 5 | <img align="right" width="100%" src="image/lastcommAhz.png"> |
| -p, --show-paging | แสดงสถิติเพจ | lastcomm -p | <img align="right" width="100%" src="image/lastcommShowPaging.png"> |
| --debug | แสดงข้อมูลภายในอย่างละเอียด | lastcomm --debug | <img align="right" width="100%" src="image/lastcommDebug.png"> |
| --version | แสดง version | lastcomm --version | <img align="right" width="100%" src="image/lastcommVersion.png"> |
| --help | แสดงคำสั่งทั้งหมด | lastcomm --help | <img align="right" width="100%" src="image/lastcommHelp.png"> |
</table>
</div>
