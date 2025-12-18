## ชั่วโมงที่ 1 : พื้นฐาน Web Application และ Bootstrap

### วัตถุประสงค์ของโปรแกรม

* แสดงโครงสร้าง HTML `<html> <head> <body>`
* ใช้ Form, Input, Button, Table
* ใช้ Bootstrap จัด Layout ด้วย Grid System
* ใช้ Component พื้นฐานของ Bootstrap
* **ยังไม่ใช้ JavaScript** (ตามขอบเขตชั่วโมงที่ 1)

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
    <title>Introduction to Web Application</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body class="bg-light">

    <!-- Header -->
    <div class="container mt-4">
        <div class="row">
            <div class="col text-center">
                <h1 class="mb-3">Web Application Development</h1>
                <p class="text-muted">
                    Example for Hour 1 : HTML + CSS + Bootstrap
                </p>
            </div>
        </div>
    </div>

    <!-- Form Section -->
    <div class="container mt-4">
        <div class="row">
            <!-- Form Column -->
            <div class="col-md-6">
                <div class="card shadow-sm">
                    <div class="card-body">
                        <h4 class="card-title mb-3">Student Form</h4>

                        <form>
                            <div class="mb-3">
                                <label class="form-label">Student ID</label>
                                <input type="text" class="form-control" placeholder="Enter student ID">
                            </div>

                            <div class="mb-3">
                                <label class="form-label">Student Name</label>
                                <input type="text" class="form-control" placeholder="Enter student name">
                            </div>

                            <div class="mb-3">
                                <label class="form-label">Score</label>
                                <input type="number" class="form-control" placeholder="Enter score">
                            </div>

                            <button type="button" class="btn btn-primary">
                                Submit
                            </button>
                            <button type="reset" class="btn btn-secondary">
                                Clear
                            </button>
                        </form>
                    </div>
                </div>
            </div>

            <!-- Table Column -->
            <div class="col-md-6">
                <div class="card shadow-sm">
                    <div class="card-body">
                        <h4 class="card-title mb-3">Student List</h4>

                        <table class="table table-bordered table-striped">
                            <thead class="table-dark">
                                <tr>
                                    <th>ID</th>
                                    <th>Name</th>
                                    <th>Score</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>001</td>
                                    <td>Alice</td>
                                    <td>85</td>
                                </tr>
                                <tr>
                                    <td>002</td>
                                    <td>Bob</td>
                                    <td>78</td>
                                </tr>
                            </tbody>
                        </table>

                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <div class="container mt-5">
        <div class="row">
            <div class="col text-center text-muted">
                <p>Introduction to Web Application Development</p>
            </div>
        </div>
    </div>

</body>
</html>
```

---

## สิ่งที่ครูสามารถชี้ให้ผู้เรียนเห็นจากโปรแกรมนี้

### 1. โครงสร้าง HTML

* `<head>` : เชื่อม Bootstrap
* `<body>` : เนื้อหาที่แสดงบนหน้าจอ

### 2. Bootstrap Grid System

```html
<div class="row">
    <div class="col-md-6">...</div>
    <div class="col-md-6">...</div>
</div>
```

→ แบ่งหน้าจอเป็น 2 คอลัมน์

### 3. Bootstrap Components

* `form-control`
* `btn btn-primary`
* `table table-bordered`
* `card`

---

## กิจกรรมทดลอง (สำหรับนักเรียน)

ให้นักเรียนลอง

1. เปลี่ยนสีปุ่ม

   ```html
   btn-primary → btn-success
   ```
2. เปลี่ยน Layout เป็น 3 คอลัมน์
3. เพิ่มแถวข้อมูลใน Table
4. เปลี่ยน `bg-light` เป็น `bg-white`
5. ลบ Bootstrap แล้วดูความแตกต่าง

