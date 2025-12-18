# โปรแกรมฉบับสมบูรณ์

## ชั่วโมงที่ 4 : Google Apps Script และ CRUD Google Sheets

---

## วัตถุประสงค์ของโปรแกรม

* ใช้ Google Apps Script เป็น Backend แบบ Serverless
* ใช้ Google Sheets เป็น Database
* เข้าใจและใช้งาน CRUD (Create / Read / Update / Delete)
* สร้าง Web API และเรียกผ่าน URL ได้จริง
* เตรียมพร้อมสำหรับการเชื่อมต่อกับ Web Page (ชั่วโมงที่ 5)

---

## ส่วนที่ 1 : เตรียม Google Sheets (Database)

1. เปิด **Google Sheets**
2. สร้างไฟล์ใหม่
3. ตั้งชื่อ Sheet ว่า **`data`**
4. แถวที่ 1 ใส่หัวตารางดังนี้

| A  | B    | C     |
| -- | ---- | ----- |
| id | name | score |

---

## ส่วนที่ 2 : สร้าง Google Apps Script

1. ไปที่ **Extensions → Apps Script**
2. ลบโค้ดเดิมทั้งหมด
3. วางโค้ดด้านล่างลงในไฟล์ `Code.gs`

---

## `Code.gs` (ฉบับสมบูรณ์)

```javascript
/* =========================
   READ : อ่านข้อมูลทั้งหมด
   ========================= */
function doGet() {
  let sheet = SpreadsheetApp
    .getActiveSpreadsheet()
    .getSheetByName("data");

  let rows = sheet.getDataRange().getValues();
  let result = [];

  for (let i = 1; i < rows.length; i++) {
    result.push({
      id: rows[i][0],
      name: rows[i][1],
      score: rows[i][2]
    });
  }

  return ContentService
    .createTextOutput(JSON.stringify(result))
    .setMimeType(ContentService.MimeType.JSON);
}

/* =========================
   CREATE / UPDATE / DELETE
   ========================= */
function doPost(e) {
  let sheet = SpreadsheetApp
    .getActiveSpreadsheet()
    .getSheetByName("data");

  let action = e.parameter.action;
  let data = JSON.parse(e.postData.contents);

  /* ----- CREATE ----- */
  if (action === "create") {
    sheet.appendRow([data.id, data.name, data.score]);
    return response("Create success");
  }

  /* ----- UPDATE ----- */
  if (action === "update") {
    let rows = sheet.getDataRange().getValues();
    for (let i = 1; i < rows.length; i++) {
      if (rows[i][0] == data.id) {
        sheet.getRange(i + 1, 2).setValue(data.name);
        sheet.getRange(i + 1, 3).setValue(data.score);
      }
    }
    return response("Update success");
  }

  /* ----- DELETE ----- */
  if (action === "delete") {
    let rows = sheet.getDataRange().getValues();
    for (let i = rows.length - 1; i > 0; i--) {
      if (rows[i][0] == data.id) {
        sheet.deleteRow(i + 1);
      }
    }
    return response("Delete success");
  }
}

/* =========================
   Response Helper
   ========================= */
function response(message) {
  return ContentService
    .createTextOutput(message)
    .setMimeType(ContentService.MimeType.TEXT);
}
```

---

## ส่วนที่ 3 : Deploy เป็น Web App

1. คลิก **Deploy → New deployment**
2. Type: **Web app**
3. Execute as: **Me**
4. Who has access: **Anyone**
5. คลิก **Deploy**
6. อนุญาตสิทธิ์
7. **คัดลอก URL** (สำคัญมาก)

---

## ส่วนที่ 4 : การทดสอบผ่าน URL (กิจกรรมปฏิบัติ)

### 1. ทดสอบ Read (GET)

* เปิด URL ที่ได้จากการ Deploy
* จะเห็นข้อมูลในรูป JSON

ตัวอย่างผลลัพธ์

```json
[
  { "id": "1", "name": "Alice", "score": 80 },
  { "id": "2", "name": "Bob", "score": 70 }
]
```

---

### 2. ทดสอบ Create / Update / Delete (เชิงแนวคิด)

> การเรียก `POST` จะถูกใช้งานจริงในชั่วโมงที่ 5 ผ่าน `fetch()`
> ชั่วโมงนี้เน้น **เข้าใจโครงสร้าง Backend และ CRUD**

---

## สิ่งที่ครูสามารถอธิบายจากโปรแกรมนี้

### 1. Serverless Backend

* ไม่มี Server
* ใช้ Google Cloud โดยอัตโนมัติ

### 2. Google Sheets = Database

* แถว = Record
* คอลัมน์ = Field

### 3. CRUD Mapping

| Operation | Apps Script |
| --------- | ----------- |
| Create    | appendRow   |
| Read      | getValues   |
| Update    | setValue    |
| Delete    | deleteRow   |

---

## กิจกรรมในชั้นเรียน (แนะนำ)

ให้นักเรียนลอง

1. เพิ่มข้อมูลโดยพิมพ์ใน Google Sheets
2. Refresh URL ดู JSON เปลี่ยน
3. เปลี่ยนชื่อ Sheet แล้วดู Error
4. เพิ่มคอลัมน์ใหม่ แล้วอภิปรายผลกระทบ
5. อธิบายการทำงานทีละขั้น (Client → API → Sheet)

---

## ขอบเขตของชั่วโมงที่ 4

✔ Google Apps Script
✔ Serverless
✔ CRUD
✔ Web API
✔ JSON Response
✘ HTML / fetch() (จะทำเต็มในชั่วโมงที่ 5)

