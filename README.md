# การพัฒนาเว็บแอปพลิเคชันเบื้องต้น (Introduction to Web Application Development)

## 1. ข้อมูลทั่วไปของหลักสูตร

### ชื่อหลักสูตร
การพัฒนาเว็บแอปพลิเคชันเบื้องต้น (Introduction to Web Application Development)

### กลุ่มเป้าหมาย
นักเรียนชั้นมัธยมศึกษาปีที่ 4 ที่มีพื้นฐานการเขียนโปรแกรมภาษา Python

### ระยะเวลาอบรม
รวม 5 ชั่วโมง (อบรมเชิงปฏิบัติการ)

### รูปแบบการอบรม
บรรยายสั้น + ลงมือปฏิบัติ (Hands-on Practice)  
ไม่มีการทำโปรเจกต์ปลายคอร์ส เน้นการฝึกเป็นช่วง ๆ ตามหัวข้อ

---

## 2. วัตถุประสงค์ของหลักสูตร (Learning Objectives)

เมื่อสิ้นสุดการอบรม ผู้เรียนสามารถ

1. อธิบายโครงสร้างพื้นฐานของ Web Application ได้  
2. สร้างหน้าเว็บด้วย HTML และตกแต่งด้วย CSS ผ่าน Bootstrap ได้  
3. ใช้ JavaScript พื้นฐานในการควบคุมพฤติกรรมของหน้าเว็บ  
   จัดการข้อมูลรูปแบบ JSON และเชื่อมต่อ Web API เบื้องต้น  
4. ใช้ Google Apps Script เพื่อทำ CRUD กับ Google Sheets  
5. เชื่อมต่อหน้าเว็บกับ Google Sheets เพื่อบันทึกและเรียกดูข้อมูลได้  

---

## 3. โครงสร้างเนื้อหาหลักสูตร

### [ชั่วโมงที่ 1 : พื้นฐาน Web Application และ Bootstrap](md/module-1.md)

ผู้เรียนจะได้เรียนรู้แนวคิดของ Web Application และโครงสร้างการทำงานแบบ Client–Server ในเชิงอธิบาย เพื่อให้เข้าใจบทบาทของเว็บเบราว์เซอร์และฝั่งประมวลผล จากนั้นศึกษาพื้นฐาน HTML สำหรับสร้างโครงสร้างหน้าเว็บ เช่น `<html>`, `<head>`, `<body>`, form, input, button และ table รวมถึง CSS เบื้องต้นสำหรับการตกแต่งหน้าเว็บ ปิดท้ายด้วยการใช้ Bootstrap เพื่อจัด Layout ด้วย Grid System และใช้งาน Component พื้นฐาน พร้อมกิจกรรมสร้างหน้าเว็บฟอร์มอย่างง่าย

[Handout](pdf/01-Bootstrap_Web_App_Builder.pdf)

---

### [ชั่วโมงที่ 2 : JavaScript Syntax และ DOM](md/module-2.md)

ชั่วโมงนี้มุ่งเน้นบทบาทของ JavaScript ในการทำให้เว็บโต้ตอบกับผู้ใช้ ผู้เรียนจะได้ฝึก JavaScript Syntax พื้นฐาน ได้แก่ ตัวแปร เงื่อนไข ลูป และฟังก์ชัน โดยเปรียบเทียบแนวคิดกับภาษา Python เพื่อเสริมความเข้าใจ จากนั้นเรียนรู้ DOM และการเข้าถึง HTML Element รวมถึงการใช้ Event Handling เช่น `onclick` และ `onchange` เพื่อควบคุมปุ่มและฟอร์มผ่าน JavaScript

[Handout](pdf/02-JavaScript_Web_Interactivity.pdf)
---

### [ชั่วโมงที่ 3 : JSON และ Web API](md/module-3.md)

ผู้เรียนจะได้เข้าใจแนวคิดของ JSON ในฐานะรูปแบบข้อมูลมาตรฐานของ Web Application ศึกษาโครงสร้าง Object และ Array ใน JavaScript การแปลงข้อมูล JSON และแนวคิด Web API จากนั้นฝึกเรียกใช้ Web API ด้วย `fetch()` ทดลองอ่านข้อมูล JSON จาก API สาธารณะ และแสดงผลข้อมูลบนหน้าเว็บ

---

### [ชั่วโมงที่ 4 : Google Apps Script และ CRUD Google Sheets](md/module-4.md)

ชั่วโมงนี้อธิบายแนวคิด Serverless และการใช้ Google Apps Script เป็น Backend อย่างง่าย ผู้เรียนจะได้เรียนรู้โครงสร้างของ Google Apps Script การเชื่อมต่อกับ Google Sheets และแนวคิด CRUD ได้แก่ Create, Read, Update และ Delete พร้อมกิจกรรมสร้าง Google Sheet เขียน Script จัดการข้อมูล และ Deploy เป็น Web App เพื่อทดสอบผ่าน URL

[Handout](pdf/04-Build_a_Serverless_API_with_Google_Sheets.pdf)
---

### [ชั่วโมงที่ 5 : เชื่อมต่อ Web Page กับ Google Sheets](md/module-5.md)

ผู้เรียนจะนำความรู้ทั้งหมดมาประยุกต์ใช้งานจริง โดยเชื่อมต่อหน้าเว็บกับ Google Apps Script ส่งข้อมูลจากฟอร์มไปบันทึกใน Google Sheets และดึงข้อมูลกลับมาแสดงผลบนหน้าเว็บในรูป JSON พร้อมเรียนรู้การจัดการ Error เบื้องต้น และอภิปรายแนวทางการนำไปประยุกต์ใช้ในระบบงานจริง เช่น ระบบบันทึกข้อมูลหรือแบบฟอร์มออนไลน์

[Handout](pdf/05-สร้าง_Web_App_ด้วย_Google_Sheets.pdf)
