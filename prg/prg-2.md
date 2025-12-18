# โปรแกรมฉบับสมบูรณ์

## ชั่วโมงที่ 2 : JavaScript Syntax และ DOM

### วัตถุประสงค์ของโปรแกรม

* ใช้ JavaScript ควบคุมพฤติกรรมของหน้าเว็บ
* อ่านค่าจาก Form ด้วย DOM
* ใช้ Event Handling (`onclick`, `onchange`)
* แสดงผลลัพธ์บนหน้าเว็บแบบทันที
* เชื่อมโยงแนวคิด JavaScript กับ Python

---

## วิธีใช้งาน

1. เปิด Notepad / VS Code
2. บันทึกไฟล์ชื่อ `index.html`
3. ดับเบิลคลิกเปิดด้วย Web Browser

---

## `index.html` (ฉบับสมบูรณ์)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hour 2 : JavaScript and DOM</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body class="bg-light">

<div class="container mt-4">

    <!-- Title -->
    <div class="text-center mb-4">
        <h2>JavaScript Syntax and DOM</h2>
        <p class="text-muted">Hour 2 : Control Web Page with JavaScript</p>
    </div>

    <!-- Input Form -->
    <div class="card shadow-sm mb-4">
        <div class="card-body">
            <h4 class="card-title mb-3">Student Information</h4>

            <div class="mb-3">
                <label class="form-label">Student Name</label>
                <input type="text" id="name" class="form-control" placeholder="Enter your name">
            </div>

            <div class="mb-3">
                <label class="form-label">Score</label>
                <input type="number" id="score" class="form-control" placeholder="Enter score" onchange="checkScore()">
            </div>

            <button class="btn btn-primary" onclick="showResult()">
                Show Result
            </button>
        </div>
    </div>

    <!-- Output Section -->
    <div class="card shadow-sm">
        <div class="card-body">
            <h4 class="card-title">Result</h4>
            <p id="outputName">Name : -</p>
            <p id="outputScore">Score : -</p>
            <p id="outputStatus">Status : -</p>
        </div>
    </div>

</div>
```

Javascript
```html
<script>
    // Function to show name and score
    function showResult() {
        let name = document.getElementById("name").value;
        let score = document.getElementById("score").value;

        document.getElementById("outputName").innerHTML =
            "Name : " + name;

        document.getElementById("outputScore").innerHTML =
            "Score : " + score;
    }

    // Function to check pass/fail
    function checkScore() {
        let score = document.getElementById("score").value;
        let status = "";

        if (score >= 50) {
            status = "Pass";
            document.getElementById("outputStatus").style.color = "green";
        } else {
            status = "Fail";
            document.getElementById("outputStatus").style.color = "red";
        }

        document.getElementById("outputStatus").innerHTML =
            "Status : " + status;
    }
</script>

</body>
</html>
```

---

## สิ่งที่ครูสามารถอธิบายจากโปรแกรมนี้

### 1. JavaScript Syntax

```javascript
let name = document.getElementById("name").value;
```

* `let` → ตัวแปร (เทียบกับ Python)
* `.value` → อ่านค่าจาก input

---

### 2. DOM (Document Object Model)

```javascript
document.getElementById("outputName").innerHTML = "...";
```

* JavaScript เข้าถึง HTML
* เปลี่ยนข้อความบนหน้าเว็บได้ทันที

---

### 3. Event Handling

| Event      | ตำแหน่ง          |
| ---------- | ---------------- |
| `onclick`  | ปุ่ม Show Result |
| `onchange` | ช่อง Score       |

---

### 4. เงื่อนไข (If–Else)

```javascript
if (score >= 50) {
    status = "Pass";
} else {
    status = "Fail";
}
```

→ แนวคิดเดียวกับ Python

---

## กิจกรรมทดลอง (สำหรับนักเรียน)

ให้นักเรียนลอง

1. เปลี่ยนเกณฑ์ผ่านจาก 50 → 60
2. เพิ่มสถานะ “Excellent” เมื่อคะแนน ≥ 80
3. เปลี่ยนสีพื้นหลังเมื่อ Pass / Fail
4. เพิ่ม input อายุ แล้วแสดงผลเพิ่ม
5. เปลี่ยนข้อความภาษาอังกฤษเป็นภาษาไทย

