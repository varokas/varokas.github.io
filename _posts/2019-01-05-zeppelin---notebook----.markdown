---
layout:	post
title:	"Zeppelin — Notebook สำหรับApache Sparks"
date:	2019-01-05
---

  ![](/img/1*bJigZtBnodqs4vw8QbezEA.png)สำหรับคนที่ติดใจเขียนโปรแกรมแบบ notebook ผ่าน jupyter ตอนนี้มีโปรเจคที่ค่อนข้างใหม่ชื่อ Apache Zeppelin เหมาะมากสำหรับสาย data ที่ใช้ Apache Sparks
<!--more-->

ข้อดีหลักๆ

* Integrate กับ Sparks และ SQL เนียนๆ visualization สวยๆ
* วาง widget ไว้แนวขวางได้ด้วย ไม่ต้องเป็นแนวนอนอย่างเดียว
* ปรับแต่ง UI ได้ด้วย Angular
#### วิธีลง

ลง Sparks ก่อน เวลาลงถ้าไม่ได้ใช้ java8 ตัว brew จะบ่นๆ

brew cask install homebrew/cask-versions/java8  
brew install apache-sparkจากนั้นลง Zeppelin ได้เลย ไม่จำเป็นต้องลง scala

brew install apache-zeppelin#### ใช้งาน

เรียกใช้ server แบบนี้

zeppelin-daemon.sh startจากนั้นก็ไปที่ <http://localhost:8080> ได้เลย ตัว script จะรันแบบ daemon ไม่จำเป็นต้องเปิด terminal ทิ้งไว้

![](/img/1*t6TTUf1nh3lktld-U-V6bg.png)เปิดตัวอย่าง Basic Features ขึ้นมาแล้วก็เลือก Run All paragraphs

![](/img/1*MUoSJyRMxXiHoCriPSn3eA.png)![](/img/1*tys4wJ80RajCGMLiAQr3fw.png)เมื่อรันเสร็จแล้วสามารถไปดู Job ใน Sparks UI ได้ด้วย

![](/img/1*UE-oV1Fa2XvnBuoJhxZrpg.png)![](/img/1*WiuFWLgZ9CO8871ujtStLw.png)#### Troubleshooting

ถ้าตอนที่รันเจอ error แบบนี้

error: scala.reflect.internal.MissingRequirementError: object scala in compiler mirror not found.ให้ลบ Java Version อื่นๆ ออกจากเครื่อง เก็น Java8 ที่ลงผ่าน brew ไว้อย่างเดียว

  
