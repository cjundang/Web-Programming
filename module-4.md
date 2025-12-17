# ชั่วโมงที่ 4 : Google Apps Script และ CRUD Google Sheets

---

## 1. แนวคิด Serverless ด้วย Google Apps Script

### 1.1 แนวคิด Serverless (เชิงอธิบาย)

Serverless คือแนวคิดการพัฒนาแอปพลิเคชันที่ผู้พัฒนา **ไม่ต้องดูแลเซิร์ฟเวอร์เอง**
ระบบจะรันโค้ดให้โดยอัตโนมัติบน Cloud เมื่อมีการเรียกใช้งาน

ข้อดีของ Serverless

* ไม่ต้องติดตั้ง Server
* ไม่ต้องดูแลฐานข้อมูล
* ใช้งานง่าย เหมาะสำหรับผู้เริ่มต้น

---

### 1.2 Google Apps Script

Google Apps Script คือแพลตฟอร์มเขียนโปรแกรมด้วยภาษา JavaScript ที่ทำงานบน Google Cloud
สามารถเชื่อมต่อบริการของ Google ได้โดยตรง เช่น

* Google Sheets
* Google Drive
* Google Forms

ในชั่วโมงนี้
**Google Sheets จะทำหน้าที่เป็นฐานข้อมูล (Database)**
**Google Apps Script จะทำหน้าที่เป็น Backend และ Web API**

---

## 2. โครงสร้าง Google Apps Script

### 2.1 ส่วนประกอบหลัก

* Project : โปรเจกต์ของสคริปต์
* `Code.gs` : ไฟล์หลักสำหรับเขียนโค้ด
* Function : หน่วยคำสั่งที่ใช้ทำงาน

---

### 2.2 ฟังก์ชัน doGet และ doPost

Google Apps Script ใช้ฟังก์ชันพิเศษเพื่อสื่อสารผ่าน URL

* `doGet()` : ใช้รับข้อมูลแบบ GET
* `doPost()` : ใช้รับข้อมูลแบบ POST

ตัวอย่างโครงสร้างพื้นฐาน

```javascript
function doGet() {
  return ContentService.createTextOutput("Hello World");
}
```

เมื่อ Deploy แล้ว สามารถเรียกฟังก์ชันนี้ผ่าน Browser ได้ทันที

---

## 3. การเตรียม Google Sheets (กิจกรรมปฏิบัติที่ 1)

### ขั้นตอน

1. สร้าง Google Sheets ใหม่
2. ตั้งชื่อ Sheet ว่า `data`
3. กำหนดหัวตารางแถวที่ 1

| คอลัมน์ | ข้อมูล |
| ------- | ------ |
| A       | id     |
| B       | name   |
| C       | score  |

Google Sheets นี้จะทำหน้าที่เป็นฐานข้อมูลของระบบ

---

## 4. CRUD Operation กับ Google Sheets

CRUD เป็นแนวคิดพื้นฐานในการจัดการข้อมูล ประกอบด้วย

* Create : เพิ่มข้อมูล
* Read : อ่านข้อมูล
* Update : แก้ไขข้อมูล
* Delete : ลบข้อมูล

---

### 4.1 Read : อ่านข้อมูลจาก Google Sheets

```javascript
function doGet() {
  let sheet = SpreadsheetApp
    .getActiveSpreadsheet()
    .getSheetByName("data");

  let data = sheet.getDataRange().getValues();

  return ContentService
    .createTextOutput(JSON.stringify(data))
    .setMimeType(ContentService.MimeType.JSON);
}
```

**อธิบายแนวคิด**

* อ่านข้อมูลทั้งหมดจาก Sheet
* แปลงเป็น JSON
* ส่งกลับไปยัง Client

---

### 4.2 Create : เพิ่มข้อมูลใหม่

```javascript
function doPost(e) {
  let sheet = SpreadsheetApp
    .getActiveSpreadsheet()
    .getSheetByName("data");

  let obj = JSON.parse(e.postData.contents);

  sheet.appendRow([
    obj.id,
    obj.name,
    obj.score
  ]);

  return ContentService
    .createTextOutput("Insert success");
}
```

แนวคิด

* รับข้อมูล JSON จาก Client
* เพิ่มข้อมูลเป็นแถวใหม่ใน Google Sheets

---

### 4.3 Update : แก้ไขข้อมูล (เชิงแนวคิด)

```javascript
function updateData(id, newScore) {
  let sheet = SpreadsheetApp
    .getActiveSpreadsheet()
    .getSheetByName("data");

  let rows = sheet.getDataRange().getValues();

  for (let i = 1; i < rows.length; i++) {
    if (rows[i][0] == id) {
      sheet.getRange(i + 1, 3).setValue(newScore);
    }
  }
}
```

แนวคิด

* ค้นหาข้อมูลจาก id
* แก้ไขค่าที่ต้องการ

---

### 4.4 Delete : ลบข้อมูล (เชิงแนวคิด)

```javascript
function deleteData(id) {
  let sheet = SpreadsheetApp
    .getActiveSpreadsheet()
    .getSheetByName("data");

  let rows = sheet.getDataRange().getValues();

  for (let i = rows.length - 1; i > 0; i--) {
    if (rows[i][0] == id) {
      sheet.deleteRow(i + 1);
    }
  }
}
```

แนวคิด

* ค้นหาแถวที่ตรงกับ id
* ลบแถวนั้นออก

---

## 5. การ Deploy เป็น Web App

### ขั้นตอนการ Deploy

1. คลิก **Deploy → New deployment**
2. เลือกประเภท **Web app**
3. Execute as: **Me**
4. Who has access: **Anyone**
5. คลิก Deploy และอนุญาตสิทธิ์

หลังจาก Deploy จะได้ **URL ของ Web App**

---

### การทดสอบผ่าน URL (กิจกรรมปฏิบัติที่ 2)

* เปิด URL ใน Browser
* หากแสดง JSON แสดงว่า Web API ทำงานถูกต้อง
* แก้ไขข้อมูลใน Google Sheets แล้ว Refresh หน้าเว็บ

---

## 6. กิจกรรมปฏิบัติในชั้นเรียน

### กิจกรรมที่ 1

* สร้าง Google Sheet และใส่ข้อมูลตัวอย่าง

### กิจกรรมที่ 2

* เขียน Script เพื่ออ่านข้อมูล (Read)
* Deploy และเรียกผ่าน URL

### กิจกรรมที่ 3

* เพิ่มข้อมูลผ่าน Script
* ตรวจสอบผลลัพธ์ใน Google Sheets

---

## 7. สรุปท้ายชั่วโมง

ในชั่วโมงนี้ ผู้เรียนได้เรียนรู้ว่า

* Google Apps Script สามารถใช้เป็น Backend แบบ Serverless
* Google Sheets สามารถใช้แทนฐานข้อมูลได้
* แนวคิด CRUD เป็นหัวใจของการจัดการข้อมูล
* สามารถสร้าง Web API และเรียกใช้งานผ่าน URL ได้จริง


