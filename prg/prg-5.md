
# โปรแกรมฉบับสมบูรณ์

## ชั่วโมงที่ 5 : เชื่อมต่อ Web Page กับ Google Sheets

---

## ภาพรวมการทำงาน

```
HTML Form
   ↓
JavaScript (fetch + JSON)
   ↓
Google Apps Script (Web API)
   ↓
Google Sheets (Database)
```

---

## เงื่อนไขก่อนเริ่ม

✔ ทำ **ชั่วโมงที่ 4** เรียบร้อยแล้ว
✔ มี Google Sheets + Apps Script ที่ Deploy เป็น Web App
✔ มี **SCRIPT_URL** จากการ Deploy

---

## ส่วนที่ 1 : Backend (ทบทวน – ใช้จากชั่วโมงที่ 4)

> ใช้ `Code.gs` เดิม **ไม่ต้องแก้ไข**

รองรับ:

* GET → Read
* POST + action=create / update / delete

---

## ส่วนที่ 2 : Frontend (HTML + JavaScript)

### วิธีใช้งาน

1. เปิด Notepad / VS Code
2. บันทึกไฟล์ชื่อ `index.html`
3. แก้ไข `YOUR_SCRIPT_URL`
4. เปิดไฟล์ด้วย Web Browser

---

## `index.html` (ฉบับสมบูรณ์)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hour 5 : Web App with Google Sheets</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body class="bg-light">

<div class="container mt-4">

    <!-- Title -->
    <div class="text-center mb-4">
        <h2>Student Management System</h2>
        <p class="text-muted">Hour 5 : Frontend + Google Apps Script</p>
    </div>

    <!-- Form -->
    <div class="card shadow-sm mb-4">
        <div class="card-body">
            <h4 class="card-title mb-3">Student Form</h4>

            <div class="mb-3">
                <label class="form-label">Student ID</label>
                <input type="text" id="id" class="form-control">
            </div>

            <div class="mb-3">
                <label class="form-label">Student Name</label>
                <input type="text" id="name" class="form-control">
            </div>

            <div class="mb-3">
                <label class="form-label">Score</label>
                <input type="number" id="score" class="form-control">
            </div>

            <button class="btn btn-success" onclick="createData()">Create</button>
            <button class="btn btn-warning" onclick="updateData()">Update</button>
            <button class="btn btn-danger" onclick="deleteData()">Delete</button>
            <button class="btn btn-primary" onclick="loadData()">Load</button>
        </div>
    </div>

    <!-- Table -->
    <div class="card shadow-sm">
        <div class="card-body">
            <h4 class="card-title mb-3">Student List</h4>

            <table class="table table-bordered">
                <thead class="table-dark">
                    <tr>
                        <th>ID</th>
                        <th>Name</th>
                        <th>Score</th>
                    </tr>
                </thead>
                <tbody id="tableBody">
                    <tr>
                        <td colspan="3" class="text-center">No data</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

</div>

<script>
/* =========================
   CONFIG
   ========================= */
const SCRIPT_URL = "YOUR_SCRIPT_URL";

/* =========================
   READ
   ========================= */
function loadData() {
    fetch(SCRIPT_URL)
        .then(res => res.json())
        .then(data => {
            let table = document.getElementById("tableBody");
            table.innerHTML = "";

            data.forEach(s => {
                table.innerHTML += `
                    <tr>
                        <td>${s.id}</td>
                        <td>${s.name}</td>
                        <td>${s.score}</td>
                    </tr>`;
            });
        })
        .catch(() => alert("Error loading data"));
}

/* =========================
   CREATE / UPDATE / DELETE
   ========================= */
function createData() {
    sendData("create");
}

function updateData() {
    sendData("update");
}

function deleteData() {
    sendData("delete");
}

function sendData(action) {
    let data = {
        id: document.getElementById("id").value,
        name: document.getElementById("name").value,
        score: document.getElementById("score").value
    };

    if (data.id === "") {
        alert("ID is required");
        return;
    }

    fetch(SCRIPT_URL + "?action=" + action, {
        method: "POST",
        body: JSON.stringify(data)
    })
    .then(() => loadData())
    .catch(() => alert("Error sending data"));
}
</script>

</body>
</html>
```

---

## สิ่งที่นักเรียนได้เรียนรู้จากโปรแกรมนี้

### 1. การส่งข้อมูลจากหน้าเว็บ

```javascript
fetch(SCRIPT_URL, {
    method: "POST",
    body: JSON.stringify(data)
});
```

---

### 2. การรับข้อมูล JSON จาก Google Sheets

```javascript
fetch(SCRIPT_URL)
  .then(res => res.json())
```

---

### 3. การแสดงผลข้อมูลด้วย DOM

```javascript
table.innerHTML += `<tr>...</tr>`;
```

---

### 4. Error Handling เบื้องต้น

```javascript
.catch(() => alert("Error"));
```

---

## กิจกรรมทดลอง (แนะนำสำหรับชั้นเรียน)

ให้นักเรียนลอง

1. เพิ่มข้อมูล → ตรวจสอบใน Google Sheets
2. แก้ไขข้อมูล → ดูผลการ Update
3. ลบข้อมูล → ตรวจสอบแถวถูกลบ
4. กรอก ID ซ้ำ → วิเคราะห์ผล
5. ปิดอินเทอร์เน็ต → ดู Error Handling

---

## ขอบเขตของชั่วโมงที่ 5

✔ HTML
✔ JavaScript
✔ fetch()
✔ JSON
✔ Google Apps Script
✔ Google Sheets
✔ CRUD
✔ Web Application ครบวงจร


