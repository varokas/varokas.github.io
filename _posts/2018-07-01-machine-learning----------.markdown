---
layout:	post
title:	"Machine Learning สำหรับสาวก"
date:	2018-07-01
---

  #### ทำได้เองง่ายๆวันนี้บนเครื่องตัวเองตั้งแต่ต้นจนจบ

สาวกหลายๆคนเห็นวิดีโอสาธิต [CreateML](https://developer.apple.com/documentation/create_ml) ของ macOS 10.14 ที่เอารูปดอกไม้มาโยนใส่ใน directory ย่อยๆ แล้วสร้าง Machine Learning โมเดลไปใช้เองได้ทันที ก็คงอยากจะลองไปทำบ้าง

ตามดูได้จาก 1:00:08 เป็นต้นไป ที่นี่ <https://developer.apple.com/videos/play/wwdc2018/102/>

![](/img/1*mhtO2fo15i57nQF21wW07g.jpeg)มันเป็นปาฎิหารย์!!ติดอยู่ที่สาวกหลายคนอาจจะยังศรัทธาไม่พอจะเอา macOS mojave beta มาลงที่เครื่องตัวเองตอนนี้ แต่อาจจะยังไม่รู้ว่า จริงๆแล้วสามารถบันดาลสิ่งเหล่านี้ได้เลยวันนี้

มาลองทำ Machine Learning แยกรูปกันเองดู​ (ง่ายมาก)​ เริ่มกันตั้งแต่มีรูป ไปจนถึงใช้บน iOS ได้เลย

#### TuriCreate

อันนี้เป็น opensource ที่ Apple ปล่อยออกมาตั้งแต่ปลายปีที่แล้ว ชื่อว่า [turicreate](https://github.com/apple/turicreate) มีพลังอภินิหารย์ในการสร้างโมเดลคล้ายกับ CreateML มาก เพียงแต่ต้องเอาไปรันใน python แทนที่จะเป็น swift

วิธีลงก็ตามที่อยู่ในหน้าเวป <https://github.com/apple/turicreate> แต่หลักๆคือ ตามนี้

brew install python3# Prepare virtualenv  
pip3 install virtualenv  
virtualenv venv  
source venv/bin/activate# If done correctly there should be `(venv)` in front of the prompt. # (venv) ~/p/apple-orange ❯❯❯ \_# Install turicreate  
pip3 install -U turicreate#### 1. หาข้อมูล

ที่จะลองทำวันนี้คือ ทำให้โมเดลเรา แยกระหว่าง แอปเปิ้ล กับ ส้ม ให้ออก สิ่งที่จำเป็นต้องมีคือ รูปของทั้งสองประเภทเยอะๆ จากนั้นก็โยนเข้าไปให้ turicreate มันเรียนเอาเองว่าอะไรเป็นอะไร

ข้อมูลรูป จะไปหาใน Google แล้วคอยโหลดๆมาก็ได้ แต่วันนี้มาทางลัด คือ ไปหารูปที่เค้าจำแนกไว้แล้วที่ <http://image-net.org/>

![](/img/1*enSuBEMdyt5LcGBrR82leQ.png)![](/img/1*q2EbVfbJUO4jr-PGL5oeKw.png)![](/img/1*PRMaMiAT4aoObzePC6LMEg.png)ถ้าเราไปกดที่ปุ่ม URLs จากรูปก็จะได้ url ของรูปมาเป็นลิสต์แบบนี้

http://farm2.static.flickr.com/1353/1230897342\_2bd7c7569f.jpg  
http://farm2.static.flickr.com/1016/1306604645\_3993048c41.jpg  
http://farm1.static.flickr.com/81/207747002\_37e2540d6c.jpg  
...  
... (มีอีกยาว)เสร็จแล้วก็เขียน script ง่ายๆ ไปอ่าน URL ทั้งหมดของแต่ละผลไม้มาใส่ไว้ใน​ directory ชื่อ /data/apples กับ /data/oranges ตามแต่ละประเภทของมัน

จากสคริปต์ที่เขียน ก็จะเอามาแค่ 400 ลิงก์แรก มีเยอะเกินก็เหนื่อย จากนั้นลองโหลดได้ บาง url จะโหลดไม่ผ่านบ้างก็ช่างมัน

เสร็จแล้วถ้าเข้าไปดูรูปที่อยู่ใน data/apples ก็จะเจอรูปแอปเปิ้ลในอิริยาบทต่างๆ แบบนี้ มีรูปที่มันเสียบ้างก็ช่างมัน ให้ turicreate มันไปเรียนเอาเอง (แกล้ง machine เล่นๆ)

![](/img/1*-mup9n72R5fNxxAFRh5fvQ.png)#### 2. เตรียมข้อมูลให้กับ TuriCreate

หลังจากขั้นตอนแรกเสร็จแล้วเราควรจะได้ directory แบบนี้

/data  
 /oranges -> มีรูปส้ม 400 รูป  
 /apples -> มีรูปแอปเปิ้ล 400 รูปซึ่ง turicreate มันก็ไม่รู้หรอกว่า อะไรเป็นอะไร จนกว่าเราจะไปเตรียมตารางเป็นรูปกับชื่อประเภทให้มัน ซึ่งโชคดีมากว่าทำได้ง่ายมากๆ

หลักการ โหลดข้อมูลทุกอย่างจาก /data เข้าไปเป็นตาราง จากนั้นสร้าง column ชื่อ label ขึ้นมา ถ้าใน path มีคำว่า apple ก็คือ เป็นแอปเปิ้ล

พิมพ์ python3 ที่ shell ตามนี้ได้เลย

ถ้าอยากดูข้อมูลตาราง พิมพ์ data.explore() เข้าไปเพื่อแอบดูได้

![](/img/1*KELwBolFFQFwLgQP2gzfHQ.png)#### 3. สร้างโมเดลจากข้อมูล

จากนั้นก็เอาข้อมูลที่ได้มาสร้างเป็นโมเดล จริงๆ ตามขั้นตอนนี้

1. โหลดข้อมูลจากขั้นที่แล้วมา
2. แบ่งเป็นข้อมูลที่ใช้ train กับข้อมูลที่ใช้ test ว่าโมเดลถูกหรือยัง
3. รัน training (เสียงพัดลมดังแป๊บนึง)
4. ลองมันกับ test data ที่แบ่งไว้ในข้อ (2) แล้ววัดความแม่น
5. save เป็น mlmodel ไว้ใช้กับ ios
มีหลายขั้นเหมือนจะยาก แต่จริงๆ เป็น โค้ดไม่กี่บรรทัด ดูตามได้ง่ายมาก

ทำตามหมดนี้ ใน directory เราก็จะมีไฟล์ ApplesOranges.mlmodel เอามาใช้ได้เลย

#### 4. เอาไปใช้ใน iOS

อันนี้ขอโกงหน่อยคือ ขี้เกียจสร้าง Project ขี้นมาใหม่ เอาไปใส่ไว้ใน playground แล้วกันนะ

เปิด XCode แล้วสร้าง Playground ขี้นมา

![](/img/1*DToSicgYcsEGNaNTKNN1Kw.png)เลือกเป็น iOS แล้วก็ blank จากนั้น ใส่ชื่อ project แล้วก็ save ไว้

![](/img/1*V3ACD4ptdOJapGrxrGK2Cg.png)กด ⌘+1 เพื่อเปิด directory ทางด้านขวา

1. ลากโมเดลที่เราเทรนมาอย่างยากลำบาก (หรอ?) เข้าไปไว้ใน resource
2. ไปหารูปส้มกับแอปเปิ้ลมาสัก 2–3 รูป เพื่อเอามาลอง โยนไว้ที่เดียวกัน
![](/img/1*Q1RPxQNPig_XcVOajfykGQ.png)ทำเสร็จแล้วจะมีรูปกับโมเดลขึ้นด้านซ้ายแบบนี้

![](/img/1*FZXNvWQqsej-SLgkMj-4dg.png)จากนั้นก็ใส่โค้ดเพื่อลองใช้ CoreML กับ Vision ดู หลักๆ ก็ก๊อปเอามาจากลิงก์นี้

[**Classifying Images with Vision and Core ML**  
*With the Core ML framework, you can use a trained machine learning model to classify input data. The Vision framework…*developer.apple.com](https://developer.apple.com/documentation/vision/classifying_images_with_vision_and_core_ml "https://developer.apple.com/documentation/vision/classifying_images_with_vision_and_core_ml")[](https://developer.apple.com/documentation/vision/classifying_images_with_vision_and_core_ml)โดยตัดพวก callback กับ async ออกให้หมด (งานจริงอย่างทำแบบนี้นะ…)

เสร็จแล้วเราก็ได้ผลลัพธ์ออกมาแบบนี้ (อย่าลืมกดปุ่ม​โชว์ข้างๆ บรรทัดที่โหลดรูป มันจะได้วาดเป็นรูปสวยงาม)

![](/img/1*4QuBu4y0gMWMhDfOzS1M4w.png)![](/img/1*yJe2s0YBd7iC-Gy9m3DBgg.png)เสร็จแล้ว !! โค้ดทั้งหมดกับ Playground ไปดูได้ที่นี่

<https://github.com/varokas/turi-examples>

ขอให้ทุกคนสนุกกับการเทรนโมเดลครับ

#### Bonus : พิสูจน์ศรัทธา…

ไหนเอาแอปเปิ้ลแบบนี้ไปลองซิ๊

![](/img/1*SdiSYqsEjUGZBIUjiDVVzA.jpeg)apple-logo.jpg![](/img/1*c4IWber-ohe21BwOz_L-nw.png)อ้าวกลายเป็นส้มไปซะ 99% เลย 555+ เราคงต้องกลับไปเทรนโมเดลเพื่ออัพศรัทธาใหม่

  