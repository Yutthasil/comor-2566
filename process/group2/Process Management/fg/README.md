# คำสั่ง`fg`
เป็นคำสั่งที่ใช้ในการย้ายงาน background ใน shell ปัจจุบันขึ้นมาทำงาน foreground
|อาร์กิวเมนต์|คำอธิบาย|ตัวอย่าง|
|---|-----------|-----|
|`%n`|อ้างอิงถึง ID ของงานนั้นๆ|`fg %1`|
|`%+` หรือ `%%`|อ้างอิงถึงงานปัจจุบัน|`fg %+`|
|`%-`|อ้างออิงถึงงานก่อนหน้า|`fg %-`|
|`%string`|อ้างอิงถึงงานใดก็ตามที่ขึ้นต้นด้วยคำนี้|`fg %sleep`|
|`%?string`|อ้างอิงถึงงานใดก็ตามที่ประกอบด้วยคำนี้|`fg %?leep`|
## ตัวอย่างการนำไปใช้
- แสดงรายการงานที่ทำงานอยู่ background
> jobs

![fgjobs.png](../../Assets/fg&bg/fgjobs.png)
- การย้ายงานที่ทำงานอยู่ background ขึ้นมาทำงานที่ foreground โดยอ้างอิงจาก ID
> fg %4

![fg4.png](../../Assets/fg&bg/fg4.png)
***
# แหล่งอ้างอิง
- https://www.geeksforgeeks.org/process-control-commands-unixlinux/
- https://ioflood.com/blog/fg-linux-command/
