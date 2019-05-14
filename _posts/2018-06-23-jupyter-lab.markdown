---
layout:	post
title:	"Jupyter Lab : Interactive Programming"
date:	2018-06-23
---

  ![](/img/1*l1XLXj-1x14z8hqWG7Ik3Q.png)ผมสนใจเรื่องการเขียนโปรแกรมแบบที่ไม่ต้องมาเปิดสร้างโปรเจค คอมไพล์อะไรกันเยอะๆเสียเวลาอยู่แล้ว หลังๆนี้ก็ชอบลองเขียนโปรแกรมแนว notebook ที่มันจะมีคำอธิบายแทรกอยู่กับ code ที่ execute กันให้ดูทีละบรรทัด แล้วแสดงผลลัพธ์ออกมาเลย

ที่เด็ดที่สุด คือ ถ้าผลลัพธ์เป็น รูป เป็นเสียง ก็แสดงออกมาเลยไม่ต้องเอาผลลัพธ์ไปโยนไปใส่อะไรเพื่อแสดงอีก

![](/img/1*gULDGXMbsX_ZS87uswup6A.png)ที่เคยเห็น มีเครื่องมือหลักๆตามนี้

1. [Jupyter](http://jupyter.org/index.html) — ตัวนี้ดูจะเก่าแก่สุด นิยมมากในหมู่พวก data scientist เมื่อไม่นานมานี้เพิ่งออก Jupyter Lab ที่ใช้งานง่ายขึ้นมาก
2. [Swift Playground](https://www.apple.com/swift/playgrounds/) — สำหรับสาวกผู้รัก Swift อันนี้อยากจะชอบแต่ทำใจชอบลำบากเพราะมันช้า
3. [Observable](https://beta.observablehq.com/) — อันนี้น่าเล่นมาก เป็น JS อยู่บนเวป มีคอนเซปน่าสนใจหลายอย่าง เช่น graph execution, async ยังใหม่และล้ำไปหน่อย
#### Installation

เป็นสาวก เราถือว่า มี [brew](https://brew.sh/) อยู่ในเครื่องอยู่แล้วละกันนะ ตอนแรกลง python3 ก่อน ใครใช้ Linux หรือ Windows ก็ไปหาวิธีลงกันเอง

brew install python3เสร็จแล้วก็ลง package Jupyter Lab ผ่าน pip3

pip3 install jupyterlabแพกเกจอื่นๆอันนี้ไม่จำเป็นต้องลง แต่ถ้าลงจะเล่น Jupyter สนุกขึ้นอีกเยอะ แนะนำว่าลงไปเถอะ เดี๋ยวก็ได้ใช้ สำหรับช่วยคำนวณและวาดกราฟ

pip3 install numpy scipy matplotlib pandas scikit-learn#### Usage

Jupyter ไม่ต้องมีโปรเจคอะไรยุ่งยาก cd เข้าไปใน directory โล่งๆ แล้วเริ่มใช้ได้เลย

> mkdir myproject  
> cd myproject  
> jupyter labเสร็จแล้วมันจะเปิด browser ให้เอง พร้อมกับโหลด <http://localhost:8888/lab> เอง

![](/img/1*WzrwkXKQ8vxUvs4H5mHeZg.png)![](/img/1*-LEgoL273VtS1ctOpf3LDg.png)#### Interactive Programming

เวลาเราพิมพ์อะไรใน Jupyter ผลลัพธ์ของบรรทัดนั้นๆ ก็ออกมาแสดงได้เลย

![](/img/1*hdWNbYdNlXzWxbGJhYn1-w.png)![](/img/1*w1XWnKbnD2pHSUa0aiupEA.png)![](/img/1*73im3ES7kW9qyHSBGum4dw.png)#### Markdown Documentation

คอมเมนท์เป็น text ธรรมดามันจืดไป ใช้ markdown บรรยายได้เลย

![](/img/1*Q6wBWSkB5yKOOMTQkdy79Q.jpeg)![](/img/1*9jDKYmxKQ88MuumBvp9DPA.jpeg)![](/img/1*PuGLaOOE_k1pJQQxz1wBAw.png)ถ้าต้องการเปลี่ยน cell ไหนกลับเป็น code ก็กด Esc ออกมาเป็น Command Mode แล้วกดปุ่ม Y

B - Insert Cell in newline  
Y - Change Cell to Code  
M - Change Cell to Markdown  
Esc - Exit to Command Mode#### Rich Output

ถ้า cell ไหน มีผลลัพธ์เป็น matplotlib ก็สามารถจะ render ออกมาเป็นรูปสวยๆ ได้เลย

กด B สร้าง Cell ใหม่ แล้วก็อปโค้ดนี้แปะลงไป เสร็จแล้วก็กด Ctrl + ⮐

import matplotlib.pyplot as pltdata = [1,2,3,5,8,13,21]  
plt.plot(data)![](/img/1*-dl_-oeynMagCj-pJIw1xA.png)#### Publish to nbviewer

สำหรับ notebook ที่เขียนเสร็จแล้ว จะแชร์ออกไปให้คนอื่นดู​ ก็ทำได้ด้วยการเอาไปแปะไว้ที่ public hosting (Github / Gist ก็เป็นตัวเลือกที่ดี) จากนั้นก็เอา nbviewer ชี้มาที่ url นั้นก็จะได้ notebook สวยๆ ไปดู

คิดว่าสร้าง repo ใน GitHub เป็นกันแล้วนะ สมมติว่าอยู่ใน repo หน้าตาเป็นแบบนี้

![](/img/1*ixE7PFB941s-sWWrdvX19w.png)จริงๆ แล้ว GitHub ก็ render Jupyter Notebook ได้ระดับหนึ่งแล้ว แต่ถ้าอยากให้สวยขึ้นไปอีกต้องเอาลิงก์ไปไว้ที่ nbviewer

![](/img/1*xPwj1ClPFIJ8BcuV7uL6zQ.png)![](/img/1*HHmUY3Q-vGLae-AJpDu5Yg.png)จากนั้นเข้าไปที่ <https://nbviewer.jupyter.org> แล้วก็แปะ​ URL ลงไป

![](/img/1*FtjSVx9Hy-H-S4QE8qWtBQ.png)จากนั้นก็ copy URL เอาไปใช้ได้เลย สังเกตว่า render ได้เร็วกว่า github มาก

![](/img/1*SIzeDKF7ZvNCI-z-cdCFwA.png)  