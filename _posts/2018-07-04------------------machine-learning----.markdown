---
layout:	post
title:	"จัดการเครื่องมือ Machine Learning ด้วย Conda"
date:	2018-07-04
---

  ![](/img/1*B5etcYpv-MSsxMxg94-A7w.png)เดี๋ยวนี้เริ่มเล่นเครื่องมือ ML ต่างๆ ตัว Python Environment มีหลาย dependency ตีกันมั่วไปหมด แล้วก็แชร์โค้ดให้เพื่อนลองเล่นยากต้องเขียนวิธีลง package ต่างๆ ไว้ใน README.md

มาลองใช้ Conda กันดูว่าจะช่วยได้ยังไง

#### Install

เนื่องจากเราเป็นสาวก ลงอะไรก็ง่าย แต่รอโหลดนานหน่อย

brew cask install anacondaเสร็จแล้วใส่บรรทัดนี้ไว้ใน .bash\_profile หรือ .zshrc

export PATH=/usr/local/anaconda3/bin:"$PATH"#### Create Environment

หลังจากนั้นเราก็สร้าง Environment ขึ้นมาใช้ได้ตามใจชอบ ซึ่งจะต่างกับใช้ virtualenv ตรงที่ environment พวกนี้จะสร้างไว้รวมกันที่เดียวไม่รก environment ที่ใช้

สมมติว่าเราจะสร้าง environment ไว้สำหรับลองเล่น Keras (ตั้งชื่อว่า keras)โดยใช้ python 3.7 ก็พิมพ์ตามนี้

conda create -n keras python=3.7![](/img/1*bl0rXLdISPeV63zhxv34ow.png)#### Activate/Deactivate Environment

สร้างเสร็จก็ switch เข้าไปที่ environment นั้นได้เลย

source activate kerasถ้าจะออกมาก็ใช้

source deactivateสังเกตว่าตอนที่เรา switch เข้าไป ตัว prompt จะมีชื่อ environment ในวงเล็บนำหน้า

![](/img/1*Ci7oPdiRPYRAxaMZ5KAjgQ.png)#### Install Packages

ตอนนี้ได้แต่ environement เปล่าๆ ยังไม่มีประโยชน์ ลองลง package ที่ต้องใช้ดู

conda install keras jupyterlabหลังจากเราลงไปแล้วก็เปิด jupyter lab แล้วใช้ keras ได้ทันที

![](/img/1*t4y3_WBqGLJQOusE3yltrQ.png)#### Share Environment

ของเด็ดอยู่ตรงนี้ คือ เราสามารถบอก spec ของ environment เราลงไฟล์ที่จะโยนงานไปให้เพื่อนทำต่อได้

conda env export > environment.ymlจากนั้นก็ checkin ไฟล์ environment.yml เข้าไปพร้อมกับโปรเจค

ถึงเวลาอีกฝั่งหนึ่ง clone git เสร็จแล้ว ก็สร้าง environment ได้เหมือนกันแบบนี้

conda env create -f environment.yml#### Reference

* <https://conda.io/docs/user-guide/tasks/manage-environments.html>
  