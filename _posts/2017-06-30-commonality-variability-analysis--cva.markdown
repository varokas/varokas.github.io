---
layout:	post
title:	"Commonality-Variability Analysis (CVA)"
date:	2017-06-30
---

  #### เลิก “ใช้” Design Patterns กันเถอะ

#### สรุปแบบขี้เกียจอ่าน

ในการออกแบบแทนที่จะดูว่าตรงกับ Pattern ไหน ให้เน้นไปดูว่าควรจะซ่อนความซับซ้อน (Encapsulate Variations) อย่างไร แล้ว Design Pattern จะออกมาให้เห็นเอง

* สิ่งที่เหมือนกัน Common ทำเป็น Abstract / Interface
* สิ่งที่ต่างกัน Variable แยกออกมาใส่เป็น Class ต่างๆ
* โดยพิจารณา Context of Use จะได้ทำเฉพาะสิ่งที่จำเป็น
#### มันคืออะไร?

Commonality-Variability Analysis เป็นหลักการวิเคราะห์ระบบและดีไซน์ว่าทำ encapsulation ได้ถูกจุดไหม ครบถ้วนแล้วหรือยัง มาจาก[วิทยานิพนธ์](http://tobeagile.com/wp-content/uploads/2011/12/CoplienThesis.pdf)ของ James Coplien เขียนไว้ปี 2000

#### ทำไปทำไม?

CVA เป็นเครื่องมือหนึ่งในการ Encapsulate Variations ที่สอนง่ายและเข้าใจง่าย


> เลิกมองว่า Design Pattern คือ เครื่องมือเอามาใช้ซ่อนความซับซ้อน
> ให้มองว่า Design Pattern เป็นผลลัพธ์โดยธรรมชาติจากกระบวนการซ่อนความซับซ้อน#### Commonaility

หาจุดที่เหมือนกันเอามาเขียนเป็น class เดียวกัน ตัวอย่างเช่นเช่น ดินสอ กับ ปากกา จะได้แบบนี้

![](/img/1*KXeHTAQt_WD2AhnFDFdSHg.png)#### Variability

เอาจุดที่ต่างกัน แยกออกมาใส่ไว้ใน subclass/implementation

![](/img/1*lyRouuERA46FupvAMx8tDA.png)#### Context of Use

จะเห็นได้ว่าสองอย่างนี้ มีอะไรเหมือนและต่างกันมากมาย แต่ที่มีประโยชน์ก็แค่ส่วนที่โปรแกรมเราจะใช้

สมมติว่าเป็นโปรแกรมวาดรูป เหลือที่ใช้แค่นี้

![](/img/1*Kln4NpHQ4sAZgnJX1Kj-Uw.png)เอาสิ่งที่ไม่เกี่ยวออกไป แล้วแก้ชื่อ Interface ให้ดีขึ้น ก็เหลือแค่นี้

![](/img/1*ywox9OXnO3stugcO321vnA.png)ภาษาไฮโซเค้าเรียกว่า Strategy Pattern#### เคล็ดวิชา

* ย้ำอีกครั้งว่า กระบวนการ encapsulate variations เป็นเหตุที่ทำให้เกิด design patterns ไม่ใช่ในทางกลับกัน
* ตอนทำจริง ให้ดู Context of Use ก่อน แล้วค่อยไปดู​ Common-Variable (อธิบายในนี้สลับกันเพราะเข้าใจง่ายกว่า)
* ถ้าตั้งชื่อ interface/abstract ไม่ถูก ลองทบทวน Context of Use ดีๆ (อาจมีซ้อนกัน)
* สิ่งที่ “เป็น” ต่างกันมักจะกลายเป็น Properties
* สิ่งที่ “ทำ” ต่างกันมักจะกลายเป็น Methods/Functions
  