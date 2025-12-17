# ชั่วโมงที่ 5 : เชื่อมต่อ Web Page กับ Google Sheets

---

## 1. ภาพรวมการทำงานของระบบ Web Application

ก่อนเริ่มเนื้อหา ให้ผู้เรียนเห็นภาพรวมการทำงานของระบบดังนี้

1. ผู้ใช้กรอกข้อมูลบนหน้าเว็บ (HTML Form)
2. JavaScript รับข้อมูลจากฟอร์ม
3. JavaScript ส่งข้อมูลไปยัง Google Apps Script ผ่าน Web API
4. Google Apps Script บันทึกข้อมูลลง Google Sheets
5. Google Apps Script ส่งข้อมูลกลับมาในรูป JSON
6. JavaScript แสดงผลข้อมูลบนหน้าเว็บ

กระบวนการนี้สะท้อนการทำงานจริงของ Web Application ในระดับพื้นฐาน

---

## 2. การส่งข้อมูลจากหน้าเว็บไปยัง Google Apps Script

### 2.1 บทบาทของ JavaScript ในการส่งข้อมูล

JavaScript ทำหน้าที่เป็นตัวกลางระหว่างหน้าเว็บ (HTML) และ Backend (Google Apps Script)
ข้อมูลจากผู้ใช้จะถูกจัดรูปแบบเป็น JSON ก่อนส่งไปยัง Server

---

### 2.2 ตัวอย่างการรับค่าจากฟอร์ม

```javascript
let data = {
    id: document.getElementById("id").value,
    name: document.getElementById("name").value,
    score: document.getElementById("score").value
};
```

แนวคิดสำคัญ

* อ่านค่าจาก HTML ผ่าน DOM
* เก็บข้อมูลใน Object

---

### 2.3 การส่งข้อมูลด้วย fetch()

```javascript
fetch(SCRIPT_URL, {
    method: "POST",
    body: JSON.stringify(data)
});
```

* ใช้ `POST` เพื่อส่งข้อมูล
* ส่งข้อมูลในรูป JSON ไปยัง Google Apps Script

---

## 3. การรับค่ากลับมาในรูป JSON

### 3.1 ข้อมูลที่ Server ส่งกลับ

Google Apps Script จะส่งข้อมูลกลับมาในรูป JSON เช่น

```json
[
  { "id": "1", "name": "Alice", "score": 80 },
  { "id": "2", "name": "Bob", "score": 70 }
]
```

---

### 3.2 การรับและแปลง JSON ใน JavaScript

```javascript
fetch(SCRIPT_URL)
  .then(response => response.json())
  .then(data => {
      console.log(data);
  });
```

* `response.json()` ใช้แปลงข้อมูล JSON เป็น JavaScript Object
* สามารถนำข้อมูลไปแสดงผลบนหน้าเว็บได้ทันที

---

## 4. การแสดงข้อมูลจาก Google Sheets บนหน้าเว็บ

### 4.1 แนวคิดการแสดงผล

ข้อมูลที่ได้จาก API มักอยู่ในรูป Array ของ Object
ต้องใช้ Loop เพื่อแสดงข้อมูลแต่ละรายการ

---

### 4.2 ตัวอย่างการแสดงผลในรูป Table

```javascript
let table = document.getElementById("tableBody");
table.innerHTML = "";

data.forEach(item => {
    table.innerHTML += `
        <tr>
            <td>${item.id}</td>
            <td>${item.name}</td>
            <td>${item.score}</td>
        </tr>
    `;
});
```

แนวคิด

* ใช้ DOM สร้าง HTML แบบอัตโนมัติ
* แสดงข้อมูลจากฐานข้อมูลจริง

---

## 5. การจัดการ Error เบื้องต้น

### 5.1 ความจำเป็นของ Error Handling

ในการใช้งานจริง อาจเกิดปัญหา เช่น

* ไม่สามารถเชื่อมต่อ API ได้
* ข้อมูลไม่ครบ
* ผู้ใช้กรอกข้อมูลผิดรูปแบบ

---

### 5.2 ตัวอย่างการจัดการ Error ด้วย JavaScript

```javascript
fetch(SCRIPT_URL)
  .then(response => response.json())
  .then(data => {
      console.log(data);
  })
  .catch(error => {
      alert("เกิดข้อผิดพลาดในการเชื่อมต่อ");
  });
```

แนวคิด

* ป้องกันโปรแกรมหยุดทำงาน
* แจ้งผู้ใช้เมื่อเกิดปัญหา

---

## 6. กิจกรรมปฏิบัติ : ส่งข้อมูลจากฟอร์มไปบันทึกใน Google Sheets

### ตัวอย่างหน้าเว็บแบบสมบูรณ์ (สาธิต)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Student Form</title>
</head>
<body>

<h3>Student Form</h3>

<input id="id" placeholder="ID">
<input id="name" placeholder="Name">
<input id="score" placeholder="Score">

<button onclick="saveData()">Save</button>
<button onclick="loadData()">Load</button>

<table border="1">
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Score</th>
        </tr>
    </thead>
    <tbody id="tableBody"></tbody>
</table>

<script>
const SCRIPT_URL = "YOUR_SCRIPT_URL";

function saveData() {
    let data = {
        id: id.value,
        name: name.value,
        score: score.value
    };

    fetch(SCRIPT_URL, {
        method: "POST",
        body: JSON.stringify(data)
    }).then(() => loadData());
}

function loadData() {
    fetch(SCRIPT_URL)
        .then(res => res.json())
        .then(data => {
            let body = document.getElementById("tableBody");
            body.innerHTML = "";

            data.forEach(s => {
                body.innerHTML += `
                    <tr>
                        <td>${s.id}</td>
                        <td>${s.name}</td>
                        <td>${s.score}</td>
                    </tr>`;
            });
        });
}
</script>

</body>
</html>
```

---

## 7. การทดลองแก้ไขโค้ดและทดสอบการทำงาน

ให้ผู้เรียนทดลอง:

* เปลี่ยนรูปแบบการแสดงผล (Table → List)
* เพิ่มเงื่อนไขตรวจสอบข้อมูลก่อนส่ง
* เพิ่มข้อความแจ้งเตือนเมื่อบันทึกสำเร็จ
* ลองปิดอินเทอร์เน็ตเพื่อดู Error Handling

---

## 8. แนวคิดการนำไปประยุกต์ใช้งานจริง

ตัวอย่างการประยุกต์

* ระบบบันทึกคะแนนนักเรียน
* แบบฟอร์มลงทะเบียนกิจกรรม
* แบบสำรวจออนไลน์
* ระบบเก็บข้อมูลโครงงาน

แนวคิดสำคัญ

> โครงสร้างนี้เป็นพื้นฐานของ Web Application จริงในระดับอุตสาหกรรม
> เพียงเปลี่ยน Backend หรือ Database ก็สามารถพัฒนาต่อยอดได้

---

## 9. สรุปท้ายชั่วโมงและสรุปหลักสูตร

เมื่อจบชั่วโมงที่ 5 ผู้เรียนสามารถ

* ส่งข้อมูลจาก Web Page ไปยัง Backend ได้
* รับข้อมูลจาก Google Sheets ในรูป JSON
* แสดงข้อมูลจากฐานข้อมูลจริงบนหน้าเว็บ
* เข้าใจโครงสร้าง Web Application แบบครบวงจร

หลักสูตรนี้ช่วยวางรากฐานสำคัญสำหรับการเรียนรู้

* Web Application ระดับสูง
* REST API
* Framework ฝั่ง Frontend และ Backend ในอนาคต
