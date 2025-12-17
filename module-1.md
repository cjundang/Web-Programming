
# ชั่วโมงที่ 1 : พื้นฐาน Web Application และ Bootstrap


## 1. แนวคิด Web Application

### 1.1 ความหมายของ Web Application

Web Application คือโปรแกรมคอมพิวเตอร์ที่ทำงานผ่านเว็บเบราว์เซอร์ โดยผู้ใช้สามารถเข้าถึงและใช้งานได้ผ่านเครือข่ายอินเทอร์เน็ตโดยไม่จำเป็นต้องติดตั้งโปรแกรมเพิ่มเติมบนเครื่องคอมพิวเตอร์

จุดเด่นของ Web Application คือ

* สามารถใช้งานได้จากหลายอุปกรณ์
* ผู้ใช้เข้าถึงได้ง่าย
* รองรับการโต้ตอบกับผู้ใช้แบบเรียลไทม์

**ตัวอย่าง Web Application**

* Google Forms : รับข้อมูลจากผู้ใช้
* ระบบสมัครสมาชิกออนไลน์
* ระบบบันทึกคะแนนนักเรียน



## 2. โครงสร้างการทำงาน Client–Server (เชิงแนวคิด)

### 2.1 Client

Client คือฝั่งผู้ใช้งาน ซึ่งโดยทั่วไปคือเว็บเบราว์เซอร์ เช่น Google Chrome หรือ Microsoft Edge
หน้าที่ของ Client คือ

* แสดงผลหน้าเว็บ
* รับข้อมูลจากผู้ใช้
* ส่งคำขอ (Request) ไปยัง Server

### 2.2 Server

Server คือฝั่งที่ประมวลผลข้อมูลและจัดเก็บข้อมูล
หน้าที่ของ Server คือ

* รับคำขอจาก Client
* ประมวลผลข้อมูล
* ส่งผลลัพธ์กลับไปยัง Client

> ในชั่วโมงนี้จะมุ่งเน้นการพัฒนา **ฝั่ง Client (Frontend)** ซึ่งประกอบด้วย HTML, CSS และ Bootstrap



## 3. HTML พื้นฐาน

### 3.1 บทบาทของ HTML

HTML (HyperText Markup Language) เป็นภาษาที่ใช้กำหนดโครงสร้างของหน้าเว็บ
HTML ไม่ได้ใช้คำนวณ แต่ใช้บอกว่า “อะไรคืออะไร” บนหน้าเว็บ


### 3.2 โครงสร้างพื้นฐานของ HTML

```html
<!DOCTYPE html>
<html>
<head>
    <title>My First Web</title>
</head>
<body>
    <h1>Hello Web Application</h1>
</body>
</html>
```

**คำอธิบาย**

* `<html>` : โครงสร้างหลักของเอกสาร
* `<head>` : ข้อมูลเกี่ยวกับหน้าเว็บ เช่น ชื่อเว็บ
* `<body>` : เนื้อหาที่แสดงบนหน้าจอ


### 3.3 Form, Input และ Button

Form ใช้สำหรับรับข้อมูลจากผู้ใช้

```html
<form>
    <label>Name</label>
    <input type="text">
    <button>Submit</button>
</form>
```

* `<input>` : ช่องกรอกข้อมูล
* `<button>` : ปุ่มสั่งงาน


### 3.4 Table สำหรับแสดงข้อมูล

```html
<table border="1">
    <tr>
        <th>Name</th>
        <th>Score</th>
    </tr>
    <tr>
        <td>Student A</td>
        <td>80</td>
    </tr>
</table>
```

Table ใช้แสดงข้อมูลที่มีโครงสร้างเป็นแถวและคอลัมน์


## 4. CSS เบื้องต้น

### 4.1 บทบาทของ CSS

CSS (Cascading Style Sheets) ใช้สำหรับตกแต่งหน้าเว็บ เช่น

* สี
* ขนาดตัวอักษร
* ระยะห่าง
* ตำแหน่งขององค์ประกอบ


### 4.2 ตัวอย่าง CSS อย่างง่าย

```html
<p style="color: blue; font-size: 20px;">
    Welcome to Web Application
</p>
```

CSS ช่วยให้หน้าเว็บอ่านง่ายและสวยงามมากขึ้น


## 5. Bootstrap

### 5.1 แนวคิดของ Bootstrap

Bootstrap เป็น CSS Framework ที่มีรูปแบบสำเร็จรูปให้ใช้งาน
ช่วยลดเวลาในการเขียน CSS และรองรับการแสดงผลบนหลายขนาดหน้าจอ


### 5.2 การใช้งาน Bootstrap

เชื่อม Bootstrap ผ่าน CDN

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
```


### 5.3 Grid System

Bootstrap แบ่งหน้าจอออกเป็น 12 ส่วน

```html
<div class="container">
    <div class="row">
        <div class="col-6">Left</div>
        <div class="col-6">Right</div>
    </div>
</div>
```

ช่วยจัด Layout ได้อย่างเป็นระบบ


### 5.4 Component พื้นฐาน

**Button**

```html
<button class="btn btn-primary">Save</button>
```

**Form**

```html
<input type="text" class="form-control">
```

**Table**

```html
<table class="table table-bordered">
```

---

## 6. กิจกรรมปฏิบัติ : สร้างหน้าเว็บฟอร์มด้วย Bootstrap

### ตัวอย่างหน้าเว็บฟอร์มอย่างง่าย

```html
<!DOCTYPE html>
<html>
<head>
    <title>Student Form</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>

<body>
<div class="container mt-5">
    <h3>Student Registration</h3>

    <div class="mb-3">
        <label>Name</label>
        <input type="text" class="form-control">
    </div>

    <div class="mb-3">
        <label>Score</label>
        <input type="number" class="form-control">
    </div>

    <button class="btn btn-success">Submit</button>
</div>
</body>
</html>
```

## 7. แนวทางการทดลองปรับ Layout และ Style

ให้ผู้เรียนทดลอง:

* เปลี่ยนสีปุ่มจาก `btn-success` เป็น `btn-primary`
* เพิ่ม `mt-3`, `mb-3` เพื่อดูผลระยะห่าง
* แบ่งหน้าจอเป็น 2 คอลัมน์ด้วย Grid System

## 8. สรุปท้ายชั่วโมง

ในชั่วโมงนี้ ผู้เรียนได้เรียนรู้ว่า

* Web Application ทำงานบนแนวคิด Client–Server
* HTML ใช้สร้างโครงสร้างหน้าเว็บ
* CSS ใช้ตกแต่งหน้าเว็บ
* Bootstrap ช่วยจัด Layout และ Component ได้อย่างรวดเร็ว

เนื้อหานี้เป็นพื้นฐานสำคัญสำหรับการเขียน JavaScript และการพัฒนา Web Application ในชั่วโมงถัดไป
