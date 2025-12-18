
# โปรแกรมฉบับสมบูรณ์

## ชั่วโมงที่ 3 : JSON และ Web API

### วัตถุประสงค์ของโปรแกรม

* เข้าใจโครงสร้างข้อมูลแบบ JSON
* ใช้ Object และ Array ใน JavaScript
* เรียก Web API ด้วย `fetch()`
* รับข้อมูล JSON และแสดงผลบนหน้าเว็บ
* เตรียมพื้นฐานสำหรับ Backend ในชั่วโมงที่ 4

---

## วิธีใช้งาน

1. เปิด Notepad / VS Code
2. บันทึกไฟล์ชื่อ `index.html`
3. เปิดไฟล์ด้วย Web Browser
4. กดปุ่มเพื่อทดสอบการทำงาน

---

## `index.html` (ฉบับสมบูรณ์)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hour 3 : JSON and Web API</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body class="bg-light">

<div class="container mt-4">

    <!-- Title -->
    <div class="text-center mb-4">
        <h2>JSON and Web API</h2>
        <p class="text-muted">Hour 3 : Fetch data from API</p>
    </div>

    <!-- JSON from Variable -->
    <div class="card shadow-sm mb-4">
        <div class="card-body">
            <h4 class="card-title">JSON from JavaScript Object</h4>
            <button class="btn btn-secondary mb-3" onclick="showLocalJSON()">
                Show Local JSON
            </button>
            <p id="localOutput">-</p>
        </div>
    </div>

    <!-- Web API Section -->
    <div class="card shadow-sm">
        <div class="card-body">
            <h4 class="card-title">Web API : User List</h4>
            <button class="btn btn-primary mb-3" onclick="loadUsers()">
                Load Users from API
            </button>

            <table class="table table-bordered">
                <thead class="table-dark">
                    <tr>
                        <th>Name</th>
                        <th>Email</th>
                        <th>City</th>
                    </tr>
                </thead>
                <tbody id="userTable">
                    <tr>
                        <td colspan="3" class="text-center">No data</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

</div>

<script>
    /* ---------- Part 1 : Local JSON ---------- */
    function showLocalJSON() {
        let student = {
            name: "Alice",
            age: 16,
            score: 85
        };

        document.getElementById("localOutput").innerHTML =
            "Name: " + student.name +
            ", Age: " + student.age +
            ", Score: " + student.score;
    }

    /* ---------- Part 2 : Web API with fetch() ---------- */
    function loadUsers() {
        fetch("https://jsonplaceholder.typicode.com/users")
            .then(response => response.json())
            .then(data => {
                let table = document.getElementById("userTable");
                table.innerHTML = "";

                for (let i = 0; i < data.length; i++) {
                    table.innerHTML += `
                        <tr>
                            <td>${data[i].name}</td>
                            <td>${data[i].email}</td>
                            <td>${data[i].address.city}</td>
                        </tr>
                    `;
                }
            })
            .catch(error => {
                alert("Error loading data");
            });
    }
</script>

</body>
</html>
```

---

## สิ่งที่ครูสามารถอธิบายจากโปรแกรมนี้

### 1. JSON ใน JavaScript

```javascript
let student = {
    name: "Alice",
    age: 16,
    score: 85
};
```

* Object = JSON
* key : value
* แนวคิดเดียวกับ dictionary ใน Python

---

### 2. Array ของ Object (จาก Web API)

```javascript
data[i].name
data[i].email
```

* API ส่งข้อมูลมาเป็น Array
* ต้องใช้ Loop เพื่อแสดงผล

---

### 3. fetch() และ Web API

```javascript
fetch(url)
  .then(response => response.json())
  .then(data => { ... })
```

* Client ขอข้อมูล
* Server ส่ง JSON กลับมา
* JavaScript นำไปแสดงผล

---

### 4. DOM + JSON

```javascript
document.getElementById("userTable").innerHTML += ...
```

* แสดงข้อมูลจาก API บนหน้าเว็บ
* เชื่อม JSON → HTML

---

## กิจกรรมทดลอง (สำหรับนักเรียน)

ให้นักเรียนลอง

1. แสดงเฉพาะชื่อ (ไม่แสดง email)
2. เปลี่ยน Table เป็น List (`<ul>`)
3. นับจำนวนผู้ใช้ที่ได้จาก API
4. เปลี่ยน API Endpoint
5. เพิ่มเงื่อนไขแสดงเฉพาะเมืองที่ต้องการ

---

## ขอบเขตของโปรแกรม (ตามหลักสูตร)

✔ JSON
✔ Object / Array
✔ Web API
✔ fetch()
✔ DOM
✘ Backend (จะเริ่มในชั่วโมงที่ 4)

