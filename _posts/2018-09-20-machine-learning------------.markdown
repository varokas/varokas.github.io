---
layout:	post
title:	"Machine Learning สำหรับสาวกภาค 10.14"
date:	2018-09-20
---

  #### จบในห้านาที

#### Machine Learning มีขั้นตอนประมาณนี้

1. เก็บข้อมูล / หาข้อมูล
2. Train Model
3. Test Model
4. Export เอาไปใช้
วันนี้จะทำให้ดูบน CreateML ของ MacOS ตัวใหม่ ง่ายมาก 5 นาทีเสร็จแน่นอน (ไม่รวมเก็บข้อมูลนะ)

จริงๆ คือ จะเอาที่เคย[เขียนไว้แล้ว](https://varokas.com/ml-turicreate-43dcc87ef794) ที่แยกแอปเปิ้ลกับส้ม มาปรับใช้ แต่อยู่ๆ [image-net.org](https://image-net.org) ก็ล่ม!! เลยต้องเปลี่ยนแผนใหม่ เอาเป็นแยกพันธุ์สุนัขก็แล้วกันนะ

#### Siberian Husky and Alaskan Malamute

สุนัขสองพันธ์นี้ใกล้เคียงกันมาก มนุษย์หลายคนดูรูปยังแยกไม่ออกเลย เนื่องจากเราเป็นมนุษย์ขี้เกียจ แทนที่จะไปศึกษาดูว่ามันต่างกันยังไง วันนี้ลองมาพึ่งอภินิหารของ CreateML กันดู

![](/img/1*MoyB5SjXG7GwXOeI7hFJ_A.jpeg)ซ้าย: Malamute, ขวา: Husky ([ref](https://www.animalwised.com/differences-between-the-alaskan-malamute-and-the-siberian-husky-669.html))อย่างที่บอก image-net.org มันล่ม เราเลยต้องไปเข้า Flickr หรือ Google images โหลดๆ มาเอง (ตอนไปโหลดหลายคนที่ลงรูปยังสับสนสองพันธุ์นี้เลย)

![](/img/1*Qw8xgZN7ZfYp_LX7I2IrSQ.png)จากนั้นโยนใส่ Folder แยกกันไว้ เก็บมาไว้ซักพันธุ์ละ 50 รูปขึ้นไป

![](/img/1*yoIhPNQEFYTkAyW0S4Cp-g.png)อย่าลืมทำไว้อีก folder นึงเป็นรูปเอาไว้ทดสอบด้วยว่าโมเดลที่ได้มันแม่นไหม

![](/img/1*Yz8KWad-PPP58o6uULah0Q.png)#### Model Training

ไม่ต้องเขียน Python ไม่ต้องซื้อการ์ดจอ ไม่ต้อง[เรียนคอร์ส Andrew Ng](https://www.coursera.org/learn/machine-learning) (แต่ผมแนะนำให้ไปดูนะหลังจากนี้ 555 สอนดีมากๆ)

แค่ไปโหลด MacOS Mojave โหลด XCode แล้วเปิด Playground พิมพ์สามบรรทัดตามนี้

![](/img/1*W4995zWZW5icMDsNkQ8x1A.png)import CreateMLUI**let** builder = MLImageClassifierBuilder()  
builder.showInLiveView()จากนั้นก็ลากเอา Folder data ที่มี Folder ย่อยสองอัน (Siberian Husky, Alaskan Malamute) เข้าไป รอแป๊บนึง ซักนาทีสองนาที ช้าเร็วขึ้นกับพลังศรัทธาของสาวก(ความแพงของแมค) ก็จะขึ้นมาให้ว่าโมเดลเราแม่นเท่าไหร่

![](/img/1*omzJDCtQqLVx8WMHjIEZaA.png)#### Test Model

ถึงเวลาพิสูจน์ศรัทธา โดยเอารูปที่เราเตรียมไว้เทสแยกไว้ต่างหากซึ่งโมเดลเรายังไม่เคยเห็นมาก่อนโยนเข้าไป มันก็จะบอกว่าเราแม่นกี่​ %

![](/img/1*Rc1JC1Yk0R2DLqaZB3e4dA.png)#### Export ไปใช้ใน iOS

จากนั้นเราก็ export เป็น .mlmodel เอาไปใช้ได้

![](/img/1*sldPmR0xeNrczSAvTu0KZA.png)วิธีเอาไปใช้ ก็เหมือนกับขั้นสุดท้ายของบทความเดิม

[**Machine Learning สำหรับสาวก**  
*ทำได้เองง่ายๆวันนี้บนเครื่องตัวเองตั้งแต่ต้นจนจบ*varokas.com](https://varokas.com/ml-turicreate-43dcc87ef794 "https://varokas.com/ml-turicreate-43dcc87ef794")[](https://varokas.com/ml-turicreate-43dcc87ef794)เสร็จแล้ว !!

#### References

* [https://developer.apple.com/documentation/createml/creating\_an\_image\_classifier\_model](https://developer.apple.com/documentation/createml/creating_an_image_classifier_model)
  