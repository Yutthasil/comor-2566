# Docker

Docker คือแพลตฟอร์มซอฟต์แวร์ที่ช่วยให้สามารถสร้าง ทดสอบ และติดตั้งแอปพลิเคชั่นที่ใช้ได้จริงอย่างรวดเร็ว โดยลักษณะการทำงานจะบรรจุซอฟท์แวร์ลงไปในหน่วยที่เป็นมาตรฐานเรียกว่า **คอนเทนเนอร์** 
โดยภายในคอนเทนเนอร์จะมีทุกสิ่งที่ซอฟท์แวร์ต้องใช้ในการเรียกใช้งาน รวมถึงไลบรารี เครื่องมือระบบ โค้ด และรันไทม์ โดยที่คุณจะสามารถติดตั้งใช้ได้จริงและปรับขนาดแอปพลิเคชั่นให้เหมาะกับสภาพแวดล้อมและสามารถเรียกใช้ได้อย่างรวดเร็ว [1]

## วิธีการใช้งาน Docker บนระบบปฏิบัติการ Linux [2]

1. ทำการเปิด terminal โดยใช้คำสั่ง Ctrl + Alt + T

2. ทำการลบ Docker file ที่มีอยู่ในเครื่องโดยใช้คำสั่ง

        sudo apt-get remove docker docker-engine docker.io

3. ก่อนทำการติดตั้ง ให้เช็คว่าเครื่องรันอยู่บนเวอร์ชั่นล่าสุดก่อนโดยใช้คำสั่ง

        sudo apt-get update

4. ทำการลง Docker โดยใช้คำสั่งดังนี้

        sudo apt install docker.io

    เมื่อรับแจ้งให้ดำเนินการต่อให้กด Y บนแป้นพิมพ์แล้ว Enter

5. ทำการลง dependency package โดยใช้คำสั่ง


        sudo snap install docker

6. ก่อนทำการทดสอบ Docker ให้เช็คเวอร์ชั่นของ Docker ก่อนโดยใช้คำสั่ง


        docker --version

7. สั่งให้ docker ไปเตรียมเอา Container Image มาเตรียมไว้ในเครื่อง [3]

        sudo docker run hello-world

8. ทำการเช็คว่า docker ได้นำ Container Image มาเตรียมไว้แล้ว โดยใช้คำสั่ง

        sudo docker images

9. แสดง Container Image ทั้งหมดโดยใช้คำสั่ง 

        sudo docker ps -a

10. เช็ค State ของ Container Image 

        sudo docker ps


## Reference

https://aws.amazon.com/th/docker/ [1]

https://www.simplilearn.com/tutorials/docker-tutorial/how-to-install-docker-on-ubuntu [2]

https://www.saladpuk.com/basic/docker-1/exercise01 [3]


